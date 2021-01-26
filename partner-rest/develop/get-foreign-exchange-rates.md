---
title: Hämta växelkurser
description: Hämta valutakurser för den aktuella månaden.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 1e718624db54dcc2ed2b5d2d93dfd1cef0e6f96f
ms.sourcegitcommit: bb3f5f7ee0489bded86fe52e55018c1f4f5032e2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/07/2020
ms.locfileid: "97770628"
---
# <a name="get-foreign-exchange-rates"></a><span data-ttu-id="dd9e2-103">Hämta växelkurser</span><span class="sxs-lookup"><span data-stu-id="dd9e2-103">Get foreign exchange rates</span></span>

<span data-ttu-id="dd9e2-104">Gäller för:</span><span class="sxs-lookup"><span data-stu-id="dd9e2-104">Applies to:</span></span>

- <span data-ttu-id="dd9e2-105">Partner-API</span><span class="sxs-lookup"><span data-stu-id="dd9e2-105">Partner API</span></span>

<span data-ttu-id="dd9e2-106">I det här avsnittet beskrivs hur du hämtar utländska växelkurser för en månad.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-106">This topic explains how to get foreign exchange rates for a given month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd9e2-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="dd9e2-107">Prerequisites</span></span>

- <span data-ttu-id="dd9e2-108">Autentiseringsuppgifter enligt beskrivningen i [partner-API-autentisering](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="dd9e2-108">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="dd9e2-109">Det här scenariot har endast stöd för autentisering av program användare.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-109">This scenario only supports application user authentication.</span></span> <span data-ttu-id="dd9e2-110">Endast program stöds inte ännu.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-110">Application-only is not yet supported.</span></span>
- <span data-ttu-id="dd9e2-111">Detta API stöder för närvarande endast användar åtkomst där partners måste vara i någon av följande roller: global admin, administratörs agent eller försäljnings agent.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-111">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>


## <a name="details"></a><span data-ttu-id="dd9e2-112">Information</span><span class="sxs-lookup"><span data-stu-id="dd9e2-112">Details</span></span>

- <span data-ttu-id="dd9e2-113">Används för närvarande med [Hämta pris dokument-API](get-a-price-sheet.md) för att beräkna förväntade avgifter för lokala Azure-prenumerationer.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-113">Currently used with [get price sheet API](get-a-price-sheet.md) to calculate expected charges for Azure plan CSP local currencies.</span></span>
- <span data-ttu-id="dd9e2-114">Utländska växelkurser är sanna för hela månaden som de publiceras.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-114">Foreign exchange rates hold true for the entire month they are posted.</span></span>
- <span data-ttu-id="dd9e2-115">Mer information om [priser](pricing.md) för Azure-prenumeration finns i [pris dokumentationen för Azure-prenumerationen](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span><span class="sxs-lookup"><span data-stu-id="dd9e2-115">More information about Azure plan [pricing](pricing.md) can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="dd9e2-116">Partner priser och API: er för externa växelkurser ingår inte i [partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span><span class="sxs-lookup"><span data-stu-id="dd9e2-116">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="dd9e2-117">Den här metoden returnerar resultat som en fil ström.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-117">This method returns results as a file stream.</span></span> <span data-ttu-id="dd9e2-118">Fil data strömmen är antingen en CSV-fil eller en zip-komprimerad version av. csv.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-118">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="dd9e2-119">Information om hur du begär komprimerade filer finns nedan.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-119">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="dd9e2-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="dd9e2-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dd9e2-121">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="dd9e2-121">Request syntax</span></span>

| <span data-ttu-id="dd9e2-122">Metod</span><span class="sxs-lookup"><span data-stu-id="dd9e2-122">Method</span></span>   | <span data-ttu-id="dd9e2-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="dd9e2-123">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dd9e2-124">**TA**</span><span class="sxs-lookup"><span data-stu-id="dd9e2-124">**GET**</span></span> | <span data-ttu-id="dd9e2-125"> https://api.partner.microsoft.com/v1.0/sales/fxrates(Month={month})/$value</span><span class="sxs-lookup"><span data-stu-id="dd9e2-125">https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='{month}')/$value</span></span>                                  |

### <a name="uri-required-parameters"></a><span data-ttu-id="dd9e2-126">URI-obligatoriska parametrar</span><span class="sxs-lookup"><span data-stu-id="dd9e2-126">URI required parameters</span></span>

<span data-ttu-id="dd9e2-127">Använd följande Sök vägs parametrar för att begära månaden för de valutakurser som du vill använda.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-127">Use the following path parameters to request the month of foreign exchange rates you want.</span></span>

| <span data-ttu-id="dd9e2-128">Namn</span><span class="sxs-lookup"><span data-stu-id="dd9e2-128">Name</span></span>                   | <span data-ttu-id="dd9e2-129">Typ</span><span class="sxs-lookup"><span data-stu-id="dd9e2-129">Type</span></span>     | <span data-ttu-id="dd9e2-130">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="dd9e2-130">Required</span></span> | <span data-ttu-id="dd9e2-131">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="dd9e2-131">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="dd9e2-132">Månad</span><span class="sxs-lookup"><span data-stu-id="dd9e2-132">Month</span></span>                      | <span data-ttu-id="dd9e2-133">sträng</span><span class="sxs-lookup"><span data-stu-id="dd9e2-133">string</span></span>   | <span data-ttu-id="dd9e2-134">Yes</span><span class="sxs-lookup"><span data-stu-id="dd9e2-134">Yes</span></span>       | <span data-ttu-id="dd9e2-135">Måste vara i YYYMM-format.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-135">Must be in YYYMM format.</span></span> <span data-ttu-id="dd9e2-136">Om den utelämnas som standard till den aktuella månaden.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-136">If omitted defaults to current month.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="dd9e2-137">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="dd9e2-137">Request headers</span></span>

- <span data-ttu-id="dd9e2-138">Mer information finns i [partner rest-rubriker](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="dd9e2-138">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="dd9e2-139">Förutom ovanstående rubriker kan filer hämtas som komprimerad minskande bandbredd och nedladdnings tider.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-139">In addition to the above headers, files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="dd9e2-140">Som standard komprimeras inte filerna.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-140">By default the files are not compressed.</span></span> <span data-ttu-id="dd9e2-141">Om du vill hämta komprimerade versioner av filerna kan du inkludera värdet under rubrik.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-141">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="dd9e2-142">Tänk på att komprimerade blad endast är tillgängliga från april 2020 och alla begär Anden före den april 2020 är bara tillgängliga som ej komprimerade.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-142">Realize that compressed sheets are only available from April 2020 onward, all requests prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="dd9e2-143">Huvud</span><span class="sxs-lookup"><span data-stu-id="dd9e2-143">Header</span></span>                   | <span data-ttu-id="dd9e2-144">Värdetyp</span><span class="sxs-lookup"><span data-stu-id="dd9e2-144">Value Type</span></span>     | <span data-ttu-id="dd9e2-145">Värde</span><span class="sxs-lookup"><span data-stu-id="dd9e2-145">Value</span></span> | <span data-ttu-id="dd9e2-146">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="dd9e2-146">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="dd9e2-147">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="dd9e2-147">Accept-Encoding</span></span>| <span data-ttu-id="dd9e2-148">sträng</span><span class="sxs-lookup"><span data-stu-id="dd9e2-148">string</span></span>   | <span data-ttu-id="dd9e2-149">DEFLATE</span><span class="sxs-lookup"><span data-stu-id="dd9e2-149">deflate</span></span>| <span data-ttu-id="dd9e2-150">Valfritt.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-150">Optional.</span></span> <span data-ttu-id="dd9e2-151">Om den utelämnade fil strömmen inte är komprimerad.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-151">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="dd9e2-152">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="dd9e2-152">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='201909')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="dd9e2-153">REST-svar</span><span class="sxs-lookup"><span data-stu-id="dd9e2-153">REST response</span></span>

<span data-ttu-id="dd9e2-154">Om det lyckas returnerar den här metoden utländska växelkurser som en fil ström.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-154">If successful, this method returns foreign exchange rates as a file stream.</span></span> <span data-ttu-id="dd9e2-155">Fil data strömmen är antingen en CSV-fil eller en zip-komprimerad version av. csv.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-155">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dd9e2-156">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="dd9e2-156">Response success and error codes</span></span>

<span data-ttu-id="dd9e2-157">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dd9e2-158">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="dd9e2-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dd9e2-159">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="dd9e2-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="dd9e2-160">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="dd9e2-160">Response example</span></span>

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 18548
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=fxrates
Request-ID: 65fb6e59-051b-42f7-8771-c8c139b3c901
Date: Wed, 02 Oct 2019 03:42:54 GMT

"CurrencyCode","USDPerUnit","Month"
"AED","0.27224589249009701","2019”
======= Truncated ==============

```
