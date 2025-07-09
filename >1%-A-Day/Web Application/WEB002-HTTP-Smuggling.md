---
ID: WEB002
Date: 2025-06-29
Tags: #http #smuggling #websecurity #burp
Category: Web Application
---

# WEB002 – HTTP Request Smuggling

## 🧠 What I Learned

**HTTP Request Smuggling** is a vulnerability that exploits **inconsistent parsing** of HTTP requests between two systems, typically between a front-end proxy (like a load balancer) and a back-end server (like Apache or Node.js).

By crafting a specially structured request, attackers can "smuggle" a hidden HTTP request past security filters and manipulate how the backend processes it.

---

## 🔍 How It Works

Web architectures often include:

- A **frontend (reverse proxy)** – like Nginx, Varnish, or HAProxy
- A **backend (origin server)** – like Apache, Express, or Tomcat

Both parse headers like `Content-Length` and `Transfer-Encoding`. If they **disagree** on how to handle the request body, the attacker can exploit this desynchronization.

---

## 💣 Example: CL.TE Attack (Content-Length vs Transfer-Encoding)

```http
POST / HTTP/1.1
Host: victim.com
Content-Length: 6
Transfer-Encoding: chunked

0

GPOST /evil HTTP/1.1
X-Ignore: ignore
```
- Frontend uses Content-Length → thinks the body is only 0
- Backend uses Transfer-Encoding → processes the smuggled GPOST as a new request

## 🧪 Real-World Impact

- Bypass authentication or WAFs  
- Hijack requests of other users  
- Cache poisoning  
- Request queue poisoning    

---

## 🛡️ Mitigations

- Normalize all requests at the **proxy** layer  
- Disable ambiguous headers:
  - Use **either** `Content-Length` **or** `Transfer-Encoding`, **never both**  
- Use backends that **reject malformed or conflicting headers**  
- Keep proxies, load balancers, and WAFs **fully patched**  

---

## 🔗 Resources

- [PortSwigger: HTTP Request Smuggling](https://portswigger.net/web-security/request-smuggling)  
- [Practical Smuggling Labs](https://portswigger.net/web-security/request-smuggling/lab-basic-cl-te)  
- [RFC 7230 – HTTP/1.1 Syntax](https://datatracker.ietf.org/doc/html/rfc7230)  
