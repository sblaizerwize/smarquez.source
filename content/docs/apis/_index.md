---
title: API documentation
type: docs
weight: 1
---

# BlueSnap Implementation
Last updated: 23/01/2020

---
## Purpose
This document explains the implementation of BlueSnap payment processor with SampleClient web services. It describes the payment logic, provides use cases, and shows the payment sequence diagrams for each case. 

## Audience
The target audience of this document includes stakeholders, developers, and project managers from SampleClient and MyEnterprise.

---
## Overview
SampleClient requires to integrate [BlueSnap](https://home.bluesnap.com/) as an alternative payment processor for its web services. SampleClient payment processors include:

*   [Stripe](https://stripe.com/en-mx)
*   [Humboldt](https://hbms.com/)
*   [Paysafe](https://www.paysafe.com/en/)
*   [Safecharge](https://www.safecharge.com/)

The first stage of BlueSnap implementation with SampleClient enables payments using a credit card. This document describes the payment flow of a New Vaulted Shopper Making a Purchase.

---
## A New Vaulted Shopper Making a Purchase

The scenario for this purchase case is the following:  

1. A new shopper signs up for the first-time to the SampleClient web services. 
2. The shopper decides to buy credits to have access to SampleClient content using a credit card. 
3. The shopper selects the number of credits and proceeds to the **checkout form**.
4. The SampleClient payment logic selects BlueSnap as payment processor from among several processors (Stripe, Humboldt, Paysafe, and Safecharge) to make a purchase with a credit card. 
5. The shopper fills up all required fields to complete the transaction. 
6. The payment processor asks permission to store the credit card information for future transactions. 
7. The shopper clicks the **Buy securely now** button.   
8. The shopper receives a notification status about the purchase transaction. 

---
## Sequence Diagram

The following diagram shows the payment logic for a shopper making a purchase using BlueSnap payment processor.

![Sequence Diagram]({{< resource url="sequence_diagram.png" >}})
***Figure 1. Payment Sequence Diagram for a Shopper Making a Purchase using BlueSnap Processor***\
&nbsp;

The process of the payment sequence for a shopper making a purchase is the following:

1. The frontend sends a GET request to the backend to load the BlueSnap payment form with the Hosted Payment Fields.  
2. The backend sends a POST request to the BlueSnap API to retrieve a Hosted Payment Fields token (`pfToken`). 
3. The BlueSnap API returns the `pfToken` on the Location header. 
4. The backend returns to the frontend the following parameters: `pfToken`, `base_url`, and `billing_workflow`. 
5. The frontend loads the **checkout form** with BlueSnap Hosted Payment Fields. 
6. The shopper clicks the **Buy securely now** button after filling out all of the fields. 
7. The frontend sends three PUT requests to the BlueSnap API to protect customer-sensitive data (CCN, Expiration date, and CVV).
8. The frontend receives a confirmation of the binding between the `pfToken` and shopper’s card information. 
9. The frontend sends a POST request to backend to make a purchase using the `pfToken` and shopper’s payment details. 
10. The backend sends a POST request to BlueSnap API to vault a new shopper. 
11. The backend receives a BlueSnap Customer ID associated with the new vaulted shopper.
12. The backend sends a POST request to BlueSnap API to make a purchase using the BlueSnap Customer ID.
13. The backend receives a notification of the payment status.
14. The backend sends back the notification of the payment status to the frontend.
15. The frontend displays a window with the payment status. 

---
## Endpoints

The following table lists the endpoints involved in the payment logic described above: 

{{< rawhtml >}}
<table>
  <tr>
   <td><strong>From </strong>
   </td>
   <td><strong>To </strong>
   </td>
   <td><strong>Endpoint</strong>
   </td>
  </tr>
  <tr>
   <td>
    <code>Frontend </code>
   </td>
   <td>
    <code>Backend </code>
   </td>
   <td>
    <code>GET /v2/billing/creditcard </code>
   </td>
  </tr>
  <tr>
   <td>
    <code>Backend </code>
   </td>
   <td>
    <code>BlueSnap API </code>
   </td>
   <td>
    <code>POST /payment-fields-tokens </code>
   </td>
  </tr>
  <tr>
   <td>
    <code>Frontend </code>
   </td>
   <td>
    <code>BlueSnap API </code>
   </td>
   <td>
    <code>PUT /payment-fields-tokens/ </code>
   </td>
  </tr>
  <tr>
   <td>
    <code>Frontend </code>
   </td>
   <td>
    <code>Backend </code>
   </td>
   <td>
    <code>POST /v2/billing/creditcard </code>
   </td>
  </tr>
  <tr>
   <td>
    <code>Backend </code>
   </td>
   <td>
    <code>BlueSnap API </code>
   </td>
   <td>
    <code>POST /vaulted-shoppers </code>
   </td>
  </tr>
  <tr>
   <td>
    <code>Backend</code>
   </td>
   <td>
    <code>BlueSnap API </code>
   </td>
   <td><code> POST /transactions</code>
   </td>
  </tr>
</table>
{{< /rawhtml >}}


### **GET /v2/billing/creditcard**

This request enables the frontend to receive a transaction token and load the BlueSnap payment form.
 
#### URL
```
  http://api-dev.sampleclient.com/v2/billing/creditcard/?is_mobile=1 \
```

#### Header Parameters

The following table lists the header parameters used in the request.

{{< rawhtml >}}
<table>
  <tr>
   <td><strong>Parameter</strong>
   </td>
   <td><strong>Description</strong>
   </td>
   <td><strong>Type</strong>
   </td>
   <td><strong>Required / Optional</strong>
   </td>
  </tr>
  <tr>
   <td><strong><code>Authorization</code></strong>
   </td>
   <td>Specifies the bearer token for SampleClient API authentication. <strong>Value:</strong> Bearer [USER_TOKEN].
   </td>
   <td>string
   </td>
   <td>required
   </td>
  </tr>
  <tr>
   <td><strong><code>Content-Type</code></strong>
   </td>
   <td>Specifies the format of the content response. <strong>Value:</strong> application/x-www-form-urlencoded. 
   </td>
   <td>string
   </td>
   <td>required
   </td>
  </tr>
  <tr>
   <td><strong><code>cache-control</code></strong>
   </td>
   <td>Indicates whether there is a cache control. <strong>Value: </strong>cache and no-cache.
   </td>
   <td>string
   </td>
   <td>required
   </td>
  </tr>
</table>
{{< /rawhtml >}}


#### Query Parameters

The following table lists the query parameters used in the request.

{{< rawhtml >}}
<table>
  <tr>
   <td><strong>Parameter</strong>
   </td>
   <td><strong>Description</strong>
   </td>
   <td><strong>Type</strong>
   </td>
   <td><strong>Required / Optional</strong>
   </td>
  </tr>
  <tr>
   <td><strong><code>is_mobile</code></strong>
   </td>
   <td>Specifies whether the shopper is using a mobile device. If true, <strong>value:</strong> 1.
   </td>
   <td>integer
   </td>
   <td>required
   </td>
  </tr>
  <tr>
   <td><strong><code>packages</code></strong>
   </td>
   <td>Specifies the number of credits the shopper is buying. <strong>Value:</strong> 5, 11, 22.
   </td>
   <td>integer
   </td>
   <td>required
   </td>
  </tr>
</table>
{{< /rawhtml >}}


#### Sample Request

The following is an example of a command-line request.


```
curl -X GET \
  'http://api-dev.sampleclient.com/v2/billing/creditcard/?is_mobile=1&packages=11' \
  -H 'Authorization: Bearer [USER_TOKEN]' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -H 'cache-control: no-cache' \
```



#### Response Body

The following table lists the elements commonly used from the response. 

{{< rawhtml >}}
<table>
  <tr>
   <td colspan="2" ><strong>Element</strong>
   </td>
   <td><strong>Description</strong>
   </td>
   <td colspan="2" ><strong>Type</strong>
   </td>
  </tr>
  <tr>
   <td colspan="2" ><strong><code>bluesnap_pars</code></strong>
   </td>
   <td>Contains information on the transaction token. 
   </td>
   <td colspan="2" >data object
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td><strong><code>base_url</code></strong>
   </td>
   <td>Specifies the base API URLs for the BlueSnap environments. <strong>Values:</strong> sandbox and production.
   </td>
   <td colspan="2" >string
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td><strong><code>hostedFieldToken</code></strong>
   </td>
   <td>Specifies the generated transaction token. 
   </td>
   <td colspan="2" >long
   </td>
  </tr>
  <tr>
   <td colspan="2" ><strong><code>rebuy</code></strong>
   </td>
   <td>Contains information about the stored payment methods of a vaulted shopper. 
   </td>
   <td colspan="2" >array
   </td>
  </tr>
</table>
{{< /rawhtml >}}

{{< hint danger >}}
**Important:**  
The elements listed in the response body table are in blue color in the Sample Response Body.
{{< /hint >}} 


#### Sample Response Body

The following is an extract of a typical response showing some of the elements returned for this request. 

```
{
  "creditcardform": [
    {
      "type": "select",
      "options": [],
      "multi": 1,
      "name": "packages"
    },
    {
      "type": "text",
      "label": "Name on Credit Card",
      "name": "cc_fullname"
    },
    {
      "type": "text",
      "label": "Street Address",
      "name": "street"
    },
    {
      "type": "text",
      "label": "City",
      "value": "Beverly Hills",
      "name": "city"
    },
    {
      "type": "select",
      "label": "Location ",
      "value": "225",
      "options": [
        {
          "id": -1,
          "name": "--------------"
        },
        {
          "id": 1,
          "name": "AFGHANISTAN"
        }, 
        ...
        {
          "id": 239,
          "name": "ZIMBABWE"
        }
      ],
      "name": "country"
    },
    {
      "type": "text",
      "label": "ZIP/Postal Code",
      "value": "90210",
      "name": "postal_code"
    },
    {
      "type": "boolean",
      "label": "rebuy",
      "name": "rebuy"
    },
    {
      "type": "boolean",
      "label": "MIC",
      "value": false,
      "name": "fic_opt_in"
    },
    {
      "type": "boolean",
      "label": "MPlus",
      "value": false,
      "name": "mplus_opt_in"
    },
    {
      "type": "boolean",
      "label": "Check here to top up your credits when you run out so that you are ready for any encounter.",
      "value": 1,
      "name": "autobill_opt_in"
    },
    {
      "type": "text",
      "label": "Credit Card number",
      "name": "cc_number"
    },
    {
      "type": "select",
      "label": "Credit Card Expiration Date",
      "options": [
        {
          "id": 1,
          "name": "01"
        },
        ...
        {
          "id": 12,
          "name": "12"
        }
      ],
      "name": "cc_month"
    },
    {
      "type": "select",
      "label": "Credit Card Expiration Date",
      "options": [
        {
          "id": 2019,
          "name": "2019"
        },
        ...
        {
          "id": 2068,
          "name": "2068"
        }
      ],
      "name": "cc_year"
    },
    {
      "type": "text",
      "label": "Card Verification Code (CVV) #",
      "name": "cc_cvv"
    }
  ]
}
```
### **POST /payment-fields-tokens**

This method enables to create a Hosted Payment Fields token (`pfToken`) when using Hosted Payment Fields. It is a server-to-server request from SampleClient to BlueSnap when the customer access the **checkout form**. The token serves to protect sensitive shopper information during a transaction. The transactions using a `pfToken` are: 

*   Processing a purchase. 
*   Creating a vaulted shopper.
*   Updating a vaulted shopper with a new credit card. 

{{< hint danger >}}
**Important:**  
The Hosted Payment Fields token expires after 60 minutes. 
{{< /hint >}} 

#### URL
```
https://sandbox.bluesnap.com/services/2/payment-fields-tokens
```

#### Header Parameters

The following table lists the header parameters used in the request.

{{< rawhtml >}}
<table>
  <tr>
   <td><strong>Parameter</strong>
   </td>
   <td><strong>Description</strong>
   </td>
   <td><strong>Type</strong>
   </td>
   <td><strong>Required / Optional</strong>
   </td>
  </tr>
  <tr>
   <td><strong><code>Content-Type</code></strong>
   </td>
   <td>Specifies that the format of the response body is a JSON object.
<p>
<strong>Value:<code> application/json. </code></strong>
   </td>
   <td>string
   </td>
   <td>required
   </td>
  </tr>
  <tr>
   <td><strong><code>Accept</code></strong>
   </td>
   <td>Specifies that the format of the accepted request is a JSON object.
<p>
<strong>Value:<code> application/json.</code></strong>
   </td>
   <td>string
   </td>
   <td>required
   </td>
  </tr>
  <tr>
   <td><strong><code>Authorization</code></strong>
   </td>
   <td>Specifies the bearer token for BlueSnap API authentication. <strong>Value:</strong> Bearer [USER_TOKEN]
   </td>
   <td>string
   </td>
   <td>required
   </td>
  </tr>
</table>
{{< /rawhtml >}}


#### Sample Request

The following is an example of a command-line request.


```
curl -I -X POST \
  https://sandbox.bluesnap.com/services/2/payment-fields-tokens \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer [USER_TOKEN]' \
```



#### Sample Response Body

The following is an example of a typical response that shows all the elements of the Hosted Payment Field token generation.


```
HTTP/1.1 201 201
Date: Wed, 27 Nov 2019 17:24:47 GMT
Set-Cookie: JSESSIONID=XXXXXXXX; Path=/services; Secure; HttpOnly
Location: https://sandbox.bluesnap.com/services/2/payment-fields-tokens/XXXXXXXX_
Content-Length: 0
Strict-Transport-Security: max-age=31536000 ; includeSubDomains
Set-Cookie: XXXXXXX; Path=/
Set-Cookie: XXXXXXX; path=/services
Via: 1.1 sjc1-bit32

```



####  Hosted Payment Fields Token Errors

The following table lists the errors returned from a request related to the Hosted Payment Field token.

{{< rawhtml >}}
<table>
  <tr>
   <td><strong>Code</strong>
   </td>
   <td colspan="2" ><strong>Name</strong>
   </td>
   <td><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td><strong>14040</strong>
   </td>
   <td colspan="2" >EXPIRED_TOKEN
   </td>
   <td>Token is expired
   </td>
  </tr>
  <tr>
   <td><strong>14041</strong>
   </td>
   <td colspan="2" >TOKEN_NOT_FOUND
   </td>
   <td>Token is not found
   </td>
  </tr>
  <tr>
   <td><strong>14042</strong>
   </td>
   <td colspan="2" >NO_PAYMENT_DETAILS_LINKED_TO_TOKEN
   </td>
   <td>Token is no associated with a payment method
   </td>
  </tr>
</table>
{{< /rawhtml >}}