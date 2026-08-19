## Day 3: Authentication & Brute-Force Attacks

Today I focused on **authentication vulnerabilities** and practiced exploiting them using **Burp Suite** and PortSwigger Web Security Academy labs.

---

## Topics Covered

* Authentication vulnerabilities
* Username enumeration
* Brute-force attacks
* Intruder in Burp Suite
* Session cookies
* Stay-logged-in functionality
* Authentication responses
* Response differences
* Cookie-based authentication
* Password attacks

---

## Authentication

Authentication is the process of verifying **who a user is**.

Common authentication methods include:

* Username and password
* Multi-factor authentication (MFA)
* Session cookies
* Tokens
* OAuth
* SSO

Weak authentication mechanisms can allow attackers to gain unauthorized access to accounts.

---

## Username Enumeration

Username enumeration occurs when an application behaves differently depending on whether a username exists.

For example:

```text
Invalid username or password
```

versus:

```text
Incorrect password
```

The second response reveals that the username exists.

### Lab Solved

**Username enumeration via subtly different responses**

I identified differences in the application's responses to determine valid usernames and used the discovered information to progress through the lab.

---

## Brute-Force Attacks

A brute-force attack attempts multiple possible passwords until the correct password is found.

A typical attack looks like:

```text
Username + Password List
        ↓
Try Login
        ↓
Analyze Response
        ↓
Identify Successful Login
```

Important factors when identifying a successful brute-force attempt include:

* HTTP status code
* Response length
* Response content
* Redirect behavior
* Error messages

---

## Burp Suite Intruder

I practiced using **Burp Suite Intruder** to automate repeated requests.

### Workflow

1. Capture the login request using Proxy.
2. Send the request to Intruder.
3. Select the parameter to attack.
4. Load the payload list.
5. Start the attack.
6. Compare responses.
7. Identify the request with different behavior.

I initially struggled with Intruder, but eventually figured it out and successfully used it to solve the lab.

---

## Stay-Logged-In Cookies

I also learned how applications can use cookies to keep users authenticated after logging in.

A vulnerable implementation may store information such as:

```text
stay-logged-in=<username>:<encoded-password>
```

If the cookie is predictable or weakly protected, an attacker may be able to manipulate or brute-force it.

### Lab Solved

**Brute-forcing a stay-logged-in cookie**

I analyzed the cookie structure and used Burp Suite to brute-force the value and gain authenticated access.

---

## Labs Completed

### Authentication

* Username enumeration via subtly different responses
* Brute-forcing a stay-logged-in cookie

### Burp Suite

* Practiced Intruder
* Used Intruder for automated requests
* Compared response lengths and behaviors
* Identified successful authentication attempts

---

## Key Takeaways

* Authentication is different from authorization.
* Applications should avoid revealing whether a username exists.
* Response differences can leak useful information to attackers.
* Brute-force attacks can target passwords as well as authentication tokens and cookies.
* Burp Suite Intruder can automate large numbers of requests.
* Authentication cookies should be unpredictable and securely protected.
* Session and persistent-login mechanisms need careful security controls.

---

## What I Learned

Day 3 helped me understand that authentication vulnerabilities are not limited to weak passwords. **Username enumeration, predictable cookies, inconsistent responses, and poorly implemented persistent-login mechanisms can all lead to account compromise.**

I also became more comfortable with **Burp Suite Intruder**, which was initially confusing but became much easier after practicing with the lab.

---

## Progress

**Web Security Journey**

* Web fundamentals
* HTTP requests & responses
* Cookies & sessions
* Authentication & authorization
* Burp Suite Proxy
* Burp Suite Repeater
* Burp Suite Intruder
* Authentication vulnerabilities
* Continuing with PortSwigger Web Security Academy

---