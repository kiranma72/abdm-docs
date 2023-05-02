+++
title = "Setup Auto-Approval"
date = 2023-05-02T03:53:25+05:30
weight = 5
chapter = true
pre = "<b>5.5 </b>"
+++

# Setting up Auto-Approval

## Functionality Overview



## Test Cases



## API Sequence Diagram


## API Information Request Response


#### Auto Approval

**1. Notification to HIU**

**BASE URLs:** https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /consents/auto-approve$" >}}

#### Enable/Disable Auto-Approval 

**2. Disable Auto-Approval Policy**

**BASE URLs:** https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /consents/auto-approval-policy/{auto-approval-id}/disable$" >}}

**3. Enable Auto-Approval Policy**

**BASE URLs:** https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /consents/auto-approval-policy/{auto-approval-id}/enable$" >}}

