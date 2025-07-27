---
ID: WEB003
Date: 2025-07-01
Tags: #clickjacking #websecurity #headers
Category: Web Security
---

# WEB003 – Clickjacking

## 🧠 What I Learned

**Clickjacking** (a.k.a. UI redress attack) is a technique where an attacker tricks a user into clicking on something different from what they perceive, essentially "hijacking" their clicks.

This is done by **embedding a legitimate site inside a hidden iframe** and overlaying it with misleading visuals. The user thinks they're clicking a visible button, but they're actually interacting with the invisible embedded content.

---

## 🎯 Real-World Impact

- Trick a user into:
  - Submitting a form (e.g., changing email/password)
  - Clicking “Buy Now” or “Delete Account”
  - Granting permissions (e.g., OAuth)
- Often combined with **social engineering**

---

## 🧪 Simple Clickjacking PoC

```html
<iframe src="https://targetsite.com/change-email" style="opacity: 0; position: absolute; top: 0; left: 0; z-index: 9999; width: 100%; height: 100%;"></iframe>
```
---

## 🧪 Attack Mechanics

The `<iframe>` is **invisible**, but placed over a fake UI.

The user's click is hijacked into interacting with the hidden iframe instead of the visible content.

---

## 🛡️ Mitigations

### ✅ Use `X-Frame-Options` Header

- `DENY`: Don’t allow framing at all  
- `SAMEORIGIN`: Only allow if same domain

```http
X-Frame-Options: DENY
```

---

## 🛡️ Mitigation Techniques

### ✅ Use `Content-Security-Policy` (modern method)

```http
Content-Security-Policy: frame-ancestors 'none';
```
This completely prevents the page from being embedded in any frame, on any domain.

---

### ✅ Frame busters

```java
if (top !== self) top.location = self.location;
```
This script prevents your site from being loaded in a frame by breaking out of it.

---

### ✅ Visual cues

- Flashing background when embedded  
- Warning banners or frame detection overlays

---

## 🔧 Detection

- Use **browser developer tools** to inspect frame behavior  
- Use **Burp Suite** or:

```bash
curl -I https://example.com
```
to check for `X-Frame-Options` or `Content-Security-Policy` headers  
- Run **OWASP ZAP** or similar scanners to detect missing protections

---

## 🔗 Resources

- [Clickjacking – OWASP](https://owasp.org/www-community/attacks/Clickjacking)  
- [MDN: X-Frame-Options](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options)  
- [PortSwigger: Clickjacking](https://portswigger.net/web-security/clickjacking)  

---
