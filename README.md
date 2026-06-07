# Week 5: Active-Footprinting

URL: `https://salah.com/`

<img width="975" height="488" alt="image" src="https://github.com/user-attachments/assets/058b3f0e-4f49-4cd9-a5cc-8b98a9086c06" />

### Domain Enumeration

**1. WHOIS**
   
```
whois salah.com
```

<img width="975" height="483" alt="image" src="https://github.com/user-attachments/assets/d70c2b07-5ba4-46b0-bb4d-3eb251dad195" />

What to find:
- Registrar
- Creation date
- Expiry
- Name servers

### DNS Enumeration

**1. NSLOOKUP**

```
nslookup salah.com
```

<img width="438" height="228" alt="image" src="https://github.com/user-attachments/assets/b6820688-df75-4df2-b792-388ad9f5ad10" />

**2. DIG**

```
dig salah.com
```

<img width="878" height="558" alt="image" src="https://github.com/user-attachments/assets/37718c8f-10d8-46aa-9178-05771c5818a1" />

What to find:
- IP address
- Mail servers (MX)
- Subdomains (if visible)

### Technology Footprinting

**1. Buildwith**

```
buildwith - https://builtwith.com/
```

<img width="975" height="734" alt="image" src="https://github.com/user-attachments/assets/ebd35cb3-8d74-48f2-bed7-99831ba5ccba" />

### Web Header & Basic Info

```
curl -I https://salah.com
```

<img width="561" height="205" alt="image" src="https://github.com/user-attachments/assets/3b6de80a-a671-4129-99b5-2fa701aa793a" />

```
curl https://vulnbank.org/robots.txt
```

What to find:
- Server type & version leakage
- Security headers:
1. X-Frame-Options
2. Content-Security-Policy (CSP)
3. Strict-Transport-Security (HSTS)
- Hidden directories
- Admin panels
- Disallowed paths

### WAF Detection

```
wafw00f https://salah.com
```

<img width="952" height="423" alt="image" src="https://github.com/user-attachments/assets/87b91411-5e7c-4913-9929-45f12416d669" />

What to find:
- Detect Cloudflare / AWS WAF
- Helps understand protection level

### SSL / TLS Info

```
SSLlabs - https://www.ssllabs.com/ssltest/
```

<img width="975" height="639" alt="image" src="https://github.com/user-attachments/assets/e0ee01e9-ed00-4418-8569-bd8cbfe0e07f" />

<img width="936" height="1124" alt="image" src="https://github.com/user-attachments/assets/242c46f5-3446-480e-99a5-a5dcbe3293ba" />

<img width="933" height="147" alt="image" src="https://github.com/user-attachments/assets/f8553a94-9879-4698-bdc8-4929464dcade" />

<img width="933" height="1047" alt="image" src="https://github.com/user-attachments/assets/6633a87d-7b86-4cb6-b6a7-09ac5fe7c854" />

What to find:
- Certificate issuer
- Expiry
- Weak TLS version

## SUMMARY

| Step | Tool | Finding | Interpretation | Mitigation |
|------|------|--------|----------------|-----------|
| WHOIS | `whois` | Domain registrar, creation & expiry date | Shows ownership & lifecycle of domain | Use domain privacy protection |
| DNS Enumeration | `nslookup`, `dig` | IP address, MX records, DNS info | Reveals infrastructure & mail servers | Restrict unnecessary DNS records |
| Subdomain Discovery | Netcraft | Subdomains discovered (if any) | Expands attack surface | Limit exposure of unused subdomains |
| Technology Fingerprinting | BuiltWith, Wappalyzer | Web server, CMS, framework | Identifies technology stack | Keep software updated & patched |
| Web Headers | `curl -I` | Server info, missing security headers | Possible misconfiguration | Implement security headers (CSP, HSTS, XFO) |
| robots.txt | `curl /robots.txt` | Hidden paths (e.g. `/admin`) | Information disclosure | Avoid exposing sensitive paths |
| WAF Detection | `wafw00f` | WAF presence or absence | Indicates security protection level | Implement WAF if missing |
| SSL/TLS Analysis | SSL Labs | Certificate details, TLS version | Detect weak encryption | Enforce strong TLS (1.2/1.3) |
