# Active Directory: Group Policy and Managing Accounts

<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

## Project Summary

This project demonstrates how Group Policy is used to manage account security and control user access in an Active Directory environment.

An account lockout policy was configured to lock users after repeated failed login attempts. The behavior of locked accounts was tested, followed by unlocking and password resets. Additional account management actions such as disabling and re-enabling users were performed. Authentication activity was then reviewed using Event Viewer to observe how these actions are logged.

---

## Environment & Tools

### Environment
- Microsoft Azure Virtual Machines
- Windows Server (Domain Controller – DC-1)
- Windows 10 (Client-1)

### Technologies Used
- Active Directory
- Group Policy Management
- Event Viewer
- PowerShell (gpupdate)

---

## Demonstration

# Part 1: Account Lockout Policy

## Step 1: Configure Account Lockout Policy

On **DC-1**, open **Group Policy Management** and configure an account lockout policy.

### Steps:
1. Open **Group Policy Management**
2. Edit the appropriate Group Policy Object (Default Domain Policy or a custom GPO)
3. Navigate to:

```
Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Account Lockout Policy
```

4. Set **Account lockout threshold** to **5 invalid logon attempts**

<img src="https://i.postimg.cc/BQ9J8Fx8/01-gpo-account-lockout-threshold.png" width="500">

This setting ensures that an account will be locked after 5 failed login attempts.

---

## Step 2: Apply Group Policy Update

On **Client-1**, force a Group Policy update.

### Steps:
1. Open Command Prompt or PowerShell
2. Run:

```powershell
gpupdate /force
```

<img src="https://i.postimg.cc/rFXqd4S0/02-client1-gpupdate-force.png" width="500">

This ensures the new policy is applied immediately instead of waiting for the automatic refresh cycle.

---

## Step 3: Simulate Failed Login Attempts

Attempt to log in to **Client-1** using a domain user account with the wrong password multiple times.

- Enter an incorrect password at least **6 times**

This exceeds the configured threshold and triggers account lockout.

---

## Step 4: Observe Account Lockout

After exceeding the failed login limit, the account becomes locked.

<img src="https://i.postimg.cc/L6KmqPzZ/03-login-attempt-account-locked.png" width="500">

Verify the lockout status in Active Directory:

<img src="https://i.postimg.cc/ZKtJ9Nrv/04-ad-account-locked-out.png" width="500">

This confirms that the Group Policy is working as intended.

---

## Step 5: Unlock Account and Reset Password

On **DC-1**, unlock the account and reset the password.

### Steps:
1. Open **Active Directory Users and Computers**
2. Locate the user account
3. Right-click → **Properties**
4. Unlock the account
5. Reset the password

<img src="https://i.postimg.cc/YqKt4F1F/05-ad-account-unlocked-password-reset.png" width="500">

Attempt login again on **Client-1**:

<img src="https://i.postimg.cc/sDd3BWp5/06-login-success-after-unlock.png" width="500">

Successful login confirms the account has been restored.

---

# Part 2: Disabling and Enabling Accounts

## Step 1: Disable the Account

On **DC-1**, disable the same user account.

### Steps:
1. Open **Active Directory Users and Computers**
2. Right-click the user account
3. Select **Disable Account**

<img src="https://i.postimg.cc/rFXqd4SW/07-ad-account-disabled.png" width="500">

Attempt to log in with the disabled account:

<img src="https://i.postimg.cc/SNFmX9WC/08-login-failed-account-disabled.png" width="500">

The login fails, confirming the account is inactive.

---

## Step 2: Re-enable the Account

Re-enable the account in Active Directory.

### Steps:
1. Right-click the user account
2. Select **Enable Account**

<img src="https://i.postimg.cc/SNFmX9WW/09-reenable-account.png" width="500">

Login functionality is restored after re-enabling the account.

---

# Part 3: Reviewing Security Logs

## Step 1: Open Event Viewer

On both **DC-1** and **Client-1**, open **Event Viewer**.

### Steps:
1. Open **Event Viewer**
2. Navigate to:

```
Windows Logs → Security
```

---

## Step 2: Review Authentication Events

Look for events related to:
- Failed login attempts
- Account lockouts
- Successful logins

<img src="https://i.postimg.cc/PrsdLDmb/10-event-viewer-account-lockout.png" width="500">

These logs provide visibility into authentication activity and are critical for troubleshooting and security monitoring.
