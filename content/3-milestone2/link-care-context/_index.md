+++
title = "Link Care Context"
date = 2023-04-03T04:10:00+05:30
weight = 3
chapter = true
pre = "<b>3.3 </b>"
+++

# Link Care Context

Linking of a care context can happen in 2 scenarios

**Scenario 1:**
- [User has shared ABHA Address during Registration](/abdm-docs/2-milestone1/verify-abha-address/index.html)
- HRP is expectated to initiate HIP initiated linking whenever a new health record is created for this user. It uses the linking token obtained and saved during registration to link a care context)

**Scenario 2:**
- User has not shared ABHA Address during Registration.
- HRP is expected to call a SMS notification API whenever a new health record is created for this user. 
- This triggers a SMS with a deep link. The user will be able to initiate a discovery process, find their records and link them with their ABHA address 

The discovery process can also be used by the user at anytime to find their health records at the facilities they have visited. 

![M2 Linking and Discovery](../M2_link_and_discover.png)

## This section covers:
{{% notice %}}
1. [HIP Initiated linking](/abdm-docs/3-milestone2/link-care-context/hip-initiated-linking/)
2. [Notification to Mobile](/abdm-docs/3-milestone2/link-care-context/notification-mobile/)
3. [Discovery & Link](/abdm-docs/3-milestone2/link-care-context/discovery-link/)
{{% /notice %}}
