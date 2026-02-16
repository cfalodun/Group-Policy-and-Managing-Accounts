# <p align="center">Group Policy and Managing Accounts
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

## Objective

Configure account lockout policies using Group Policy, manage user account states (lock, unlock, disable, enable), and observe authentication-related security logs in Active Directory and client systems.

---

# Part 1 – Account Lockout Policy

## Step 1 – Simulate Failed Login Attempts

- Logged into **DC-1**
- Selected a previously created domain user
- Attempted login with incorrect password multiple times

Configured Group Policy to enforce account lockout after 5 failed attempts.

<img src="https://i.postimg.cc/BQ9J8Fx8/01-gpo-account-lockout-threshold.png" width="500">

Applied policy update on Client-1:

<img src="https://i.postimg.cc/rFXqd4S0/02-client1-gpupdate-force.png" width="500">

Attempted login 6 times with incorrect password.

---

## Step 2 – Account Lockout Observed

Login attempt failed due to account lockout:

<img src="https://i.postimg.cc/L6KmqPzZ/03-login-attempt-account-locked.png" width="500">

Verified account shows as locked in Active Directory:

<img src="https://i.postimg.cc/ZKtJ9Nrv/04-ad-account-locked-out.png" width="500">

---

## Step 3 – Unlock & Reset Password

- Unlocked account
- Reset password

<img src="https://i.postimg.cc/YqKt4F1F/05-ad-account-unlocked-password-reset.png" width="500">

Attempted login again successfully:

<img src="https://i.postimg.cc/sDd3BWp5/06-login-success-after-unlock.png" width="500">

---

# Part 2 – Disabling & Enabling Accounts

## Step 1 – Disable Account

Disabled the same domain user account in Active Directory.

<img src="https://i.postimg.cc/rFXqd4SW/07-ad-account-disabled.png" width="500">

Attempted login and observed error:

<img src="https://i.postimg.cc/SNFmX9WC/08-login-failed-account-disabled.png" width="500">

---

## Step 2 – Re-enable Account

Re-enabled the account in Active Directory.

<img src="https://i.postimg.cc/SNFmX9WW/09-reenable-account.png" width="500">

Login functionality restored.

---

# Part 3 – Observing Security Logs

Reviewed authentication logs:

- Domain Controller (Event Viewer)
- Client-1 Event Viewer

Observed account lockout events.

<img src="https://i.postimg.cc/PrsdLDmb/10-event-viewer-account-lockout.png" width="500">

---

# Key Concepts Demonstrated

- Configuring Account Lockout Threshold via Group Policy
- Applying Group Policy updates
- Account lockout behavior
- Unlocking and resetting user accounts
- Disabling and enabling domain accounts
- Authentication event monitoring
- Security log analysis fundamentals

---

# Operational Insight

Understanding account lockout behavior and authentication logging is foundational for:

- Help Desk troubleshooting
- Identity and Access Management (IAM)
- Security Operations
- Cybersecurity incident response
