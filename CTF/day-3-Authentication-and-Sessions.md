# Day 3: Authentication & Session Security

**Focus:** Authentication, Sessions, Session Management, Burp Suite

---

## Objectives

- Understand how web application authentication works.
- Understand how authenticated sessions are maintained.
- Inspect authentication and session-related HTTP requests using Burp Suite.
- Learn common session security concepts.
- Get introduced to Burp Intruder for automated request testing.

---

## Concepts Learned

### 1. Authentication

Authentication answers:

> Who are you?

A web application typically verifies a user's credentials during login before creating an authenticated session.

Basic flow:

```text
User
 ↓
Login form
 ↓
POST /login
 ↓
Server verifies credentials
 ↓
Authentication successful
 ↓
Session created
```

### 2. Authentication Flow

```text
Username + Password
        ↓
   POST /login
        ↓
 Server verifies credentials
        ↓
 Authentication successful
        ↓
 Server creates session
        ↓
 Set-Cookie: session=...
        ↓
 Browser stores cookie
        ↓
 Cookie sent with future requests
        ↓
 Server identifies authenticated session
```

The password is normally used during authentication, while the resulting session identifier maintains the authenticated state.

---

## 3. Session Cookies

After successful authentication, a server may send:

```http
Set-Cookie: session=abc123
```

The browser then sends the cookie with subsequent requests:

```http
GET /my-account HTTP/2
Cookie: session=abc123
```

The server can use the session identifier to determine which authenticated session the request belongs to.

---

##  4. Session Lifecycle

```text
LOGIN
  ↓
Credentials verified
  ↓
Session created
  ↓
Session ID issued
  ↓
Browser stores cookie
  ↓
Cookie sent with requests
  ↓
Server identifies session
  ↓
Protected resources accessed
  ↓
LOGOUT
  ↓
Session invalidated
```

Each stage can introduce security risks if implemented incorrectly.

---

## 5. Session Security Concepts

### Session Fixation

Session fixation occurs when an attacker is able to cause a victim to use a session identifier that the attacker already knows.

### Session Hijacking

Session hijacking occurs when an attacker obtains a valid session identifier and uses it to impersonate the associated user.

### Session Expiration

Authenticated sessions should not remain valid indefinitely. Expiration can reduce the impact of stolen or abandoned sessions.

### Session Invalidation

When a user logs out, the application should invalidate the relevant session so that the previous session identifier can no longer be used to access protected resources.

---

## 6. Secure Cookie Concepts

Authentication cookies can include security-related attributes such as:

```text
Secure
HttpOnly
SameSite
```

These attributes influence how browsers transmit and expose cookies and can help reduce certain attacks when configured correctly.

---

## Burp Suite Practice

### Tools Used

- Burp Suite Community Edition
- Proxy
- HTTP History
- Repeater
- Intruder
- Firefox

### Authentication Request Inspection

Practiced inspecting authentication-related HTTP requests and understanding the relationship between:

```text
Login Request
     ↓
Authentication Response
     ↓
Set-Cookie
     ↓
Authenticated Request
     ↓
Session Cookie
```

### Session Cookie Inspection

Examined how an authenticated request can contain a session cookie:

```http
GET /my-account HTTP/2
Cookie: session=abc123
```

---

## Burp Intruder

Introduced Burp Intruder as a tool for automatically sending multiple variations of an HTTP request.

Basic concept:

```text
Original Request
      ↓
Mark variable parameter
      ↓
Provide payload list
      ↓
Intruder sends variations
      ↓
Compare responses
```

Intruder was attempted during the authentication lab practice.

The practical brute-force portion of the authentication labs was not completed.

---

## PortSwigger Practice

Attempted authentication/session-related labs involving automated username/password testing.

The labs were not fully completed because the remaining steps required brute-force or automated request attacks.

Rather than continuing without understanding the underlying concepts, the focus was shifted toward understanding authentication and session management.

---

## Key Takeaways

1. Authentication determines the identity of a user.
2. Authorization determines what an authenticated user is allowed to access.
3. Sessions allow applications to maintain authentication state across multiple HTTP requests.
4. Session cookies are commonly used to associate requests with authenticated sessions.
5. A session identifier should be protected because possession of a valid session identifier can allow impersonation.
6. Session fixation and session hijacking are different session security threats.
7. Sessions should have appropriate expiration and invalidation mechanisms.
8. Burp Repeater is useful for manually inspecting and modifying authentication/session requests.
9. Burp Intruder can automate repeated request variations and is useful for controlled authentication testing.

---