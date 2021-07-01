---
title: Hämta ett prisdokument
description: Hämta ett prisblad för en viss marknad och vy. Stöder filter för att hämta historik per månad.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 7571e8fce861dbfe463000a1ac4094115af08ffa
ms.sourcegitcommit: 9e64d6358ef4e1ac2d3e0d36cd63490a5f760b38
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/01/2021
ms.locfileid: "113125524"
---
# <a name="get-a-price-sheet"></a><span data-ttu-id="c82fe-104">Hämta ett prisdokument</span><span class="sxs-lookup"><span data-stu-id="c82fe-104">Get a price sheet</span></span>

<span data-ttu-id="c82fe-105">Gäller för:</span><span class="sxs-lookup"><span data-stu-id="c82fe-105">Applies to:</span></span>

- <span data-ttu-id="c82fe-106">Partner-API</span><span class="sxs-lookup"><span data-stu-id="c82fe-106">Partner API</span></span>

<span data-ttu-id="c82fe-107">Det här avsnittet beskriver hur du hämtar ett prisblad för en viss marknad och vy.</span><span class="sxs-lookup"><span data-stu-id="c82fe-107">This topic explains how to get a price sheet for a given market and view.</span></span> <span data-ttu-id="c82fe-108">Den här metoden stöder filter för att hämta historik per månad.</span><span class="sxs-lookup"><span data-stu-id="c82fe-108">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c82fe-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="c82fe-109">Prerequisites</span></span>

