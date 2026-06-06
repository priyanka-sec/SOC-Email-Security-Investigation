# Sigma Rule — Suspicious SMTP Tool Detection

title: Suspicious SMTP Tool Detected in Email Header

id: EMAIL-001

status: experimental

description: Detects emails containing swaks tool fingerprint inside X-Mailer header.

logsource:

product: email

service: smtp

detection:

selection:

x_mailer|contains:

* swaks

condition: selection

falsepositives:

* SMTP testing performed by administrators

level: high

tags:

* attack.initial_access

* attack.t1566.002

