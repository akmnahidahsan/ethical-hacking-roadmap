# 🕸️ Web Security Testing Cheatsheet

> Methodology reference for authorized web application testing (Burp Suite / OWASP ZAP labs, bug bounty programs with permission, or your own lab).

---

## OWASP Top 10 (2021) — Quick Reference

| # | Category | What to check |
|---|---|---|
| A01 | Broken Access Control | Can you access other users' data by changing IDs/params? |
| A02 | Cryptographic Failures | Sensitive data sent/stored unencrypted? Weak TLS config? |
| A03 | Injection | SQLi, XSS, command injection via unsanitized input |
| A04 | Insecure Design | Missing security controls at the architecture level |
| A05 | Security Misconfiguration | Default creds, verbose errors, open directories |
| A06 | Vulnerable Components | Outdated libraries/frameworks with known CVEs |
| A07 | Identification & Auth Failures | Weak password policy, session fixation, no rate limiting |
| A08 | Software & Data Integrity Failures | Unsigned updates, insecure deserialization |
| A09 | Logging & Monitoring Failures | No audit trail for sensitive actions |
| A10 | SSRF | Server can be tricked into requesting internal resources |

## Testing Methodology (mirrors OWASP WSTG)

1. **Information Gathering** — technology stack, robots.txt, sitemap, headers, wappalyzer
2. **Configuration & Deployment Testing** — HTTP methods allowed, TLS config, default files
3. **Identity Management Testing** — registration flow, username enumeration
4. **Authentication Testing** — brute-force protection, password reset flow, MFA bypass
5. **Authorization Testing** — IDOR, privilege escalation, path traversal
6. **Session Management Testing** — cookie flags, session fixation, logout behavior
7. **Input Validation Testing** — XSS, SQLi, command injection, XXE
8. **Error Handling Testing** — stack traces, verbose error messages
9. **Business Logic Testing** — workflow bypass, race conditions
10. **Client-Side Testing** — DOM XSS, CORS misconfig, clickjacking

## Common Manual Checks

| Area | What to try |
|---|---|
| Cookies | `HttpOnly`, `Secure`, `SameSite` flags set? |
| Headers | `Content-Security-Policy`, `X-Frame-Options`, `Strict-Transport-Security` present? |
| Forms | Autocomplete off on sensitive fields? CSRF token present? |
| IDs in URLs | Sequential/guessable IDs → test IDOR by changing them |
| File upload | Extension filtering only (client-side)? MIME-type spoofing possible? |
| Error pages | Do 500 errors leak stack traces or DB info? |

## Burp Suite / ZAP Workflow

```
1. Configure browser proxy → intercept traffic
2. Map the application (spider/crawl)
3. Passive scan for obvious misconfigurations
4. Manually walk through each feature while intercepting
5. Send interesting requests to Repeater/Manual Request Editor
6. Test parameters individually — one variable at a time
7. Document request/response pairs for the report
```

## Safe Practice Targets

- OWASP Juice Shop
- OWASP WebGoat
- PortSwigger Web Security Academy labs
- TryHackMe / Hack The Box web modules

## Reporting Checklist for Each Finding

- [ ] Steps to reproduce
- [ ] Request/response evidence
- [ ] Impact assessment
- [ ] CVSS or severity rating
- [ ] Remediation recommendation

---

**Related:** [Web Application Security phase](../roadmap/09-web-application-security.md) · [Reporting phase](../roadmap/22-reporting.md)
