This script automates the login + 4-digit OTP verification flow and repeatedly submits a hardcoded OTP until the application responds with a successful 2FA bypass (dashboard redirect).

The script relies on session handling and manual redirect inspection (302) to detect success or failure.

## What This Script Does

Logs in using provided email & password

Submits a 4-digit OTP (split into code-1 to code-4)

### Checks server responses:

- Login success → proceeds to OTP

- Redirect to dashboard → 2FA bypass successful

- Redirect to login → OTP failed

- Repeats until success

## Configuration Required

Edit these values in the script before running:

### URLs
login_url       → Login endpoint
otp_url         → OTP verification endpoint
dashboard_url   → Dashboard redirect after successful 2FA

### Credentials
email
password

### Headers

Origin

Referer

Any domain-specific values must match the target app

## OTP Logic

OTP is hardcoded:

otp_str = '1337'


### Digits are sent as:

code-1, code-2, code-3, code-4

## Success Detection Logic

Login success:
Page contains "User Verification" with HTTP 200

### OTP success:
HTTP 302 redirect to dashboard

### OTP failure:

Redirect to login

Login page HTML detected

Session cookies are printed on success

Usage
python3 brute-force.py


Runs indefinitely until a successful OTP bypass occurs.

## Notes

Uses a new session per attempt

Redirects are handled manually (allow_redirects=False)
