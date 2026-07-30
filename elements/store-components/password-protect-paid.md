---
description: Protect pages and sections with a shared password login system
---

# Password Protect (Paid)

{% hint style="success" %}
Password Protect is available as a **paid product via the Elements Store**. Install the current version of Elements before adding it to a project.
{% endhint %}

Password Protect is a four-component pack for restricting an entire page or a selected section of content. Passwords are verified on the server, protected content is withheld until authentication succeeds, and matching Session IDs can share a login state across components and pages.

The pack includes dedicated Login and Logout components, optional remembered-device access, and WebAuthn-based biometric unlocking on compatible devices and browsers.

<a href="elementsapp://storeProduct/com.elementsplatform.passwordprotect" class="button primary" data-icon="store">Purchase Password Protect</a>

{% embed url="https://www.youtube.com/watch?v=OrB7npyl13E&pp=2AbIAQ%3D%3D" %}

### Features

* **Password Page** — Protects an entire page before its content is sent to the visitor.
* **Password Section** — Restricts selected child components inside a page.
* **Login and Logout components** — Create a consistent access flow across multiple protected areas.
* **Server-side verification** — Uses PHP and bcrypt password hashes rather than checking a plain-text password in the browser.
* **Shared sessions** — Reuse a Session ID to carry authentication between related components.
* **Remember Device** — Keep a visitor signed in for a configurable number of days.
* **Biometric unlock** — Offer Touch ID, Face ID, Windows Hello, or another supported platform authenticator after enrolment.
* **Customisable forms** — Style modal, input, button, overlay, and error states with theme controls.

### Requirements

Before using Password Protect, make sure you have:

* The Password Protect pack installed from the Elements Store.
* Hosting with PHP and PHP sessions enabled.
* A `.php` extension for every page containing a Password Protect component.
* HTTPS on the published site when using biometric authentication.
* Matching passwords and Session IDs where several components should share the same login state.

{% hint style="warning" %}
Do not publish a Password Protect page as HTML. Set its extension to `.php` and remove any older `.html` copy of the same page from the server, otherwise visitors may receive an error or reach the wrong file.
{% endhint %}

### Supported Content and File Types

Password Protect supports:

* Entire Elements pages through Password Page.
* Any Elements components inside a Password Section.
* Custom Login Trigger, Logout Content, form header, and modal header dropzones.
* Shared password access rather than individual user accounts.

{% hint style="info" %}
Password Protect is intended for shared-password access. It does not create user accounts, roles, password reset emails, or an administration area.
{% endhint %}

### How to Use Password Protect

You’ll find the four components under **Security** in the Components list.

1. Set the page extension to `.php`.
2. Add **Password Page** to protect the whole page, or add **Password Section** and place components in its Protected Content dropzone.
3. Replace the default password with a strong password.
4. Give the protected area a clear **Session ID**.
5. Add Login or Logout components where visitors need explicit controls, using the same Session ID.
6. Configure Remember Device, biometric access, styling, and error text.
7. Publish to a PHP server and test in a private browser window.

### Choose the Right Component

#### Password Page

Use Password Page when nothing on the page should be delivered before authentication. The password form gates the complete page and includes a **Form Header** dropzone for custom introductory content.

#### Password Section

Use Password Section when only part of a page needs protection. Place restricted components in **Protected Content**, build the locked-state control in **Login Trigger**, and use the modal **Form Header** for instructions or branding.

#### Login

Use Login to authenticate visitors before they reach a protected page or section. Its **Login Trigger** dropzone opens the login modal, while **Modal Header** provides space for a heading, explanation, or logo.

#### Logout

Use Logout to end the selected shared session. Its **Logout Content** dropzone provides the visible control. An optional confirmation modal can include custom **Modal Header** content.

### Shared Sessions

The Session ID connects the four components.

* Use the same Session ID and password on Password Page, Password Section, and Login when one successful login should unlock them together.
* Use the same Session ID on Logout to end that shared session.
* Use different Session IDs for unrelated protected areas.

The default Session ID is `elements`. Rename it to something meaningful and consistent when a project contains more than one protected area.

### Component Settings

#### Password Page

**Preview In Edit**

Shows the password form in the editor. It is enabled by default so the form can be styled without publishing.

**Password**

Sets the shared password. The pack generates a bcrypt hash for server-side verification.

**Shared Session ID**

Identifies the authentication state that related Login, Logout, Page, and Section components can share.

**Form Background**

Controls form gap, background colour, border radius, shadow, and padding.

**Input Styling**

Sets placeholder text, background, text and placeholder colours, normal and focus border colours, border width, radius, and padding.

**Button Styling**

Sets the submit button’s background, text colour, and radius.

