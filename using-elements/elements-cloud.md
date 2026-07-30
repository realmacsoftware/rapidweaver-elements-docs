---
description: Sign up for a free Elements Cloud account
icon: cloud-check
---

# Elements Cloud

Every Elements Cloud account comes with **1 GB of free cloud storage**. An active licence is required for continued use of Elements Cloud. You can sign up in the app.

Elements Cloud gives every user a simple, reliable place to **store purchased products**, **back up their projects, and share** them when needed.

{% embed url="https://youtu.be/dBj6pkVy2-4" %}

Below are instructions on [how to sign up](elements-cloud.md#account-sign-up) for a free account and [share or back up your project](elements-cloud.md#sharing-projects).

{% hint style="warning" %}
An active subscription is required to use Elements Cloud.
{% endhint %}

### Account Sign-Up

You can sign-up (or sign-in) to your account in the Account Preferences within Elements. Simply enter your email address and click the "Send Sign-in Link" button. An account will be created for you, or you will be logged in (if you already have an account).

<figure><img src="../.gitbook/assets/CleanShot 2024-09-10 at 1 .34.01@2x.png" alt="Elements Account preferences with an email field and Send Sign-In Link button"><figcaption><p>Elements Account Sign-up</p></figcaption></figure>

A link will be sent to the email address you entered, click this email link within 3 minutes to register or log in to your account.

<figure><img src="../.gitbook/assets/CleanShot 2024-09-10 at 1 .35.27@2x.png" alt="Elements Account preferences waiting for the emailed sign-in link"><figcaption><p>Elements Account Sign-up</p></figcaption></figure>

Once you are signed in, you can share the open project using the Cloud icon in the Elements toolbar. You can manage uploaded files and storage from the Account preferences.

<figure><img src="../.gitbook/assets/CleanShot 2024-09-10 at 2 .09.44@2x.png" alt="Elements Account preferences showing uploaded documents and storage usage"><figcaption></figcaption></figure>

Every Elements Cloud account comes with 1GB of free cloud storage. This is the perfect place to make backups and upload files for sharing.

### Sharing Projects

Once you are [signed in to your Elements Cloud account](elements-cloud.md), you can share the open project using the Cloud icon in the Elements toolbar.

To upload your project to Elements Cloud, just follow these steps:

1. Open your project in Elements.
2. Click the "Cloud" share button in the top-left corner.
3. Press the "Upload Project" button in the pop-over window.
4. Once the upload is complete, you can share the link to your project.

<figure><img src="../.gitbook/assets/CleanShot 2025-07-22 at 9 .44.45@2x.png" alt="Elements Cloud toolbar menu with controls to copy, download, open or delete a project"><figcaption></figcaption></figure>

#### Converting an Elements App link to a direct download

To generate a direct download link from an Elements App link, simply append the unique identifier from the original link to the elementsapp.cloud URL.

* Elements App link: `elementsapp://downloadDocument/UNIQUE-ID`

* Direct download link: `https://dl.elementsapp.cloud/g/UNIQUE-ID`



### Troubleshooting

A troubleshooting guide for Elements Cloud Issues.

<details>

<summary>I'm unable to Upload to Elements Cloud</summary>

This is often caused by a network administrator blocking traffic to AWS. You may see an error message like the following:

```
The operation could not be completed, Amplify…
```

In Terminal.app try running the following command. If there’s no response or high packet loss, your network might be blocking AWS services.

```
ping amplify.aws
```

You can also try opening [https://aws.amazon.com/amplify/](https://aws.amazon.com/amplify/) in your browser. If it doesn’t load or is slow, your network might be restricting access.

If possible, connect to another network and try uploading your files again.

If issues persist, try these steps:

1. Log out and back into Elements Cloud.
2. Attempt to send the project to Elements Cloud again.
3. Go to the Help Menu and select **Copy Support Logs**. Send the file to [support@realmacsoftware.com](mailto:support@realmacsoftware.com).

You can also post about any issues you might be having on the [Elements Forum](https://forums.realmacsoftware.com/).

</details>

<details>

<summary>"Elements Cloud service has encountered an error…" message</summary>

This is often caused by an app or network administrator blocking traffic to AWS. You may see an error message like the following:

<figure><img src="../.gitbook/assets/Screenshot 2025-11-14 at 11.48.35 AM.png" alt="Elements Cloud window displaying a service error message"><figcaption></figcaption></figure>

```
Elements Cloud service has encountered an error.
```

Check whether anything installed on your Mac filters or blocks network traffic. Tools such as **Little Snitch**, **NetBarrier**, **Radio Silence** and some antivirus packages can quietly block app requests and cause behaviour like this.

{% hint style="danger" %}
**NetBarrier** constantly monitors network activity whether the application is running or not, which means its network extension can persist even when the main app is disabled.

**Ensure the NetBarrier network extension is fully disabled,** before trying again.
{% endhint %}

If you’re running any of those, try temporarily disabling them or adding Elements to the allow list. If possible connect to another network and try to log-in again.

If issues persist, please contact [support@realmacsoftware.com](mailto:support@realmacsoftware.com).

</details>
