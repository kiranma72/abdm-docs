+++
title = "Handling Notifications"
date = 2023-05-02T03:53:25+05:30
weight = 6
chapter = true
pre = "<b>5.6 </b>"
+++

# Handling Notifications

## Functionality Overview



## Test Cases

**HIP initiated linking flow**  - When health records are linked with ABHA address at the health facility / health programme

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1|{{% badge style="blue" %}}Mandatory{{% /badge %}}  Post linking of health records with ABHA address by the HIP with patient consent| the individual can view the health records on the PHR mobile app|Health data will be visible in PHR app once HIP link health records with the ABHA address.|Once Individual visits the hospital. • ABHA address is shared with the health programme / health facility. • Individual validates the ABHA address with the mobile OTP. • Post linking of health records with ABHA address by the HIP| the individual can open any PHR app  and click on "Pull Records" button against the visited health programme / health facility| where the record is created and linked to ABHA address to view the record in mobile device.



## API Sequence Diagram


## API Information Request Response

#### Change Notification to an ABHA address

Notification to subscribers if care contexts is added / updated.

**8. Notification to HIU**

**BASE URLs:** https://your-hrp-server.com

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/subscriptions/hiu/notify$" >}}

**9. Acknowledge Receipt Of Notification**

**BASE URLs:**  https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/subscriptions/hiu/on-notify$" >}}
