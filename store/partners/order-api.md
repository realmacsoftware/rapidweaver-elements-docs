---
description: Record Elements Store orders and refunds from your own sales system
---

# Recording Orders

Use the Order API when a purchase happens outside the Elements Store, for example in FastSpring. Your system calls the API when the payment succeeds. Elements stores the order and returns a single-use voucher code. It does not create an account and it does not grant the products.

FastSpring shows that code on the receipt and in the order email. The buyer then signs in to Elements and redeems the code into the account they are signed in to. The email address on the order is kept for support. It is not the account that receives the products.

{% hint style="warning" %}
This page is not in the published manual yet.

While the API is in private test:

* **API Keys** on the Account page, and **Redeem Voucher** on Purchases, are visible to Elements admins only. Both are labelled "Admin only".
* Call `https://api-dev.elementsapp.cloud/v1`. Production (`https://api.elementsapp.cloud/v1`) does not serve this API yet.

Remove this hint, and switch the samples to the production base URL, before adding the page to the manual.
{% endhint %}

## Create an API key

An API key authorises your server to record orders. Create it in Elements, then store it with your other secrets. The raw key is shown once.

1. Open **Elements Cloud** in Elements.
2. Choose **Account** in the sidebar.
3. Scroll past **Payment Settings** to **API Keys**.
4. Enter a name, for example `FastSpring connector`.
5. Click **Create API Key**.
6. Copy the key from the sheet. It starts with `eok_`. This is the only time the full key is shown.
7. Click **Done**. The list then shows the name, a short hint, and the date it was created.

You can keep up to 10 keys. To revoke one, click the trash icon and confirm. Deletion takes effect immediately. Anything still sending that key receives `401 unauthorized`.

Each key has the `orders` scope. A key can record orders only for products owned by that seller. An admin's key sells Elements Platform products. A creator's key sells that creator's products. One order can contain several products, and every product in the order must belong to that seller. If any product is unknown or belongs to someone else, the whole order is rejected and nothing is stored.

## Product ID and version

Each line item is a product ID plus a version number. Both are on the product in Elements: open the pack and copy **Product ID** and **Version No.**

