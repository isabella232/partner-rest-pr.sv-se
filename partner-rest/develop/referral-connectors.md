---
title: Hänvisnings kopplingar.
description: Synkronisera partner hänvisningar med Dynamics 365 CRM-leads med hjälp av Microsoft Flow.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0a62023feb03114bb7ba1136b7700875f24c2e01
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770595"
---
# <a name="referral-connectors"></a>Hänvisnings kopplingar

Du kan använda referral-kopplingar för att synkronisera partner hänvisningar med leads för kund Relations hantering (CRM). Du kan skapa en hänvisnings koppling med [Microsoft Flow](https://flow.microsoft.com) som https-slutpunkt för att ta emot partner hänvisningar. Du kan sedan skriva den hänvisning som mottagits av flödet till ett CRM-system som ett lead.

## <a name="prerequisites"></a>Förutsättningar

* Microsoft Flow-prenumeration
  * Konto med administratörs åtkomst till den här prenumerationen
* Azure Active Directory (Azure AD) program-ID, användar-ID, lösen ord och klient-ID (används för att få åtkomst till partner-API). Installations anvisningar finns i [partner Authentication](api-authentication.md).
* [Azure Function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) -prenumeration.
* [Partner Center-webhook-händelse](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) prenumeration på [referens som skapats](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) och hänvisning till [uppdaterade](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event) händelser.
* [Microsoft Dynamics 365](https://dynamics.microsoft.com) -prenumeration
  * Sales-modulen är aktive rad
  * Konto med administratörs åtkomst till den här prenumerationen

## <a name="flow-overview"></a>Flödes översikt

Hänvisningarna importeras till CRM med följande flöde:

1. Partner konfigurerar en webhook för att ta emot hänvisnings meddelanden.
2. Partner registrerar webhooken med partner Center. Partnern prenumererar också på webhook-händelser när hänvisningar skapas eller uppdateras.
3. Referens klienten skapar eller uppdaterar en hänvisning.
4. Partner Center-webhook-system söker efter partnerns registrering och skickar ett meddelande till webhooken.
5. Webhook tar emot meddelandet.
6. Flow-dokument i Microsoft Flow använder en token för att anropa API: et för partner Center.
7. Flow-slutpunkten hämtar referensen.
8. Flow-slutpunkten skapar CRM-leadet.

![Flödes diagram som visar stegen i det här avsnittet för att importera partner hänvisningar till CRM.](../images/referralwebhook.png)

## <a name="flow-document-process"></a>Flödes dokument process

Flödes dokumentet för en hänvisnings koppling synkroniserar en partner hänvisning med ett CRM-lead från Dynamics 365.

1. Anslutningen hämtar en token för att ansluta till `https://api.partner.microsoft.com/v1.0/engagements/referrals` .
2. Koppling hämtar hänvisning som utlöste anslutnings tjänsten med hjälp av `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}` .
3. Connector ansluter till Dynamics 365.
4. Anslutnings programmet skapar ett nytt lead eller uppdaterar ett befintligt lead med den senaste informationen om referensen.
5. Referens för Connector-uppdateringar med de senaste uppdateringarna från CRM-leadet.

![Flödes diagram som visar stegen i det här avsnittet för flödes dokument processen.](../images/ReferralFlowSteps.png)

## <a name="sample-referral-connector"></a>Exempel på hänvisnings koppling

Följande exempel på en *hänvisnings koppling* visar hur du synkroniserar Partner Center-hänvisningar till CRM-leads i Dynamics 365.

> [!IMPORTANT]
> Du kan skriva till olika CRMs genom att ersätta [flödes kopplingarna](https://flow.microsoft.com/en-us/connectors/) i exempel koden.

### <a name="import-flow-synchronization-package"></a>Paket för import flödes synkronisering

Hämta och importera *exempel kods paketet* till Microsoft Flow och Anslut till Dynamics 365:

1. Ladda ned [Flow-synkroniseringsschemat](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) från [GitHub-lagrings platsen](https://github.com/microsoft/Partner-Center-Referrals).
2. Logga in på [Microsoft Flow](https://flow.microsoft.com) med rätt autentiseringsuppgifter.
3. Välj **mina flöden** i navigerings menyn. Välj sedan **Importera**.
4. På sidan **Importera paket** väljer du det flöde för Flow-synkronisering som du laddade ned. Välj sedan **Ladda upp**.

    ![Skärmen för att importera paket för paketfiler](../images/importPackage.png)

5. När paketet har överförts hittar du det paket som du laddade upp i **gransknings paketets innehåll** .

    ![Information om fönstret för att importera paket](../images/importPackageDetails.png)

6. Välj knappen **åtgärd** (Penn ikonen) för det uppladdade paketet. Då öppnas bladet **Importera konfiguration** .
7. Välj **installations** typ.

    * Om du vill skapa ett nytt flöde väljer du **skapa som nytt** och anger ett nytt **resurs namn**.
    * Om du vill uppdatera ett befintligt flöde med samma namn väljer du **Uppdatera**.

    ![Skapa eller uppdatera ny paket-skärm](../images/CreateNewConnection.png)

8. På sidan **Importera paket** letar du upp din Dynamics 365-anslutning i avsnittet **Granska paket innehåll** under **relaterade resurser**.
9. Välj knappen **åtgärd** (Penn ikonen) för din Dynamics 365-anslutning. Då öppnas bladet **Importera konfiguration** för den här relaterade resursen.
10. Välj **Skapa nytt** för att skapa en ny Dynamics 365-anslutning eller Välj en befintlig anslutning.
11. Kontrol lera att sidan **Importera paket** visar den valda flödes installations typen och Dynamics 365-anslutningen. Välj sedan **Importera**.

    ![Status skärm för import paket](../images/importStatus.png)

12. Kontrol lera att din flödes resurs nu har skapats eller uppdaterats.

### <a name="configure-flow-parameters"></a>Konfigurera flödes parametrar

Konfigurera parametrarna för din flödes resurs:

1. I [Microsoft Flow](https://flow.microsoft.com)väljer du **mina flöden** i navigerings menyn.
2. Välj den flödes resurs som du skapade eller uppdaterade i föregående avsnitt.
3. På sidan flöde väljer du **Redigera flöde**.
4. Välj variabeln **AAD-Application (klient) ID** och ange ID: t för ditt Azure AD-program.
5. Välj **UserID** -variabeln och ange ditt användar-ID.
6. Välj **userPassword** -variabeln och ange ditt användar lösen ord.
7. Välj variabeln **AAD-Directory (klient) ID** . Ange klient-ID för ditt Azure AD-program.
8. Spara ditt flöde genom att välja **Spara** .

    ![Skärmen Inställningar för flödes variabler](../images/SetFlowVariables.png)

### <a name="authenticate-the-callback"></a>Autentisera motringningen

Autentisera återanrops händelsen från Partner Center:

> [!TIP]
> Ett exempel på en exempel funktion finns i [appens exempel kod](#sample-function-app-code) i följande avsnitt.

1. [Skapa en Azure Function-app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) som [autentiserar återanrops händelsen från Partner Center](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback).

    1. Kontrol lera att de nödvändiga rubrikerna finns (**auktorisering**, **x-MS-Certificate-URL** och **x-MS-Signature-algorithm**).
    2. Hämta certifikatet som används för att signera innehållet (**x-MS-Certificate-URL**).
    3. Verifiera certifikat kedjan.
    4. Verifiera certifikatets **organisation** .
    5. Läs innehållet med UTF-8-kodning i en buffert.
    6. Skapa en RSA-Krypto-Provider.
    7. [Kontrol lera att signaturen matchar](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) vad som har signerats med angiven hash-algoritm (till exempel SHA256).
    8. Om verifieringen lyckas returneras ett **OK** -meddelande.

2. Observera den genererade återanrops-URI: n för funktions appens HTTP-slutpunkt. Denna URI visas när du skapar din Function-app. Du kan också hitta denna URI på funktions appens Azure-resurs sida.
3. I [Microsoft Flow](https://flow.microsoft.com)redigerar du flödet "partner hänvisning till Microsoft Dynamics CRM-lead" som du importerade i avsnittet *[import Flow-synkroniseringsjobb](#import-flow-synchronization-package)*.

    1. Lägg till värdet för Function-appens URI i steget "Web Hook Certificate Validation".
    2. Kopiera och klistra in funktions appens återanrops-URI i flödes dokumentet.
    3. Spara ditt flödes dokument.

#### <a name="sample-function-app-code"></a>Exempel kod för app-funktion

```csharp
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using Microsoft.Azure.WebJobs;
using Microsoft.Extensions.Logging;
using System;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Security.Cryptography.X509Certificates;
using System.Text;
using System.Threading.Tasks;

public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
{
    string requestBody = null;
    if (!string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-certificate-url")) && !string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-signature-algorithm")))
    {
        var certificateUrl = req?.Headers["x-ms-certificate-url"].First();
        try
        {
            string resultContent = null;
            using (var client = new HttpClient())
            {
                var result = await client.GetAsync(req.Headers["x-ms-certificate-url"].First());
                resultContent = await result.Content.ReadAsStringAsync();
                log.LogInformation(resultContent);
            }
            if (!string.IsNullOrEmpty(resultContent))
            {
                var certificate = new X509Certificate2(Encoding.UTF8.GetBytes(resultContent));
                var validationResult = certificate.Verify() && certificate.Issuer.Contains("O=Microsoft Corporation");
                if (validationResult)
                {
                    return new OkResult();
                }
                else
                {
                    return new BadRequestResult();
                }
            }
        }
        catch (Exception)
        {
            new BadRequestObjectResult("Certificate could not be retrieved, invalid caller to flow");
        }

        requestBody = await new StreamReader(req.Body).ReadToEndAsync();
        dynamic data = JsonConvert.DeserializeObject(requestBody);
    }
    else
    {
        new BadRequestObjectResult("Missing headers");
    }

    return new BadRequestObjectResult("Certificate validation failed");
}

private static string GetFirstValueFromHeader(HttpRequest request, string headerName)
{
    StringValues matchingHeaderValues;
    request.Headers.TryGetValue(headerName, out matchingHeaderValues);
    return matchingHeaderValues.Count != 0 ? matchingHeaderValues.First() : string.Empty;
}
```

### <a name="register-flow-with-partner-center"></a>Registrera flöde med partner Center

Registrera din Flow-resurs med partner Center för att utlösa flödet och ta emot webhook-händelser:

1. I [Microsoft Flow](https://flow.microsoft.com)väljer du **mina flöden** i navigerings menyn.
2. Välj det flöde som du skapade eller uppdaterade.
3. På sidan flöde väljer du **Redigera flöde**.
4. Kopiera och spara flödets **http post-URL**. Du måste använda denna URL för att utlösa flödet.
5. [Registrera dig för att ta emot webhook-händelser](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) när hänvisningar skapas eller uppdateras. Använd följande text format:

```json
{
    "WebhookUrl": "<<FlowUrl>>",
    "WebhookEvents": [
        "referral-created",
        "referral-updated"
    ],
    "signatureTokenToMsSignatureHeader": true
}
```
