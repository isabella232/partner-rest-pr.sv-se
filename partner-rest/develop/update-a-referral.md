---
title: Uppdatera ett lead eller en affärs möjlighet (föråldrad)
description: Gör att du kan uppdatera lead-eller affärs möjlighets information. Den här metoden för att uppdatera ett lead eller en affärs möjlighet är föråldrad och vi recommmend istället för att använda PATCH-anropet.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 9705db1c21dbec7099cfefebdc7bb23ec65e428c
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770644"
---
# <a name="update-a-lead-or-opportunity-obsolete"></a><span data-ttu-id="06605-104">Uppdatera ett lead eller en affärs möjlighet (föråldrad)</span><span class="sxs-lookup"><span data-stu-id="06605-104">Update a lead or opportunity (Obsolete)</span></span>

<span data-ttu-id="06605-105">Gäller för:</span><span class="sxs-lookup"><span data-stu-id="06605-105">Applies to:</span></span>

- <span data-ttu-id="06605-106">Partner-API</span><span class="sxs-lookup"><span data-stu-id="06605-106">Partner API</span></span>

<span data-ttu-id="06605-107">I det här avsnittet beskrivs hur du uppdaterar lead-eller affärs möjlighets information, till exempel avtals värde, uppskattat stängnings datum eller hantera försäljnings stegen i annan information.</span><span class="sxs-lookup"><span data-stu-id="06605-107">This topic explains how to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.</span></span> 


> [!IMPORTANT]
<span data-ttu-id="06605-108">Den här metoden för att uppdatera ett lead eller en affärs möjlighet är föråldrad och vi recommmend istället för att använda [patch](patch-a-referral.md) -anropet.</span><span class="sxs-lookup"><span data-stu-id="06605-108">This method of updating a lead or opportunity is obsolete and we recommmend using the [PATCH](patch-a-referral.md) call instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06605-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="06605-109">Prerequisites</span></span>