The public catalogue lists the same values: [https://store.elementsapp.cloud/catalog.json](https://store.elementsapp.cloud/catalog.json). See [Store API & Deep Linking](store-api-and-deep-linking.md).

Put these on the FastSpring product as custom attributes named `packId` and `version`. A bundle is one FastSpring product whose `packs` attribute lists several pairs, for example `com.elementsplatform.essentials:1,com.developer.gallery.95cb45db:2`. That bundle is one order and one voucher. The Store does not know FastSpring product paths.

## How the buyer redeems

1. Open **Elements Cloud** and sign in to the account that should own the products.
2. Choose **Purchases**.
3. Click **Redeem Voucher**.
4. Enter the code and click **Check**. The sheet lists the products and the signed-in email. A product the account already owns is marked "Already in your account."
5. Click **Redeem**. Every product on the voucher is added to that account, including ones already owned.

The code works once. A second attempt is rejected. Redeeming a product the account already owns does not remove the earlier purchase. Refunding this voucher removes only the claims it added. The account keeps the product while any other completed claim remains, from the Store, a free claim, or another voucher.

## Calling the API

| | |
| --- | --- |
| Testing base URL | `https://api-dev.elementsapp.cloud/v1` |
| Production base URL | `https://api.elementsapp.cloud/v1` |
| Authentication | Header `x-api-key: eok_…` |
| Body | `Content-Type: application/json` |

Send the key only to these endpoints, over HTTPS. Both order methods accept at most 10 requests per second, with a burst of 20. Above that the gateway responds with **429**.

### Record an order

`POST /orders`

```json
{
  "provider": "fastspring",
  "externalOrderId": "REA220721-1322-97157:essentials",
  "buyer": { "email": "buyer@example.com" },
  "items": [
    { "packId": "com.elementsplatform.essentials", "version": 1, "amount": 19900, "currency": "USD" }
  ],
  "invoiceUrl": "https://example.onfastspring.com/account/order/…/invoice/…",
  "source": "REA220721-1322-97157"
}
```

| Field | Rule |
| --- | --- |
| `provider` | 1–32 characters: a letter or digit, then letters, digits, or hyphens. Use `fastspring`. |
| `externalOrderId` | 1–128 characters from `A–Z`, `a–z`, `0–9`, `.`, `_`, `:`, `-`. For FastSpring use `{reference}:{product}`. |
| `buyer.email` | The email from the order. Stored in lowercase for support. It does not receive the products. |
| `items` | 1–20 entries. The same product and version cannot appear twice. |
| `items[].packId` | Product ID, 1–200 characters. |
| `items[].version` | Integer, 1 or greater. |
| `items[].amount` | Integer, 0 or greater. Minor units of `currency` (cents, pence). `19900` is $199.00. `0` is a free order. |
| `items[].currency` | Three-letter currency code. |
| `invoiceUrl` | Optional. Must start with `https://` and be at most 2048 characters. |
| `source` | Optional note, at most 500 characters. The FastSpring order reference fits here. |
| `test` | Optional boolean. `true` checks the order and writes nothing. The response has no `voucherCode`. |

A successful call returns **200**:

```json
{
  "status": "recorded",
  "orderId": "fastspring:REA220721-1322-97157:essentials",
  "voucherCode": "ABCD-EFGH-JKMN-PQRS",
  "items": [{ "packId": "com.elementsplatform.essentials", "version": 1 }]
}
```

`orderId` is `provider` and `externalOrderId` joined with a colon. `voucherCode` is 16 characters in groups of four. Show that string to the buyer. Elements does not email it.

Sending the same `provider` and `externalOrderId` again is safe. The response is **200** with the original body and `"status": "duplicate"`, including the same `voucherCode`. A different body does not change the stored order. A different seller using the same id receives **409** `order_conflict`.

`"test": true` returns `"dryRun": true` and no `voucherCode`.

### Refund an order

`POST /orders/refund`

Refunds the whole order. There is no per-item refund.

```json
{
  "provider": "fastspring",
  "externalOrderId": "REA220721-1322-97157:essentials"
}
```

| Status | Body | Meaning |
| --- | --- | --- |
| 200 | `{ "status": "refunded", "orderId": "fastspring:…", "claimsRemoved": [], "revoked": [] }` | The voucher had not been redeemed. It can no longer be redeemed. |
| 200 | `{ "status": "refunded", "orderId": "fastspring:…", "claimsRemoved": [{ "packId": "…", "version": 1 }], "revoked": [{ "packId": "…", "version": 1 }] }` | The voucher had been redeemed. `claimsRemoved` is every product on the order. `revoked` is the products the account no longer has any completed claim for. |
| 200 | `{ "status": "already-refunded", "orderId": "fastspring:…", "claimsRemoved": [], "revoked": [] }` | This order was already refunded. |
| 404 | `{ "status": "not-found", "orderId": "fastspring:…" }` | No order with that id for this seller. |

`revoked` can be empty while `claimsRemoved` is not. That happens when the account still owns the product through another purchase or another voucher. `"test": true` adds `"dryRun": true` and writes nothing. On a dry run, `revoked` lists products this order is the only completed claim for.

The 404 body is the status object above. It is not wrapped in `error`.

### Errors

Validation and permission failures return **400**. Nothing is written.

```json
{
  "error": {
    "code": "item_not_permitted",
    "message": "Not permitted for this API key: com.example.pack v2",
    "items": [{ "packId": "com.example.pack", "version": 2 }]
  }
}
```

`items` is present for `unknown_item`, `item_not_permitted`, and `duplicate_item`.

| HTTP | `error.code` | What to do |
| --- | --- | --- |
| 400 | `invalid_request`, `invalid_email`, `duplicate_item`, `unknown_item`, `item_not_permitted` | Permanent. Fix the payload or the product attributes. Retrying the same body will fail again. |
| 401 | `unauthorized` | The key is missing, malformed, or deleted. |
| 403 | `insufficient_scope` | The key does not have the `orders` scope. |
| 409 | `order_conflict` | That order id was already recorded by another seller. |
| 429 | | Slow down and retry. |
| 500 | `internal_error` | Retry. Repeating the same order id is safe. |

Redeeming is done in the app, not with the API key. A code that does not exist returns **404** `not_found`. A code already redeemed returns **409** `voucher_redeemed`. A refunded code returns **409** `voucher_refunded`.

## FastSpring

Delivery uses **remote license fulfillment**, the same pattern as the DevAnt license generator (`services/fastspring.devant.io/src/generateLicense.js`). A webhook handles refunds only.

FastSpring calls the license URL once per product while it processes the order. Set the fulfillment output to **Single License Only**, so quantity does not produce extra codes. One FastSpring order with two products becomes two Elements orders and two vouchers. The id for each is `{reference}:{product}`. A bundle stays one product, so it stays one voucher.

The license request is form-encoded. A captured DevAnt request included `email`, `product`, `productName`, `reference`, `quantity`, `name`, `subscription`, `test`, `referrer`, `tags`, and `productAttributes` (the product's custom attributes as a JSON string; `attributes` carried the same JSON). It also included `security_request_hash`. It did not include the charged price.

On the fulfillment's Parameters page, include `email`, `product`, `reference`, and `productAttributes`. If that page offers a price and a currency, include those too, under the names `price` and `currency`. The private key is on the fulfillment's Security page. It is not sent in the request.

Check the hash the way FastSpring's own template does, which is what DevAnt does:

1. Take every parameter except `security_request_hash`.
2. Sort the names and concatenate the values, in that order.
3. Append the private key and take the MD5 hex digest.
4. Compare it with `security_request_hash`.

The script responds with the voucher code as plain text and nothing else. FastSpring puts that text on the receipt and in the email. `Content-Type: text/plain` matches the Single License Only format. DevAnt returns the same kind of body as `application/octet-stream`; either is the license string.

Set `packId` and `version` as custom attributes on a single-pack product. On a bundle, set `packs` to comma-separated `packId:version` pairs. `product` must use only letters, digits, `.`, `_`, and `-`, because it becomes part of `externalOrderId`.

The webhook subscribes to `return.created` only. Enable the HMAC secret. FastSpring posts `{ "events": [ … ] }`. Verify `X-FS-Signature` before you parse the body. The signature is base64 HMAC-SHA256 of the raw body, using the webhook secret. Header capitalisation varies by host, so compare the name case-insensitively.

| FastSpring | Order API |
| --- | --- |
| License request `reference` + `:` + `product` | `externalOrderId` |
| `return.created` `data.original.reference` + `:` + each returned item's `product` | the same `externalOrderId` for that product |
| License request `email` | `buyer.email` |
| `productAttributes.packId` and `productAttributes.version` | one item |
| `productAttributes.packs` | several items, one voucher |
| `price` and `currency`, when the license request includes them | `items[].amount` (minor units) and `items[].currency` |
| License request `reference` | `source` |
| `test` `true`, or webhook `data.live` `false` | a FastSpring test order |

Refund each returned item on its own. A return of one product from a two-product order refunds that product's voucher and leaves the other. A bundle is one product, so one return refunds every pack on that voucher.

When the license request has no price, the sample records `amount: 0` and `currency: usd`. Purchase stats then show zero for that order. Turn on `price` and `currency` in the fulfillment parameters if FastSpring lists them.

Amounts, when present, are decimals in the order currency. Multiply by 100 and round, except for zero-decimal currencies (JPY, KRW, VND, and the others in the sample), where the amount is already the minor unit.

FastSpring treats the webhook response as follows:

* **200** means every event in the POST was processed.
* **202**, with the processed event ids in the body, one id per line, acknowledges only those events.
* Anything else is a failure. FastSpring retries for up to 7 days.

Acknowledge permanent failures (400, 404, 409) so they do not retry for a week, and alert a person. Leave out 401, 403, 429, 500, and network failures so FastSpring retries them. Other event types can be acknowledged and ignored.

A license-generator failure is different. Return **500** when the Order API is unavailable, so FastSpring can try the fulfillment again. Return **400** with a short plain-text reason for a permanent rejection. The same `{reference}:{product}` returns the same code, so a retry is safe.

On the dev API, record FastSpring test orders for real (`"test": false`) so the buyer receives a code. On production, send `"test": true` when the license request's `test` is `true`, or when a refund event has `data.live` `false`.

### PHP license generator

Point each product's remote license URL at this script. POST, UTF-8. Output format: Single License Only. PHP with curl.

```php
<?php
declare(strict_types=1);

const ELEMENTS_API_BASE = 'https://api-dev.elementsapp.cloud/v1';
const ELEMENTS_API_KEY = 'eok_replace_me';
const FASTSPRING_PRIVATE_KEY = 'replace_with_security_tab_private_key';

// false on the dev API, so FastSpring test orders really issue a code.
// true on production, so FastSpring test orders are a dry run.
const DRY_RUN_FASTSPRING_TEST_ORDERS = false;

const ZERO_DECIMAL_CURRENCIES = [
    'bif', 'clp', 'djf', 'gnf', 'jpy', 'kmf', 'krw', 'mga',
    'pyg', 'rwf', 'ugx', 'vnd', 'vuv', 'xaf', 'xof', 'xpf',
];

$request = $_POST;
$hash = (string) ($request['security_request_hash'] ?? '');
unset($request['security_request_hash']);
if ($hash === '' || !hash_equals(request_hash($request), $hash)) {
    http_response_code(401);
    echo 'Invalid license request';
    exit;
}

$reference = (string) ($request['reference'] ?? '');
$product = (string) ($request['product'] ?? '');
$email = (string) ($request['email'] ?? '');
if ($reference === '' || $product === '' || $email === '') {
    http_response_code(400);
    echo 'License request is missing reference, product, or email';
    exit;
}

$items = map_items($request);
if ($items === []) {
    http_response_code(400);
    echo 'Product has no packId attributes';
    exit;
}

$body = [
    'provider' => 'fastspring',
    'externalOrderId' => $reference . ':' . $product,
    'buyer' => ['email' => $email],
    'items' => $items,
    'source' => $reference,
];
if (DRY_RUN_FASTSPRING_TEST_ORDERS && ($request['test'] ?? 'false') === 'true') {
    $body['test'] = true;
}

$result = elements_post('/orders', $body);
$status = $result['status'];
$code = is_array($result['body']) ? (string) ($result['body']['voucherCode'] ?? '') : '';
if ($status === 200 && $code !== '') {
    header('Content-Type: text/plain; charset=utf-8');
    echo $code;
    exit;
}

error_log('Elements order failed ' . $status . ' ' . json_encode($result['body']));
$permanent = in_array($status, [400, 401, 403, 409], true);
http_response_code($permanent ? 400 : 500);
echo $permanent ? 'Order rejected' : 'Order API unavailable';

/** @param array<string, mixed> $request */
function request_hash(array $request): string
{
    ksort($request);
    $data = '';
    foreach ($request as $value) {
        // PHP has already decoded the form body. stripslashes matches FastSpring's template.
        $data .= stripslashes((string) $value);
    }
    return md5($data . FASTSPRING_PRIVATE_KEY);
}

/** @param array<string, mixed> $request @return list<array<string, mixed>> */
function map_items(array $request): array
{
    $attributes = product_attributes($request);
    $currency = strtolower((string) ($request['currency'] ?? 'usd'));
    $price = isset($request['price']) ? (float) $request['price'] : 0.0;

    $packs = trim((string) ($attributes['packs'] ?? ''));
    if ($packs !== '') {
        $items = [];
        foreach (explode(',', $packs) as $pair) {
            $parts = explode(':', trim($pair), 2);
            if (count($parts) !== 2 || $parts[0] === '' || !is_numeric($parts[1])) {
                continue;
            }
            $items[] = item($parts[0], (int) $parts[1], $price, $currency);
        }
        return $items;
    }

    $packId = trim((string) ($attributes['packId'] ?? ''));
    if ($packId === '' || !isset($attributes['version']) || !is_numeric($attributes['version'])) {
        return [];
    }
    return [item($packId, (int) $attributes['version'], $price, $currency)];
}

/** @param array<string, mixed> $request @return array<string, mixed> */
function product_attributes(array $request): array
{
    foreach (['productAttributes', 'attributes'] as $key) {
        $raw = $request[$key] ?? null;
        if (!is_string($raw) || $raw === '') {
            continue;
        }
        $decoded = json_decode($raw, true);
        if (is_array($decoded)) {
            return $decoded;
        }
    }
    return [];
}

/** @return array<string, mixed> */
function item(string $packId, int $version, float $price, string $currency): array
{
    return [
        'packId' => $packId,
        'version' => $version,
        'amount' => minor_units($price, $currency),
        'currency' => $currency,
    ];
}

function minor_units(float $amount, string $currency): int
{
    if (in_array($currency, ZERO_DECIMAL_CURRENCIES, true)) {
        return (int) round($amount);
    }
    return (int) round($amount * 100);
}

/** @param array<string, mixed> $body @return array{status: int, body: ?array} */
function elements_post(string $path, array $body): array
{
    $ch = curl_init(ELEMENTS_API_BASE . $path);
    curl_setopt_array($ch, [
        CURLOPT_POST => true,
        CURLOPT_HTTPHEADER => [
            'Content-Type: application/json',
            'x-api-key: ' . ELEMENTS_API_KEY,
        ],
        CURLOPT_POSTFIELDS => json_encode($body, JSON_UNESCAPED_SLASHES),
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_TIMEOUT => 20,
    ]);
    $raw = curl_exec($ch);
    $status = (int) curl_getinfo($ch, CURLINFO_RESPONSE_CODE);
    curl_close($ch);
    $decoded = json_decode($raw === false ? '' : $raw, true);
    return ['status' => $status, 'body' => is_array($decoded) ? $decoded : null];
}
```

### PHP refund webhook

A second script. Subscribe it to `return.created` only.

```php
<?php
declare(strict_types=1);

const ELEMENTS_API_BASE = 'https://api-dev.elementsapp.cloud/v1';
const ELEMENTS_API_KEY = 'eok_replace_me';
const FASTSPRING_HMAC_SECRET = 'replace_me';
const DRY_RUN_FASTSPRING_TEST_ORDERS = false;

$raw = file_get_contents('php://input');
if ($raw === false || $raw === '') {
    http_response_code(401);
    exit;
}

$signature = header_value('X-FS-Signature');
$computed = base64_encode(hash_hmac('sha256', $raw, FASTSPRING_HMAC_SECRET, true));
if ($signature === null || !hash_equals($computed, $signature)) {
    http_response_code(401);
    exit;
}

$payload = json_decode($raw, true);
$events = is_array($payload['events'] ?? null) ? $payload['events'] : [];
$acknowledged = [];
$retry = false;

foreach ($events as $event) {
    $eventId = (string) ($event['id'] ?? '');
    $type = (string) ($event['type'] ?? '');
    $data = is_array($event['data'] ?? null) ? $event['data'] : [];
    $outcome = $type === 'return.created' ? refund_return($data) : 'ack';

    if ($outcome === 'retry') {
        $retry = true;
        continue;
    }
    if ($eventId !== '') {
        $acknowledged[] = $eventId;
    }
}

if ($retry) {
    http_response_code($acknowledged === [] ? 500 : 202);
    echo implode("\n", $acknowledged);
    exit;
}

http_response_code(200);

function refund_return(array $data): string
{
    $original = is_array($data['original'] ?? null) ? $data['original'] : [];
    $reference = (string) ($original['reference'] ?? '');
    $items = is_array($data['items'] ?? null) ? $data['items'] : [];
    if ($reference === '' || $items === []) {
        error_log('FastSpring return has no reference or items');
        return 'ack';
    }

    $worst = 'ack';
    foreach ($items as $item) {
        $product = (string) ($item['product'] ?? '');
        if ($product === '') {
            continue;
        }
        $body = [
            'provider' => 'fastspring',
            'externalOrderId' => $reference . ':' . $product,
        ];
        if (DRY_RUN_FASTSPRING_TEST_ORDERS && ($data['live'] ?? true) === false) {
            $body['test'] = true;
        }
        $result = elements_post('/orders/refund', $body);
        $status = $result['status'];
        if ($status === 404) {
            error_log('Refund for an order Elements never recorded: ' . $body['externalOrderId']);
            continue;
        }
        if ($status === 200) {
            continue;
        }
        if (in_array($status, [400, 409], true)) {
            error_log('Elements refund rejected ' . $status . ' ' . json_encode($result['body']));
            continue;
        }
        error_log('Elements refund failed ' . $status);
        $worst = 'retry';
    }
    return $worst;
}

/** @param array<string, mixed> $body @return array{status: int, body: ?array} */
function elements_post(string $path, array $body): array
{
    $ch = curl_init(ELEMENTS_API_BASE . $path);
    curl_setopt_array($ch, [
        CURLOPT_POST => true,
        CURLOPT_HTTPHEADER => [
            'Content-Type: application/json',
            'x-api-key: ' . ELEMENTS_API_KEY,
        ],
        CURLOPT_POSTFIELDS => json_encode($body, JSON_UNESCAPED_SLASHES),
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_TIMEOUT => 20,
    ]);
    $raw = curl_exec($ch);
    $status = (int) curl_getinfo($ch, CURLINFO_RESPONSE_CODE);
    curl_close($ch);
    $decoded = json_decode($raw === false ? '' : $raw, true);
    return ['status' => $status, 'body' => is_array($decoded) ? $decoded : null];
}

function header_value(string $name): ?string
{
    $name = strtolower($name);
    foreach (getallheaders() ?: [] as $key => $value) {
        if (strtolower((string) $key) === $name) {
            return (string) $value;
        }
    }
    return null;
}
```

To try a single order without FastSpring:

```bash
curl -sS -X POST "https://api-dev.elementsapp.cloud/v1/orders" \
  -H "content-type: application/json" \
  -H "x-api-key: eok_replace_me" \
  -d '{"provider":"fastspring","externalOrderId":"T-0001:essentials","test":true,"buyer":{"email":"buyer@example.com"},"items":[{"packId":"com.elementsplatform.essentials","version":1,"amount":19900,"currency":"usd"}]}'
```

`"test": true` writes nothing and returns no code. Remove it to issue a voucher. Redeem that code from Purchases in Elements.
