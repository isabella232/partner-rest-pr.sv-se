---
title: Hämta en lead eller en affärsmöjlighet utifrån ID
description: Få ett lead eller en affärs möjlighet utifrån ID.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: dcfaea393afc6a9d09946b4c31b7168ba26aa255
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770636"
---
# <a name="get-a-lead-or-opportunity-by-id"></a><span data-ttu-id="28b5d-103">Hämta en lead eller en affärsmöjlighet utifrån ID</span><span class="sxs-lookup"><span data-stu-id="28b5d-103">Get a lead or opportunity by Id</span></span>

<span data-ttu-id="28b5d-104">Gäller för:</span><span class="sxs-lookup"><span data-stu-id="28b5d-104">Applies to:</span></span>

- <span data-ttu-id="28b5d-105">Partner-API</span><span class="sxs-lookup"><span data-stu-id="28b5d-105">Partner API</span></span>

<span data-ttu-id="28b5d-106">I det här avsnittet förklaras hur du får en lead-eller co Sälj-affärs möjlighet efter ID.</span><span class="sxs-lookup"><span data-stu-id="28b5d-106">This topic explains how to get a lead or co-sell opportunity by Id.</span></span>

> [!Note]
> <span data-ttu-id="28b5d-107">Leads som tas emot från Microsofts kommersiella marknads platser (Azure Marketplace och AppSource) stöds inte.</span><span class="sxs-lookup"><span data-stu-id="28b5d-107">Leads received from the Microsoft commercial marketplace (Azure Marketplace and AppSource) are not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="28b5d-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="28b5d-108">Prerequisites</span></span>

- <span data-ttu-id="28b5d-109">Autentiseringsuppgifter enligt beskrivningen i [partner-API-autentisering](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="28b5d-109">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="28b5d-110">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="28b5d-110">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="28b5d-111">Detta API stöder för närvarande endast användar åtkomst där partners måste vara i någon av följande roller: global administratör, referens administratör eller hänvisnings användare.</span><span class="sxs-lookup"><span data-stu-id="28b5d-111">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="28b5d-112">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="28b5d-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="28b5d-113">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="28b5d-113">Request syntax</span></span>

| <span data-ttu-id="28b5d-114">Metod</span><span class="sxs-lookup"><span data-stu-id="28b5d-114">Method</span></span>   | <span data-ttu-id="28b5d-115">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="28b5d-115">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="28b5d-116">**TA**</span><span class="sxs-lookup"><span data-stu-id="28b5d-116">**GET**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}>                                     |

### <a name="uri-parameter"></a><span data-ttu-id="28b5d-117">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="28b5d-117">URI parameter</span></span>


| <span data-ttu-id="28b5d-118">Namn</span><span class="sxs-lookup"><span data-stu-id="28b5d-118">Name</span></span>                   | <span data-ttu-id="28b5d-119">Typ</span><span class="sxs-lookup"><span data-stu-id="28b5d-119">Type</span></span>     | <span data-ttu-id="28b5d-120">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="28b5d-120">Required</span></span> | <span data-ttu-id="28b5d-121">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="28b5d-121">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="28b5d-122">Id</span><span class="sxs-lookup"><span data-stu-id="28b5d-122">Id</span></span>                      | <span data-ttu-id="28b5d-123">sträng</span><span class="sxs-lookup"><span data-stu-id="28b5d-123">string</span></span>   | <span data-ttu-id="28b5d-124">Yes</span><span class="sxs-lookup"><span data-stu-id="28b5d-124">Yes</span></span>       | <span data-ttu-id="28b5d-125">Den unika identifieraren för en lead eller en samförsäljnings möjlighet</span><span class="sxs-lookup"><span data-stu-id="28b5d-125">The unique identifier for a lead or co-sell opportunity</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="28b5d-126">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="28b5d-126">Request headers</span></span>

<span data-ttu-id="28b5d-127">Mer information finns i [partner rest-rubriker](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="28b5d-127">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="28b5d-128">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="28b5d-128">Request body</span></span>

<span data-ttu-id="28b5d-129">Inga.</span><span class="sxs-lookup"><span data-stu-id="28b5d-129">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="28b5d-130">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="28b5d-130">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id} HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="28b5d-131">REST-svar</span><span class="sxs-lookup"><span data-stu-id="28b5d-131">REST response</span></span>

<span data-ttu-id="28b5d-132">Om det lyckas innehåller svars texten [lead eller affärs möjlighet](referral-resources.md) som matchar ID: t.</span><span class="sxs-lookup"><span data-stu-id="28b5d-132">If successful, the response body contains the [lead or opportunity](referral-resources.md) matching the Id.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="28b5d-133">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="28b5d-133">Response success and error codes</span></span>

<span data-ttu-id="28b5d-134">Varje svar levereras med en [HTTP-statuskod](error-codes.md) som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="28b5d-134">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="28b5d-135">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="28b5d-135">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="28b5d-136">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="28b5d-136">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Type: application/json
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731

{
    "@odata.context": "https://api.partner.microsoft.com/v1.0/engagments/referrals/$metadata#Referrals/$entity",
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
      "notes": "We are interested in deploying Microsoft 365 and are looking forsupport in training our employees. Can you help?",
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
        "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'",
        "method": "GET"
      },
      "self": {
        "uri": "https://api.partner.microsoft.com/v1.0/engagements/referralsc5fbb3b6-be74-4795-9fb5-4324c73fed37",
        "method": "GET"
      }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\""
}
```

> [!Note]
> <span data-ttu-id="28b5d-137">Fälten i exemplet illustratration ovan är inte uttömmande.</span><span class="sxs-lookup"><span data-stu-id="28b5d-137">The fields in the example illustratration above are not exhaustive.</span></span> <span data-ttu-id="28b5d-138">Det faktiska API-svaret innehåller fler fält som kund-och partner team.</span><span class="sxs-lookup"><span data-stu-id="28b5d-138">The actual API response contains more fields like the customer and partner teams.</span></span> <span data-ttu-id="28b5d-139">En fullständig lista över vilka fält som stöds finns i avsnittet om [referens resurser](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="28b5d-139">For the full list of supported fields, see [referral resources](referral-resources.md).</span></span>