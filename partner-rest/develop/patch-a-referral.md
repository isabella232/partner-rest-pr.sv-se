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
# <a name="update-a-lead-or-opportunity"></a><span data-ttu-id="96746-103">Uppdatera en lead eller en affärsmöjlighet</span><span class="sxs-lookup"><span data-stu-id="96746-103">Update a lead or opportunity</span></span>

<span data-ttu-id="96746-104">Gäller för:</span><span class="sxs-lookup"><span data-stu-id="96746-104">Applies to:</span></span>

- <span data-ttu-id="96746-105">Partner-API</span><span class="sxs-lookup"><span data-stu-id="96746-105">Partner API</span></span>

<span data-ttu-id="96746-106">I det här avsnittet beskrivs hur du uppdaterar lead-eller affärs möjlighets information, till exempel avtals värde, uppskattat stängnings datum eller hantera försäljnings stegen i annan information.</span><span class="sxs-lookup"><span data-stu-id="96746-106">This topic explains how to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96746-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="96746-107">Prerequisites</span></span>

- <span data-ttu-id="96746-108">Autentiseringsuppgifter enligt beskrivningen i [partner-API-autentisering](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="96746-108">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="96746-109">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="96746-109">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="96746-110">Detta API stöder för närvarande endast användar åtkomst där partners måste vara i någon av följande roller: global administratör, referens administratör eller hänvisnings användare.</span><span class="sxs-lookup"><span data-stu-id="96746-110">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="96746-111">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="96746-111">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="96746-112">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="96746-112">Request syntax</span></span>

| <span data-ttu-id="96746-113">Metod</span><span class="sxs-lookup"><span data-stu-id="96746-113">Method</span></span>  | <span data-ttu-id="96746-114">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="96746-114">Request URI</span></span>                                                       |
|---------|-------------------------------------------------------------------|
| <span data-ttu-id="96746-115">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="96746-115">**PATCH**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="uri-parameter"></a><span data-ttu-id="96746-116">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="96746-116">URI parameter</span></span>


| <span data-ttu-id="96746-117">Namn</span><span class="sxs-lookup"><span data-stu-id="96746-117">Name</span></span>                   | <span data-ttu-id="96746-118">Typ</span><span class="sxs-lookup"><span data-stu-id="96746-118">Type</span></span>     | <span data-ttu-id="96746-119">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="96746-119">Required</span></span> | <span data-ttu-id="96746-120">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="96746-120">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="96746-121">Id</span><span class="sxs-lookup"><span data-stu-id="96746-121">Id</span></span>                      | <span data-ttu-id="96746-122">sträng</span><span class="sxs-lookup"><span data-stu-id="96746-122">string</span></span>   | <span data-ttu-id="96746-123">Yes</span><span class="sxs-lookup"><span data-stu-id="96746-123">Yes</span></span>       | <span data-ttu-id="96746-124">Den unika identifieraren för en lead eller en samförsäljnings möjlighet</span><span class="sxs-lookup"><span data-stu-id="96746-124">The unique identifier for a lead or co-sell opportunity</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="96746-125">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="96746-125">Request headers</span></span>

<span data-ttu-id="96746-126">Mer information finns i [partner rest-rubriker](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="96746-126">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="96746-127">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="96746-127">Request body</span></span>

<span data-ttu-id="96746-128">Begär ande texten följer [JSON-patch](https://tools.ietf.org/html/rfc6902) -formatet.</span><span class="sxs-lookup"><span data-stu-id="96746-128">The request body follows the [Json Patch](https://tools.ietf.org/html/rfc6902) format.</span></span> <span data-ttu-id="96746-129">Ett JSON-patch-dokument har en matris med åtgärder.</span><span class="sxs-lookup"><span data-stu-id="96746-129">A JSON Patch document has an array of operations.</span></span> <span data-ttu-id="96746-130">Varje åtgärd identifierar en viss typ av ändring.</span><span class="sxs-lookup"><span data-stu-id="96746-130">Each operation identifies a particular type of change.</span></span> <span data-ttu-id="96746-131">Exempel på sådana ändringar är att lägga till ett mat ris element eller ersätta ett egenskaps värde.</span><span class="sxs-lookup"><span data-stu-id="96746-131">Examples of such changes include adding an array element or replacing a property value.</span></span>

> [!Important]
> <span data-ttu-id="96746-132">API: et stöder för närvarande endast- `replace` och- `add` åtgärder.</span><span class="sxs-lookup"><span data-stu-id="96746-132">The API currently only supports the `replace` and `add` operations.</span></span>

### <a name="request-example"></a><span data-ttu-id="96746-133">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="96746-133">Request example</span></span>

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
> <span data-ttu-id="96746-134">Om rubriken **If-Match** skickas, används den för samtidighets kontroll.</span><span class="sxs-lookup"><span data-stu-id="96746-134">If the **If-Match** header is passed, it will be used for concurrency control.</span></span>

## <a name="rest-response"></a><span data-ttu-id="96746-135">REST-svar</span><span class="sxs-lookup"><span data-stu-id="96746-135">REST Response</span></span>

<span data-ttu-id="96746-136">Om det lyckas innehåller svars texten den uppdaterade [leaden eller affärs möjligheten](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="96746-136">If successful, the response body contains the updated [lead or opportunity](referral-resources.md).</span></span>


### <a name="response-success-and-error-codes"></a><span data-ttu-id="96746-137">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="96746-137">Response success and error codes</span></span>

<span data-ttu-id="96746-138">Varje svar levereras med en [HTTP-statuskod](error-codes.md) som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="96746-138">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="96746-139">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="96746-139">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="96746-140">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="96746-140">Response example</span></span>

``` http
HTTP/1.1 204 No Content
Content-Length: 0
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
```

> [!Tip]
> <span data-ttu-id="96746-141">Svars texten är beroende av **föredra** -rubriken.</span><span class="sxs-lookup"><span data-stu-id="96746-141">The response body depends on the **Prefer** header.</span></span> <span data-ttu-id="96746-142">Om värdet för huvudet utelämnas i begäran är svars texten Tom med HTTP-statuskod 204.</span><span class="sxs-lookup"><span data-stu-id="96746-142">If the header value is omitted in the request, the response body is empty with a HTTP Status code 204.</span></span> <span data-ttu-id="96746-143">Lägg till i `Prefer: return=representation` rubriken för att få den uppdaterade leaden eller affärs möjligheten.</span><span class="sxs-lookup"><span data-stu-id="96746-143">Add `Prefer: return=representation` to the header to get the updated lead or opportunity.</span></span>

## <a name="sample-requests"></a><span data-ttu-id="96746-144">Exempel förfrågningar</span><span class="sxs-lookup"><span data-stu-id="96746-144">Sample requests</span></span>

1. <span data-ttu-id="96746-145">Uppdaterar det avtalade värdet för affärs möjligheten till 10000 och uppdaterar anteckningarna.</span><span class="sxs-lookup"><span data-stu-id="96746-145">Updates the deal value for the opportunity to 10000 and updates the notes.</span></span> <span data-ttu-id="96746-146">Det finns inga samtidighets kontroller på grund av avsaknad i `If-Match` huvudet.</span><span class="sxs-lookup"><span data-stu-id="96746-146">There are no concurrency checks because of the absense of the `If-Match` header.</span></span>
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace","path":"/details/dealValue","value":"10000"},
        {"op":"replace","path":"/details/notes","value":"Lorem ipsum dolor sit amet."}
    ]
    ```

2. <span data-ttu-id="96746-147">Uppdaterar statusen för ett lead eller en affärs möjlighet till uppnådd.</span><span class="sxs-lookup"><span data-stu-id="96746-147">Updates the status of a lead or opportunity to Won.</span></span>
    
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
    > <span data-ttu-id="96746-148">`status`Fälten och `substatus` ska överensstämma med den tillåtna uppsättningen över gångs värden enligt beskrivningen [här](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="96746-148">The `status` and `substatus` fields should conform to the allowed set of transition values as described [here](referral-resources.md).</span></span>

3. <span data-ttu-id="96746-149">Lägger till en ny medlem från din organisation i lead-eller affärs möjlighets teamet.</span><span class="sxs-lookup"><span data-stu-id="96746-149">Adds a new member from your organization to the lead or opportunity team.</span></span> <span data-ttu-id="96746-150">Svaret kommer att innehålla det uppdaterade leadet eller affärs möjligheten på grund av förekomsten av `Prefer: return=representation` huvudet.</span><span class="sxs-lookup"><span data-stu-id="96746-150">The response will contain the updated lead or opportunity because of the presence of the `Prefer: return=representation` header.</span></span>

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
