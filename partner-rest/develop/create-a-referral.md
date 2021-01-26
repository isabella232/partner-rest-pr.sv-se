---
title: Skapa en hänvisning
description: 'Skapa oberoende eller delade referenser i partner-API: et.'
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6aab4b5f45030c3c16294b2929b1a6d3086fb951
ms.sourcegitcommit: 3c165938f544ff226cbe11ca21ed5aa00448d9b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "97770611"
---
# <a name="create-a-referral"></a>Skapa en hänvisning

Gäller för:

- Partner-API

I det här avsnittet beskrivs hur du skapar en hänvisning. Det finns två typer av [ReferralType](referral-resources.md#referraltype):

1. Oberoende: där en hänvisning är synlig för en partner.
2. Delad: där en hänvisning är synlig för två parter som arbetar tillsammans. Om exempelvis Microsoft och en partner arbetar tillsammans i ett samordnat avtal, kan en hänvisning delas mellan båda parter. Mer information finns i avsnittet [skapa en delad hänvisning](#create-a-shared-referral).

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner-API-autentisering](api-authentication.md). Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                  |
|---------|--------------------------------------------------------------|
| **EFTER** | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

### <a name="request-headers"></a>Begärandehuvuden

- Mer information finns i [partner API rest-huvuden](headers.md) .

### <a name="request-body"></a>Begärandetext

Den här tabellen beskriver [hänvisnings](referral-resources.md) egenskaperna i begär ande texten för en varumärkes ny hänvisning.

| Egenskap            | Typ                                                                 | Beskrivning                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Name                | sträng                                                               | Namnet på referensen.                                                                                            |
| ExternalReferenceId | sträng                                                               | En extern identifierare för referensen. Till exempel ditt eget Dynamics 365-lead eller affärs möjlighets-ID.                   |
| Status              | [ReferralStatus](referral-resources.md#referralstatus)               | En [uppräkning](https://docs.microsoft.com/dotnet/api/system.enum) med värden som anger hänvisnings status.          |
| Substatus           | [ReferralSubstatus](referral-resources.md#referralsubstatus)         | En [Enum](https://docs.microsoft.com/dotnet/api/system.enum) med värden som anger hänvisningens under status.       |
| StatusReason        | sträng                                                               | Ett beskrivande meddelande om status. Förklara till exempel varför hänvisningen bröts.                            |
| ReferralType        | [ReferralType](referral-resources.md#referraltype)                   | Representerar referens typen. **Kunna.**                                                                                        |
| Kvalificering       | [ReferralQualification](referral-resources.md#referralqualification) | Representerar referensens kvalitet.                                                                              |
| CustomerProfile     | [CustomerProfile](referral-resources.md#customerprofile)             | Kundens kontakt uppgifter.  **Kunna.**                                                                                      |
| Samtycke             | [Samtycke](referral-resources.md#consent)                             | Medgivande flaggor runt delning av information med andra organisationer och gör det möjligt för dem att kontakta användare. **Obligatoriskt.**               |
| Information             | [ReferralDetails](referral-resources.md#referraldetails)             | Kund information, noteringar, avtals värde, valuta stängnings datum. **Kunna.**                                                           |
| Team                | [Medlem](referral-resources.md#member)                               | Representerar användare i organisationer som ingår i partner engagemang.                                   |
| InviteContext       | [InviteContext](referral-resources.md#invitecontext)                 | Representerar ytterligare information som en användare kan tillhandahålla när de bjuder in en annan organisation till partner engagemang. |
| Mål         | [ReferralTarget](referral-resources.md#target)        | Representerar ytterligare information som en användare kan tillhandahålla när de bjuder in en annan organisation till partner engagemang.  |

#### <a name="status--substatus-transition-states"></a>Status & över gångs status för under status

| Status | Tillåten status över gång | Tillåten under status            |
|--------|---------------------------|------------------------------|
| Ny    | Nytt, aktivt, stängt       | Väntar, mottaget            |
| Aktiv | Aktiv, stängd            | Har godkänts                     |
| Stängd | Stängd                    | Vann, förlorad, avböjd, upphör att gälla |

### <a name="request-example"></a>Exempel på begäran

```http
POST https://api.partner.microsoft.com/v1.0/engagements/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "name": "Test Cosell Invite_20",
    "status": "New",
    "substatus": "Pending",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
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
    }
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden den ifyllda [hänvisnings](referral-resources.md) resursen i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "name": "Test Cosell Invite_20",
    "externalReferenceId": null,
    "createdDateTime": "2019-02-23T02:05:23.2931817Z",
    "updatedDateTime": "2019-02-23T02:05:23.2931817Z",
    "expirationDateTime": null,
    "status": "Active",
    "substatus": "Accepted",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "eTag": "\"00006d10-0000-0000-0000-5c70aa630000\"",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
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

## <a name="create-a-shared-referral"></a>Skapa en delad hänvisning

Det finns två steg för att skapa en hänvisning till den **delade** [hänvisnings typen](referral-resources.md#referraltype).

1. [Skapa din delade hänvisning](#create-your-referral)
2. [Skapa en ansluten hänvisning för den andra parten](#create-a-connected-referral)

Följande flödes diagram illustrerar de här två stegen i skapa en delad referens.

![Flödes diagram som visar en delad hänvisning med 2 hänvisningar som är anslutna via Microsoft partner-API: et](../images/SharedReferral.png)

### <a name="create-your-referral"></a>Skapa din hänvisning

1. Skapa en hänvisning med [ReferralType](referral-resources.md#referraltype) inställt på delad.
2. Kopiera **engagementId** från retur svaret.

[ReferralTarget](referral-resources.md#target) -exempel för hänvisning

```json
"target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-ABC-DEF"
        }
    ]
```

### <a name="create-a-connected-referral"></a>Skapa en ansluten hänvisning

1. Skapa en annan hänvisning för Microsoft.
2. Inkludera **enagementId** från din hänvisning så att de är kopplade till varandra.

[ReferralTarget](referral-resources.md#target) -exempel för Microsoft referral

```json
"target": [
        {
            "type": "BusinessProfileLocation",
            "id": "msft"
        }
    ]
```