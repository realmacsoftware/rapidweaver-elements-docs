---
description: Configure and use the Pro AI writing tools inside the Online Editor.
icon: sparkles
---

# AI Writing Assistant

The **AI Writing Assistant** is a Pro feature for the Online Editor. It adds writing tools directly to the WYSIWYG Markdown editor, so editors can rewrite, continue, summarise, translate, fix grammar, or run a custom prompt without leaving the page they are editing.

The feature uses your own AI provider account. Elements CMS does not include bundled AI usage or bill you for generated text; the site owner brings an API key from Anthropic, OpenAI, or Google and pays that provider directly.

### Requirements

To use the AI Writing Assistant, your site needs:

* An active **Pro** license.
* The Online Editor running on PHP 8.1 or newer, including the `curl` extension.
* An owner account to configure AI settings.
* An API key from Anthropic, OpenAI, or Google.

The editor stores provider keys on your server. When PHP `libsodium` is available, keys are encrypted at rest. If `libsodium` is not available, the Online Editor shows a warning before storing keys in plaintext.

### Set up an AI provider

Sign in to the Online Editor as an owner, then open **AI → Providers**.

1. Choose a provider: **Anthropic**, **OpenAI**, or **Google**.
2. Paste the provider API key.
3. Click **Save key**.
4. Choose the default text provider and model.

The Online Editor verifies the key before saving it, so obvious provider authentication errors appear during setup instead of the first time an editor tries to generate text.

#### How to generate and use an OpenAI API key

Learn how to generate an OpenAI API key and add it to the Markdown Editor for the AI Writing Assistant.

{% embed url="https://youtu.be/Vx6Nbb3lN3Y" %}

#### How to generate and use a Claude API key

Learn how to generate an Anthropic Claude API key and add it to the Markdown Editor for the AI Writing Assistant.

{% embed url="https://youtu.be/VqQjN8TYIRw" %}



### Enable the writing assistant

After saving a provider key, open **AI → Features**.

1. Turn on **AI features enabled**.
2. Enable **Writing assistant**.
3. Optionally add **Custom instructions** for the site.

Custom instructions are sent with every writing-assistant request. Use them for house style, audience, language preference, words to avoid, or other guidance the AI should always follow.

{% hint style="info" %}
Turning off the master **AI features enabled** switch disables the writing assistant and prevents the Online Editor from calling any configured AI provider.
{% endhint %}

### Use the writing assistant

Open a Markdown file in the Online Editor. When the feature is enabled, a Sparkles button appears in the editor toolbar. When you select text, the same Sparkles action is also available from the selection bubble.

Some actions require selected text. Rewrite, summarise, translate, and grammar fixes work on the current selection. **Continue writing** and **Custom prompt** can also work from the current cursor position or surrounding document context.

When you run an action, the Online Editor shows a suggestion before changing the document. Choose:

* **Accept** to apply the suggestion.
* **Reject** to close it without changing the document.
* **Try again** to generate a new suggestion with the same action.

{% hint style="warning" %}
The Sparkles button is available in the WYSIWYG Markdown editor. It does not appear while editing in raw Markdown mode.
{% endhint %}

### Available actions

The AI Writing Assistant includes:

* **Rewrite → Professional** — rewrites selected text in a more professional tone.
* **Rewrite → Friendly** — rewrites selected text in a warmer, friendlier tone.
* **Rewrite → Concise** — shortens selected text while preserving the meaning.
* **Rewrite → Expand** — adds detail and context to selected text.
* **Continue writing** — continues from the current document context.
* **Summarise** — summarises selected text.
* **Translate** — translates selected text into a chosen language.
* **Fix grammar & spelling** — corrects selected text without changing its meaning.
* **Custom prompt** — follows your instruction while preserving Markdown.

### Troubleshooting

**I do not see the AI page.**\
AI features require Pro. Open **Workspace → License** and confirm the site has an active Pro license.

**I do not see the Sparkles button in the editor.**\
Check **AI → Features** and confirm both **AI features enabled** and **Writing assistant** are turned on. The button is hidden in raw Markdown mode.

**The writing assistant says no API key is configured.**\
Open **AI → Providers**, save a provider API key, and confirm that provider is selected as the default text provider.

**The provider key will not save.**\
Confirm the key is valid with the provider, then check that the server has outbound HTTPS access and the PHP `curl` extension is enabled.

**Generated text does not match the site voice.**\
Add or revise **Custom instructions** under **AI → Features**. Keep instructions short and direct, for example: "Write in British English for a small-business audience. Be clear, practical, and avoid hype."
