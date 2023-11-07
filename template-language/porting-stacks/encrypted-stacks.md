---
description: How to Identify encrypted stacks
---

# Identify Encrypted stacks

{% hint style="info" %}
The documentation and process detailed here is for third-party **developers only**.
{% endhint %}

If you're trying to convert a stack to an Element and it's not showing up, it might be because the stack you're trying to convert is encrypted. Please re-try the conversion process on your un-encrypted stacks.&#x20;

You can follow the steps below to find out what stacks on your system are encrypted.

### How to check for encrypted stacks

To see if you have any encrypted stacks you can do the following using Terminal.app on your Mac.

1. Open Terminal.app
2. Type "cd " into the terminal window and drag the "stacks" folder in, this will automatically enter the path for you. Then press “Enter”.
3. Now type (or copy and paste the following) exactly as it appears below and press “Enter”.

`grep -ril stackData plist .`

The resulting list will be all your encrypted stacks.

{% embed url="https://youtu.be/7AM9A2t8egg" %}

### How to move encrypted stacks to another folder

The following terminal command will move all the found encrypted stacks to another folder named "EncryptedStacks".

1. Open [Terminal.app](https://terminal.app/)
2. Type "cd " into the terminal window and drag the "stacks" folder in, this will automatically enter the path for you. Then press “Enter”.
3. Run the command below to move all encrypted stacks to the encrypted

{% code overflow="wrap" %}
```
`mkdir "../EncryptedStacks"; files=(); ARRAY=(`find . -name "*.plist" -print0 | xargs -0 grep -l stackData`); for FILE in $ARRAY; do files+=(`echo $FILE | cut -d"/" -f2`); done; STACKS=(`echo $files | tr ' ' '\n' | sort -u`); for FILE in $STACKS; do mv "./$FILE" "../EncryptedStacks/"; done`
```
{% endcode %}

