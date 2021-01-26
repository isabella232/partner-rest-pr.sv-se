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
# <a name="referral-connectors"></a><span data-ttu-id="4d611-103">Hänvisnings kopplingar</span><span class="sxs-lookup"><span data-stu-id="4d611-103">Referral connectors</span></span>

<span data-ttu-id="4d611-104">Du kan använda referral-kopplingar för att synkronisera partner hänvisningar med leads för kund Relations hantering (CRM).</span><span class="sxs-lookup"><span data-stu-id="4d611-104">You can use referral connectors to synchronize partner referrals with customer relationship management (CRM) leads.</span></span> <span data-ttu-id="4d611-105">Du kan skapa en hänvisnings koppling med [Microsoft Flow](https://flow.microsoft.com) som https-slutpunkt för att ta emot partner hänvisningar.</span><span class="sxs-lookup"><span data-stu-id="4d611-105">You can create a referral connector using [Microsoft Flow](https://flow.microsoft.com) as the HTTPS endpoint to receive partner referrals.</span></span> <span data-ttu-id="4d611-106">Du kan sedan skriva den hänvisning som mottagits av flödet till ett CRM-system som ett lead.</span><span class="sxs-lookup"><span data-stu-id="4d611-106">You can then write the referral received by the flow to a CRM system as a lead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d611-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="4d611-107">Prerequisites</span></span>

* <span data-ttu-id="4d611-108">Microsoft Flow-prenumeration</span><span class="sxs-lookup"><span data-stu-id="4d611-108">Microsoft Flow subscription</span></span>
  * <span data-ttu-id="4d611-109">Konto med administratörs åtkomst till den här prenumerationen</span><span class="sxs-lookup"><span data-stu-id="4d611-109">Account with administrator access to this subscription</span></span>
* <span data-ttu-id="4d611-110">Azure Active Directory (Azure AD) program-ID, användar-ID, lösen ord och klient-ID (används för att få åtkomst till partner-API).</span><span class="sxs-lookup"><span data-stu-id="4d611-110">Azure Active Directory (Azure AD) application ID, user id, password and tenant ID (used to access the Partner API).</span></span> <span data-ttu-id="4d611-111">Installations anvisningar finns i [partner Authentication](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4d611-111">For setup instructions, see [Partner authentication](api-authentication.md).</span></span>
* <span data-ttu-id="4d611-112">[Azure Function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) -prenumeration.</span><span class="sxs-lookup"><span data-stu-id="4d611-112">[Azure function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) subscription.</span></span>
* <span data-ttu-id="4d611-113">[Partner Center-webhook-händelse](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) prenumeration på [referens som skapats](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) och hänvisning till [uppdaterade](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event) händelser.</span><span class="sxs-lookup"><span data-stu-id="4d611-113">[Partner Center webhook event](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) subscription to [Referral Created](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) and [Referral Updated](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event) events.</span></span>
* <span data-ttu-id="4d611-114">[Microsoft Dynamics 365](https://dynamics.microsoft.com) -prenumeration</span><span class="sxs-lookup"><span data-stu-id="4d611-114">[Microsoft Dynamics 365](https://dynamics.microsoft.com) subscription</span></span>
  * <span data-ttu-id="4d611-115">Sales-modulen är aktive rad</span><span class="sxs-lookup"><span data-stu-id="4d611-115">Sales module enabled</span></span>
  * <span data-ttu-id="4d611-116">Konto med administratörs åtkomst till den här prenumerationen</span><span class="sxs-lookup"><span data-stu-id="4d611-116">Account with administrator access to this subscription</span></span>

## <a name="flow-overview"></a><span data-ttu-id="4d611-117">Flödes översikt</span><span class="sxs-lookup"><span data-stu-id="4d611-117">Flow overview</span></span>

<span data-ttu-id="4d611-118">Hänvisningarna importeras till CRM med följande flöde:</span><span class="sxs-lookup"><span data-stu-id="4d611-118">Referrals are imported into the CRM using the following flow:</span></span>

1. <span data-ttu-id="4d611-119">Partner konfigurerar en webhook för att ta emot hänvisnings meddelanden.</span><span class="sxs-lookup"><span data-stu-id="4d611-119">Partner sets up a webhook to receive referral notifications.</span></span>
2. <span data-ttu-id="4d611-120">Partner registrerar webhooken med partner Center.</span><span class="sxs-lookup"><span data-stu-id="4d611-120">Partner registers the webhook with Partner Center.</span></span> <span data-ttu-id="4d611-121">Partnern prenumererar också på webhook-händelser när hänvisningar skapas eller uppdateras.</span><span class="sxs-lookup"><span data-stu-id="4d611-121">The partner also subscribes to webhook events for when referrals are created or updated.</span></span>
3. <span data-ttu-id="4d611-122">Referens klienten skapar eller uppdaterar en hänvisning.</span><span class="sxs-lookup"><span data-stu-id="4d611-122">Referral client creates or updates a referral.</span></span>
4. <span data-ttu-id="4d611-123">Partner Center-webhook-system söker efter partnerns registrering och skickar ett meddelande till webhooken.</span><span class="sxs-lookup"><span data-stu-id="4d611-123">Partner Center webhook system checks for the partner's registration and sends a notification to the webhook.</span></span>
5. <span data-ttu-id="4d611-124">Webhook tar emot meddelandet.</span><span class="sxs-lookup"><span data-stu-id="4d611-124">Webhook receives the notification.</span></span>
6. <span data-ttu-id="4d611-125">Flow-dokument i Microsoft Flow använder en token för att anropa API: et för partner Center.</span><span class="sxs-lookup"><span data-stu-id="4d611-125">Flow document in Microsoft flow uses a token to make a call to the Partner Center referral API.</span></span>
7. <span data-ttu-id="4d611-126">Flow-slutpunkten hämtar referensen.</span><span class="sxs-lookup"><span data-stu-id="4d611-126">Flow endpoint gets the referral.</span></span>
8. <span data-ttu-id="4d611-127">Flow-slutpunkten skapar CRM-leadet.</span><span class="sxs-lookup"><span data-stu-id="4d611-127">Flow endpoint creates the CRM lead.</span></span>

![Flödes diagram som visar stegen i det här avsnittet för att importera partner hänvisningar till CRM.](../images/referralwebhook.png)

## <a name="flow-document-process"></a><span data-ttu-id="4d611-129">Flödes dokument process</span><span class="sxs-lookup"><span data-stu-id="4d611-129">Flow document process</span></span>

<span data-ttu-id="4d611-130">Flödes dokumentet för en hänvisnings koppling synkroniserar en partner hänvisning med ett CRM-lead från Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="4d611-130">The flow document for a referral connector synchronizes a partner referral with a CRM lead from Dynamics 365.</span></span>

1. <span data-ttu-id="4d611-131">Anslutningen hämtar en token för att ansluta till `https://api.partner.microsoft.com/v1.0/engagements/referrals` .</span><span class="sxs-lookup"><span data-stu-id="4d611-131">Connector gets a token to connect to `https://api.partner.microsoft.com/v1.0/engagements/referrals`.</span></span>
2. <span data-ttu-id="4d611-132">Koppling hämtar hänvisning som utlöste anslutnings tjänsten med hjälp av `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}` .</span><span class="sxs-lookup"><span data-stu-id="4d611-132">Connector obtains referral that triggered the connector using `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}`.</span></span>
3. <span data-ttu-id="4d611-133">Connector ansluter till Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="4d611-133">Connector connects to Dynamics 365.</span></span>
4. <span data-ttu-id="4d611-134">Anslutnings programmet skapar ett nytt lead eller uppdaterar ett befintligt lead med den senaste informationen om referensen.</span><span class="sxs-lookup"><span data-stu-id="4d611-134">Connector creates a new lead or updates an existing lead with the latest information on the referral.</span></span>
5. <span data-ttu-id="4d611-135">Referens för Connector-uppdateringar med de senaste uppdateringarna från CRM-leadet.</span><span class="sxs-lookup"><span data-stu-id="4d611-135">Connector updates referral with the latest updates from the CRM lead.</span></span>

![Flödes diagram som visar stegen i det här avsnittet för flödes dokument processen.](../images/ReferralFlowSteps.png)

## <a name="sample-referral-connector"></a><span data-ttu-id="4d611-137">Exempel på hänvisnings koppling</span><span class="sxs-lookup"><span data-stu-id="4d611-137">Sample referral connector</span></span>

<span data-ttu-id="4d611-138">Följande exempel på en *hänvisnings koppling* visar hur du synkroniserar Partner Center-hänvisningar till CRM-leads i Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="4d611-138">The following *sample referral connector* shows how to synchronize Partner Center referrals to CRM leads in Dynamics 365.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d611-139">Du kan skriva till olika CRMs genom att ersätta [flödes kopplingarna](https://flow.microsoft.com/en-us/connectors/) i exempel koden.</span><span class="sxs-lookup"><span data-stu-id="4d611-139">You can write to different CRMs by replacing the [flow connectors](https://flow.microsoft.com/en-us/connectors/) in the sample code.</span></span>

### <a name="import-flow-synchronization-package"></a><span data-ttu-id="4d611-140">Paket för import flödes synkronisering</span><span class="sxs-lookup"><span data-stu-id="4d611-140">Import flow synchronization package</span></span>

<span data-ttu-id="4d611-141">Hämta och importera *exempel kods paketet* till Microsoft Flow och Anslut till Dynamics 365:</span><span class="sxs-lookup"><span data-stu-id="4d611-141">Download and import the *sample code package* into Microsoft Flow and connect to Dynamics 365:</span></span>

1. <span data-ttu-id="4d611-142">Ladda ned [Flow-synkroniseringsschemat](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) från [GitHub-lagrings platsen](https://github.com/microsoft/Partner-Center-Referrals).</span><span class="sxs-lookup"><span data-stu-id="4d611-142">Download the [flow synchronization package](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) from the [GitHub repo](https://github.com/microsoft/Partner-Center-Referrals).</span></span>
2. <span data-ttu-id="4d611-143">Logga in på [Microsoft Flow](https://flow.microsoft.com) med rätt autentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="4d611-143">Sign in to [Microsoft Flow](https://flow.microsoft.com) using the appropriate credentials.</span></span>
3. <span data-ttu-id="4d611-144">Välj **mina flöden** i navigerings menyn.</span><span class="sxs-lookup"><span data-stu-id="4d611-144">Choose **My Flows** in the navigation menu.</span></span> <span data-ttu-id="4d611-145">Välj sedan **Importera**.</span><span class="sxs-lookup"><span data-stu-id="4d611-145">Then choose **Import**.</span></span>
4. <span data-ttu-id="4d611-146">På sidan **Importera paket** väljer du det flöde för Flow-synkronisering som du laddade ned.</span><span class="sxs-lookup"><span data-stu-id="4d611-146">On the **Import package** page, select the flow synchronization package that you downloaded.</span></span> <span data-ttu-id="4d611-147">Välj sedan **Ladda upp**.</span><span class="sxs-lookup"><span data-stu-id="4d611-147">Then choose **Upload**.</span></span>

    ![Skärmen för att importera paket för paketfiler](../images/importPackage.png)

5. <span data-ttu-id="4d611-149">När paketet har överförts hittar du det paket som du laddade upp i **gransknings paketets innehåll** .</span><span class="sxs-lookup"><span data-stu-id="4d611-149">After the package upload is complete, find the package you uploaded in the **Review Package Content** .</span></span>

    ![Information om fönstret för att importera paket](../images/importPackageDetails.png)

6. <span data-ttu-id="4d611-151">Välj knappen **åtgärd** (Penn ikonen) för det uppladdade paketet.</span><span class="sxs-lookup"><span data-stu-id="4d611-151">Choose the **Action** button (pencil icon) for your uploaded package.</span></span> <span data-ttu-id="4d611-152">Då öppnas bladet **Importera konfiguration** .</span><span class="sxs-lookup"><span data-stu-id="4d611-152">This opens the **Import setup** blade.</span></span>
7. <span data-ttu-id="4d611-153">Välj **installations** typ.</span><span class="sxs-lookup"><span data-stu-id="4d611-153">Choose your **Setup** type.</span></span>

    * <span data-ttu-id="4d611-154">Om du vill skapa ett nytt flöde väljer du **skapa som nytt** och anger ett nytt **resurs namn**.</span><span class="sxs-lookup"><span data-stu-id="4d611-154">To create a new flow, select **Create as new**, and enter a new **Resource name**.</span></span>
    * <span data-ttu-id="4d611-155">Om du vill uppdatera ett befintligt flöde med samma namn väljer du **Uppdatera**.</span><span class="sxs-lookup"><span data-stu-id="4d611-155">To update an existing flow with the same name, select **Update**.</span></span>

    ![Skapa eller uppdatera ny paket-skärm](../images/CreateNewConnection.png)

8. <span data-ttu-id="4d611-157">På sidan **Importera paket** letar du upp din Dynamics 365-anslutning i avsnittet **Granska paket innehåll** under **relaterade resurser**.</span><span class="sxs-lookup"><span data-stu-id="4d611-157">On the **Import package** page, find your Dynamics 365 connection in the **Review Package Content** section under **Related Resources**.</span></span>
9. <span data-ttu-id="4d611-158">Välj knappen **åtgärd** (Penn ikonen) för din Dynamics 365-anslutning.</span><span class="sxs-lookup"><span data-stu-id="4d611-158">Choose the **Action** button (pencil icon) for your Dynamics 365 connection.</span></span> <span data-ttu-id="4d611-159">Då öppnas bladet **Importera konfiguration** för den här relaterade resursen.</span><span class="sxs-lookup"><span data-stu-id="4d611-159">This opens the **Import setup** blade for this related resource.</span></span>
10. <span data-ttu-id="4d611-160">Välj **Skapa nytt** för att skapa en ny Dynamics 365-anslutning eller Välj en befintlig anslutning.</span><span class="sxs-lookup"><span data-stu-id="4d611-160">Choose **Create new** to create a new Dynamics 365 connection, or select an existing connection.</span></span>
11. <span data-ttu-id="4d611-161">Kontrol lera att sidan **Importera paket** visar den valda flödes installations typen och Dynamics 365-anslutningen.</span><span class="sxs-lookup"><span data-stu-id="4d611-161">Verify that the **Import package** page now shows your selected flow setup type and Dynamics 365 connection.</span></span> <span data-ttu-id="4d611-162">Välj sedan **Importera**.</span><span class="sxs-lookup"><span data-stu-id="4d611-162">Then choose **Import**.</span></span>

    ![Status skärm för import paket](../images/importStatus.png)

12. <span data-ttu-id="4d611-164">Kontrol lera att din flödes resurs nu har skapats eller uppdaterats.</span><span class="sxs-lookup"><span data-stu-id="4d611-164">Verify that your flow resource is now created or updated.</span></span>

### <a name="configure-flow-parameters"></a><span data-ttu-id="4d611-165">Konfigurera flödes parametrar</span><span class="sxs-lookup"><span data-stu-id="4d611-165">Configure flow parameters</span></span>

<span data-ttu-id="4d611-166">Konfigurera parametrarna för din flödes resurs:</span><span class="sxs-lookup"><span data-stu-id="4d611-166">Configure the parameters of your flow resource:</span></span>

1. <span data-ttu-id="4d611-167">I [Microsoft Flow](https://flow.microsoft.com)väljer du **mina flöden** i navigerings menyn.</span><span class="sxs-lookup"><span data-stu-id="4d611-167">In [Microsoft Flow](https://flow.microsoft.com), choose **My Flows** in the navigation menu.</span></span>
2. <span data-ttu-id="4d611-168">Välj den flödes resurs som du skapade eller uppdaterade i föregående avsnitt.</span><span class="sxs-lookup"><span data-stu-id="4d611-168">Choose the flow resource you created or updated in the previous section.</span></span>
3. <span data-ttu-id="4d611-169">På sidan flöde väljer du **Redigera flöde**.</span><span class="sxs-lookup"><span data-stu-id="4d611-169">On the flow page, choose **Edit flow**.</span></span>
4. <span data-ttu-id="4d611-170">Välj variabeln **AAD-Application (klient) ID** och ange ID: t för ditt Azure AD-program.</span><span class="sxs-lookup"><span data-stu-id="4d611-170">Choose the **AAD-Application (client) ID** variable and enter the ID of your Azure AD application.</span></span>
5. <span data-ttu-id="4d611-171">Välj **UserID** -variabeln och ange ditt användar-ID.</span><span class="sxs-lookup"><span data-stu-id="4d611-171">Choose the **UserId** variable and enter your user ID.</span></span>
6. <span data-ttu-id="4d611-172">Välj **userPassword** -variabeln och ange ditt användar lösen ord.</span><span class="sxs-lookup"><span data-stu-id="4d611-172">Choose the **UserPassword** variable and enter your user password.</span></span>
7. <span data-ttu-id="4d611-173">Välj variabeln **AAD-Directory (klient) ID** .</span><span class="sxs-lookup"><span data-stu-id="4d611-173">Select the **AAD-Directory (tenant) ID** variable.</span></span> <span data-ttu-id="4d611-174">Ange klient-ID för ditt Azure AD-program.</span><span class="sxs-lookup"><span data-stu-id="4d611-174">Enter the tenant ID of your Azure AD application.</span></span>
8. <span data-ttu-id="4d611-175">Spara ditt flöde genom att välja **Spara** .</span><span class="sxs-lookup"><span data-stu-id="4d611-175">Choose **Save** to save your flow.</span></span>

    ![Skärmen Inställningar för flödes variabler](../images/SetFlowVariables.png)

### <a name="authenticate-the-callback"></a><span data-ttu-id="4d611-177">Autentisera motringningen</span><span class="sxs-lookup"><span data-stu-id="4d611-177">Authenticate the callback</span></span>

<span data-ttu-id="4d611-178">Autentisera återanrops händelsen från Partner Center:</span><span class="sxs-lookup"><span data-stu-id="4d611-178">Authenticate the callback event from the Partner Center:</span></span>

> [!TIP]
> <span data-ttu-id="4d611-179">Ett exempel på en exempel funktion finns i [appens exempel kod](#sample-function-app-code) i följande avsnitt.</span><span class="sxs-lookup"><span data-stu-id="4d611-179">For an example, see the [sample function app code](#sample-function-app-code) in the following section.</span></span>

1. <span data-ttu-id="4d611-180">[Skapa en Azure Function-app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) som [autentiserar återanrops händelsen från Partner Center](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback).</span><span class="sxs-lookup"><span data-stu-id="4d611-180">[Create an Azure function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) that [authenticates the callback event from the Partner Center](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback).</span></span>

    1. <span data-ttu-id="4d611-181">Kontrol lera att de nödvändiga rubrikerna finns (**auktorisering**, **x-MS-Certificate-URL** och **x-MS-Signature-algorithm**).</span><span class="sxs-lookup"><span data-stu-id="4d611-181">Verify that the required headers are present (**Authorization**, **x-ms-certificate-url**, and **x-ms-signature-algorithm**).</span></span>
    2. <span data-ttu-id="4d611-182">Hämta certifikatet som används för att signera innehållet (**x-MS-Certificate-URL**).</span><span class="sxs-lookup"><span data-stu-id="4d611-182">Download the certificate used to sign the content (**x-ms-certificate-url**).</span></span>
    3. <span data-ttu-id="4d611-183">Verifiera certifikat kedjan.</span><span class="sxs-lookup"><span data-stu-id="4d611-183">Verify the certificate chain.</span></span>
    4. <span data-ttu-id="4d611-184">Verifiera certifikatets **organisation** .</span><span class="sxs-lookup"><span data-stu-id="4d611-184">Verify the **Organization** of the certificate.</span></span>
    5. <span data-ttu-id="4d611-185">Läs innehållet med UTF-8-kodning i en buffert.</span><span class="sxs-lookup"><span data-stu-id="4d611-185">Read the content with UTF-8 encoding into a buffer.</span></span>
    6. <span data-ttu-id="4d611-186">Skapa en RSA-Krypto-Provider.</span><span class="sxs-lookup"><span data-stu-id="4d611-186">Create an RSA Crypto Provider.</span></span>
    7. <span data-ttu-id="4d611-187">[Kontrol lera att signaturen matchar](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) vad som har signerats med angiven hash-algoritm (till exempel SHA256).</span><span class="sxs-lookup"><span data-stu-id="4d611-187">[Verify that the signature matches](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) what was signed with the specified hash algorithm (for example, SHA256).</span></span>
    8. <span data-ttu-id="4d611-188">Om verifieringen lyckas returneras ett **OK** -meddelande.</span><span class="sxs-lookup"><span data-stu-id="4d611-188">If the verification succeeds, an **OK** message is returned.</span></span>

2. <span data-ttu-id="4d611-189">Observera den genererade återanrops-URI: n för funktions appens HTTP-slutpunkt.</span><span class="sxs-lookup"><span data-stu-id="4d611-189">Note the generated callback URI for your function app's HTTP endpoint.</span></span> <span data-ttu-id="4d611-190">Denna URI visas när du skapar din Function-app.</span><span class="sxs-lookup"><span data-stu-id="4d611-190">This URI is displayed when you create your function app.</span></span> <span data-ttu-id="4d611-191">Du kan också hitta denna URI på funktions appens Azure-resurs sida.</span><span class="sxs-lookup"><span data-stu-id="4d611-191">You can also find this URI on your function app's Azure resource page.</span></span>
3. <span data-ttu-id="4d611-192">I [Microsoft Flow](https://flow.microsoft.com)redigerar du flödet "partner hänvisning till Microsoft Dynamics CRM-lead" som du importerade i avsnittet *[import Flow-synkroniseringsjobb](#import-flow-synchronization-package)*.</span><span class="sxs-lookup"><span data-stu-id="4d611-192">In [Microsoft Flow](https://flow.microsoft.com), edit the flow "Partner Referral to Microsoft Dynamics CRM Lead" that you imported in the section *[Import flow synchronization package](#import-flow-synchronization-package)*.</span></span>

    1. <span data-ttu-id="4d611-193">Lägg till värdet för Function-appens URI i steget "Web Hook Certificate Validation".</span><span class="sxs-lookup"><span data-stu-id="4d611-193">Add the value of the function app's URI to the "web hook certificate validation" step.</span></span>
    2. <span data-ttu-id="4d611-194">Kopiera och klistra in funktions appens återanrops-URI i flödes dokumentet.</span><span class="sxs-lookup"><span data-stu-id="4d611-194">Copy and paste your function app's callback URI into the flow document.</span></span>
    3. <span data-ttu-id="4d611-195">Spara ditt flödes dokument.</span><span class="sxs-lookup"><span data-stu-id="4d611-195">Save your flow document.</span></span>

#### <a name="sample-function-app-code"></a><span data-ttu-id="4d611-196">Exempel kod för app-funktion</span><span class="sxs-lookup"><span data-stu-id="4d611-196">Sample function app code</span></span>

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

### <a name="register-flow-with-partner-center"></a><span data-ttu-id="4d611-197">Registrera flöde med partner Center</span><span class="sxs-lookup"><span data-stu-id="4d611-197">Register flow with Partner Center</span></span>

<span data-ttu-id="4d611-198">Registrera din Flow-resurs med partner Center för att utlösa flödet och ta emot webhook-händelser:</span><span class="sxs-lookup"><span data-stu-id="4d611-198">Register your flow resource with the Partner Center to trigger the flow and receive webhook events:</span></span>

1. <span data-ttu-id="4d611-199">I [Microsoft Flow](https://flow.microsoft.com)väljer du **mina flöden** i navigerings menyn.</span><span class="sxs-lookup"><span data-stu-id="4d611-199">In [Microsoft Flow](https://flow.microsoft.com), choose **My Flows** in the navigation menu.</span></span>
2. <span data-ttu-id="4d611-200">Välj det flöde som du skapade eller uppdaterade.</span><span class="sxs-lookup"><span data-stu-id="4d611-200">Choose the flow you created or updated.</span></span>
3. <span data-ttu-id="4d611-201">På sidan flöde väljer du **Redigera flöde**.</span><span class="sxs-lookup"><span data-stu-id="4d611-201">On the flow page, choose **Edit flow**.</span></span>
4. <span data-ttu-id="4d611-202">Kopiera och spara flödets **http post-URL**.</span><span class="sxs-lookup"><span data-stu-id="4d611-202">Copy and save the flow's **HTTP POST URL**.</span></span> <span data-ttu-id="4d611-203">Du måste använda denna URL för att utlösa flödet.</span><span class="sxs-lookup"><span data-stu-id="4d611-203">You will need to use this URL to trigger the flow.</span></span>
5. <span data-ttu-id="4d611-204">[Registrera dig för att ta emot webhook-händelser](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) när hänvisningar skapas eller uppdateras.</span><span class="sxs-lookup"><span data-stu-id="4d611-204">[Register to receive webhook events](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) when referrals are created or updated.</span></span> <span data-ttu-id="4d611-205">Använd följande text format:</span><span class="sxs-lookup"><span data-stu-id="4d611-205">Use the following body format:</span></span>

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
