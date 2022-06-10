+++
title = "Create Consent Request"
date = 2022-06-09T10:53:25+05:30
weight: 1
draft: false
+++
 
 # Create Consent Request
 
 
 
 
 ### Overview of the functionality 
 
From an HIU perspective, the flow begins when the HIU (e.g., a Doctor at a Hospital) requests consent to view the patient’s data.
Upon receipt of such a request from Gateway, CM acknowledges and sends back a consent request ID to the HIU via the gateway.
The CM then notifies the patient that an HIU has made a consent request.
The patient can view the request details and choose to either grant consent or deny it.
Subsequently, the CM notifies the HIU requester of the patient’s consent or denial status via the gateway.

- If the request is granted, the CM sends across the Ids of the consent artefacts that were created against the request, to the HIU.

- If the request is denied, the CM simply notifies the HIU of the denial of the request.

  
 
 
 
