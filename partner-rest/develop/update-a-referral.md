---
title: Uppdatera ett lead eller en affärs möjlighet (föråldrad)
description: Gör att du kan uppdatera lead-eller affärs möjlighets information. Den här metoden för att uppdatera ett lead eller en affärs möjlighet är föråldrad och vi recommmend istället för att använda PATCH-anropet.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 9705db1c21dbec7099cfefebdc7bb23ec65e428c
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770644"
---
# <a name="update-a-lead-or-opportunity-obsolete"></a>Uppdatera ett lead eller en affärs möjlighet (föråldrad)

Gäller för:

- Partner-API

I det här avsnittet beskrivs hur du uppdaterar lead-eller affärs möjlighets information, till exempel avtals värde, uppskattat stängnings datum eller hantera försäljnings stegen i annan information. 


> [!IMPORTANT]
Den här metoden för att uppdatera ett lead eller en affärs möjlighet är föråldrad och vi recommmend istället för att använda [patch](patch-a-referral.md) -anropet.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner-API-autentisering](api-authentication.md). Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.
- Detta API stöder för närvarande endast användar åtkomst där partners måste vara i någon av följande roller: global administratör, referens administratör eller hänvisnings användare.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                       |
|---------|-------------------------------------------------------------------|
| **PUT** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="request-headers"></a>Begärandehuvuden

- Mer information finns i [partner API rest-rubriker](headers.md).

> [!IMPORTANT]
> Se till att ange **If-Match-** huvudet.

### <a name="request-body"></a>Begärandetext

Den här tabellen beskriver [hänvisnings](referral-resources.md) egenskaperna i begär ande texten.

| Egenskap            | Typ                                                                 | Description                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Id                  | sträng                                                               | ID för den här hänvisningen.                                                                                            |
| EngagementId        | sträng                                                               | EngagementID för den här referensen. Flera hänvisningar kan associeras med en enda EngagementID                    |
| Name                | sträng                                                               | Namnet på referensen.                                                                                            |
| ExternalReferenceId | sträng                                                               | En extern identifierare för referensen. Exempel: lagra ditt eget Dynamics 365-lead/affärs möjlighets-ID                    |
| CreatedDateTime     | sträng i UTC-datum/tid-format                                       | Datumet då hänvisningen skapades.                                                                                   |
| UpdatedDateTime     | sträng i UTC-datum/tid-format                                       | Datumet då hänvisningen senast uppdaterades.                                                                              |
| ExpirationDateTime  | sträng i UTC-datum/tid-format                                       | Datumet då hänvisningen upphör att gälla.                                                                                   |
| Status              | [ReferralStatus](referral-resources.md#referralstatus)               | En [uppräkning](https://docs.microsoft.com/dotnet/api/system.enum) med värden som anger hänvisnings status.          |
| Substatus           | [ReferralSubstatus](referral-resources.md#referralsubstatus)         | En [Enum](https://docs.microsoft.com/dotnet/api/system.enum) med värden som anger del status för hänvisning.      |
| StatusReason        | sträng                                                               | Ett beskrivande meddelande om status. Förklara till exempel varför hänvisningen bröts.                              |
| ReferralType        | [ReferralType](referral-resources.md#referraltype)                   | Representerar referens typen.                                                                                        |
| Kvalificering       | [ReferralQualification](referral-resources.md#referralqualification) | Representerar referensens kvalitet.                                                                              |
| CustomerProfile     | [CustomerProfile](referral-resources.md#customerprofile)             | Kundens kontakt uppgifter.                                                                                        |
| Samtycke             | [Samtycke](referral-resources.md#consent)                             | Medgivande flaggor runt delning av information med andra organisationer och gör det möjligt för dem att kontakta användare.                |
| Information             | [ReferralDetails](referral-resources.md#referraldetails)             | Kund information, noteringar, avtals värde, valuta stängnings datum.                                                          |
| Team                | [Medlem](referral-resources.md#member)                               | Representerar användare i organisationer som ingår i partner engagemang.                                   |
| InviteContext       | [InviteContext](referral-resources.md#invitecontext)                 | Representerar ytterligare information som en användare kan tillhandahålla när de bjuder in en annan organisation till partner engagemang. |
| Mål         | [ReferralTarget](referral-resources.md#target)        | Representerar ytterligare information som en användare kan tillhandahålla när de bjuder in en annan organisation till partner engagemang.  |

### <a name="status-and-substatus-transition-states"></a>Status och under status över gångs tillstånd

| Status | Tillåten status över gång | Tillåten under status            |
|--------|---------------------------|------------------------------|
| Ny    | Nytt, aktivt, stängt       | Väntar, mottaget            |
| Aktiv | Aktiv, stängd            | Har godkänts                     |
| Stängd | Stängd                    | Vann, förlorad, avböjd, upphör att gälla |

### <a name="request-example"></a>Exempel på begäran

```http
PUT https://api.partner.microsoft.com/v1.0/engagements/referrals/49d90c72-3326-4f61-aacc-2cb57970448c HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "id": "49d90c72-3326-4f61-aacc-2cb57970448c",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:40:42.6178337Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "closingDateTime": "2018-11-14T00:00:00Z",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",

}
```

> [!IMPORTANT]
> Ta bort `"links": { }` objektet från placerings resursen.

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden den ifyllda [hänvisnings](referral-resources.md) resursen i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:43:38.9948636Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",
    "links": {
        "relatedReferrals": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals?$filter=engagementId eq '37ef26aa-1d15-4533-9f93-a69bd33ab1e5'",
            "method": "GET"
        },
        "self": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals/4111fffc-f9ee-4d53-bba6-569135228642",
            "method": "GET"
        }
    }
}
```