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
# <a name="get-an-offer-matrix"></a>Hämta en erbjudandematris

Gäller för:

- Partner-API
- Den tekniska förhandsversionen av den nya handelsupplevelsen M365/D365. Nedanstående nya handelsändringar är för närvarande endast tillgängliga för partner som ingår i den tekniska förhandsversionen av den nya M365/D365-handelsupplevelsen.

Det här avsnittet beskriver hur du hämtar en erbjudandematris för en viss månad. Erbjudandematrisen innehåller egenskaper och inköpsregler för produkterna och SKU:erna. Den här metoden stöder filter för att hämta historik per månad.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen [i Partner-API autentisering](api-authentication.md). Det här scenariot stöder endast användarautentisering för program. Endast program stöds inte ännu. Partner som får **http-fel:400 bör** läsa dokumentationen [Partner-API autentisering.](api-authentication.md)
- Det här API:et stöder för närvarande endast användaråtkomst där partner måste ha någon av följande roller: global administratör, administratörsagent eller försäljningsagent.

## <a name="details"></a>Information

- Aktuella returnerar endast data för uppdaterade nya handelslicensbaserade produkter.
- Aktuella priser omfattar produkter som är tillgängliga under den aktuella månaden fram till det datum då API:et anropas. Föregående månader inkluderar datum från och med den sista dagen i den valda månaden.
- Den här metoden returnerar data som en filström. Filströmmen är antingen en .csv eller en komprimerad zip-version av .csv. Information om hur du begär komprimerade filer finns nedan.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Få** | https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month={date})/$value |

### <a name="uri-filter-parameters"></a>URI-filterparametrar

Använd följande filterparametrar.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Månad| sträng   | No | Måste följa YYYYMM för det prisark som begärs. |

### <a name="request-headers"></a>Begärandehuvuden

- Mer information finns i Partner REST-huvuden. [](headers.md)

Förutom ovanstående huvuden kan prisfiler hämtas som komprimerade, vilket minskar bandbredden och nedladdningstiderna. Som standard komprimeras inte filerna. Om du vill hämta komprimerade versioner av filerna kan du inkludera rubrikvärdet nedan. Kom ihåg att komprimerade blad endast är tillgängliga från april 2020 och framåt. Alla blad före april 2020 är bara tillgängliga som inte komprimerade.

| Huvud                   | Värdetyp     | Värde | Beskrivning                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| sträng   | Tömma| Valfritt. Om den utelämnas komprimeras inte filströmmen.       |

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='202101')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en erbjudandematris som en filström. Filströmmen är antingen en .csv eller en komprimerad zip-version av .csv.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

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
