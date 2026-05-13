# Authentication Vulnerabilities

## 1. What is Authentication?
Authentication is the process of verifying the identity of a user or client.
(The website checks whether the person trying to log in is really the correct user or not.)

**Example**
Suppose a user enters:
- Username: Carlos123
- Password: mypassword

The website checks:
- Does this username exist?
- Is the password correct?

If both are correct: **Access Granted**  
If incorrect: **Access Denied**

## 2. Why Authentication is Important
- Websites are available on the internet for everyone.
- Because of this:
    - Attackers can also try to access accounts
    - Websites must verify users properly
- Weak authentication can allow unauthorized access

**Authentication is one of the most important parts of web security.**

## 3. Types of Authentication
There are mainly 3 types of authentication factors.

### 3.1 Something You Know
This means information only the user should know.

**Examples:**
- Password
- PIN
- Security question answer

These are called: **Knowledge Factors**

**Example**
- Password: Hello@123

The website assumes:
> "If the user knows the password, then they are the real user."

### 3.2 Something You Have
This means a physical object the user owns.

**Examples:**
- Mobile phone
- OTP device
- Security token
- Smart card

These are called: **Possession Factors**

**Example**
- OTP sent to mobile phone

Only the real user should have access to that phone.

### 3.3 Something You Are or Do
This is based on biometrics or behavior.

**Examples:**
- Fingerprint
- Face recognition
- Voice recognition
- Typing pattern

These are called: **Inherence Factors**

## 4. Authentication vs Authorization
Many beginners confuse these two terms.

| Authentication | Authorization |
| :--- | :--- |
| Checks: *"Who are you?"* | Checks: *"What are you allowed to do?"* |
| Verifies the identity of the user. | Verifies permissions. |

**Example**

**Step 1 — Authentication**
- User logs in with:
    - Username: Carlos123
    - Password: pass123
- Website verifies credentials.
- If correct: User authenticated successfully

**Step 2 — Authorization**
- Now website checks permissions.
- Example questions:
    - Can the user delete accounts?
    - View admin panel?
    - Edit other users?
- If not allowed: **Access Denied**

## 5. How Authentication Vulnerabilities Arise
Authentication vulnerabilities mainly happen in 2 ways.

### 5.1 Weak Authentication Mechanisms
The website does not properly protect against attacks like:
- Brute-force attacks
- Password guessing
- Username enumeration

**Example**
If a website allows unlimited login attempts:
> Attacker can try thousands of passwords

### 5.2 Broken Authentication Logic
Sometimes developers make coding mistakes.
These mistakes allow attackers to bypass authentication completely.
This is called: **Broken Authentication**

**Example**
Suppose developer writes incorrect login logic.
> Attacker may log in without knowing password.

## 6. Impact of Vulnerable Authentication
Authentication vulnerabilities are very dangerous.

**Possible Impacts**

- **6.1 Account Takeover**  
  Attacker gains access to another user's account.

- **6.2 Access to Sensitive Data**  
  Attacker may access:
    - Personal information
    - Business data
    - Private messages

- **6.3 Admin Account Compromise**  
  If attacker gains admin access:
    - Full website compromise may happen
    - Possible actions:
        - Delete users
        - Modify database
        - Access internal systems

- **6.4 Additional Attack Surface**  
  Even low-level accounts may expose hidden pages.
  These pages may contain more vulnerabilities.

## 7. Password-Based Login Systems
Most websites use username + password login systems.

**Login Flow**
1. User enters: Username + Password
2. Website checks database.
3. If credentials are correct: User logged in
4. If incorrect: Login failed

## 8. Brute-Force Attacks
A brute-force attack means:
> Trying many usernames and passwords repeatedly until correct credentials are found.

**Attack Process**

1. Attacker prepares username list (e.g., admin, administrator, carlos, john, support).
2. Attacker prepares password list (e.g., 123456, password, admin123, welcome, qwerty).
3. Automated tools try combinations rapidly.

**Why Brute Force Works**
Many users choose weak passwords like:
- password123
- admin123
- hello123

These are easy to guess.

## 9. Brute-Forcing Usernames
Usernames are often predictable.

**Common Username Patterns**
- Email Format: `firstname.lastname@company.com`
- Predictable Admin Names: admin, administrator, root, support

**Information Disclosure**
Sometimes websites accidentally expose usernames.

**Example Sources**
- Public user profiles
- HTTP responses
- Support pages
- Email leaks

## 10. Brute-Forcing Passwords
Attackers also try guessing passwords.

## 11. Password Policies
Websites often require strong passwords.

**Common Password Rules**
- Minimum Length (e.g., at least 8 characters)
- Uppercase + Lowercase Letters (e.g., HelloWorld)
- Special Characters (e.g., Hello@123)

## 12. Human Behavior Weakness
Even with strong password rules, users still create predictable passwords.

**Example**
- Original password: `mypassword` (rejected)
- User changes it to: `Mypassword1!`

This still follows a predictable pattern.

**More Examples**
- `Mypassword1?`
- `Mypassword2!`
- `Myp4$$w0rd`

Attackers know these patterns. This makes brute-force attacks more effective.

## 13. Username Enumeration
Username enumeration means:
> Finding valid usernames by observing website behavior

**Why It is Dangerous**
If attacker knows valid usernames:
> Brute-force attack becomes much easier

## 14. How Username Enumeration Happens
It usually happens in:
- Login forms
- Registration forms
- Forgot password pages

## 15. Username Enumeration Through Status Codes
Different HTTP status codes may reveal valid usernames.

**Example**
- Invalid Username: `HTTP/1.1 401 Unauthorized`
- Valid Username but Wrong Password: `HTTP/1.1 200 OK`

**Why This is Dangerous**
Different responses indicate: Username exists

## 16. Username Enumeration Through Error Messages
Different error messages may expose valid usernames.

**Example**
- **Case 1** (Invalid Username): `Invalid username`
- **Case 2** (Valid Username but Wrong Password): `Incorrect password`

**Why This is Dangerous**
Attacker learns: Username is correct. Now attacker only needs password.

## 17. Username Enumeration Through Response Time
Sometimes websites process valid usernames differently. This creates response time differences.

**Example**
- Invalid Username: Website immediately rejects request. Response time: ~100 ms
- Valid Username: Website additionally checks password. Response time: ~500 ms

**Why This Happens**
Extra password verification takes more time. Attackers measure these delays to identify valid usernames.

## 18. Long Password Timing Attack
Attackers may submit extremely long passwords.
- Example:
`aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa`

**Why?**
- If username is valid:
    - Website processes long password
    - More computation happens
    - Response becomes slower
- This helps attacker identify valid usernames.

![Username enumeration via different responses lab](image.png)
