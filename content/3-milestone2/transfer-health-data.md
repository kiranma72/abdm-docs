+++
title = "Transferring Health Data"
date = 2023-04-11T05:10:00+05:30
weight = 9
chapter = true
pre = "<b>3.9 </b>"
+++

# Transferring Health Data

## Firewall Rules

- **DataPush URL** - can be any URL specified by the HIU. The HRP system must ensure that its firewall rules are setup in such a way that the outbound HTTPs requests can be to any URL

- Security is ensured by making sure that the encrypted data can be only decrypted by requesting HIU

## Posting the Data

- The encrypted data must be pushed to the HIU by the HRP within a short time frame. Current timeout is set to 20 minutes.

- If the data is very large, for example: running into 100s of MBs for CT scans, MRIs etc, the data can be pushed in parts.

- It is also encouraged for large files to use a streaming approach instead of pushing data to HIU.


- Once the data push is complete, the HRP must notify the HIE-CM that it has transferred the data (health-information/notify).

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
HIP/HRP Repository-->>HIU System: Direct data transfer<br/>POST/datapush-url
HIP/HRP Repository->>Gateway:Notify on the transfer<br/>POST/health-information/notify
{{< /mermaid >}}


## Testing & Verifying Data Transfer

**Testing with PHR Application**

- On the PHR app side, log in with an SBX ABHA address
- Register a patient with same SBX ABHA address in your HIP/HRP
- Create a new health record for this patient
- Link a care context for this health record using HIP initiated linking
- PHR App should automatically make a request for the health record along with apt consents
- Prepare the health record, encrypt & transfer to the data push URL provided by the PHR app
- Your record should be successfully displayed in the ABHA PHR app



