# Burp Suite Notes
**Apex Planet Cybersecurity Internship**

## What is Burp Suite?

Burp Suite is a web application security testing tool that acts as an intercepting proxy between a browser and a web server. It lets you view — and optionally modify — HTTP/HTTPS requests and responses in real time before they reach their destination.

## Why it matters

- Reveals exactly what data a browser sends: headers, cookies, form parameters, authentication tokens.
- Foundational for testing web app vulnerabilities such as parameter tampering, session handling flaws, or hidden form fields.
- Used here purely for interception and inspection of Metasploitable's HTTP traffic (port 80) — no exploitation performed.

## Lab Setup

1. Launch Burp Suite → Temporary project → Use Burp defaults.
2. Configure Kali's browser to route traffic through Burp's proxy at `127.0.0.1:8080`.
3. Enable Intercept in the Proxy tab.
4. Visit `http://192.168.56.101` (Metasploitable's web server) in the proxied browser.
5. Burp captures the raw HTTP request before it's sent — method, URL, headers, and any parameters are visible and editable.
6. Forward the request to let the page load normally.

## Observation

Since Metasploitable serves plain HTTP rather than HTTPS, everything — including any credentials submitted through its login forms — is visible in cleartext inside Burp. This is the same exposure risk covered in the Networking notes' HTTP vs. HTTPS section.

---
*Documented as part of the Apex Planet Cybersecurity Internship lab.*
