---
title: Uppdatera en lead eller en affärsmöjlighet
description: Gör att du kan uppdatera lead-eller affärs möjlighets information.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: abfe7308f46cd65b9358b369f6fa05bcca4c1df2
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770643"
---
# <a name="update-a-lead-or-opportunity"></a>Uppdatera en lead eller en affärsmöjlighet

Gäller för:

- Partner-API

I det här avsnittet beskrivs hur du uppdaterar lead-eller affärs möjlighets information, till exempel avtals värde, uppskattat stängnings datum eller hantera försäljnings stegen i annan information.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner-API-autentisering](api-authentication.md). Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.
- Detta API stöder för närvarande endast användar åtkomst där partners måste vara i någon av följande roller: global administratör, referens administratör eller hänvisnings användare.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                       |
|---------|-------------------------------------------------------------------|
| **9.0a** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="uri-parameter"></a>URI-parameter


| Namn                   | Typ     | Obligatorisk | Beskrivning                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Id                      | sträng   | Yes       | Den unika identifieraren för en lead eller en samförsäljnings möjlighet       |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner rest-rubriker](headers.md) .

### <a name="request-body"></a>Begärandetext

Begär ande texten följer [JSON-patch](https://tools.ietf.org/html/rfc6902) -formatet. Ett JSON-patch-dokument har en matris med åtgärder. Varje åtgärd identifierar en viss typ av ändring. Exempel på sådana ändringar är att lägga till ett mat ris element eller ersätta ett egenskaps värde.

> [!Important]
> API: et stöder för närvarande endast- `replace` och- `add` åtgärder.

### <a name="request-example"></a>Exempel på begäran

```http
PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
Authorization: Bearer <token>
Content-Type: application/json
Prefer: return=representation

[
    {
        "op": "replace",
        "path": "/details/dealValue",
        "value": "10000"
    },
    {
        "op": "add",
        "path": "/team/-",
        "value": {
            "email": "jane.doe@contoso.com",
            "firstName": "Jane",
            "lastName": "Doe",
            "phoneNumber": "0000000001"
        }
    }
]
```

> [!Note]
> Om rubriken **If-Match** skickas, används den för samtidighets kontroll.

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svars texten den uppdaterade [leaden eller affärs möjligheten](referral-resources.md).


### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en [HTTP-statuskod](error-codes.md) som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.

### <a name="response-example"></a>Exempel på svar

``` http
HTTP/1.1 204 No Content
Content-Length: 0
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
```

> [!Tip]
> Svars texten är beroende av **föredra** -rubriken. Om värdet för huvudet utelämnas i begäran är svars texten Tom med HTTP-statuskod 204. Lägg till i `Prefer: return=representation` rubriken för att få den uppdaterade leaden eller affärs möjligheten.

## <a name="sample-requests"></a>Exempel förfrågningar

1. Uppdaterar det avtalade värdet för affärs möjligheten till 10000 och uppdaterar anteckningarna. Det finns inga samtidighets kontroller på grund av avsaknad i `If-Match` huvudet.
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace","path":"/details/dealValue","value":"10000"},
        {"op":"replace","path":"/details/notes","value":"Lorem ipsum dolor sit amet."}
    ]
    ```

2. Uppdaterar statusen för ett lead eller en affärs möjlighet till uppnådd.
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace", "path":"/status", "value":"Closed"},
        {"op":"replace", "path":"/substatus", "value":"Won"}
    ]
    ```

    > [!Important]
    > `status`Fälten och `substatus` ska överensstämma med den tillåtna uppsättningen över gångs värden enligt beskrivningen [här](referral-resources.md).

3. Lägger till en ny medlem från din organisation i lead-eller affärs möjlighets teamet. Svaret kommer att innehålla det uppdaterade leadet eller affärs möjligheten på grund av förekomsten av `Prefer: return=representation` huvudet.

    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    Prefer: return=representation
    
    [
        {
            "op": "add",
            "path": "/team/-",
            "value": {
                "email": "jane.doe@contoso.com",
                "firstName": "Jane",
                "lastName": "Doe",
                "phoneNumber": "0000000001"
            }
        }
    ]
    ```
