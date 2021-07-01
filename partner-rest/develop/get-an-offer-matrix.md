---
title: Hämta en erbjudandematris
description: Hämta en erbjudandematris för ett visst datum. Stöder filter för att hämta historik per månad.
ms.date: 02/11/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e53276c1170febab002d35a42c88c1f96f7b7428
ms.sourcegitcommit: 9e64d6358ef4e1ac2d3e0d36cd63490a5f760b38
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/01/2021
ms.locfileid: "113131305"
---
# <a name="get-an-offer-matrix"></a><span data-ttu-id="bb26e-104">Hämta en erbjudandematris</span><span class="sxs-lookup"><span data-stu-id="bb26e-104">Get an offer matrix</span></span>

<span data-ttu-id="bb26e-105">Gäller för:</span><span class="sxs-lookup"><span data-stu-id="bb26e-105">Applies to:</span></span>

- <span data-ttu-id="bb26e-106">Partner-API</span><span class="sxs-lookup"><span data-stu-id="bb26e-106">Partner API</span></span>
- <span data-ttu-id="bb26e-107">Den tekniska förhandsversionen av den nya handelsupplevelsen M365/D365.</span><span class="sxs-lookup"><span data-stu-id="bb26e-107">The M365/D365 New Commerce experience technical preview.</span></span> <span data-ttu-id="bb26e-108">Nedanstående nya handelsändringar är för närvarande endast tillgängliga för partner som ingår i den tekniska förhandsversionen av den nya M365/D365-handelsupplevelsen.</span><span class="sxs-lookup"><span data-stu-id="bb26e-108">The below New Commerce changes are currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

<span data-ttu-id="bb26e-109">Det här avsnittet beskriver hur du hämtar en erbjudandematris för en viss månad.</span><span class="sxs-lookup"><span data-stu-id="bb26e-109">This topic explains how to get an offer matrix for a given month.</span></span> <span data-ttu-id="bb26e-110">Erbjudandematrisen innehåller egenskaper och inköpsregler för produkterna och SKU:erna.</span><span class="sxs-lookup"><span data-stu-id="bb26e-110">The offer matrix includes properties and purchase rules for the products and skus.</span></span> <span data-ttu-id="bb26e-111">Den här metoden stöder filter för att hämta historik per månad.</span><span class="sxs-lookup"><span data-stu-id="bb26e-111">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb26e-112">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="bb26e-112">Prerequisites</span></span>

- <span data-ttu-id="bb26e-113">Autentiseringsuppgifter enligt beskrivningen [i Partner-API autentisering](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bb26e-113">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="bb26e-114">Det här scenariot stöder endast användarautentisering för program.</span><span class="sxs-lookup"><span data-stu-id="bb26e-114">This scenario only supports application user authentication.</span></span> <span data-ttu-id="bb26e-115">Endast program stöds inte ännu.</span><span class="sxs-lookup"><span data-stu-id="bb26e-115">Application-only is not yet supported.</span></span> <span data-ttu-id="bb26e-116">Partner som får **http-fel:400 bör** läsa dokumentationen [Partner-API autentisering.](api-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="bb26e-116">Partners that experience **http error:400** should consult the [Partner API authentication](api-authentication.md) documentation.</span></span>
- <span data-ttu-id="bb26e-117">Det här API:et stöder för närvarande endast användaråtkomst där partner måste ha någon av följande roller: global administratör, administratörsagent eller försäljningsagent.</span><span class="sxs-lookup"><span data-stu-id="bb26e-117">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="bb26e-118">Information</span><span class="sxs-lookup"><span data-stu-id="bb26e-118">Details</span></span>

- <span data-ttu-id="bb26e-119">Aktuella returnerar endast data för uppdaterade nya handelslicensbaserade produkter.</span><span class="sxs-lookup"><span data-stu-id="bb26e-119">Current returns data only for updated new commerce license-based products.</span></span>
- <span data-ttu-id="bb26e-120">Aktuella priser omfattar produkter som är tillgängliga under den aktuella månaden fram till det datum då API:et anropas.</span><span class="sxs-lookup"><span data-stu-id="bb26e-120">Current pricing includes products available during the current month to the date the API is called.</span></span> <span data-ttu-id="bb26e-121">Föregående månader inkluderar datum från och med den sista dagen i den valda månaden.</span><span class="sxs-lookup"><span data-stu-id="bb26e-121">Previous months include date as of the last day of the selected month.</span></span>
- <span data-ttu-id="bb26e-122">Den här metoden returnerar data som en filström.</span><span class="sxs-lookup"><span data-stu-id="bb26e-122">This method returns data as a file stream.</span></span> <span data-ttu-id="bb26e-123">Filströmmen är antingen en .csv eller en komprimerad zip-version av .csv.</span><span class="sxs-lookup"><span data-stu-id="bb26e-123">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="bb26e-124">Information om hur du begär komprimerade filer finns nedan.</span><span class="sxs-lookup"><span data-stu-id="bb26e-124">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="bb26e-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="bb26e-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bb26e-126">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="bb26e-126">Request syntax</span></span>

| <span data-ttu-id="bb26e-127">Metod</span><span class="sxs-lookup"><span data-stu-id="bb26e-127">Method</span></span>   | <span data-ttu-id="bb26e-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="bb26e-128">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bb26e-129">**Få**</span><span class="sxs-lookup"><span data-stu-id="bb26e-129">**GET**</span></span> | <span data-ttu-id="bb26e-130"> https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month={date})/$value</span><span class="sxs-lookup"><span data-stu-id="bb26e-130">https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='{date}')/$value</span></span> |

