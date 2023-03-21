+++
title = "By scan & share"
date = 2023-03-16T09:30:25+05:30
weight = 1
chapter = true
pre = "<b>2.3.1 </b>"
+++

# By Scan & Share

## Scan QR Code

Description: Patients can scan a Health Facility QR code pasted at the facility registration counter on their PHR mobile app. This can be done in 2 ways:
1. By scanning HIP QR Code
2. By scanning PHR address

## By scanning HIP QR Code

Steps to scan an HIP QR Code:
1. Patient must have a PHR app and have a valid PHR address
2. Hospital must generate a HIP QR code and display it at the registration counter
3. Patient scans the QR code from his phone camera or his PHR app 
	- *If scanned from phone camera* -- The list of installed PHR apps is shown on the phone. The user can select any of the apps 
	- *If scanned from within the PHR app*, the app will call the share-profile API on the HIE-CM 
4. The HIE-CM will verify this is a registered healthcare provider and identify the HRP linked to this HIP in the ABDM registry 
5. The Gateway will call the share-profile api on the callback URL registered for this HRP
6. The HRP software must create a screen to display all the scanned profiles for a (counter) code
7. The operator (at a counter) should be able to select a shared profile and perform a fast user registration 
8. Remember to correctly handle this for both new and returning patients


## Create a QR code for your Health Facility

- Patient must have a PHR app and have a valid PHR address.
- Hospital must generate a HIP QR code and display it at the registration counter.

Generate a QR code for the data in below format. You can use something like [Sample QR Generator](https://www.the-qrcode-generator.com/). ABDM will shortly release a QR code generator that can be used.

Your HIP ID is the same as the Health Facility Registry ID. You must have linked this HIP ID to your HRP

```json
{
    "hipId": "HFR1010342452",
    "code": "any information you want to get back with the scan, e,g counterId, Dept Id"
}
```

- Go to ABHA Mobile Application, then My Profile and Find Scan option on the top right.
- Scan the QR code, the app should fetch details of QR code along with User profile details.
- Click on share which will make HIE-CM call the expected API on HIP side.
- The successful message would be shown on app once the on-share callback is given.


## API Sequence Diagram

*(confirm with Kiran)*

[![](https://mermaid.ink/img/pako:eNqVkU9LA0EMxb_KkJPC1vHiZQ4FpaCXYnE9yVziTrY7sJOs80ctpd_dqdaTpdRbCO_3XsjbQieOwECit0Lc0cLjOmKwfHu3WKoW2b3Kp7rHTB-4mc3nD08rs3psn_W7XN3oCbMnzklPUXo_kk4DRrJcVVV7zOIULDw7l7-ufEkUNZY8aM8-K6UuHAVR-83lyfuPetTwvc2_szvh3sdzHvYn74BCA4FiQO9qD1vLSlnIAwWyYOroqMcyZguWd1VaYWk33IHJsVADZXI161AbmB7HVLfkfJa4_On2u-IGJuQXkV_N7guWsayK?type=png)](https://mermaid.live/edit#pako:eNqVkU9LA0EMxb_KkJPC1vHiZQ4FpaCXYnE9yVziTrY7sJOs80ctpd_dqdaTpdRbCO_3XsjbQieOwECit0Lc0cLjOmKwfHu3WKoW2b3Kp7rHTB-4mc3nD08rs3psn_W7XN3oCbMnzklPUXo_kk4DRrJcVVV7zOIULDw7l7-ufEkUNZY8aM8-K6UuHAVR-83lyfuPetTwvc2_szvh3sdzHvYn74BCA4FiQO9qD1vLSlnIAwWyYOroqMcyZguWd1VaYWk33IHJsVADZXI161AbmB7HVLfkfJa4_On2u-IGJuQXkV_N7guWsayK)
