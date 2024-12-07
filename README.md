# motoradmin-CSSQLI
exploit of CSSQLI in motor admin
Motor admin
Client side SQL injection
 
The motor-admin panel allows administrators to execute database queries.
Queries are passed via the location.hash fragment in the URL like this (e.g., admin.com/queries/1#base64(query)),admin panel takes the value 
from location.hash and executes it as a database query.
he location.hash value is client-controlled, meaning an attacker can manipulate it.
![Request and response](https://github.com/alirezacsp/Zero/blob/main/Picture10.png)
If the admin clicks a malicious link containing a crafted hash admin.com/queries/1#base64(execute database query), the admin panel might execute the attacker's query

Sample:
http://localhost:3000/queries/1#eyJzcWxfYm9keSI6IlNFTEVDVCB2ZXJzaW9uKClcbiIsInByZWZlcmVuY2VzIjp7InF1ZXJ5X3R5cGUiOiJzcWwiLCJkYXRhYmFzZSI6IkRlZmF1bHQiLCJ2aXN1YWxpemF0aW9uIjoidmFsdWUiLCJ2aXN1YWxpemF0aW9uX29wdGlvbnMiOnt9LCJ2YXJpYWJsZXMiOltdfX0= 

when admin open this url version() query will executed.

Consequences

Privilege Escalation:
•	Attackers might alter administrative configurations, such as adding new superusers or escalating their privileges, gaining full control over the database and potentially other linked systems
Service Downtime:
•	Execution of malicious queries can crash the application by removing critical structures or locking resources (e.g., locking rows, filling disk space).
•	This downtime can disrupt business operations, result in financial loss, and erode user trust
Server Takeover via SQL Features:
•	If the database allows the execution of system-level commands (e.g., xp_cmdshell in SQL Server, COPY TO PROGRAM in PostgreSQL), attackers could gain direct access to the operating system.
•	This could lead to complete server compromise, enabling the installation of backdoors, ransomware, or launching further attacks on internal systems.
Launching External Attacks (HTTP Requests):
•	If the database supports making HTTP requests (e.g., UTL_HTTP in Oracle or http_get in PostgreSQL), attackers could abuse this functionality to:
o	Send sensitive data to external servers controlled by the attacker.
o	Perform SSRF (Server-Side Request Forgery) attacks to target internal services.
o	Exploit other systems by proxying malicious requests through the database server.
•  Chained Exploits:
•	This vulnerability could serve as a stepping stone for broader attacks, such as:
o	Pivoting to other internal systems.
o	Establishing persistence in the network.
o	Leveraging the compromised server to target customers or partners.
•  Regulatory and Legal Implications:
•	A breach resulting from such an attack may violate data protection regulations (e.g., GDPR, CCPA).
•	This could lead to lawsuits, fines, and mandatory disclosures, further harming the organization's reputation and financial stability.
