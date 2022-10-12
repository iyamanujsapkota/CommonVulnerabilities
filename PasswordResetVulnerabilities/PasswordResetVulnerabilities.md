# Password Reset Vulnerabilities

<img alt="Image" src="./image.jpg">

## Summary

Most of the web application provides users  "password reset" functionality via email. This functionality has given which allow users to recover their account, generate a new password, and repair their own problems. so let’s start and learn how to look for bugs in this function.

### Password Reset Link Not Expiring

It is standard practice to send a password reset link to a user who requests a password change; however, the link should expire after a certain amount of time. If it is not expiring and you can use the password reset link multiple times to reset the password. Then you can consider it as vulnerability.

**Hackerone Reports**

- https://hackerone.com/reports/685007
- https://hackerone.com/reports/898841

### No rate limiting on password reset

Rate limiting is used to control the amount of incoming and outgoing traffic to or from a network. Basically, no rate limit means there is no mechanism to protect against requests you made in a short frame of time. So try to send lots of requests, if it is not blocking you then you can consider it as vulnerability.

**How to Find:**

1. Intercept the password reset request using burp suite
2. Send to intruder (Ctrl+I)
3. Use Numbers Payload

**Hackerone Report**
- https://hackerone.com/reports/838572


### Denial of service when entering a long password

Normally passwords have 8–12–24 or up to 48 digits. if there is no word limit while keeping a password you can consider it as vulnerability. you can check when you setting the password while changing passwords or creating accounts as a long string which can lead to DOS.

**Hackerone Report**

- https://hackerone.com/reports/840598

### Password reset token leak via referer

The HTTP referrer is an optional HTTP header field that identifies the address of the webpage which is linked to the resource being requested. The Referer request-header contains the address of the previous web page from which a link to the currently requested page was followed. So it is possible that the password reset token is leaking via referrer request-header.

**How to Find**

1. Request password reset to your email address
2. Open on the password reset link
3. Make sure you don’t change the password there
4. On Password Reset Page Click On Social Media Links Given Below And Capture The Request Using Burp Suite
5. Check if the referer header is a leaking password reset token

**Hackerone Report**

- https://hackerone.com/reports/751581

