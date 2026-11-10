## Account Takeover through OTP Bypass in TaskBear

## OWASP Top 10
A07:2025 – Authentication Failures

## Description 

While testing the TaskBear registration workflow, I observed that the application allowed progression through the sign-up process even after an invalid OTP was submitted. By intercepting and modifying the server response in Burp Suite, I was able to proceed with the registration flow despite the failed OTP validation.

After completing the remaining registration steps and submitting the form, an account was successfully created, and access to the dashboard was granted. This behavior suggests that OTP verification may not be adequately enforced on the server side. Further investigation is recommended to determine whether email verification is being properly validated before account creation.

## Affected Endpoint 

- **Web Application:** TaskBear
- **Affected URL:** https://taskbear.com.au/auth/sign-up?redirect=/onboarding/address?redirect=%2F

## Proof of Concept (PoC)

### Screenshot 1: Sign-Up Page

