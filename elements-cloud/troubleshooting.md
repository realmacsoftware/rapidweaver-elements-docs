---
description: A troubleshooting guide for Elements Cloud Issues
icon: cloud-xmark
---

# Troubleshooting

#### Q: I'm unable to Upload to Elements Cloud (The operation could not be completed, Amplify…)

A: This is often due to an issue on the network, it could be down to the network administrators blocking traffic to AWS.

In Terminal.app try running the following command. If there’s no response or high packet loss, your network might be blocking AWS services.

```
ping amplify.aws
```

You can also try opening [https://aws.amazon.com/amplify/](https://aws.amazon.com/amplify/) in your browser. If it doesn’t load or is slow, your network might be restricting access.

If possible connect to another network and try to re-upload your files.&#x20;

If issues persist, try these steps:

1. Log out and back into Elements Cloud.
2. Attempt to send the project to Elements Cloud again.
3. Go to the Help Menu and select **Copy Support Logs**. Send the file to [support@realmacsoftware.com](mailto:support@realmacsoftware.com).

You can also post about any issues you might be having on the [Elements Forum](https://forums.realmacsoftware.com/).
