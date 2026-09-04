---
description: Chat and edit pages in Elements using your own OpenAI or Anthropic API key
---

# Elements AI Assistant

The Elements AI Assistant lets you chat about your project and edit pages using your own OpenAI or Anthropic (Claude) account. Add your API key in the Elements Preferences to get started.

## Supported providers

| Provider | Features |
| --- | --- |
| OpenAI | Chat and image generation |
| Anthropic (Claude) | Chat |

You can add a key for either provider, or add both. **Image generation requires an OpenAI API key.**

## Add your API key

1. In Elements, open **Settings** to show the Preferences window.
2. Select **AI**, then **API Keys**.
3. Paste your key into the **OpenAI** or **Anthropic** field, depending on your provider.
4. Check that **Key saved** appears beside the field.

The full settings path is **Settings > AI > API Keys**.

<figure><img src="../../.gitbook/assets/elements-ai-api-keys.png" alt="Elements Preferences showing AI > API Keys, with OpenAI supporting Chat and Image Generation and Anthropic supporting Chat"><figcaption><p>Add your OpenAI and Anthropic API keys in Settings > AI > API Keys.</p></figcaption></figure>

To remove a saved key, click **Remove** next to the provider.

## Privacy and billing

Your API keys are stored in the **macOS Keychain**. When you use the assistant, Elements sends your prompts and project context directly to the provider you choose.

Usage is billed to your account with that provider.
