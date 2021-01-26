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
# <a name="get-the-list-of-leads-and-opportunities"></a><span data-ttu-id="7d70c-103">Hämta listan över leads och affärsmöjligheter</span><span class="sxs-lookup"><span data-stu-id="7d70c-103">Get the list of leads and opportunities</span></span>

<span data-ttu-id="7d70c-104">Gäller för:</span><span class="sxs-lookup"><span data-stu-id="7d70c-104">Applies to:</span></span>

- <span data-ttu-id="7d70c-105">Partner-API</span><span class="sxs-lookup"><span data-stu-id="7d70c-105">Partner API</span></span>

 <span data-ttu-id="7d70c-106">I det här avsnittet beskrivs hur du hämtar listan över leads som tas emot från Microsoft Solution Provider-sidan och samförsäljnings möjligheter som tagits emot från Microsofts säljare eller andra partner.</span><span class="sxs-lookup"><span data-stu-id="7d70c-106">This topic explains how to get the list of leads received from Microsoft solution provider page and co-sell opportunities received from Microsoft sellers or other partners.</span></span> <span data-ttu-id="7d70c-107">Detta kommer också att hämta listan över samförsäljnings möjligheter eller pipeline-avtal som skapats av din organisation.</span><span class="sxs-lookup"><span data-stu-id="7d70c-107">This will also fetch the list of co-sell opportunities or pipeline deals created by your organization.</span></span>

> [!Note]
> <span data-ttu-id="7d70c-108">Leads som tas emot från Microsofts kommersiella marknads platser (Azure Marketplace och AppSource) stöds inte.</span><span class="sxs-lookup"><span data-stu-id="7d70c-108">Leads received from the Microsoft commercial marketplace (Azure Marketplace and AppSource) are not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d70c-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="7d70c-109">Prerequisites</span></span>

