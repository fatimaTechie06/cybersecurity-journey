# Day 2: Access Control & Burp Suite

**Focus:** Web Security, Access Control, Burp Suite, PortSwigger Web Security Academy

---

## Objectives

- Understand access control and why it is important.
- Strengthen the difference between authentication and authorization.
- Learn common broken access control scenarios.
- Practice identifying access-control weaknesses using Burp Suite.
- Use Burp Suite Repeater to modify and resend HTTP requests.
- Complete beginner-level access control labs in PortSwigger Web Security Academy.

---

## Concepts Learned

### 1. Authentication vs Authorization

**Authentication** answers:

> Who are you?

It verifies the identity of a user.

**Authorization** answers:

> What are you allowed to do?

It determines which resources or actions a user can access.

A user being authenticated does not automatically mean they are authorized to access every resource or function.

---

### 2. Access Control

Access control is the mechanism used by an application to determine whether a user is allowed to access a particular resource or perform a particular action.

A secure application should enforce these checks on the server side.

---

### 3. Broken Access Control

Broken access control occurs when an application fails to properly enforce authorization rules, allowing users to access resources or perform actions that they should not be permitted to.

Examples include:

- Accessing administrative functionality as a normal user.
- Accessing another user's resources.
- Modifying a request parameter to change privileges.
- Bypassing URL-based restrictions.
- Bypassing restrictions by changing the HTTP method.

---

### 4. Vertical Privilege Escalation

Vertical privilege escalation occurs when a lower-privileged user gains access to functionality intended for a higher-privileged user.

Example:

```text
Normal User
    ↓
Accesses /admin
    ↓
Admin functionality becomes available
```

A properly secured application should prevent this.

---

### 5. Horizontal Privilege Escalation

Horizontal privilege escalation occurs when one user accesses another user's resources or functionality at the same privilege level.

Example:

```text
User A
    ↓
Attempts to access
    ↓
User B's account/data
```

This is closely related to insecure direct object references (IDOR).

---

### 6. Parameter-Based Access Control

Some applications make authorization decisions using values supplied by the client.

Examples include:

```text
?role=user
?admin=false
?user_id=123
```

If the application blindly trusts these values, a user may be able to modify them and gain unauthorized functionality.

For example:

```text
role=user
```

being changed to:

```text
role=admin
```

is dangerous if the server does not independently verify the user's actual privileges.

---

### 7. URL-Based Access Control

Applications may restrict access to sensitive URLs such as:

```text
/admin
/admin/deleteUser
/admin/settings
```

Simply hiding these URLs from normal users is not sufficient security.

The server must verify authorization whenever the resource is requested.

---

### 8. Method-Based Access Control

Access-control rules may sometimes be applied differently depending on the HTTP method.

For example:

```http
POST /admin/deleteUser
```

may be restricted while another HTTP method is accidentally allowed.

This can result in an access-control bypass if the application performs the same sensitive action without consistently enforcing authorization.

---

### 9. Security by Obscurity

Hiding a sensitive URL or making it difficult to guess is not a reliable security mechanism.

For example:

```text
/admin-panel-x7k92
```

is not secure merely because the URL is unpredictable.

Sensitive functionality must still have proper server-side authorization checks.

---

## Practical Work

### Tools Used

- Burp Suite Community Edition
- Burp Proxy
- HTTP History
- Burp Repeater
- Firefox
- PortSwigger Web Security Academy

### Burp Suite Workflow

Used the following workflow while solving the labs:

```text
Application
    ↓
HTTP Request
    ↓
Burp Proxy
    ↓
HTTP History
    ↓
Send request to Repeater
    ↓
Modify request
    ↓
Send request
    ↓
Analyze HTTP Response
```

---

## PortSwigger Labs Completed

The following access-control labs were completed successfully:

- [x] Unprotected admin functionality
- [x] Unprotected admin functionality with unpredictable URL
- [x] User role controlled by request parameter
- [x] User role can be modified in user profile
- [x] URL-based access control can be circumvented
- [x] Method-based access control can be circumvented

---

## What I Practiced

During the labs, I practiced:

- Inspecting HTTP requests.
- Identifying parameters that influence application behavior.
- Sending requests to Burp Repeater.
- Modifying request parameters.
- Modifying HTTP methods.
- Testing restricted URLs in a controlled lab environment.
- Comparing server responses after modifying requests.
- Understanding how authorization decisions can be bypassed when the server trusts client-controlled values.

---

## Key Takeaways

1. **Authentication and authorization are different.**
2. Being logged in does not mean a user is authorized to perform every action.
3. Access control must be enforced on the server side.
4. Client-controlled parameters should not be blindly trusted for authorization decisions.
5. Hiding administrative URLs is not a substitute for proper authorization.
6. Authorization checks should be consistently applied across HTTP methods.
7. Burp Repeater is useful for testing how an application responds to modified requests.
8. Comparing responses is an important skill when investigating web application behavior.

---
