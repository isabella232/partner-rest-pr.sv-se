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
# <a name="get-foreign-exchange-rates"></a>Hämta växelkurser

Gäller för:

- Partner-API

I det här avsnittet beskrivs hur du hämtar utländska växelkurser för en månad.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner-API-autentisering](api-authentication.md). Det här scenariot har endast stöd för autentisering av program användare. Endast program stöds inte ännu.
- Detta API stöder för närvarande endast användar åtkomst där partners måste vara i någon av följande roller: global admin, administratörs agent eller försäljnings agent.


## <a name="details"></a>Information

- Används för närvarande med [Hämta pris dokument-API](get-a-price-sheet.md) för att beräkna förväntade avgifter för lokala Azure-prenumerationer.
- Utländska växelkurser är sanna för hela månaden som de publiceras.
- Mer information om [priser](pricing.md) för Azure-prenumeration finns i [pris dokumentationen för Azure-prenumerationen](https://docs.microsoft.com/partner-center/azure-plan-price-list).
- Partner priser och API: er för externa växelkurser ingår inte i [partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).
- Den här metoden returnerar resultat som en fil ström. Fil data strömmen är antingen en CSV-fil eller en zip-komprimerad version av. csv. Information om hur du begär komprimerade filer finns nedan.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **TA** | https://api.partner.microsoft.com/v1.0/sales/fxrates(Month={month})/$value                                  |

### <a name="uri-required-parameters"></a>URI-obligatoriska parametrar

Använd följande Sök vägs parametrar för att begära månaden för de valutakurser som du vill använda.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Månad                      | sträng   | Yes       | Måste vara i YYYMM-format. Om den utelämnas som standard till den aktuella månaden.       |

### <a name="request-headers"></a>Begärandehuvuden

- Mer information finns i [partner rest-rubriker](headers.md) .

Förutom ovanstående rubriker kan filer hämtas som komprimerad minskande bandbredd och nedladdnings tider. Som standard komprimeras inte filerna. Om du vill hämta komprimerade versioner av filerna kan du inkludera värdet under rubrik. Tänk på att komprimerade blad endast är tillgängliga från april 2020 och alla begär Anden före den april 2020 är bara tillgängliga som ej komprimerade.

| Huvud                   | Värdetyp     | Värde | Beskrivning                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| sträng   | DEFLATE| Valfritt. Om den utelämnade fil strömmen inte är komprimerad.       |

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='201909')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden utländska växelkurser som en fil ström. Fil data strömmen är antingen en CSV-fil eller en zip-komprimerad version av. csv.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

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