- <span data-ttu-id="06605-110">Autentiseringsuppgifter enligt beskrivningen i [partner-API-autentisering](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="06605-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="06605-111">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="06605-111">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="06605-112">Detta API stöder för närvarande endast användar åtkomst där partners måste vara i någon av följande roller: global administratör, referens administratör eller hänvisnings användare.</span><span class="sxs-lookup"><span data-stu-id="06605-112">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="06605-113">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="06605-113">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="06605-114">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="06605-114">Request syntax</span></span>

| <span data-ttu-id="06605-115">Metod</span><span class="sxs-lookup"><span data-stu-id="06605-115">Method</span></span>  | <span data-ttu-id="06605-116">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="06605-116">Request URI</span></span>                                                       |
|---------|-------------------------------------------------------------------|
| <span data-ttu-id="06605-117">**PUT**</span><span class="sxs-lookup"><span data-stu-id="06605-117">**PUT**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="request-headers"></a><span data-ttu-id="06605-118">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="06605-118">Request headers</span></span>

- <span data-ttu-id="06605-119">Mer information finns i [partner API rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="06605-119">For more information, see [Partner API REST headers](headers.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06605-120">Se till att ange **If-Match-** huvudet.</span><span class="sxs-lookup"><span data-stu-id="06605-120">Be sure to set the **If-Match** header.</span></span>

### <a name="request-body"></a><span data-ttu-id="06605-121">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="06605-121">Request body</span></span>

<span data-ttu-id="06605-122">Den här tabellen beskriver [hänvisnings](referral-resources.md) egenskaperna i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="06605-122">This table describes the [Referral](referral-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="06605-123">Egenskap</span><span class="sxs-lookup"><span data-stu-id="06605-123">Property</span></span>            | <span data-ttu-id="06605-124">Typ</span><span class="sxs-lookup"><span data-stu-id="06605-124">Type</span></span>                                                                 | <span data-ttu-id="06605-125">Description</span><span class="sxs-lookup"><span data-stu-id="06605-125">Description</span></span>                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="06605-126">Id</span><span class="sxs-lookup"><span data-stu-id="06605-126">Id</span></span>                  | <span data-ttu-id="06605-127">sträng</span><span class="sxs-lookup"><span data-stu-id="06605-127">string</span></span>                                                               | <span data-ttu-id="06605-128">ID för den här hänvisningen.</span><span class="sxs-lookup"><span data-stu-id="06605-128">The ID for this Referral.</span></span>                                                                                            |
| <span data-ttu-id="06605-129">EngagementId</span><span class="sxs-lookup"><span data-stu-id="06605-129">EngagementId</span></span>        | <span data-ttu-id="06605-130">sträng</span><span class="sxs-lookup"><span data-stu-id="06605-130">string</span></span>                                                               | <span data-ttu-id="06605-131">EngagementID för den här referensen.</span><span class="sxs-lookup"><span data-stu-id="06605-131">The EngagementID for this Referral.</span></span> <span data-ttu-id="06605-132">Flera hänvisningar kan associeras med en enda EngagementID</span><span class="sxs-lookup"><span data-stu-id="06605-132">Multiple referrals can be associated to a single EngagementID</span></span>                    |
| <span data-ttu-id="06605-133">Name</span><span class="sxs-lookup"><span data-stu-id="06605-133">Name</span></span>                | <span data-ttu-id="06605-134">sträng</span><span class="sxs-lookup"><span data-stu-id="06605-134">string</span></span>                                                               | <span data-ttu-id="06605-135">Namnet på referensen.</span><span class="sxs-lookup"><span data-stu-id="06605-135">The name of the Referral.</span></span>                                                                                            |
| <span data-ttu-id="06605-136">ExternalReferenceId</span><span class="sxs-lookup"><span data-stu-id="06605-136">ExternalReferenceId</span></span> | <span data-ttu-id="06605-137">sträng</span><span class="sxs-lookup"><span data-stu-id="06605-137">string</span></span>                                                               | <span data-ttu-id="06605-138">En extern identifierare för referensen.</span><span class="sxs-lookup"><span data-stu-id="06605-138">An external identifier for the referral.</span></span> <span data-ttu-id="06605-139">Exempel: lagra ditt eget Dynamics 365-lead/affärs möjlighets-ID</span><span class="sxs-lookup"><span data-stu-id="06605-139">Example: Store your own Dynamics 365 lead/opportunity ID</span></span>                    |
| <span data-ttu-id="06605-140">CreatedDateTime</span><span class="sxs-lookup"><span data-stu-id="06605-140">CreatedDateTime</span></span>     | <span data-ttu-id="06605-141">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="06605-141">string in UTC date time format</span></span>                                       | <span data-ttu-id="06605-142">Datumet då hänvisningen skapades.</span><span class="sxs-lookup"><span data-stu-id="06605-142">The date the referral was created.</span></span>                                                                                   |
| <span data-ttu-id="06605-143">UpdatedDateTime</span><span class="sxs-lookup"><span data-stu-id="06605-143">UpdatedDateTime</span></span>     | <span data-ttu-id="06605-144">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="06605-144">string in UTC date time format</span></span>                                       | <span data-ttu-id="06605-145">Datumet då hänvisningen senast uppdaterades.</span><span class="sxs-lookup"><span data-stu-id="06605-145">The date the referral was last updated.</span></span>                                                                              |
| <span data-ttu-id="06605-146">ExpirationDateTime</span><span class="sxs-lookup"><span data-stu-id="06605-146">ExpirationDateTime</span></span>  | <span data-ttu-id="06605-147">sträng i UTC-datum/tid-format</span><span class="sxs-lookup"><span data-stu-id="06605-147">string in UTC date time format</span></span>                                       | <span data-ttu-id="06605-148">Datumet då hänvisningen upphör att gälla.</span><span class="sxs-lookup"><span data-stu-id="06605-148">The date the referral will expire.</span></span>                                                                                   |
| <span data-ttu-id="06605-149">Status</span><span class="sxs-lookup"><span data-stu-id="06605-149">Status</span></span>              | [<span data-ttu-id="06605-150">ReferralStatus</span><span class="sxs-lookup"><span data-stu-id="06605-150">ReferralStatus</span></span>](referral-resources.md#referralstatus)               | <span data-ttu-id="06605-151">En [uppräkning](https://docs.microsoft.com/dotnet/api/system.enum) med värden som anger hänvisnings status.</span><span class="sxs-lookup"><span data-stu-id="06605-151">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.</span></span>          |
| <span data-ttu-id="06605-152">Substatus</span><span class="sxs-lookup"><span data-stu-id="06605-152">Substatus</span></span>           | [<span data-ttu-id="06605-153">ReferralSubstatus</span><span class="sxs-lookup"><span data-stu-id="06605-153">ReferralSubstatus</span></span>](referral-resources.md#referralsubstatus)         | <span data-ttu-id="06605-154">En [Enum](https://docs.microsoft.com/dotnet/api/system.enum) med värden som anger del status för hänvisning.</span><span class="sxs-lookup"><span data-stu-id="06605-154">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral sub status.</span></span>      |
| <span data-ttu-id="06605-155">StatusReason</span><span class="sxs-lookup"><span data-stu-id="06605-155">StatusReason</span></span>        | <span data-ttu-id="06605-156">sträng</span><span class="sxs-lookup"><span data-stu-id="06605-156">string</span></span>                                                               | <span data-ttu-id="06605-157">Ett beskrivande meddelande om status.</span><span class="sxs-lookup"><span data-stu-id="06605-157">A descriptive message about the status.</span></span> <span data-ttu-id="06605-158">Förklara till exempel varför hänvisningen bröts.</span><span class="sxs-lookup"><span data-stu-id="06605-158">For example, explain why the referral was lost.</span></span>                              |
| <span data-ttu-id="06605-159">ReferralType</span><span class="sxs-lookup"><span data-stu-id="06605-159">ReferralType</span></span>        | [<span data-ttu-id="06605-160">ReferralType</span><span class="sxs-lookup"><span data-stu-id="06605-160">ReferralType</span></span>](referral-resources.md#referraltype)                   | <span data-ttu-id="06605-161">Representerar referens typen.</span><span class="sxs-lookup"><span data-stu-id="06605-161">Represents the referral type.</span></span>                                                                                        |
| <span data-ttu-id="06605-162">Kvalificering</span><span class="sxs-lookup"><span data-stu-id="06605-162">Qualification</span></span>       | [<span data-ttu-id="06605-163">ReferralQualification</span><span class="sxs-lookup"><span data-stu-id="06605-163">ReferralQualification</span></span>](referral-resources.md#referralqualification) | <span data-ttu-id="06605-164">Representerar referensens kvalitet.</span><span class="sxs-lookup"><span data-stu-id="06605-164">Represents the quality of the referral.</span></span>                                                                              |
| <span data-ttu-id="06605-165">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="06605-165">CustomerProfile</span></span>     | [<span data-ttu-id="06605-166">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="06605-166">CustomerProfile</span></span>](referral-resources.md#customerprofile)             | <span data-ttu-id="06605-167">Kundens kontakt uppgifter.</span><span class="sxs-lookup"><span data-stu-id="06605-167">Customer contact information.</span></span>                                                                                        |
| <span data-ttu-id="06605-168">Samtycke</span><span class="sxs-lookup"><span data-stu-id="06605-168">Consent</span></span>             | [<span data-ttu-id="06605-169">Samtycke</span><span class="sxs-lookup"><span data-stu-id="06605-169">Consent</span></span>](referral-resources.md#consent)                             | <span data-ttu-id="06605-170">Medgivande flaggor runt delning av information med andra organisationer och gör det möjligt för dem att kontakta användare.</span><span class="sxs-lookup"><span data-stu-id="06605-170">Consent flags around sharing information with other organizations and allowing them to contact users.</span></span>                |
| <span data-ttu-id="06605-171">Information</span><span class="sxs-lookup"><span data-stu-id="06605-171">Details</span></span>             | [<span data-ttu-id="06605-172">ReferralDetails</span><span class="sxs-lookup"><span data-stu-id="06605-172">ReferralDetails</span></span>](referral-resources.md#referraldetails)             | <span data-ttu-id="06605-173">Kund information, noteringar, avtals värde, valuta stängnings datum.</span><span class="sxs-lookup"><span data-stu-id="06605-173">Customer details, notes, deal value, currency closing date.</span></span>                                                          |
| <span data-ttu-id="06605-174">Team</span><span class="sxs-lookup"><span data-stu-id="06605-174">Team</span></span>                | [<span data-ttu-id="06605-175">Medlem</span><span class="sxs-lookup"><span data-stu-id="06605-175">Member</span></span>](referral-resources.md#member)                               | <span data-ttu-id="06605-176">Representerar användare i organisationer som ingår i partner engagemang.</span><span class="sxs-lookup"><span data-stu-id="06605-176">Represents users in the organizations that are involved in the partner engagement.</span></span>                                   |
| <span data-ttu-id="06605-177">InviteContext</span><span class="sxs-lookup"><span data-stu-id="06605-177">InviteContext</span></span>       | [<span data-ttu-id="06605-178">InviteContext</span><span class="sxs-lookup"><span data-stu-id="06605-178">InviteContext</span></span>](referral-resources.md#invitecontext)                 | <span data-ttu-id="06605-179">Representerar ytterligare information som en användare kan tillhandahålla när de bjuder in en annan organisation till partner engagemang.</span><span class="sxs-lookup"><span data-stu-id="06605-179">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span> |
| <span data-ttu-id="06605-180">Mål</span><span class="sxs-lookup"><span data-stu-id="06605-180">Target</span></span>         | [<span data-ttu-id="06605-181">ReferralTarget</span><span class="sxs-lookup"><span data-stu-id="06605-181">ReferralTarget</span></span>](referral-resources.md#target)        | <span data-ttu-id="06605-182">Representerar ytterligare information som en användare kan tillhandahålla när de bjuder in en annan organisation till partner engagemang.</span><span class="sxs-lookup"><span data-stu-id="06605-182">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span>  |

### <a name="status-and-substatus-transition-states"></a><span data-ttu-id="06605-183">Status och under status över gångs tillstånd</span><span class="sxs-lookup"><span data-stu-id="06605-183">Status and substatus transition states</span></span>

| <span data-ttu-id="06605-184">Status</span><span class="sxs-lookup"><span data-stu-id="06605-184">Status</span></span> | <span data-ttu-id="06605-185">Tillåten status över gång</span><span class="sxs-lookup"><span data-stu-id="06605-185">Allowed Status Transition</span></span> | <span data-ttu-id="06605-186">Tillåten under status</span><span class="sxs-lookup"><span data-stu-id="06605-186">Allowed Substatus</span></span>            |
|--------|---------------------------|------------------------------|
| <span data-ttu-id="06605-187">Ny</span><span class="sxs-lookup"><span data-stu-id="06605-187">New</span></span>    | <span data-ttu-id="06605-188">Nytt, aktivt, stängt</span><span class="sxs-lookup"><span data-stu-id="06605-188">New, Active, Closed</span></span>       | <span data-ttu-id="06605-189">Väntar, mottaget</span><span class="sxs-lookup"><span data-stu-id="06605-189">Pending, Received</span></span>            |
| <span data-ttu-id="06605-190">Aktiv</span><span class="sxs-lookup"><span data-stu-id="06605-190">Active</span></span> | <span data-ttu-id="06605-191">Aktiv, stängd</span><span class="sxs-lookup"><span data-stu-id="06605-191">Active, Closed</span></span>            | <span data-ttu-id="06605-192">Har godkänts</span><span class="sxs-lookup"><span data-stu-id="06605-192">Accepted</span></span>                     |
| <span data-ttu-id="06605-193">Stängd</span><span class="sxs-lookup"><span data-stu-id="06605-193">Closed</span></span> | <span data-ttu-id="06605-194">Stängd</span><span class="sxs-lookup"><span data-stu-id="06605-194">Closed</span></span>                    | <span data-ttu-id="06605-195">Vann, förlorad, avböjd, upphör att gälla</span><span class="sxs-lookup"><span data-stu-id="06605-195">Won, Lost, Declined, Expired</span></span> |

### <a name="request-example"></a><span data-ttu-id="06605-196">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="06605-196">Request example</span></span>

```http
PUT https://api.partner.microsoft.com/v1.0/engagements/referrals/49d90c72-3326-4f61-aacc-2cb57970448c HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "id": "49d90c72-3326-4f61-aacc-2cb57970448c",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:40:42.6178337Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "closingDateTime": "2018-11-14T00:00:00Z",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",

}
```

> [!IMPORTANT]
> <span data-ttu-id="06605-197">Ta bort `"links": { }` objektet från placerings resursen.</span><span class="sxs-lookup"><span data-stu-id="06605-197">Remove the `"links": { }` object from the PUT resource.</span></span>

## <a name="rest-response"></a><span data-ttu-id="06605-198">REST-svar</span><span class="sxs-lookup"><span data-stu-id="06605-198">REST Response</span></span>

<span data-ttu-id="06605-199">Om det lyckas returnerar den här metoden den ifyllda [hänvisnings](referral-resources.md) resursen i svars texten.</span><span class="sxs-lookup"><span data-stu-id="06605-199">If successful, this method returns the populated [referral](referral-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="06605-200">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="06605-200">Response success and error codes</span></span>

<span data-ttu-id="06605-201">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="06605-201">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="06605-202">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="06605-202">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="06605-203">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="06605-203">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="06605-204">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="06605-204">Response example</span></span>

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:43:38.9948636Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",
    "links": {
        "relatedReferrals": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals?$filter=engagementId eq '37ef26aa-1d15-4533-9f93-a69bd33ab1e5'",
            "method": "GET"
        },
        "self": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals/4111fffc-f9ee-4d53-bba6-569135228642",
            "method": "GET"
        }
    }
}
```