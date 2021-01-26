---
title: Hämta ett prisdokument
description: Få ett pris dokument för en specifik marknad och vy. Stöder filter för att hämta historik per månad.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 5195ebed6559bd71a7832a667e63ee801be1c82f
ms.sourcegitcommit: bb3f5f7ee0489bded86fe52e55018c1f4f5032e2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/07/2020
ms.locfileid: "97770627"
---
# <a name="get-a-price-sheet"></a><span data-ttu-id="52780-104">Hämta ett prisdokument</span><span class="sxs-lookup"><span data-stu-id="52780-104">Get a price sheet</span></span>

<span data-ttu-id="52780-105">Gäller för:</span><span class="sxs-lookup"><span data-stu-id="52780-105">Applies to:</span></span>

- <span data-ttu-id="52780-106">Partner-API</span><span class="sxs-lookup"><span data-stu-id="52780-106">Partner API</span></span>

<span data-ttu-id="52780-107">I det här avsnittet beskrivs hur du får ett pris dokument för en specifik marknad och vy.</span><span class="sxs-lookup"><span data-stu-id="52780-107">This topic explains how to get a price sheet for a given market and view.</span></span> <span data-ttu-id="52780-108">Den här metoden stöder filter för att hämta historik per månad.</span><span class="sxs-lookup"><span data-stu-id="52780-108">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52780-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="52780-109">Prerequisites</span></span>

