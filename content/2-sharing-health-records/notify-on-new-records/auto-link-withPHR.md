
# If the PHR address is available with the HRP, link the care context automatically to the address : #


## Overview of the functionality:
- Patient must have a valid PHR address
- Patient ABHA address is already available with the HIP/HRP.
- Patient already registered in the HRP system
- Demographic auhtentication performed
- Linking token is returned after Demographic authentication
- Using the "linking token" returned above for linking, HIP can subsequently add care-contexts in subsequent API call /links/link/add-contexts


Linking care context automatically is a process where the HIP can link the patient’s care context with the ABHA Address/ABHA Number when the patient already registered in the HIP and his ABHA Address is available with the HRP and has uploaded the health records in their system.

In this patient will have to share their name, YOB, gender which is forwarded to the CM. The CM validates the user details and creates a new access token just for the purpose of linking. This new access token is passed to the HIP. The HIP has to call the CM with the new access token to add the care contexts.
