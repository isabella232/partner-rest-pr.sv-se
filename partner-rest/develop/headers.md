---
title: Partners-API REST-rubriker
description: Följande HTTP-begäran och svarshuvuden stöds av partner REST API.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 955cab07da7f3a386690e18042165015906d864a
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770600"
---
# <a name="partner-rest-api-headers"></a>Partner REST API-rubriker

Partner REST API stöder följande HTTP-begäran och svarshuvuden.

> [!NOTE]
> Alla API-anrop accepterar inte alla huvuden.

## <a name="request-headers"></a>Begärandehuvuden

Följande HTTP-begärandehuvuden stöds av partner REST API.

| Huvud                       | Värdetyp | Description                                                                            |
|------------------------------|------------|----------------------------------------------------------------------------------------|
| Auktorisering           | sträng     | Krävs. Autentiseringstoken i form Bearer- &lt; token &gt; .                    |
| Acceptera                  | sträng     | Anger begäran och svars typ, "Application/JSON".                           |
| klient-begärande-ID         | GUID       | Krävs. En unik identifierare för anropet, användbart i loggar och nätverks spår för fel söknings fel. Värdet måste återställas för varje anrop. Alla åtgärder ska innehålla denna rubrik. |
| If-Match:                    | sträng     | Används för concurrency-kontroll. Vissa API-anrop kräver att ETag skickas via If-Matchs huvudet. ETag är vanligt vis på resursen och kräver därför att du får den senaste versionen. |

## <a name="response-headers"></a>Svarshuvuden

Följande HTTP-svarshuvuden kan returneras av partner REST API.

| Huvud                    | Värdetyp | Description                                                                                                               |
|-------------------|------------|--------------------------------------------------------------------------------------------------|
| Acceptera                | sträng     | Anger begäran och svars typ, "Application/JSON".                                     |
| begärande-ID        | GUID       | En unik identifierare för anropet som används för att säkerställa ID-potens. Om det är en tids gräns ska anropet för återförsök innehålla samma värde. När ett svar har tagits emot (lyckades eller Miss lyckas) måste värdet återställas för nästa anrop. |
| klient-begärande-ID| GUID| En unik identifierare för anropet, användbart loggar och nätverks spår för fel söknings fel. Värdet måste återställas för varje anrop. Alla åtgärder ska innehålla denna rubrik.                                                |
| x-MS-AGS-Diagnostic   | sträng | En sträng som innehåller diagnostisk information från tjänsten.
| timestamp|sträng | Tidsstämpel för begäran när API: et nåddes.
|ETag |sträng | ETag för resursen.