**Remember Device**

Shows a checkbox that can keep authentication active beyond the browser session. It is enabled by default with a 30-day duration. The label can include `{{days}}` to insert the chosen duration.

**Redirect After Login**

Choose a destination after successful authentication. Leave it empty to reload the current page.

**Biometric**

Enables enrolment and unlocking with a supported platform authenticator. Customise the display name, enrolment text, unlock text, loading labels, fallback label, and enabled badge. Use `{{biometricType}}` where the detected method’s name should appear.

**Error Message**

Customise invalid-password text, colour, font, size, weight, and alignment.

#### Password Section

**Preview Overlay In Edit**

Shows the locked overlay and Login Trigger while editing.

**Preview Modal In Edit**

Opens the login modal in the editor so it can be styled.

**Password and Session ID**

Set the password and the shared authentication identifier.

**Background Image and Overlay**

Choose the image shown behind the locked state, then set overlay colour, opacity, and blur.

**Form Styling**

Controls modal background, radius, shadow, padding, form gap, and the component’s minimum locked height.

Password Section also includes the same Remember Device, Biometric, Input, Button, Error Message, and Advanced controls described for Password Page.

#### Login

**Preview In Edit**

Shows the login modal while editing.

**Password and Session ID**

Use the credentials of the Password Page or Password Section this component should unlock.

**Modal, Input, and Button Styling**

Controls modal background, radius, shadow, padding, form gap, input appearance, and button appearance.

**UX Features**

Configure Remember Device and Redirect After Login.

**Biometric and Error Message**

Provide the same compatible-device enrolment, unlock, fallback, and error controls available in Password Page.

#### Logout

**Session ID**

Selects the authentication session to end.

**Logout Confirmation**

Displays a confirmation modal before logout. Enable **Preview Modal In Edit** to style it in the editor.

**Redirect After Logout**

Choose a destination after logout. Leave it empty to reload the current page.

**Logout All Sessions**

Ends every Password Protect session rather than only the matching Session ID.

**Remove Biometric Data**

Removes Password Protect biometric enrolment data stored on the current device.

**Modal and Button Styling**

These controls appear when confirmation is enabled and set the modal background, radius, shadow, padding, and confirmation button appearance.

#### Advanced

Every component provides **CSS Classes** for custom classes and **ID** for a unique HTML identifier.

### Accessibility

* Give every Login Trigger and Logout Content dropzone a clear text label; do not use an unexplained icon alone.
* Add a visible label or instruction for the password field and make error messages specific enough to understand.
* Keep strong focus indicators and sufficient contrast on inputs, buttons, links, modal content, and the Section overlay.
* Biometric login must remain optional. Keep the password fallback text visible and understandable.
* After publishing, test the complete login, error, redirect, and logout flow with a keyboard and screen reader.

### Tips and Best Practices

* **Use a strong unique password:** Shared access is only as strong as the password you distribute.
* **Publish over HTTPS:** This protects credentials in transit and is required for WebAuthn on normal published domains.
* **Keep Session IDs organised:** Use one stable ID per access group and document where it is used.
* **Choose Remember Device carefully:** Shorter durations are more appropriate for sensitive material or shared computers.
* **Test as a signed-out visitor:** Private browsing prevents an existing session or cookie from hiding setup mistakes.
* **Use full account systems for personal data:** Choose a dedicated membership or authentication service when you need named users, roles, auditing, or password recovery.

### Troubleshooting

#### Published PHP code appears as text

The page is not being processed by PHP. Change its extension to `.php`, publish to PHP-capable hosting, and remove the old `.html` file from the server.

#### Login succeeds but another component stays locked

Confirm that both components use exactly the same Session ID and password. Session IDs are case-sensitive.

#### The old HTML page still opens

Remove the `.html` version from the server and confirm that navigation links point to the `.php` URL.

#### Remember Device does not persist

Check that browser cookies are allowed, PHP sessions work on the server, and the visitor selected the Remember Device option. Retest in a normal browser window.

#### Biometric login is unavailable

Use HTTPS and test in a browser and device that support a platform authenticator. The visitor must first sign in with the password and complete biometric enrolment on that device.

#### Logout does not affect every protected area

Use matching Session IDs or enable **Logout All Sessions**. Enable **Remove Biometric Data** as well when the device’s saved biometric enrolment should be cleared.

### Related Components

* [Button](../components/button.md) — Add a clear Login Trigger or Logout Content control.
* [Modal](../components/modal.md) — Use for general dialogs that do not require password authentication.
* [Form](../components/form/README.md) — Collect visitor information rather than restricting content.

{% include "../../.gitbook/includes/common-controls.md" %}
