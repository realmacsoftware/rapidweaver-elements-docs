---
hidden: true
---

# Form Setup for Gmail

Here’s how to correctly set up the Form component in Elements to send email using a Gmail account.

### Generate a Google App Password

Google no longer allows “less secure app access,” so you’ll need to generate a one-time App Password:

1. Go to your [Google Account Security page](https://myaccount.google.com/security)
2. Make sure 2-Step Verification is enabled
3. Scroll down and click App Passwords
4. Select:
   * App: _Mail_
   * Device: _Other_ (e.g. Elements)
5. Click Generate, then copy the 16-character password\


Use this password (not your regular Gmail login) in the Elements form settings.

### Example Gmail Form Setup

| Host         | smtp.gmail.com                         |
| ------------ | -------------------------------------- |
| Port         | 587                                    |
| Encryption   | TLS                                    |
| Username     | you@gmail.com                          |
| Password     | xxxxxxxxxxxxxxxx _(your app password)_ |
| From Name    | Your name                              |
| From Address | you@gmail.com                          |
| Subject      | Subject of the email you'll receive    |
| To Name      | Recipient name                         |
| To Address   | you@gmail.com (or another)             |
