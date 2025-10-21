# 🧾 Phishing Email Analysis Report

##  1. Email Overview
**From:** CIBC-Banking.Service.Email.8@caib.com  
**Return-Path:** meztaz.logocec8@caib.com  
**To:** jsmith@technicalsolutions.com  
**Subject:** “You’ve got 1 new message [REF: 8]”  
**Date:** Wed, 10 Apr 2019 11:46:37 -0600  
**Sender IP:** 190.6.201.67 (Mail server: mail.ip.gob.hn)

---

##  2. Key Phishing Indicators (Summary)

| **Category** | **Indicator** | **Evidence / Observation** |
|---------------|----------------|-----------------------------|
| **Spoofed Sender Domain** | Domain `caib.com` misused to mimic legitimate `cibc.com` (Canadian Imperial Bank of Commerce). | From: `<CIBC-Banking.Service.Email.8@caib.com>` |
| **Failed SPF Authentication** | Sender IP not authorized to send emails for domain `caib.com`. | `spf=fail (sender IP is 190.6.201.67)` |
| **No DKIM or DMARC** | Missing DKIM signature; DMARC policy not enforced. | `dkim=none`, `dmarc=none` |
| **Suspicious IP Address** | Originating from Honduras government mail server (`mail.ip.gob.hn`) — unrelated to CIBC Bank. | `client-ip=190.6.201.67; helo=mail.ip.gob.hn;` |
| **Malicious Link** | Fake account activation link pointing to unknown domain. | `http://satole.com/conve/index.php` |
| **Urgent & Fear-Based Language** | Creates panic — “account deactivated for security reasons.” | “Please help us validate your CIBC account...” |
| **Brand Impersonation** | Uses CIBC logo and color scheme to appear legitimate. | Embedded logo from GitHub (`cibc_bank_3x1_FINAL...png`) |
| **Grammar and Formatting Errors** | Minor mistakes and inconsistent spacing. | Poorly formatted email body. |
| **Personalization for Credibility** | Includes victim’s address `jsmith@technicalsolutions.com`. | Increases trust manipulation. |

---

##  3. Header Analysis (Detailed)

###  SPF (Sender Policy Framework)
Authentication-Results: spf=fail (sender IP is 190.6.201.67)
smtp.mailfrom=caib.com;

markdown
Copy code
- SPF validation **failed**. The sending IP is **not authorized** to send on behalf of `caib.com`.

###  DKIM (DomainKeys Identified Mail)
dkim=none (message not signed)

csharp
Copy code
- The email is **not digitally signed** with DKIM. Legitimate CIBC emails would include a DKIM signature.

###  DMARC
dmarc=none action=none header.from=caib.com;

markdown
Copy code
- The domain `caib.com` **has no DMARC policy**, allowing spoofing.

###  Return-Path & Received Chain
- **Return-Path:** `meztaz.logocec8@caib.com`  
- Routed through unrelated mail servers (`mail.ip.gob.hn` — Honduras). Legitimate CIBC messages should originate from servers like `@cibc.com` or `@cibc.ca`.

###  Sender IP
X-Sender-IP: 190.6.201.67

yaml
Copy code
- IP registered in **Honduras (not Canada)** — confirms **spoofing and impersonation**.

---

##  4. Suspicious URLs Found

| **Displayed Link** | **Actual URL Target** | **Risk** |
|--------------------|------------------------|-----------|
| “Activate my account” | `http://satole.com/conve/index.php` | Malicious — credential harvesting site |
| Hidden tracking images | `http://app.e.royalmail.com/e/es?...` | Misleading tracking pixels for phishing analytics |

> **Note:** Attackers embedded external images and tracking links from unrelated domains (Royal Mail, GitHub, satole.com) to make the email appear professional and evade basic filters.

---

##  5. Social Engineering Techniques Used

| **Tactic** | **Example from Email** | **Effect on Victim** |
|-------------|------------------------|-----------------------|
| **Urgency / Fear** | “Your account has been deactivated for security reasons.” | Forces immediate response |
| **Authority / Brand Abuse** | Pretends to be from CIBC Bank using official tone and visuals | Gains victim’s trust |
| **Impersonation** | Uses CIBC logo and sender address format | Creates legitimacy illusion |
| **Personalization** | Includes recipient’s real email ID | Increases credibility |
| **Limited Time Threat** | “The link is only active for 12 hours.” | Encourages hasty action |

---

##  6. Technical Indicators of Compromise (IOCs)

| **Indicator Type** | **Value** | **Description** |
|---------------------|-----------|-----------------|
| **Sender IP** | `190.6.201.67` | Originating IP (Honduras) |
| **Fake Domain** | `caib.com` | Impersonating legitimate `cibc.com` |
| **Malicious URL** | `http://satole.com/conve/index.php` | Credential theft landing page |
| **Fake Contact** | `myaccount@secure-cibc.com` | Fraudulent “support” email address |

---

##  7. Summary of Findings
This email is a **phishing attempt** impersonating **CIBC Bank**. Multiple red flags confirm spoofing and malicious intent:
- SPF failure, DKIM and DMARC missing  
- IP/location mismatch (Honduras)  
- Fake links that lead to credential-harvesting sites  
- Social engineering via urgency, impersonation, and personalization

---

##  8. Tools Used
- MXToolbox Email Header Analyzer  
- VirusTotal (URL check)  
- WHOIS lookup tools  
- Manual inspection of headers and HTML content

---

##  9. Recommended Actions
1.  **Do not click** any links or open attachments from this email.  
2.  **Report** the email to your IT/security team and email provider.  
3.  **Block** sender domain (`caib.com`) and IP address (`190.6.201.67`).  
4.  **Implement/Enforce** SPF, DKIM, and DMARC for organizational domains.  
5.  **Educate users** to recognize urgency-based phishing and mismatched URLs.

---

##  10. Key Learnings
- How to interpret email headers and detect spoofed senders.  
- The role of **SPF, DKIM, and DMARC** in preventing email spoofing.  
- Common social engineering techniques used in phishing.  
- How to analyze phishing HTML and detect malicious URLs.

---

##  Conclusion
This is a **well-crafted phishing attack** designed to steal user credentials by impersonating CIBC Bank. Header analysis and content inspection provide conclusive evidence that the message is **not legitimate**. Implementing email authentication and user awareness training are key mitigations.

**Author:** Gowtham Roy  
**Date:** October 2025  
**Task:** Cybersecurity Internship — Phishing Email Analysis (Task 2)
