# Description
During analysis of the ecodotempo.com.br website, a Stored Cross-Site Scripting (XSS) vulnerability was discovered. This vulnerability allows an attacker to inject malicious scripts into fields that are subsequently rendered to other users without proper sanitization, specifically on the home page of the unauthenticated (disconnected) area.

# Affected endpoint
ecodotempo.com.br/colecoes/itens/cadastrar_realizar.php

# Affected parameter
name="nome" and name="descricao"

# Payload example:
<script>alert(document.cookie)</script>

# PoC


<img width="1452" height="865" alt="1" src="https://github.com/user-attachments/assets/2ba502a8-4e5a-4d7f-9602-1084a5c571dc" />
<img width="1451" height="979" alt="2" src="https://github.com/user-attachments/assets/564d9c73-3271-4ad9-8a62-71d7ba4da724" />
<img width="1448" height="960" alt="3" src="https://github.com/user-attachments/assets/8872ba75-ac0a-4c89-9b46-2ca845f33e21" />
<img width="1448" height="986" alt="4" src="https://github.com/user-attachments/assets/19125e10-fafe-4b99-b925-3b69d56ddb27" />
<img width="1445" height="1024" alt="5" src="https://github.com/user-attachments/assets/517f8d5a-c64f-4d57-bd91-ed77c584675a" />
<img width="1281" height="815" alt="6" src="https://github.com/user-attachments/assets/5d5e51a6-a8e2-41f4-84ed-d394b8026778" />


# Impact
The presence of a stored XSS vulnerability on the main page of the unauthenticated area of ecodotempo.com.br poses a significant security risk. Since the injected script is permanently stored and served to every user who accesses the affected page, it opens the door to a range of client-side attacks. An attacker could exploit this flaw to execute arbitrary JavaScript in the browser of unsuspecting visitors, potentially stealing session cookies, redirecting users to malicious websites, performing actions on behalf of users without their consent, or manipulating page content to carry out phishing attempts. Because the vulnerability is exposed in a publicly accessible area, it increases the likelihood of exploitation at scale, especially by automated bots or targeted campaigns, potentially undermining user trust and the integrity of the platform.

# Mitigation
To remediate the stored XSS vulnerability found on the main page of the unauthenticated area of ecodotempo.com.br, the following actions should be taken:

All user input must be properly sanitized and validated on both the client and server sides before being stored or rendered. Specifically, any input that will be displayed in the HTML context should have special characters like <, >, ", ', and & encoded to prevent script execution. Additionally, the application should implement output encoding based on the context where the data is injected (HTML, JavaScript, attribute, URL, etc.).

It is also strongly recommended to enforce a Content Security Policy (CSP) to limit the execution of unauthorized scripts, and to disable inline scripts and external script loading from untrusted sources. Regular code reviews and automated security testing (e.g. with tools like OWASP ZAP or Burp Suite) should be incorporated into the development lifecycle to detect and prevent similar flaws in the future.

Finally, any already stored malicious payloads should be identified and removed from the system to eliminate existing risks.
