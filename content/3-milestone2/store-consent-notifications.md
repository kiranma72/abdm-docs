+++
title = "Store Consent Notifications"
date = 2023-04-10T12:10:00+05:30
weight = 5
chapter = true
pre = "<b>3.5 </b>"
+++

# Store Consent Notifications

- Users have the option to **revoke the consent** they have provided to the Health Information User (HIU), at any time. The HIUs must remove any copy of the users' data when the consent is revoked.

- All Health Information Providers (HIPs) who are holding any data associated with this consent are notified. They must save a copy of the consent artefact in their system. Data can be shared against this consent any number of times till the **consent expires** (or is revoked by the user).

- To summarise, if the consent is revoked/expired, they have to get rid of the consent artefacts.

## API Sequence Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Notification on Consent Grant
HIE-CM->>HRP/HIP: POST/v0.5/consents/hip/notify
HRP/HIP->>HIE-CM: POST/v0.5/consents/hip/on-notify
{{< /mermaid >}}

