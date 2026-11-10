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

<img width="1006" height="802" alt="image" src="https://github.com/user-attachments/assets/5a5a7aed-8326-411f-b715-af2606a49754" />

### Screenshot 2: OTP Verification Request with Invalid OTP

<img width="887" height="543" alt="image" src="https://github.com/user-attachments/assets/1ef56ef6-5a09-435e-aff7-3f17df53dda7" />

### Screenshot 3: Valid OTP Verification Response

<img width="908" height="745" alt="image" src="https://github.com/user-attachments/assets/7422cf12-5643-40a9-a306-4c8503c8b067" />

### Screenshot 4: Manual Modification of OTP Verification Response with Different user account 

<img width="887" height="797" alt="image" src="https://github.com/user-attachments/assets/49ea470b-2278-467c-a74d-92514be6159f" />


### Screenshot 4: Successful Creation of Account 


<img width="1240" height="847" alt="image" src="https://github.com/user-attachments/assets/5aa713b7-913b-4fbb-b459-6363dfbf91c1" />

<img width="992" height="937" alt="image" src="https://github.com/user-attachments/assets/6d055119-f838-476d-a039-647d443e4b08" />

## Impact

- A user may be able to complete the sign-up process without entering the correct email OTP.
- Accounts could be created with email addresses that have not been verified if the server does not properly check the OTP.
- The application's email verification process may be bypassed without confirming ownership of the email address.

## Remediation

1. **Verify OTP on the Server:** The backend should check whether the OTP is correct before marking the email address as verified.
2. **Improve OTP Security:** Link each OTP to the correct email address and registration session. OTPs should expire after a set time, and repeated incorrect attempts should be limited.
3. **Block Unverified Accounts:** Do not activate the account or allow access to protected features until the server confirms that email verification was successful.

