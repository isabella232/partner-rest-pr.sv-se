---
title: Fel koder för partner-API REST
description: 'Partner REST-API: er returnerar ett JSON-objekt med en status kod om din begäran har lyckats eller misslyckats.'
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0829f48e5028b4a19e8a6f7b89fbb41d83a50cab
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770615"
---
# <a name="partner-api-rest-error-codes"></a>Fel koder för partner-API REST

Gäller för:

- Partner-API

Fel i partner REST-API: er returneras med HTTP-standardstatus koder och ett JSON-felsvars objekt.

## <a name="http-status-codes"></a>HTTP-statuskoder

I följande tabell visas och beskrivs de HTTP-statuskod som kan returneras.

| Statuskod | Statusmeddelande                  | Description                                                                                                                            |
|:------------|:--------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------|
| 400         | Felaktig begäran                     | Det går inte att bearbeta begäran eftersom den är felaktig eller felaktig.                                                                       |
| 401         | Behörighet saknas                    | Nödvändig autentiseringsinformation saknas eller är inte giltig för resursen.                                                   |
| 403         | Förbjudet                       | Åtkomst nekas till den begärda resursen. Användaren kanske inte har tillräcklig behörighet. **Viktigt: om principer för villkorlig åtkomst tillämpas på en resurs `HTTP 403; Forbidden error=insufficent_claims` kan returneras.** Mer information om Microsoft Graph och villkorlig åtkomst finns i utvecklings [vägledning för Azure Active Directory villkorlig åtkomst](https://docs.microsoft.com/azure/active-directory/develop/active-directory-conditional-access-developer)  |
| 404         | Hittades inte                       | Den begärda resursen finns inte.                                                                                                  |
| 405         | Metoden tillåts inte              | HTTP-metoden i begäran tillåts inte på resursen.                                                                         |
| 406         | Inte acceptabelt                  | Den här tjänsten stöder inte det format som begärdes i accept-huvudet.                                                                |
| 409         | Konflikt                        | Det aktuella läget är i konflikt med vad begäran förväntar sig. Den angivna överordnade mappen kanske till exempel inte finns.                   |
| 410         | 410                            | Den begärda resursen är inte längre tillgänglig på servern.                                               |
| 411         | Längd krävs                 | En Content-Length-rubrik krävs för begäran.                                                                                    |
| 412         | Förhands villkor misslyckades             | Ett villkor som anges i begäran (till exempel ett IF-match-huvud) matchar inte resursens aktuella tillstånd.                       |
| 413         | Begär ande enheten är för stor        | Storleken på begäran överskrider max gränsen.                                                                                            |
| 415         | Medie typen stöds inte          | Innehålls typen för begäran är ett format som inte stöds av tjänsten.                                                      |
| 416         | Begärt intervall uppfyller inte kraven | Det angivna byte-intervallet är ogiltigt eller inte tillgängligt.                                                                                    |
| 422         | En entitet som inte går att bearbeta            | Det går inte att bearbeta begäran eftersom den är semantiskt felaktig.                                                                        |
| 423         | Låst                          | Den resurs som öppnas är låst.                                                                                          |
| 429         | För många begär Anden               | Klient programmet har begränsats och bör inte försöka upprepa begäran förrän en viss tid har förflutit.                |
| 500         | Internt Server fel           | Ett internt Server fel uppstod när begäran bearbetades.                                                                       |
| 501         | Inte implementerat                 | Den begärda funktionen har inte implementerats.                                                                                               |
| 503         | Tjänsten är inte tillgänglig             | Tjänsten är tillfälligt otillgänglig för underhåll eller är överbelastad. Du kan upprepa begäran efter en fördröjning, vars längd kan anges i ett Retry-After huvud.|
| 504         | Gateway-timeout                 | Servern har inte tagit emot svar i tid från den överordnade server som krävdes för att få åtkomst vid försök att slutföra begäran. Kan uppstå tillsammans med 503. |
| 507         | Otillräckligt lagrings utrymme            | Den maximala lagrings kvoten har uppnåtts.                                                                                            |
| 509         | Bandbredds gränsen har överskridits        | Din app har begränsats för att överskrida den högsta bandbredds begränsningen. Din app kan försöka utföra begäran igen när mer tid har förflutit. |

Fel svaret är ett enda JSON-objekt som innehåller en enskild egenskap med namnet **Error**. Det här objektet innehåller all information om felet. Du kan använda informationen som returneras här i stället för eller utöver HTTP-statuskoden. Följande är ett exempel på en fullständig JSON-feltext.

## <a name="error-resource-type"></a>Fel resurs typ

Fel svaret är ett enda JSON-objekt som innehåller en enskild egenskap med namnet **Error**. Det här objektet innehåller all information om felet. Du kan använda informationen som returneras här i stället för eller utöver HTTP-statuskoden. Följande är ett exempel på en fullständig JSON-feltext.

I följande tabell-och kod exempel beskrivs schemat för ett fel svar.

| Namn        | Typ   | Description                                                                                    |
|-------------|--------|------------------------------------------------------------------------------------------------|
| kod        | sträng | Returneras alltid. Anger vilken typ av fel som inträffat. Icke-null.                          |
| meddelande | sträng | Returneras alltid. Beskriver felet i detalj och ger ytterligare felsöknings information. Icke-null, icke-tomt. Maximal längd är 1024 tecken. |
| innerError        | objekt  | Valfritt. Ytterligare fel objekt som kan vara mer detaljerad än det översta nivå felet.                                   |
| fokusera      | sträng | Målet som felet kom från.                                                      |

### <a name="code-property"></a>Kod egenskap

`code`Egenskapen innehåller ett av följande möjliga värden. Dina appar bör vara för beredda för att hantera något av dessa fel.

| Kod                      | Description
|:--------------------------|:--------------
| **accessDenied**          | Anroparen har inte behörighet att utföra åtgärden.
| **generalException**      | Ett ospecificerat fel har inträffat.
| **invalidRequest**        | Begäran är felaktig eller felaktig.
| **itemNotFound**          | Det gick inte att hitta resursen.
|**preconditionFailed**     | Ett villkor som anges i begäran (till exempel ett IF-match-huvud) matchar inte resursens aktuella tillstånd.
| **resourceModified**      | Den resurs som uppdateras har ändrats sedan den senast läste den, vanligt vis en eTag-matchning.
| **serviceNotAvailable**   | Tjänsten är inte tillgänglig. Försök utföra begäran igen efter en fördröjning. Det kan finnas ett Retry-Afters huvud.
| **oautentiserade**       | Anroparen är inte autentiserad.

### <a name="message-property"></a>Meddelande egenskap

`message`Egenskapen i roten innehåller ett fel meddelande som är avsett för att utvecklaren ska kunna läsa. Fel meddelanden är inte lokaliserade och visas inte direkt för användaren. Vid hantering av fel bör din kod inte kontrol lera mot `message` värden eftersom de kan ändras när som helst, och de innehåller ofta dynamisk information som är unik för den misslyckade begäran. Du bör bara koda mot felkoder som returneras i `code` Egenskaper.

### <a name="innererror-object"></a>InnerError-objekt

`innererror`Objektet kan rekursivt innehålla fler `innererror` objekt med ytterligare, mer detaljerade felkoder. Vid hantering av ett fel bör apparna gå igenom alla felkoder som är tillgängliga och använda de mest detaljerade som de förstår.

Det finns ytterligare fel som din app kan stöta på i de kapslade `innererror` objekten. Appar krävs inte för att hantera dessa, men kan om de väljer. Tjänsten kan lägga till nya felkoder eller sluta att returnera gamla när som helst, så det är viktigt att alla appar kan hantera [Basic Error Codes]

```json
{
  "error": {
    "code": "unAuthorized",
    "message": "Caller is not authorized to access the resource.",
    "target": "referral",
    "innerError": {
      "code": "innerErrorCode",
      "message": "Unauthorized referral access"
    }
  }
}
```