- <span data-ttu-id="c82fe-110">Autentiseringsuppgifter enligt beskrivningen [i Partner-API autentisering](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c82fe-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="c82fe-111">Det här scenariot stöder endast autentisering av programanvändare.</span><span class="sxs-lookup"><span data-stu-id="c82fe-111">This scenario only supports application user authentication.</span></span> <span data-ttu-id="c82fe-112">Endast program stöds inte ännu.</span><span class="sxs-lookup"><span data-stu-id="c82fe-112">Application-only is not yet supported.</span></span> <span data-ttu-id="c82fe-113">Partner som får **http-fel:400 bör** läsa dokumentationen [Partner-API om](api-authentication.md) autentisering.</span><span class="sxs-lookup"><span data-stu-id="c82fe-113">Partners that experience **http error:400** should consult the [Partner API authentication](api-authentication.md) documentation.</span></span>
- <span data-ttu-id="c82fe-114">Detta API stöder för närvarande endast användaråtkomst där partner måste ha någon av följande roller: global administratör, administratörsagent eller försäljningsagent.</span><span class="sxs-lookup"><span data-stu-id="c82fe-114">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="c82fe-115">Information</span><span class="sxs-lookup"><span data-stu-id="c82fe-115">Details</span></span>

- <span data-ttu-id="c82fe-116">Aktuella returnerar endast data för förbruknings- och reservationsprodukter för Azure-planer.</span><span class="sxs-lookup"><span data-stu-id="c82fe-116">Current returns data only for Azure plan consumption and reservation products.</span></span>
- <span data-ttu-id="c82fe-117">Aktuella [priser](pricing.md) omfattar alla mätare och produkter som är tillgängliga under den aktuella månaden fram till det datum då API:et anropas.</span><span class="sxs-lookup"><span data-stu-id="c82fe-117">Current [pricing](pricing.md) includes all meters and products available during the current month to the date the API is called.</span></span> <span data-ttu-id="c82fe-118">Föregående månader innehåller alla mätare och produkter som är tillgängliga för den angivna månaden.</span><span class="sxs-lookup"><span data-stu-id="c82fe-118">Previous months include all meters and products available for the given month.</span></span>
- <span data-ttu-id="c82fe-119">Förbrukningspriser är bara i USD, partner använder API:et för växelkurser för att beräkna lokala valutakostnader.</span><span class="sxs-lookup"><span data-stu-id="c82fe-119">Consumption meter prices are only in USD, partners are to use the foreign exchange rates API to calculate local currency costs.</span></span>
- <span data-ttu-id="c82fe-120">Förbrukningspriser är uppskattade detaljhandelspriser.</span><span class="sxs-lookup"><span data-stu-id="c82fe-120">Consumption meter prices are estimated retail prices.</span></span> <span data-ttu-id="c82fe-121">Partnerrabatter är tillgängliga via [partner-intjänad kredit.](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation)</span><span class="sxs-lookup"><span data-stu-id="c82fe-121">Partner discounts are available via [partner earned credit](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span></span>
- <span data-ttu-id="c82fe-122">Priserna för reservationspriser inkluderar CSP-partnerrabatter.</span><span class="sxs-lookup"><span data-stu-id="c82fe-122">Reservations meter prices include the CSP partner discounts.</span></span> <span data-ttu-id="c82fe-123">Uppskattade återförsäljarpriser för reservationer finns i de delade reservationstjänster som kan laddas ned på sidan "Priser och erbjudanden" i Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="c82fe-123">Estimated retail prices for reservations can be found in the reservations shared services downloadable from the Partner Center "Pricing and offers" page.</span></span>
- <span data-ttu-id="c82fe-124">Mer information om priser för Azure-planer finns i [prisdokumentationen för Azure-plan.](https://docs.microsoft.com/partner-center/azure-plan-price-list)</span><span class="sxs-lookup"><span data-stu-id="c82fe-124">More information about Azure plan pricing can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="c82fe-125">API:er för partnerpriser och växelkurser ingår inte i [Partnercenter-SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span><span class="sxs-lookup"><span data-stu-id="c82fe-125">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="c82fe-126">Den här metoden returnerar prislistan som en filström.</span><span class="sxs-lookup"><span data-stu-id="c82fe-126">This method returns the price list as a file stream.</span></span> <span data-ttu-id="c82fe-127">Filströmmen är antingen en .csv eller en komprimerad zip-version av .csv.</span><span class="sxs-lookup"><span data-stu-id="c82fe-127">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="c82fe-128">Information om hur du begär komprimerade filer finns nedan.</span><span class="sxs-lookup"><span data-stu-id="c82fe-128">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="c82fe-129">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="c82fe-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c82fe-130">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="c82fe-130">Request syntax</span></span>

| <span data-ttu-id="c82fe-131">Metod</span><span class="sxs-lookup"><span data-stu-id="c82fe-131">Method</span></span>   | <span data-ttu-id="c82fe-132">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="c82fe-132">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c82fe-133">**Få**</span><span class="sxs-lookup"><span data-stu-id="c82fe-133">**GET**</span></span> | <span data-ttu-id="c82fe-134"> https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market={market}',PricesheetView='{view}')/$value</span><span class="sxs-lookup"><span data-stu-id="c82fe-134">https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value</span></span>                                     |

### <a name="uri-required-parameters"></a><span data-ttu-id="c82fe-135">URI-obligatoriska parametrar</span><span class="sxs-lookup"><span data-stu-id="c82fe-135">URI required parameters</span></span>

<span data-ttu-id="c82fe-136">Använd följande sökvägsparametrar för att begära vilken marknad och typ av prislapp du vill ha.</span><span class="sxs-lookup"><span data-stu-id="c82fe-136">Use the following path parameters to request which market and type of price sheet you want.</span></span>

| <span data-ttu-id="c82fe-137">Namn</span><span class="sxs-lookup"><span data-stu-id="c82fe-137">Name</span></span>                   | <span data-ttu-id="c82fe-138">Typ</span><span class="sxs-lookup"><span data-stu-id="c82fe-138">Type</span></span>     | <span data-ttu-id="c82fe-139">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="c82fe-139">Required</span></span> | <span data-ttu-id="c82fe-140">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="c82fe-140">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="c82fe-141">Marknaden</span><span class="sxs-lookup"><span data-stu-id="c82fe-141">Market</span></span>                      | <span data-ttu-id="c82fe-142">sträng</span><span class="sxs-lookup"><span data-stu-id="c82fe-142">string</span></span>   | <span data-ttu-id="c82fe-143">Ja</span><span class="sxs-lookup"><span data-stu-id="c82fe-143">Yes</span></span>       | <span data-ttu-id="c82fe-144">Landskod med två bokstäver för marknaden som begärs</span><span class="sxs-lookup"><span data-stu-id="c82fe-144">Two letter country code for the market being requested</span></span>       |
|<span data-ttu-id="c82fe-145">PricesheetView</span><span class="sxs-lookup"><span data-stu-id="c82fe-145">PricesheetView</span></span> | <span data-ttu-id="c82fe-146">sträng</span><span class="sxs-lookup"><span data-stu-id="c82fe-146">string</span></span>   | <span data-ttu-id="c82fe-147">Ja</span><span class="sxs-lookup"><span data-stu-id="c82fe-147">Yes</span></span>       | <span data-ttu-id="c82fe-148">Den typ av prisrapport som begärs, kan azure_consumption, azure_reservations eller uppdateraslicensbaserad.</span><span class="sxs-lookup"><span data-stu-id="c82fe-148">The type of price sheet being requested, this can be azure_consumption, azure_reservations or updatedlicensebased.</span></span>  |

> [!Note]
> <span data-ttu-id="c82fe-149">updatedlicensebased PriceSheetView är för närvarande endast tillgängligt för partner som ingår i den tekniska förhandsversionen av den nya M365/D365-handelsupplevelsen.</span><span class="sxs-lookup"><span data-stu-id="c82fe-149">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

### <a name="uri-filter-parameters"></a><span data-ttu-id="c82fe-150">URI-filterparametrar</span><span class="sxs-lookup"><span data-stu-id="c82fe-150">URI filter parameters</span></span>

<span data-ttu-id="c82fe-151">Använd följande filterparametrar.</span><span class="sxs-lookup"><span data-stu-id="c82fe-151">Use the following filter parameters.</span></span>

| <span data-ttu-id="c82fe-152">Namn</span><span class="sxs-lookup"><span data-stu-id="c82fe-152">Name</span></span>                   | <span data-ttu-id="c82fe-153">Typ</span><span class="sxs-lookup"><span data-stu-id="c82fe-153">Type</span></span>     | <span data-ttu-id="c82fe-154">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="c82fe-154">Required</span></span> | <span data-ttu-id="c82fe-155">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="c82fe-155">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="c82fe-156">Tidslinje</span><span class="sxs-lookup"><span data-stu-id="c82fe-156">Timeline</span></span>| <span data-ttu-id="c82fe-157">sträng</span><span class="sxs-lookup"><span data-stu-id="c82fe-157">string</span></span>   | <span data-ttu-id="c82fe-158">No</span><span class="sxs-lookup"><span data-stu-id="c82fe-158">No</span></span>| <span data-ttu-id="c82fe-159">Standardvärdet är current om det inte skickas.</span><span class="sxs-lookup"><span data-stu-id="c82fe-159">Defaults to current if not passed.</span></span> <span data-ttu-id="c82fe-160">Möjliga värden är historik, aktuell och framtida.</span><span class="sxs-lookup"><span data-stu-id="c82fe-160">Possible values are history, current and future.</span></span>       |
|<span data-ttu-id="c82fe-161">Månad</span><span class="sxs-lookup"><span data-stu-id="c82fe-161">Month</span></span>| <span data-ttu-id="c82fe-162">sträng</span><span class="sxs-lookup"><span data-stu-id="c82fe-162">string</span></span>   | <span data-ttu-id="c82fe-163">No</span><span class="sxs-lookup"><span data-stu-id="c82fe-163">No</span></span>| <span data-ttu-id="c82fe-164">Krävs endast om historik begärs, måste följa YYYYMM för prisbladet som begärs.</span><span class="sxs-lookup"><span data-stu-id="c82fe-164">Only required if history is requested, must adhere to YYYYMM for the price sheet being requested.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="c82fe-165">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="c82fe-165">Request headers</span></span>

- <span data-ttu-id="c82fe-166">Mer information finns i Partner REST-huvuden. [](headers.md)</span><span class="sxs-lookup"><span data-stu-id="c82fe-166">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="c82fe-167">Förutom ovanstående huvuden kan prisfiler hämtas som komprimerade, vilket minskar bandbredden och nedladdningstiden.</span><span class="sxs-lookup"><span data-stu-id="c82fe-167">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="c82fe-168">Som standard komprimeras inte filerna.</span><span class="sxs-lookup"><span data-stu-id="c82fe-168">By default the files are not compressed.</span></span> <span data-ttu-id="c82fe-169">Om du vill hämta komprimerade versioner av filerna kan du inkludera rubrikvärdet nedan.</span><span class="sxs-lookup"><span data-stu-id="c82fe-169">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="c82fe-170">Kom ihåg att komprimerade blad endast är tillgängliga från april 2020 och framåt. Alla blad före april 2020 är bara tillgängliga som inte komprimerade.</span><span class="sxs-lookup"><span data-stu-id="c82fe-170">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="c82fe-171">Huvud</span><span class="sxs-lookup"><span data-stu-id="c82fe-171">Header</span></span>                   | <span data-ttu-id="c82fe-172">Värdetyp</span><span class="sxs-lookup"><span data-stu-id="c82fe-172">Value Type</span></span>     | <span data-ttu-id="c82fe-173">Värde</span><span class="sxs-lookup"><span data-stu-id="c82fe-173">Value</span></span> | <span data-ttu-id="c82fe-174">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="c82fe-174">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="c82fe-175">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="c82fe-175">Accept-Encoding</span></span>| <span data-ttu-id="c82fe-176">sträng</span><span class="sxs-lookup"><span data-stu-id="c82fe-176">string</span></span>   | <span data-ttu-id="c82fe-177">Tömma</span><span class="sxs-lookup"><span data-stu-id="c82fe-177">deflate</span></span>| <span data-ttu-id="c82fe-178">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="c82fe-178">Optional.</span></span> <span data-ttu-id="c82fe-179">Om det utelämnas komprimeras inte filströmmen.</span><span class="sxs-lookup"><span data-stu-id="c82fe-179">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="c82fe-180">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="c82fe-180">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```
### <a name="request-example-for-new-commerce"></a><span data-ttu-id="c82fe-181">Exempel på begäran för ny handel</span><span class="sxs-lookup"><span data-stu-id="c82fe-181">Request example for new commerce</span></span>

> [!Note]
> <span data-ttu-id="c82fe-182">updatedlicensebased PriceSheetView är för närvarande endast tillgängligt för partner som ingår i den tekniska förhandsversionen av den nya M365/D365-handelsupplevelsen.</span><span class="sxs-lookup"><span data-stu-id="c82fe-182">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='US',PricesheetView='updatedlicensebased')/$value?timeline=history&month=202101 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="c82fe-183">REST-svar</span><span class="sxs-lookup"><span data-stu-id="c82fe-183">REST response</span></span>

<span data-ttu-id="c82fe-184">Om det lyckas returnerar den här metoden prislistan som en filström.</span><span class="sxs-lookup"><span data-stu-id="c82fe-184">If successful, this method returns the price list as a file stream.</span></span> <span data-ttu-id="c82fe-185">Filströmmen är antingen en .csv eller en komprimerad zip-version av .csv.</span><span class="sxs-lookup"><span data-stu-id="c82fe-185">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c82fe-186">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="c82fe-186">Response success and error codes</span></span>

<span data-ttu-id="c82fe-187">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="c82fe-187">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c82fe-188">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="c82fe-188">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c82fe-189">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="c82fe-189">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c82fe-190">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="c82fe-190">Response example</span></span>

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=pricesheet
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Oct 2019 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","Publisher","SkuDescription","UnitOfMeasure","TermDuration","Market","Currency","UnitPrice","PricingTierRangeMin","PricingTierRangeMax","EffectiveStartDate","EffectiveEndDate","MeterIds","MeterType","Tags“
"Advanced Data Security - SQL Database","DZH318Z0C16V","001J","Advanced Data Security - SQL Database - Standard - US East 2","Microsoft","Advanced Data Security - SQL Database - Standard - US East 2","1 Node/Month","payG-1","US","USD","15","","","3/1/2018 12:00:00 AM","11/30/9999 11:59:59 PM","cb0969aa-aaaa-4d6c-ab4b-7e182fa06aff","1 Node/Month","Azure“
======= Truncated ==============

```

### <a name="response-example-for-new-commerce"></a><span data-ttu-id="c82fe-191">Svarsexempel för ny handel</span><span class="sxs-lookup"><span data-stu-id="c82fe-191">Response example for new commerce</span></span>

> [!Note]
> <span data-ttu-id="c82fe-192">updatedlicensebased PriceSheetView är för närvarande endast tillgängligt för partner som ingår i den tekniska förhandsversionen av den nya M365/D365-handelsupplevelsen.</span><span class="sxs-lookup"><span data-stu-id="c82fe-192">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=sheets.csv
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Feb 2021 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","Publisher","SkuDescription","UnitOfMeasure","TermDuration","BillingPlan","Market","Currency","UnitPrice","PricingTierRangeMin","PricingTierRangeMax","EffectiveStartDate","EffectiveEndDate","Tags","ERP Price“
"Advanced Communications","CFQ7TTC0HDK0","0001","Advanced Communications","Microsoft Corporation","Advanced meetings, calling, workflow integration, and management tools for IT.","","P1Y","Annual","US","USD","115.2","","","2/1/2019 12:00:00 AM","2/4/2021 8:35:31 PM","License","144"
======= Truncated ==============

```