- <span data-ttu-id="52780-110">Autentiseringsuppgifter enligt beskrivningen i [partner-API-autentisering](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="52780-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="52780-111">Det här scenariot har endast stöd för autentisering av program användare.</span><span class="sxs-lookup"><span data-stu-id="52780-111">This scenario only supports application user authentication.</span></span> <span data-ttu-id="52780-112">Application-endast stöds inte ännu.</span><span class="sxs-lookup"><span data-stu-id="52780-112">Application-ony is not yet supported.</span></span>
- <span data-ttu-id="52780-113">Detta API stöder för närvarande endast användar åtkomst där partners måste vara i någon av följande roller: global admin, administratörs agent eller försäljnings agent.</span><span class="sxs-lookup"><span data-stu-id="52780-113">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="52780-114">Information</span><span class="sxs-lookup"><span data-stu-id="52780-114">Details</span></span>

- <span data-ttu-id="52780-115">Current returnerar endast data för produkter i Azure plan-förbrukning och-reservation.</span><span class="sxs-lookup"><span data-stu-id="52780-115">Current returns data only for Azure plan consumption and reservation products.</span></span>
- <span data-ttu-id="52780-116">Aktuell [prissättning](pricing.md) omfattar alla mätare och produkter som är tillgängliga under den aktuella månaden till det datum då API: et anropas.</span><span class="sxs-lookup"><span data-stu-id="52780-116">Current [pricing](pricing.md) includes all meters and products available during the current month to the date the API is called.</span></span> <span data-ttu-id="52780-117">Föregående månader inkluderar alla mätare och produkter som är tillgängliga under den aktuella månaden.</span><span class="sxs-lookup"><span data-stu-id="52780-117">Previous months include all meters and products available for the given month.</span></span>
- <span data-ttu-id="52780-118">Priserna för förbruknings mätare är bara i USD, partners använder sig av API: er för utländsk växelkurs för att beräkna lokala valuta kostnader.</span><span class="sxs-lookup"><span data-stu-id="52780-118">Consumption meter prices are only in USD, partners are to use the foreign exchange rates API to calculate local currency costs.</span></span>
- <span data-ttu-id="52780-119">Priserna för förbruknings mätare är uppskattade i detalj handels priser.</span><span class="sxs-lookup"><span data-stu-id="52780-119">Consumption meter prices are estimated retail prices.</span></span> <span data-ttu-id="52780-120">Partner rabatter är tillgängliga via [partner intjänad kredit](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span><span class="sxs-lookup"><span data-stu-id="52780-120">Partner discounts are available via [partner earned credit](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span></span>
- <span data-ttu-id="52780-121">Avgifter för reservationer omfattar CSP-partner rabatter.</span><span class="sxs-lookup"><span data-stu-id="52780-121">Reservations meter prices include the CSP partner discounts.</span></span> <span data-ttu-id="52780-122">De uppskattade detaljhandelspriserna för reservationer finns i reservations delade tjänster som hämtas från Partner Center-sidan för priser och erbjudanden.</span><span class="sxs-lookup"><span data-stu-id="52780-122">Estimated retail prices for reservations can be found in the reservations shared services downloadable from the Partner Center "Pricing and offers" page.</span></span>
- <span data-ttu-id="52780-123">Mer information om priser för Azure-prenumeration finns i [pris dokumentationen för Azure-prenumerationen](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span><span class="sxs-lookup"><span data-stu-id="52780-123">More information about Azure plan pricing can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="52780-124">Partner priser och API: er för externa växelkurser ingår inte i [partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span><span class="sxs-lookup"><span data-stu-id="52780-124">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="52780-125">Den här metoden returnerar pris listan som en fil ström.</span><span class="sxs-lookup"><span data-stu-id="52780-125">This method returns the price list as a file stream.</span></span> <span data-ttu-id="52780-126">Fil data strömmen är antingen en CSV-fil eller en zip-komprimerad version av. csv.</span><span class="sxs-lookup"><span data-stu-id="52780-126">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="52780-127">Information om hur du begär komprimerade filer finns nedan.</span><span class="sxs-lookup"><span data-stu-id="52780-127">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="52780-128">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="52780-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="52780-129">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="52780-129">Request syntax</span></span>

| <span data-ttu-id="52780-130">Metod</span><span class="sxs-lookup"><span data-stu-id="52780-130">Method</span></span>   | <span data-ttu-id="52780-131">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="52780-131">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="52780-132">**TA**</span><span class="sxs-lookup"><span data-stu-id="52780-132">**GET**</span></span> | <span data-ttu-id="52780-133"> https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market={marknad}, PricesheetView = {View})/$value</span><span class="sxs-lookup"><span data-stu-id="52780-133">https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value</span></span>                                     |

### <a name="uri-required-parameters"></a><span data-ttu-id="52780-134">URI-obligatoriska parametrar</span><span class="sxs-lookup"><span data-stu-id="52780-134">URI required parameters</span></span>

<span data-ttu-id="52780-135">Använd följande Sök vägs parametrar för att begära vilken marknad och typ av pris dokument som du vill ha.</span><span class="sxs-lookup"><span data-stu-id="52780-135">Use the following path parameters to request which market and type of price sheet you want.</span></span>

| <span data-ttu-id="52780-136">Namn</span><span class="sxs-lookup"><span data-stu-id="52780-136">Name</span></span>                   | <span data-ttu-id="52780-137">Typ</span><span class="sxs-lookup"><span data-stu-id="52780-137">Type</span></span>     | <span data-ttu-id="52780-138">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="52780-138">Required</span></span> | <span data-ttu-id="52780-139">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="52780-139">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="52780-140">Telefonförsäljning</span><span class="sxs-lookup"><span data-stu-id="52780-140">Market</span></span>                      | <span data-ttu-id="52780-141">sträng</span><span class="sxs-lookup"><span data-stu-id="52780-141">string</span></span>   | <span data-ttu-id="52780-142">Yes</span><span class="sxs-lookup"><span data-stu-id="52780-142">Yes</span></span>       | <span data-ttu-id="52780-143">Två bokstäver för landets landskod för marknaden som begärs</span><span class="sxs-lookup"><span data-stu-id="52780-143">Two letter country code for the market being requested</span></span>       |
|<span data-ttu-id="52780-144">PricesheetView</span><span class="sxs-lookup"><span data-stu-id="52780-144">PricesheetView</span></span> | <span data-ttu-id="52780-145">sträng</span><span class="sxs-lookup"><span data-stu-id="52780-145">string</span></span>   | <span data-ttu-id="52780-146">Yes</span><span class="sxs-lookup"><span data-stu-id="52780-146">Yes</span></span>       | <span data-ttu-id="52780-147">Den typ av pris dokument som begärs kan vara azure_consumption eller azure_reservations</span><span class="sxs-lookup"><span data-stu-id="52780-147">The type of price sheet being requested, this can be azure_consumption or azure_reservations</span></span>       |

### <a name="uri-filter-parameters"></a><span data-ttu-id="52780-148">Parametrar för URI-filter</span><span class="sxs-lookup"><span data-stu-id="52780-148">URI filter parameters</span></span>

<span data-ttu-id="52780-149">Använd följande filter parametrar.</span><span class="sxs-lookup"><span data-stu-id="52780-149">Use the following filter parameters.</span></span>

| <span data-ttu-id="52780-150">Namn</span><span class="sxs-lookup"><span data-stu-id="52780-150">Name</span></span>                   | <span data-ttu-id="52780-151">Typ</span><span class="sxs-lookup"><span data-stu-id="52780-151">Type</span></span>     | <span data-ttu-id="52780-152">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="52780-152">Required</span></span> | <span data-ttu-id="52780-153">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="52780-153">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="52780-154">Tidslinje</span><span class="sxs-lookup"><span data-stu-id="52780-154">Timeline</span></span>| <span data-ttu-id="52780-155">sträng</span><span class="sxs-lookup"><span data-stu-id="52780-155">string</span></span>   | <span data-ttu-id="52780-156">No</span><span class="sxs-lookup"><span data-stu-id="52780-156">No</span></span>| <span data-ttu-id="52780-157">Standardvärdet är aktuellt om det inte skickas.</span><span class="sxs-lookup"><span data-stu-id="52780-157">Defaults to current if not passed.</span></span> <span data-ttu-id="52780-158">Möjliga värden är historik, aktuella och framtida.</span><span class="sxs-lookup"><span data-stu-id="52780-158">Possible values are history, current and future.</span></span>       |
|<span data-ttu-id="52780-159">Månad</span><span class="sxs-lookup"><span data-stu-id="52780-159">Month</span></span>| <span data-ttu-id="52780-160">sträng</span><span class="sxs-lookup"><span data-stu-id="52780-160">string</span></span>   | <span data-ttu-id="52780-161">No</span><span class="sxs-lookup"><span data-stu-id="52780-161">No</span></span>| <span data-ttu-id="52780-162">Krävs endast om historik begärs, måste följa YYYYMM för det pris dokument som begärs.</span><span class="sxs-lookup"><span data-stu-id="52780-162">Only required if history is requested, must adhere to YYYYMM for the price sheet being requested.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="52780-163">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="52780-163">Request headers</span></span>

- <span data-ttu-id="52780-164">Mer information finns i [partner rest-rubriker](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="52780-164">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="52780-165">Förutom ovanstående rubriker kan du hämta prisfiler som komprimerad minskande bandbredd och hämtnings tider.</span><span class="sxs-lookup"><span data-stu-id="52780-165">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="52780-166">Som standard komprimeras inte filerna.</span><span class="sxs-lookup"><span data-stu-id="52780-166">By default the files are not compressed.</span></span> <span data-ttu-id="52780-167">Om du vill hämta komprimerade versioner av filerna kan du inkludera värdet under rubrik.</span><span class="sxs-lookup"><span data-stu-id="52780-167">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="52780-168">Tänk på att komprimerade blad endast är tillgängliga från april 2020 och att alla blad före april 2020 bara är tillgängliga som ej komprimerade.</span><span class="sxs-lookup"><span data-stu-id="52780-168">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="52780-169">Huvud</span><span class="sxs-lookup"><span data-stu-id="52780-169">Header</span></span>                   | <span data-ttu-id="52780-170">Värdetyp</span><span class="sxs-lookup"><span data-stu-id="52780-170">Value Type</span></span>     | <span data-ttu-id="52780-171">Värde</span><span class="sxs-lookup"><span data-stu-id="52780-171">Value</span></span> | <span data-ttu-id="52780-172">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="52780-172">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="52780-173">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="52780-173">Accept-Encoding</span></span>| <span data-ttu-id="52780-174">sträng</span><span class="sxs-lookup"><span data-stu-id="52780-174">string</span></span>   | <span data-ttu-id="52780-175">DEFLATE</span><span class="sxs-lookup"><span data-stu-id="52780-175">deflate</span></span>| <span data-ttu-id="52780-176">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="52780-176">Optional.</span></span> <span data-ttu-id="52780-177">Om den utelämnade fil strömmen inte är komprimerad.</span><span class="sxs-lookup"><span data-stu-id="52780-177">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="52780-178">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="52780-178">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="52780-179">REST-svar</span><span class="sxs-lookup"><span data-stu-id="52780-179">REST response</span></span>

<span data-ttu-id="52780-180">Om det lyckas returnerar den här metoden pris listan som en fil ström.</span><span class="sxs-lookup"><span data-stu-id="52780-180">If successful, this method returns the price list as a file stream.</span></span> <span data-ttu-id="52780-181">Fil data strömmen är antingen en CSV-fil eller en zip-komprimerad version av. csv.</span><span class="sxs-lookup"><span data-stu-id="52780-181">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="52780-182">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="52780-182">Response success and error codes</span></span>

<span data-ttu-id="52780-183">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="52780-183">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="52780-184">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="52780-184">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="52780-185">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="52780-185">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="52780-186">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="52780-186">Response example</span></span>

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
