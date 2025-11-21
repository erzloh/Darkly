# Darkly – Web Security Project

## Overview

Darkly is a cybersecurity learning project from the **42 Advanced Curriculum**, focused on practical, hands‑on exploration of common web vulnerabilities. The goal of the project is to analyze a deliberately vulnerable website, identify **14 distinct security flaws**, and document each of them in a structured way.

The project emphasizes understanding real‑world security concepts such as **OWASP Top 10**, **CWE**, **CVE**, and various web‑security attack vectors, as well as the use of professional tools like **OWASP ZAP** and **Burp Suite**.

To simplify the workflow, the project is run using a Docker image instead of the VM originally provided by the school.

---

## Running the Project

The website used for analysis is available as a Docker image:

```
docker pull iffigues/darkly42web
```

### Start the container

```
docker run -d -p <your-port-number>:80 -it -t iffigues/darkly42web
```

**Example:**

```
docker run -d -p 80:80 -it -t iffigues/darkly42web
```

Once the container is running, the vulnerable site becomes accessible locally for investigation.

---

## Repository Structure

Each discovered vulnerability is documented in its own directory.
Every folder contains two files:

* **flag** — the flag obtained for the vulnerability
* **vulnerability_explanation.md** — an explanation of the vulnerability, how it was found, how the exploit works, and prevention measures

---

## Learning Objectives

The project aims to deepen understanding of:

* Web application vulnerabilities and exploitation techniques
* OWASP Top 10 concepts and defensive strategies
* Passive and active scanning using OWASP ZAP and Burp Suite
* Secure coding principles and proper input validation
* The importance of server‑side validation and sanitization
* Realistic attacker perspectives and threat modeling