- <span data-ttu-id="7d70c-110">Autentiseringsuppgifter enligt beskrivningen i [partner-API-autentisering](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7d70c-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="7d70c-111">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="7d70c-111">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="7d70c-112">Detta API stöder för närvarande endast användar åtkomst där partners måste vara i någon av följande roller: global administratör, referens administratör eller hänvisnings användare.</span><span class="sxs-lookup"><span data-stu-id="7d70c-112">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="7d70c-113">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="7d70c-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7d70c-114">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="7d70c-114">Request syntax</span></span>

| <span data-ttu-id="7d70c-115">Metod</span><span class="sxs-lookup"><span data-stu-id="7d70c-115">Method</span></span>  | <span data-ttu-id="7d70c-116">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="7d70c-116">Request URI</span></span>                                                    |
|:--------|:---------------------------------------------------------------|
| <span data-ttu-id="7d70c-117">**TA**</span><span class="sxs-lookup"><span data-stu-id="7d70c-117">**GET**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

#### <a name="supported-odata-operations"></a><span data-ttu-id="7d70c-118">OData-åtgärder som stöds</span><span class="sxs-lookup"><span data-stu-id="7d70c-118">Supported OData operations</span></span>

| <span data-ttu-id="7d70c-119">Name</span><span class="sxs-lookup"><span data-stu-id="7d70c-119">Name</span></span>     | <span data-ttu-id="7d70c-120">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="7d70c-120">Description</span></span>     | <span data-ttu-id="7d70c-121">Krävs</span><span class="sxs-lookup"><span data-stu-id="7d70c-121">Required</span></span>    | <span data-ttu-id="7d70c-122">Exempel</span><span class="sxs-lookup"><span data-stu-id="7d70c-122">Example</span></span>                                                                                                                                                                                                                                                     |
|:---------|:----------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7d70c-123">$select</span><span class="sxs-lookup"><span data-stu-id="7d70c-123">$select</span></span>  | <span data-ttu-id="7d70c-124">Fält väljs</span><span class="sxs-lookup"><span data-stu-id="7d70c-124">Selects fields</span></span>  | <span data-ttu-id="7d70c-125">No</span><span class="sxs-lookup"><span data-stu-id="7d70c-125">No</span></span>          | `/referrals?$select=id,status,customerProfile`                                                                                                                                                                                                              |
| <span data-ttu-id="7d70c-126">$filter</span><span class="sxs-lookup"><span data-stu-id="7d70c-126">$filter</span></span>  | <span data-ttu-id="7d70c-127">Filter resultat</span><span class="sxs-lookup"><span data-stu-id="7d70c-127">Filters results</span></span> | <span data-ttu-id="7d70c-128">Rekommenderas</span><span class="sxs-lookup"><span data-stu-id="7d70c-128">Recommended</span></span> | `/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'` <br/> `/referrals?$filter=status eq 'New' and qualification eq 'SalesQualified'` <br/> `/referrals?$filter=customerProfile/address/country eq 'US' and direction eq 'Incoming'` |
| <span data-ttu-id="7d70c-129">$orderby</span><span class="sxs-lookup"><span data-stu-id="7d70c-129">$orderby</span></span> | <span data-ttu-id="7d70c-130">Order resultat</span><span class="sxs-lookup"><span data-stu-id="7d70c-130">Orders results</span></span>  | <span data-ttu-id="7d70c-131">Rekommenderas</span><span class="sxs-lookup"><span data-stu-id="7d70c-131">Recommended</span></span> | `/referrals?$orderby=createdDateTime desc`                                                                                                                                                                                                                  |

#### <a name="supported-orderby-parameters"></a><span data-ttu-id="7d70c-132">OrderBy-parametrar som stöds</span><span class="sxs-lookup"><span data-stu-id="7d70c-132">Supported orderby parameters</span></span>

<span data-ttu-id="7d70c-133">Använd följande $orderby parametrar för att sortera listan över leads och affärs möjligheter</span><span class="sxs-lookup"><span data-stu-id="7d70c-133">Use the following $orderby parameters to sort the list of leads and opportunities</span></span>

| <span data-ttu-id="7d70c-134">Namn</span><span class="sxs-lookup"><span data-stu-id="7d70c-134">Name</span></span>            | <span data-ttu-id="7d70c-135">Typ</span><span class="sxs-lookup"><span data-stu-id="7d70c-135">Type</span></span>     | <span data-ttu-id="7d70c-136">Description</span><span class="sxs-lookup"><span data-stu-id="7d70c-136">Description</span></span>                                       |
|:----------------|:---------|:--------------------------------------------------|
| <span data-ttu-id="7d70c-137">createdDateTime</span><span class="sxs-lookup"><span data-stu-id="7d70c-137">createdDateTime</span></span> | <span data-ttu-id="7d70c-138">DateTime</span><span class="sxs-lookup"><span data-stu-id="7d70c-138">DateTime</span></span> | <span data-ttu-id="7d70c-139">Datum och tid då lead eller affärs möjlighet skapades</span><span class="sxs-lookup"><span data-stu-id="7d70c-139">Creation date and time of the lead or opportunity</span></span> |
| <span data-ttu-id="7d70c-140">updatedDateTime</span><span class="sxs-lookup"><span data-stu-id="7d70c-140">updatedDateTime</span></span> | <span data-ttu-id="7d70c-141">DateTime</span><span class="sxs-lookup"><span data-stu-id="7d70c-141">DateTime</span></span> | <span data-ttu-id="7d70c-142">Uppdatera datum och tid för lead eller affärs möjlighet</span><span class="sxs-lookup"><span data-stu-id="7d70c-142">Update date and time of the lead or opportunity</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="7d70c-143">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="7d70c-143">Request headers</span></span>

<span data-ttu-id="7d70c-144">Mer information finns i [partner rest-rubriker](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="7d70c-144">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="7d70c-145">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="7d70c-145">Request body</span></span>

<span data-ttu-id="7d70c-146">Inga.</span><span class="sxs-lookup"><span data-stu-id="7d70c-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7d70c-147">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="7d70c-147">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$orderby=createdDateTime desc HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="7d70c-148">REST-svar</span><span class="sxs-lookup"><span data-stu-id="7d70c-148">REST response</span></span>

<span data-ttu-id="7d70c-149">Om det lyckas innehåller svars texten en samling [leads och/eller affärs möjligheter](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="7d70c-149">If successful, the response body contains a collection of [leads and/or opportunities](referral-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7d70c-150">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="7d70c-150">Response success and error codes</span></span>

<span data-ttu-id="7d70c-151">Varje svar levereras med en [HTTP-statuskod](error-codes.md) som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="7d70c-151">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7d70c-152">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="7d70c-152">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="7d70c-153">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="7d70c-153">Response example</span></span>

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

<span data-ttu-id="7d70c-154">Använd `@odata.nextLink` för att hämta nästa resultat sida.</span><span class="sxs-lookup"><span data-stu-id="7d70c-154">Use the `@odata.nextLink` to get the next page of results.</span></span>

> [!Note]
> <span data-ttu-id="7d70c-155">Fälten i exemplet illustratration ovan är inte uttömmande.</span><span class="sxs-lookup"><span data-stu-id="7d70c-155">The fields in the example illustratration above are not exhaustive.</span></span> <span data-ttu-id="7d70c-156">Det faktiska API-svaret innehåller fler fält som kund-och partner team.</span><span class="sxs-lookup"><span data-stu-id="7d70c-156">The actual API response contains more fields like the customer and partner teams.</span></span> <span data-ttu-id="7d70c-157">En fullständig lista över vilka fält som stöds finns i avsnittet om [referens resurser](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="7d70c-157">For the full list of supported fields, see [referral resources](referral-resources.md).</span></span>

## <a name="sample-requests"></a><span data-ttu-id="7d70c-158">Exempel förfrågningar</span><span class="sxs-lookup"><span data-stu-id="7d70c-158">Sample requests</span></span>

1. <span data-ttu-id="7d70c-159">Hämtar de 10 främsta senaste ingående samförsäljnings möjligheterna.</span><span class="sxs-lookup"><span data-stu-id="7d70c-159">Gets the top 10 most recent inbound co-sell opportunities.</span></span> <span data-ttu-id="7d70c-160">Begäran kommer att hämta affärs möjligheter som initieras av en Microsoft-säljare eller en annan partner som bjuder in din organisation att delta i en samförsäljnings aktivitet.</span><span class="sxs-lookup"><span data-stu-id="7d70c-160">The request will fetch opportunities initiated by a Microsoft sales representative or another partner, inviting your organization to participate in a co-selling activity.</span></span>
    
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(type eq 'Shared' and direction eq 'Incoming')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

2. <span data-ttu-id="7d70c-161">Hämtar de senaste inkommande leads och affärs möjligheter som inte har svarat på.</span><span class="sxs-lookup"><span data-stu-id="7d70c-161">Gets the most recent inbound leads and opportunities that have not been responded to.</span></span>  

    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(direction eq 'Incoming' and substatus eq 'Pending')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

    > [!Important]
    > <span data-ttu-id="7d70c-162">Om du inte svarar på ett lead eller en affärs möjlighet inom den tilldelade tiden (14 dagar), kommer vi att arkivera det som upphört att gälla och meddela antingen Microsoft eller partnern som skickade dig den här möjligheten.</span><span class="sxs-lookup"><span data-stu-id="7d70c-162">If you don't respond to a lead or opportunity within the allotted time (currently 14 days), we'll archive it as Expired and notify either Microsoft or the partner who sent you this opportunity.</span></span>

3. <span data-ttu-id="7d70c-163">Hämtar de senaste aktiva samsäljiga affärs möjligheterna som har startats av din organisation och som bearbetas av en bestämd säljare.</span><span class="sxs-lookup"><span data-stu-id="7d70c-163">Gets the most recent active co-sell opportunities initiated by your organization and being worked on by a specific seller.</span></span>
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=status eq 'Active' and direction eq 'Outgoing' and type eq 'Shared' and team/any(t:t/email eq 'r2d2@contoso.com')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```