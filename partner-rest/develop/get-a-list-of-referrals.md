---
title: Hämta en lista över leads och affärs möjligheter
description: 'Så här hämtar du en lista över leads och affärs möjligheter med partner-API: et.'
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 46243f8484a8068827e24e1d03f39ffddade1dbf
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770635"
---
# <a name="get-the-list-of-leads-and-opportunities"></a>Hämta listan över leads och affärsmöjligheter

Gäller för:

- Partner-API

 I det här avsnittet beskrivs hur du hämtar listan över leads som tas emot från Microsoft Solution Provider-sidan och samförsäljnings möjligheter som tagits emot från Microsofts säljare eller andra partner. Detta kommer också att hämta listan över samförsäljnings möjligheter eller pipeline-avtal som skapats av din organisation.

> [!Note]
> Leads som tas emot från Microsofts kommersiella marknads platser (Azure Marketplace och AppSource) stöds inte.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner-API-autentisering](api-authentication.md). Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.
- Detta API stöder för närvarande endast användar åtkomst där partners måste vara i någon av följande roller: global administratör, referens administratör eller hänvisnings användare.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                    |
|:--------|:---------------------------------------------------------------|
| **TA** | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

#### <a name="supported-odata-operations"></a>OData-åtgärder som stöds

| Name     | Beskrivning     | Krävs    | Exempel                                                                                                                                                                                                                                                     |
|:---------|:----------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| $select  | Fält väljs  | No          | `/referrals?$select=id,status,customerProfile`                                                                                                                                                                                                              |
| $filter  | Filter resultat | Rekommenderas | `/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'` <br/> `/referrals?$filter=status eq 'New' and qualification eq 'SalesQualified'` <br/> `/referrals?$filter=customerProfile/address/country eq 'US' and direction eq 'Incoming'` |
| $orderby | Order resultat  | Rekommenderas | `/referrals?$orderby=createdDateTime desc`                                                                                                                                                                                                                  |

#### <a name="supported-orderby-parameters"></a>OrderBy-parametrar som stöds

Använd följande $orderby parametrar för att sortera listan över leads och affärs möjligheter

| Namn            | Typ     | Description                                       |
|:----------------|:---------|:--------------------------------------------------|
| createdDateTime | DateTime | Datum och tid då lead eller affärs möjlighet skapades |
| updatedDateTime | DateTime | Uppdatera datum och tid för lead eller affärs möjlighet   |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner rest-rubriker](headers.md) .

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$orderby=createdDateTime desc HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svars texten en samling [leads och/eller affärs möjligheter](referral-resources.md).

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en [HTTP-statuskod](error-codes.md) som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.

### <a name="response-example"></a>Exempel på svar

``` http
HTTP/1.1 200 OK
Content-Type: application/json
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731

{
  "@odata.context": "http://api.partner.microsoft.com/v1.0/$metadata#Referrals",
  "@odata.count": 1,
  "value": [
    {
      "id": "c5fbb3b6-be74-4795-9fb5-4324c73fed37",
      "engagementId": "65edc0b5-3485-41b7-a17e-dfa9ef4706e2",
      "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
      "organizationName": "Contoso Company",
      "createdDateTime": "2020-10-30T21:03:00.0000000Z",
      "updatedDateTime": "2020-10-30T21:03:00.0000000Z",
      "status": "New",
      "substatus": "Pending",
      "qualification": "Direct",
      "type": "Independent",
      "direction": "Incoming",
      "customerProfile": {
        "name": "Fabrikam Customer Inc",
        "address": {
          "addressLine1": "One Microsoft Way",
          "addressLine2": "",
          "city": "Redmond",
          "state": "WA",
          "postalCode": "98052",
          "country": "US"
        }
      },
      "details": {
        "notes": "We are interested in deploying Microsoft 365 and are looking for support in training our employees. Can you help?",
        "dealValue": 10000,
        "currency": "USD",
        "closingDateTime": "2020-12-01T00:00:00Z",
        "requirements": {
            "industries": [ { "id": "Education" } ],
            "products": [ { "id": "Microsoft365" } ],
            "services": [ { "id": "LearningAndCertification" } ],
            "solutions": [ { "id": "SOL-Microsoft365", "name": "Microsoft365" }
          ]
        }
      },
      "links": {
        "relatedReferrals": {
          "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'",
          "method": "GET"
        },
        "self": {
          "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals/c5fbb3b6-be74-4795-9fb5-4324c73fed37",
          "method": "GET"
        }
      }
    }
  ],
  "@odata.nextLink": "http://api.partner.microsoft.com/v1.0/referrals?$skiptoken=k181pEdP0ykypkieJfcxX"
}
```

Använd `@odata.nextLink` för att hämta nästa resultat sida.

> [!Note]
> Fälten i exemplet illustratration ovan är inte uttömmande. Det faktiska API-svaret innehåller fler fält som kund-och partner team. En fullständig lista över vilka fält som stöds finns i avsnittet om [referens resurser](referral-resources.md).

## <a name="sample-requests"></a>Exempel förfrågningar

1. Hämtar de 10 främsta senaste ingående samförsäljnings möjligheterna. Begäran kommer att hämta affärs möjligheter som initieras av en Microsoft-säljare eller en annan partner som bjuder in din organisation att delta i en samförsäljnings aktivitet.
    
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(type eq 'Shared' and direction eq 'Incoming')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

2. Hämtar de senaste inkommande leads och affärs möjligheter som inte har svarat på.  

    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(direction eq 'Incoming' and substatus eq 'Pending')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

    > [!Important]
    > Om du inte svarar på ett lead eller en affärs möjlighet inom den tilldelade tiden (14 dagar), kommer vi att arkivera det som upphört att gälla och meddela antingen Microsoft eller partnern som skickade dig den här möjligheten.

3. Hämtar de senaste aktiva samsäljiga affärs möjligheterna som har startats av din organisation och som bearbetas av en bestämd säljare.
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=status eq 'Active' and direction eq 'Outgoing' and type eq 'Shared' and team/any(t:t/email eq 'r2d2@contoso.com')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```