# Flaws2.cloud — Level 1

## 1. Service(s) Involved
- API Gateway
- IAM
- AWS STS (temporary credentials)
- S3

---

## 2. Initial Access / Starting Point
Started with a public web page containing a form that submitted requests to an API Gateway endpoint.

The page performed client-side JavaScript input validation before sending requests.

---

## 3. Vulnerability / Misconfiguration
The backend API returned an overly verbose error response that exposed temporary AWS credentials (Access Key ID, Secret Access Key, and Session Token).

Sensitive credentials were disclosed to an unauthenticated user.

---

## 4. Identity Gained (IMPORTANT)
Temporary AWS credentials obtained through AWS STS.

These credentials were used to configure a new AWS CLI profile and authenticate as the leaked identity.

---

## 5. Attack Path (2–4 steps max)
1. Inspected the web application and identified the API Gateway endpoint.
2. Bypassed client-side validation by sending unexpected input directly to the API.
3. Received an error response containing temporary AWS credentials.
4. Configured an AWS CLI profile with the leaked credentials and accessed the S3 bucket containing the next challenge.

---

## 6. Why It Worked (Key Insight)
The application's error handling crossed a trust boundary by exposing valid temporary AWS credentials to an unauthenticated client.

Once those credentials were leaked, AWS treated the attacker as the associated IAM principal.

---

## 7. Impact
An attacker could:
- Authenticate to AWS as the leaked identity.
- Enumerate resources permitted by that identity.
- Access sensitive S3 objects.
- Potentially pivot further if the temporary credentials had broader permissions.

The overall impact depends on the permissions attached to the leaked credentials.

---

## 8. Detection Idea
Potential detection opportunities include:
- CloudTrail showing API activity from an unexpected IP address using the leaked temporary credentials.
- Monitoring for unusual S3 object access by the compromised identity.
- Alerting on abnormal use of temporary credentials outside expected application behavior.

---

## 9. Prevention / Fix
- Never expose credentials in application responses or error messages.
- Return generic error messages to clients.
- Log detailed debugging information only on the server side.
- Follow least privilege so any temporary credentials have minimal permissions.
- Review error handling to ensure sensitive data is sanitized before responses are returned.

---

## 🔥 10. Security Engineer Note
"This is a case of improper error handling leading to credential disclosure because sensitive temporary AWS credentials were included in a client-facing error response."

---

## 📚 Lessons Learned
- Client-side validation is not a security control.
- Error messages can leak sensitive information.
- Temporary credentials are still credentials and must be protected.
- Always inspect browser developer tools and network traffic when assessing web applications.
- Leaked credentials should immediately prompt you to ask "What can this identity do?" rather than "What service am I attacking?"