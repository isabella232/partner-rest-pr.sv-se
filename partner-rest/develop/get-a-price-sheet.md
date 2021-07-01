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
# <a name="get-a-price-sheet"></a>Hämta ett prisdokument

Gäller för:

- Partner-API

Det här avsnittet beskriver hur du hämtar ett prisblad för en viss marknad och vy. Den här metoden stöder filter för att hämta historik per månad.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen [i Partner-API autentisering](api-authentication.md). Det här scenariot stöder endast autentisering av programanvändare. Endast program stöds inte ännu. Partner som får **http-fel:400 bör** läsa dokumentationen [Partner-API om](api-authentication.md) autentisering.
- Detta API stöder för närvarande endast användaråtkomst där partner måste ha någon av följande roller: global administratör, administratörsagent eller försäljningsagent.

## <a name="details"></a>Information

- Aktuella returnerar endast data för förbruknings- och reservationsprodukter för Azure-planer.
- Aktuella [priser](pricing.md) omfattar alla mätare och produkter som är tillgängliga under den aktuella månaden fram till det datum då API:et anropas. Föregående månader innehåller alla mätare och produkter som är tillgängliga för den angivna månaden.
- Förbrukningspriser är bara i USD, partner använder API:et för växelkurser för att beräkna lokala valutakostnader.
- Förbrukningspriser är uppskattade detaljhandelspriser. Partnerrabatter är tillgängliga via [partner-intjänad kredit.](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation)
- Priserna för reservationspriser inkluderar CSP-partnerrabatter. Uppskattade återförsäljarpriser för reservationer finns i de delade reservationstjänster som kan laddas ned på sidan "Priser och erbjudanden" i Partnercenter.
- Mer information om priser för Azure-planer finns i [prisdokumentationen för Azure-plan.](https://docs.microsoft.com/partner-center/azure-plan-price-list)
- API:er för partnerpriser och växelkurser ingår inte i [Partnercenter-SDK](https://docs.microsoft.com/partner-center/develop/get-started).
- Den här metoden returnerar prislistan som en filström. Filströmmen är antingen en .csv eller en komprimerad zip-version av .csv. Information om hur du begär komprimerade filer finns nedan.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Få** | https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market={market}',PricesheetView='{view}')/$value                                     |

### <a name="uri-required-parameters"></a>URI-obligatoriska parametrar

Använd följande sökvägsparametrar för att begära vilken marknad och typ av prislapp du vill ha.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Marknaden                      | sträng   | Ja       | Landskod med två bokstäver för marknaden som begärs       |
|PricesheetView | sträng   | Ja       | Den typ av prisrapport som begärs, kan azure_consumption, azure_reservations eller uppdateraslicensbaserad.  |

> [!Note]
> updatedlicensebased PriceSheetView är för närvarande endast tillgängligt för partner som ingår i den tekniska förhandsversionen av den nya M365/D365-handelsupplevelsen.

### <a name="uri-filter-parameters"></a>URI-filterparametrar

Använd följande filterparametrar.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Tidslinje| sträng   | No| Standardvärdet är current om det inte skickas. Möjliga värden är historik, aktuell och framtida.       |
|Månad| sträng   | No| Krävs endast om historik begärs, måste följa YYYYMM för prisbladet som begärs.       |

### <a name="request-headers"></a>Begärandehuvuden

- Mer information finns i Partner REST-huvuden. [](headers.md)

Förutom ovanstående huvuden kan prisfiler hämtas som komprimerade, vilket minskar bandbredden och nedladdningstiden. Som standard komprimeras inte filerna. Om du vill hämta komprimerade versioner av filerna kan du inkludera rubrikvärdet nedan. Kom ihåg att komprimerade blad endast är tillgängliga från april 2020 och framåt. Alla blad före april 2020 är bara tillgängliga som inte komprimerade.

| Huvud                   | Värdetyp     | Värde | Beskrivning                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| sträng   | Tömma| Valfritt. Om det utelämnas komprimeras inte filströmmen.       |

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```
### <a name="request-example-for-new-commerce"></a>Exempel på begäran för ny handel

> [!Note]
> updatedlicensebased PriceSheetView är för närvarande endast tillgängligt för partner som ingår i den tekniska förhandsversionen av den nya M365/D365-handelsupplevelsen.

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='US',PricesheetView='updatedlicensebased')/$value?timeline=history&month=202101 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden prislistan som en filström. Filströmmen är antingen en .csv eller en komprimerad zip-version av .csv.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

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

### <a name="response-example-for-new-commerce"></a>Svarsexempel för ny handel

> [!Note]
> updatedlicensebased PriceSheetView är för närvarande endast tillgängligt för partner som ingår i den tekniska förhandsversionen av den nya M365/D365-handelsupplevelsen.

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
