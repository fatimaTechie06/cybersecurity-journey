# Day 12 - DevSecOps: Audit Listening Services

**Course:** Linux Security for DevSecOps  
**Lab:** 1 - Audit Listening Services  

## Objective

The goal of this lab was to audit active listening services on a Linux host and classify them based on whether they were publicly exposed or restricted to the local machine.

The exercise focused on understanding the difference between network-wide and localhost-only service bindings.

## Tasks Performed

### 1. Inspect Listening Services

Used the `ss` command to display TCP listening sockets and the processes associated with them:

```bash
ss -lntp
```

Important options:

- `-l` - Show listening sockets
- `-n` - Show numerical addresses and ports
- `-t` - Show TCP sockets
- `-p` - Show the process using the socket

The command displayed several listening services, including:

```text
0.0.0.0:18080
127.0.0.1:18081
0.0.0.0:22
[::]:22
```

### 2. Understand Service Exposure

The important distinction was between:

```text
0.0.0.0:18080
```

and:

```text
127.0.0.1:18081
```

`0.0.0.0` indicates that the service is listening on all IPv4 network interfaces, making it potentially reachable from other hosts depending on firewall and network configuration.

`127.0.0.1` is the localhost loopback address. A service bound only to `127.0.0.1` is intended to be accessible from the local machine rather than directly from external hosts.

### 3. Create a Service Classification File

Created and edited:

```text
service-classification.txt
```

The required format was:

```text
Public: <address>:<port>
Local-only: <address>:<port>
```

The final classification was:

```text
Public: 0.0.0.0:18080
Local-only: 127.0.0.1:18081
```

The file was verified using:

```bash
cat service-classification.txt
```

## Commands Practiced

```bash
ss -lntp
cat
sed
```

Also practiced creating file content using a heredoc:

```bash
cat > service-classification.txt << 'EOF'
Public: 0.0.0.0:18080
Local-only: 127.0.0.1:18081
EOF
```

## Troubleshooting

While editing the file with `sed`, I initially made a syntax error:

```text
sed: -e expression #1, char 33: unterminated 's' command
```

I corrected the command syntax and successfully produced the required classification file.

This was a useful reminder that small syntax errors in command-line tools can change the result or prevent a command from executing.

## Key Concepts Learned

- `ss` can be used to inspect active network sockets.
- Listening services represent part of a system's network attack surface.
- `0.0.0.0` and `127.0.0.1` have very different exposure implications.
- A publicly listening service is not automatically vulnerable, but it should be intentionally configured and secured.
- Local-only services can reduce unnecessary network exposure.
- Runtime evidence from active socket bindings is more reliable for exposure auditing than assumptions based only on service names or documentation.
- Service exposure is an important consideration in Linux security and DevSecOps.

## Security Takeaway

A key lesson from this lab was:

> **A service should only be exposed to the network when that exposure is necessary and intentionally secured.**

Auditing listening services helps administrators identify unnecessary exposure and provides a useful baseline for system hardening and security reviews.

## Reflection

This was my first hands-on lab from the **Linux Security for DevSecOps** course. It connected my Linux and networking knowledge with a practical security task.

I learned how to inspect live network listeners, understand IP binding, classify service exposure, and document the result for a security audit.
