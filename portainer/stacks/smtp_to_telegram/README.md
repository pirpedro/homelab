Test connection:

```
curl smtp://<hostname>:2525 --mail-from "sender@example.com" --mail-rcpt "recipient@example.com" --upload-file <(echo -e "From: sender@example.com\nTo: recipient@example.com\nSubject: Test Email\n\nThis is a test email sent via cURL.")
```
