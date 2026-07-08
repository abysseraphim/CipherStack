# CipherStack

> A two-volume technical book series on software development and offensive security.

---

## Why

Most security books teach tools. CipherStack teaches the layer underneath — how software actually works, what makes it vulnerable, and how to think about it from both sides.

The two volumes are independent but designed to be read together: Dev builds the programming foundation, Offense builds on top of it.

---

## Volumes

### CipherStack: Dev — 520 pages

Covers the programming foundations that make everything else possible.

Topics span Python, JavaScript, Go, Bash, and PHP — not as syntax references, but as tools for building real things. Each language section ends with real-world projects: a payload generator in Python, an ASN recon tool in Bash, a web crawler in JavaScript, a concurrent HTTP tool in Go, a backend API in PHP.

**DOI:** [10.5281/zenodo.20754677](https://doi.org/10.5281/zenodo.20754677)

---

### CipherStack: Offense — 343 pages

Covers offensive web security from recon to exploitation.

Starts with networking fundamentals and builds toward web application attacks: XSS (reflected, stored, DOM, postMessage), SQLi, NoSQL injection, CSRF, authentication flaws, broken access control, cache vulnerabilities, HTTP request smuggling, subdomain takeover, and more. Recon methodology, wide recon automation, and bug bounty workflows are covered in depth.

**DOI:** [10.5281/zenodo.20945302](https://doi.org/10.5281/zenodo.20945302)

---

## Sample — XSS: Fuzzing the javascript: Protocol

From **CipherStack: Offense**, Chapter: XSS

Finding every Unicode character that, when placed between `javascript` and `:`, still produces a valid `javascript:` protocol — useful against filters that rely on `startsWith('javascript:')`:

```javascript
log = []
let anchor = document.createElement('a');
for (let i = 0; i <= 0x0ffff; i++){
    anchor.href = `javascript${String.fromCodePoint(i)}:`;
    if (anchor.protocol === 'javascript:'){
        log.push(i);
    }
}
console.log(log);
log.map(x => String.fromCharCode(x));
```

Output reveals characters like `\t` (0x09) and `\n` (0x0A) that browsers normalize silently — allowing payloads like:

```html
<a href="javascript&#x09;:alert(origin)">click</a>
```

This pattern runs through the whole book: understand the spec, find what the browser normalizes, exploit the gap between what the filter sees and what executes.

---

## Sample — Bash: ASN Recon Tool

From **CipherStack: Dev**, Chapter: Bash Real World Projects

Querying RADB for a given ASN and outputting structured JSON — name, description, contact emails, and IP ranges:

```bash
asn_data=$(whois -h whois.radb.net "AS$asn")
route_data=$(whois -h whois.radb.net -i origin "AS$asn")

cat <<EOF
{
  "asn": $asn,
  "name": "$name",
  "ip_ranges": {
    "ipv4": [
$(printf '      "%s",\n' $ipv4_ranges | sed '$ s/,$//')
    ]
  }
}
EOF
```

Usage: `bash get-asn-details 15169` or `echo 15169 | bash get-asn-details`

---

## Repository Structure

```
CipherStack/
│
├── Offense/
│   ├── CipherStack-Offense.md
│   └── CipherStack-Offense.pdf
│
└── dev/
    ├── CipherStack-Dev.md
    └── CipherStack-Dev.pdf
```

---

## Citation

```
Cipher Stack: Dev
DOI: https://doi.org/10.5281/zenodo.20754677

Cipher Stack: Offense
DOI: https://doi.org/10.5281/zenodo.20945302
```

---

## License

Creative Commons Attribution 4.0 International (CC BY 4.0)

---

## Author

**Soroush Maleki** — Application Security Researcher / Developer  
GitHub: [abysseraphim](https://github.com/abysseraphim)