### <a name="uri-filter-parameters"></a><span data-ttu-id="bb26e-131">URI-filterparametrar</span><span class="sxs-lookup"><span data-stu-id="bb26e-131">URI filter parameters</span></span>

<span data-ttu-id="bb26e-132">Använd följande filterparametrar.</span><span class="sxs-lookup"><span data-stu-id="bb26e-132">Use the following filter parameters.</span></span>

| <span data-ttu-id="bb26e-133">Namn</span><span class="sxs-lookup"><span data-stu-id="bb26e-133">Name</span></span>                   | <span data-ttu-id="bb26e-134">Typ</span><span class="sxs-lookup"><span data-stu-id="bb26e-134">Type</span></span>     | <span data-ttu-id="bb26e-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="bb26e-135">Required</span></span> | <span data-ttu-id="bb26e-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="bb26e-136">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="bb26e-137">Månad</span><span class="sxs-lookup"><span data-stu-id="bb26e-137">Month</span></span>| <span data-ttu-id="bb26e-138">sträng</span><span class="sxs-lookup"><span data-stu-id="bb26e-138">string</span></span>   | <span data-ttu-id="bb26e-139">No</span><span class="sxs-lookup"><span data-stu-id="bb26e-139">No</span></span> | <span data-ttu-id="bb26e-140">Måste följa YYYYMM för det prisark som begärs.</span><span class="sxs-lookup"><span data-stu-id="bb26e-140">Must adhere to YYYYMM for the price sheet being requested.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="bb26e-141">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="bb26e-141">Request headers</span></span>

- <span data-ttu-id="bb26e-142">Mer information finns i Partner REST-huvuden. [](headers.md)</span><span class="sxs-lookup"><span data-stu-id="bb26e-142">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="bb26e-143">Förutom ovanstående huvuden kan prisfiler hämtas som komprimerade, vilket minskar bandbredden och nedladdningstiderna.</span><span class="sxs-lookup"><span data-stu-id="bb26e-143">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="bb26e-144">Som standard komprimeras inte filerna.</span><span class="sxs-lookup"><span data-stu-id="bb26e-144">By default the files are not compressed.</span></span> <span data-ttu-id="bb26e-145">Om du vill hämta komprimerade versioner av filerna kan du inkludera rubrikvärdet nedan.</span><span class="sxs-lookup"><span data-stu-id="bb26e-145">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="bb26e-146">Kom ihåg att komprimerade blad endast är tillgängliga från april 2020 och framåt. Alla blad före april 2020 är bara tillgängliga som inte komprimerade.</span><span class="sxs-lookup"><span data-stu-id="bb26e-146">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="bb26e-147">Huvud</span><span class="sxs-lookup"><span data-stu-id="bb26e-147">Header</span></span>                   | <span data-ttu-id="bb26e-148">Värdetyp</span><span class="sxs-lookup"><span data-stu-id="bb26e-148">Value Type</span></span>     | <span data-ttu-id="bb26e-149">Värde</span><span class="sxs-lookup"><span data-stu-id="bb26e-149">Value</span></span> | <span data-ttu-id="bb26e-150">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="bb26e-150">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="bb26e-151">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="bb26e-151">Accept-Encoding</span></span>| <span data-ttu-id="bb26e-152">sträng</span><span class="sxs-lookup"><span data-stu-id="bb26e-152">string</span></span>   | <span data-ttu-id="bb26e-153">Tömma</span><span class="sxs-lookup"><span data-stu-id="bb26e-153">deflate</span></span>| <span data-ttu-id="bb26e-154">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="bb26e-154">Optional.</span></span> <span data-ttu-id="bb26e-155">Om den utelämnas komprimeras inte filströmmen.</span><span class="sxs-lookup"><span data-stu-id="bb26e-155">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="bb26e-156">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="bb26e-156">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='202101')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="bb26e-157">REST-svar</span><span class="sxs-lookup"><span data-stu-id="bb26e-157">REST response</span></span>

<span data-ttu-id="bb26e-158">Om det lyckas returnerar den här metoden en erbjudandematris som en filström.</span><span class="sxs-lookup"><span data-stu-id="bb26e-158">If successful, this method returns an offer matrix as a file stream.</span></span> <span data-ttu-id="bb26e-159">Filströmmen är antingen en .csv eller en komprimerad zip-version av .csv.</span><span class="sxs-lookup"><span data-stu-id="bb26e-159">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bb26e-160">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="bb26e-160">Response success and error codes</span></span>

<span data-ttu-id="bb26e-161">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="bb26e-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bb26e-162">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="bb26e-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bb26e-163">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="bb26e-163">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bb26e-164">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="bb26e-164">Response example</span></span>

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=updatedoffice.csv
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Feb 2021 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","ProvisioningId","ProvisioningString","MinLicenses","MaxLicenses","AssetOwnershipLimit","AssetOwnershipLimitType","ProductSkuPreRequisites","ProductSkuConversion","Description","AllowedCountries" 
"Microsoft 365 Business Basic","CFQ7TTC0LH18","0001","Microsoft 365 Business Basic","3b555118-da6a-4418-894f-7df1e2096870","O365_BUSINESS_ESSENTIALS","1","300","2","ConcurrentCount","","CFQ7TTC0LDPB/0001,CFQ7TTC0LF8Q/0001","Best for businesses that need professional...","AD;AE;AF;AG;AI;AL;AM;AO..."
======= Truncated ==============

```
