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
# <a name="get-a-price-sheet"></a>Hämta ett prisdokument

Gäller för:

- Partner-API

I det här avsnittet beskrivs hur du får ett pris dokument för en specifik marknad och vy. Den här metoden stöder filter för att hämta historik per månad.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner-API-autentisering](api-authentication.md). Det här scenariot har endast stöd för autentisering av program användare. Application-endast stöds inte ännu.
- Detta API stöder för närvarande endast användar åtkomst där partners måste vara i någon av följande roller: global admin, administratörs agent eller försäljnings agent.

## <a name="details"></a>Information

- Current returnerar endast data för produkter i Azure plan-förbrukning och-reservation.
- Aktuell [prissättning](pricing.md) omfattar alla mätare och produkter som är tillgängliga under den aktuella månaden till det datum då API: et anropas. Föregående månader inkluderar alla mätare och produkter som är tillgängliga under den aktuella månaden.
- Priserna för förbruknings mätare är bara i USD, partners använder sig av API: er för utländsk växelkurs för att beräkna lokala valuta kostnader.
- Priserna för förbruknings mätare är uppskattade i detalj handels priser. Partner rabatter är tillgängliga via [partner intjänad kredit](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).
- Avgifter för reservationer omfattar CSP-partner rabatter. De uppskattade detaljhandelspriserna för reservationer finns i reservations delade tjänster som hämtas från Partner Center-sidan för priser och erbjudanden.
- Mer information om priser för Azure-prenumeration finns i [pris dokumentationen för Azure-prenumerationen](https://docs.microsoft.com/partner-center/azure-plan-price-list).
- Partner priser och API: er för externa växelkurser ingår inte i [partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).
- Den här metoden returnerar pris listan som en fil ström. Fil data strömmen är antingen en CSV-fil eller en zip-komprimerad version av. csv. Information om hur du begär komprimerade filer finns nedan.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **TA** | https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market={marknad}, PricesheetView = {View})/$value                                     |

### <a name="uri-required-parameters"></a>URI-obligatoriska parametrar

Använd följande Sök vägs parametrar för att begära vilken marknad och typ av pris dokument som du vill ha.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Telefonförsäljning                      | sträng   | Yes       | Två bokstäver för landets landskod för marknaden som begärs       |
|PricesheetView | sträng   | Yes       | Den typ av pris dokument som begärs kan vara azure_consumption eller azure_reservations       |

### <a name="uri-filter-parameters"></a>Parametrar för URI-filter

Använd följande filter parametrar.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Tidslinje| sträng   | No| Standardvärdet är aktuellt om det inte skickas. Möjliga värden är historik, aktuella och framtida.       |
|Månad| sträng   | No| Krävs endast om historik begärs, måste följa YYYYMM för det pris dokument som begärs.       |

### <a name="request-headers"></a>Begärandehuvuden

- Mer information finns i [partner rest-rubriker](headers.md) .

Förutom ovanstående rubriker kan du hämta prisfiler som komprimerad minskande bandbredd och hämtnings tider. Som standard komprimeras inte filerna. Om du vill hämta komprimerade versioner av filerna kan du inkludera värdet under rubrik. Tänk på att komprimerade blad endast är tillgängliga från april 2020 och att alla blad före april 2020 bara är tillgängliga som ej komprimerade.

| Huvud                   | Värdetyp     | Värde | Beskrivning                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| sträng   | DEFLATE| Valfritt. Om den utelämnade fil strömmen inte är komprimerad.       |

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden pris listan som en fil ström. Fil data strömmen är antingen en CSV-fil eller en zip-komprimerad version av. csv.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

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
