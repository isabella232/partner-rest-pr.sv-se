---
title: Skapa en hänvisning
description: 'Skapa oberoende eller delade referenser i partner-API: et.'
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6aab4b5f45030c3c16294b2929b1a6d3086fb951
ms.sourcegitcommit: 3c165938f544ff226cbe11ca21ed5aa00448d9b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "97770611"
---
# <a name="create-a-referral"></a><span data-ttu-id="d2655-103">Skapa en hänvisning</span><span class="sxs-lookup"><span data-stu-id="d2655-103">Create a referral</span></span>

<span data-ttu-id="d2655-104">Gäller för:</span><span class="sxs-lookup"><span data-stu-id="d2655-104">Applies to:</span></span>

- <span data-ttu-id="d2655-105">Partner-API</span><span class="sxs-lookup"><span data-stu-id="d2655-105">Partner API</span></span>

<span data-ttu-id="d2655-106">I det här avsnittet beskrivs hur du skapar en hänvisning.</span><span class="sxs-lookup"><span data-stu-id="d2655-106">This topic explains how to create a referral.</span></span> <span data-ttu-id="d2655-107">Det finns två typer av [ReferralType](referral-resources.md#referraltype):</span><span class="sxs-lookup"><span data-stu-id="d2655-107">There are two types of [ReferralType](referral-resources.md#referraltype):</span></span>

1. <span data-ttu-id="d2655-108">Oberoende: där en hänvisning är synlig för en partner.</span><span class="sxs-lookup"><span data-stu-id="d2655-108">Independent: Where a referral is visible to one partner.</span></span>
2. <span data-ttu-id="d2655-109">Delad: där en hänvisning är synlig för två parter som arbetar tillsammans.</span><span class="sxs-lookup"><span data-stu-id="d2655-109">Shared: Where a referral is visible to two parties that are working together.</span></span> <span data-ttu-id="d2655-110">Om exempelvis Microsoft och en partner arbetar tillsammans i ett samordnat avtal, kan en hänvisning delas mellan båda parter.</span><span class="sxs-lookup"><span data-stu-id="d2655-110">For example, if Microsoft and a partner are working together in a co-selling deal, a referral can be shared between both parties.</span></span> <span data-ttu-id="d2655-111">Mer information finns i avsnittet [skapa en delad hänvisning](#create-a-shared-referral).</span><span class="sxs-lookup"><span data-stu-id="d2655-111">For more information, see the section [Creating a shared referral](#create-a-shared-referral).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2655-112">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="d2655-112">Prerequisites</span></span>

- <span data-ttu-id="d2655-113">Autentiseringsuppgifter enligt beskrivningen i [partner-API-autentisering](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d2655-113">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="d2655-114">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="d2655-114">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="d2655-115">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="d2655-115">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d2655-116">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="d2655-116">Request syntax</span></span>

| <span data-ttu-id="d2655-117">Metod</span><span class="sxs-lookup"><span data-stu-id="d2655-117">Method</span></span>  | <span data-ttu-id="d2655-118">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="d2655-118">Request URI</span></span>                                                  |
|---------|--------------------------------------------------------------|
| <span data-ttu-id="d2655-119">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="d2655-119">**POST**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

### <a name="request-headers"></a><span data-ttu-id="d2655-120">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="d2655-120">Request headers</span></span>

- <span data-ttu-id="d2655-121">Mer information finns i [partner API rest-huvuden](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="d2655-121">See [Partner API REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="d2655-122">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="d2655-122">Request body</span></span>

<span data-ttu-id="d2655-123">Den här tabellen beskriver [hänvisnings](referral-resources.md) egenskaperna i begär ande texten för en varumärkes ny hänvisning.</span><span class="sxs-lookup"><span data-stu-id="d2655-123">This table describes the [Referral](referral-resources.md) properties in the request body for a brand new referral.</span></span>

| <span data-ttu-id="d2655-124">Egenskap</span><span class="sxs-lookup"><span data-stu-id="d2655-124">Property</span></span>            | <span data-ttu-id="d2655-125">Typ</span><span class="sxs-lookup"><span data-stu-id="d2655-125">Type</span></span>                                                                 | <span data-ttu-id="d2655-126">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="d2655-126">Description</span></span>                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d2655-127">Name</span><span class="sxs-lookup"><span data-stu-id="d2655-127">Name</span></span>                | <span data-ttu-id="d2655-128">sträng</span><span class="sxs-lookup"><span data-stu-id="d2655-128">string</span></span>                                                               | <span data-ttu-id="d2655-129">Namnet på referensen.</span><span class="sxs-lookup"><span data-stu-id="d2655-129">The name of the Referral.</span></span>                                                                                            |
| <span data-ttu-id="d2655-130">ExternalReferenceId</span><span class="sxs-lookup"><span data-stu-id="d2655-130">ExternalReferenceId</span></span> | <span data-ttu-id="d2655-131">sträng</span><span class="sxs-lookup"><span data-stu-id="d2655-131">string</span></span>                                                               | <span data-ttu-id="d2655-132">En extern identifierare för referensen.</span><span class="sxs-lookup"><span data-stu-id="d2655-132">An external identifier for the referral.</span></span> <span data-ttu-id="d2655-133">Till exempel ditt eget Dynamics 365-lead eller affärs möjlighets-ID.</span><span class="sxs-lookup"><span data-stu-id="d2655-133">For example, your own Dynamics 365 lead or opportunity ID.</span></span>                   |
| <span data-ttu-id="d2655-134">Status</span><span class="sxs-lookup"><span data-stu-id="d2655-134">Status</span></span>              | [<span data-ttu-id="d2655-135">ReferralStatus</span><span class="sxs-lookup"><span data-stu-id="d2655-135">ReferralStatus</span></span>](referral-resources.md#referralstatus)               | <span data-ttu-id="d2655-136">En [uppräkning](https://docs.microsoft.com/dotnet/api/system.enum) med värden som anger hänvisnings status.</span><span class="sxs-lookup"><span data-stu-id="d2655-136">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.</span></span>          |
| <span data-ttu-id="d2655-137">Substatus</span><span class="sxs-lookup"><span data-stu-id="d2655-137">Substatus</span></span>           | [<span data-ttu-id="d2655-138">ReferralSubstatus</span><span class="sxs-lookup"><span data-stu-id="d2655-138">ReferralSubstatus</span></span>](referral-resources.md#referralsubstatus)         | <span data-ttu-id="d2655-139">En [Enum](https://docs.microsoft.com/dotnet/api/system.enum) med värden som anger hänvisningens under status.</span><span class="sxs-lookup"><span data-stu-id="d2655-139">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral substatus.</span></span>       |
| <span data-ttu-id="d2655-140">StatusReason</span><span class="sxs-lookup"><span data-stu-id="d2655-140">StatusReason</span></span>        | <span data-ttu-id="d2655-141">sträng</span><span class="sxs-lookup"><span data-stu-id="d2655-141">string</span></span>                                                               | <span data-ttu-id="d2655-142">Ett beskrivande meddelande om status.</span><span class="sxs-lookup"><span data-stu-id="d2655-142">A descriptive message about the status.</span></span> <span data-ttu-id="d2655-143">Förklara till exempel varför hänvisningen bröts.</span><span class="sxs-lookup"><span data-stu-id="d2655-143">For example, explain why the referral was lost.</span></span>                            |
| <span data-ttu-id="d2655-144">ReferralType</span><span class="sxs-lookup"><span data-stu-id="d2655-144">ReferralType</span></span>        | [<span data-ttu-id="d2655-145">ReferralType</span><span class="sxs-lookup"><span data-stu-id="d2655-145">ReferralType</span></span>](referral-resources.md#referraltype)                   | <span data-ttu-id="d2655-146">Representerar referens typen.</span><span class="sxs-lookup"><span data-stu-id="d2655-146">Represents the referral type.</span></span> <span data-ttu-id="d2655-147">**Kunna.**</span><span class="sxs-lookup"><span data-stu-id="d2655-147">**Required.**</span></span>                                                                                        |
| <span data-ttu-id="d2655-148">Kvalificering</span><span class="sxs-lookup"><span data-stu-id="d2655-148">Qualification</span></span>       | [<span data-ttu-id="d2655-149">ReferralQualification</span><span class="sxs-lookup"><span data-stu-id="d2655-149">ReferralQualification</span></span>](referral-resources.md#referralqualification) | <span data-ttu-id="d2655-150">Representerar referensens kvalitet.</span><span class="sxs-lookup"><span data-stu-id="d2655-150">Represents the quality of the referral.</span></span>                                                                              |
| <span data-ttu-id="d2655-151">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="d2655-151">CustomerProfile</span></span>     | [<span data-ttu-id="d2655-152">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="d2655-152">CustomerProfile</span></span>](referral-resources.md#customerprofile)             | <span data-ttu-id="d2655-153">Kundens kontakt uppgifter.</span><span class="sxs-lookup"><span data-stu-id="d2655-153">Customer contact information.</span></span>  <span data-ttu-id="d2655-154">**Kunna.**</span><span class="sxs-lookup"><span data-stu-id="d2655-154">**Required.**</span></span>                                                                                      |
| <span data-ttu-id="d2655-155">Samtycke</span><span class="sxs-lookup"><span data-stu-id="d2655-155">Consent</span></span>             | [<span data-ttu-id="d2655-156">Samtycke</span><span class="sxs-lookup"><span data-stu-id="d2655-156">Consent</span></span>](referral-resources.md#consent)                             | <span data-ttu-id="d2655-157">Medgivande flaggor runt delning av information med andra organisationer och gör det möjligt för dem att kontakta användare. **Obligatoriskt.**</span><span class="sxs-lookup"><span data-stu-id="d2655-157">Consent flags around sharing information with other organizations and allowing them to contact users.**Required.**</span></span>               |
| <span data-ttu-id="d2655-158">Information</span><span class="sxs-lookup"><span data-stu-id="d2655-158">Details</span></span>             | [<span data-ttu-id="d2655-159">ReferralDetails</span><span class="sxs-lookup"><span data-stu-id="d2655-159">ReferralDetails</span></span>](referral-resources.md#referraldetails)             | <span data-ttu-id="d2655-160">Kund information, noteringar, avtals värde, valuta stängnings datum.</span><span class="sxs-lookup"><span data-stu-id="d2655-160">Customer details, notes, deal value, currency closing date.</span></span> <span data-ttu-id="d2655-161">**Kunna.**</span><span class="sxs-lookup"><span data-stu-id="d2655-161">**Required.**</span></span>                                                           |
| <span data-ttu-id="d2655-162">Team</span><span class="sxs-lookup"><span data-stu-id="d2655-162">Team</span></span>                | [<span data-ttu-id="d2655-163">Medlem</span><span class="sxs-lookup"><span data-stu-id="d2655-163">Member</span></span>](referral-resources.md#member)                               | <span data-ttu-id="d2655-164">Representerar användare i organisationer som ingår i partner engagemang.</span><span class="sxs-lookup"><span data-stu-id="d2655-164">Represents users in the organizations that are involved in the partner engagement.</span></span>                                   |
| <span data-ttu-id="d2655-165">InviteContext</span><span class="sxs-lookup"><span data-stu-id="d2655-165">InviteContext</span></span>       | [<span data-ttu-id="d2655-166">InviteContext</span><span class="sxs-lookup"><span data-stu-id="d2655-166">InviteContext</span></span>](referral-resources.md#invitecontext)                 | <span data-ttu-id="d2655-167">Representerar ytterligare information som en användare kan tillhandahålla när de bjuder in en annan organisation till partner engagemang.</span><span class="sxs-lookup"><span data-stu-id="d2655-167">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span> |
| <span data-ttu-id="d2655-168">Mål</span><span class="sxs-lookup"><span data-stu-id="d2655-168">Target</span></span>         | [<span data-ttu-id="d2655-169">ReferralTarget</span><span class="sxs-lookup"><span data-stu-id="d2655-169">ReferralTarget</span></span>](referral-resources.md#target)        | <span data-ttu-id="d2655-170">Representerar ytterligare information som en användare kan tillhandahålla när de bjuder in en annan organisation till partner engagemang.</span><span class="sxs-lookup"><span data-stu-id="d2655-170">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span>  |

#### <a name="status--substatus-transition-states"></a><span data-ttu-id="d2655-171">Status & över gångs status för under status</span><span class="sxs-lookup"><span data-stu-id="d2655-171">Status & Substatus transition states</span></span>

| <span data-ttu-id="d2655-172">Status</span><span class="sxs-lookup"><span data-stu-id="d2655-172">Status</span></span> | <span data-ttu-id="d2655-173">Tillåten status över gång</span><span class="sxs-lookup"><span data-stu-id="d2655-173">Allowed status transition</span></span> | <span data-ttu-id="d2655-174">Tillåten under status</span><span class="sxs-lookup"><span data-stu-id="d2655-174">Allowed substatus</span></span>            |
|--------|---------------------------|------------------------------|
| <span data-ttu-id="d2655-175">Ny</span><span class="sxs-lookup"><span data-stu-id="d2655-175">New</span></span>    | <span data-ttu-id="d2655-176">Nytt, aktivt, stängt</span><span class="sxs-lookup"><span data-stu-id="d2655-176">New, Active, Closed</span></span>       | <span data-ttu-id="d2655-177">Väntar, mottaget</span><span class="sxs-lookup"><span data-stu-id="d2655-177">Pending, Received</span></span>            |
| <span data-ttu-id="d2655-178">Aktiv</span><span class="sxs-lookup"><span data-stu-id="d2655-178">Active</span></span> | <span data-ttu-id="d2655-179">Aktiv, stängd</span><span class="sxs-lookup"><span data-stu-id="d2655-179">Active, Closed</span></span>            | <span data-ttu-id="d2655-180">Har godkänts</span><span class="sxs-lookup"><span data-stu-id="d2655-180">Accepted</span></span>                     |
| <span data-ttu-id="d2655-181">Stängd</span><span class="sxs-lookup"><span data-stu-id="d2655-181">Closed</span></span> | <span data-ttu-id="d2655-182">Stängd</span><span class="sxs-lookup"><span data-stu-id="d2655-182">Closed</span></span>                    | <span data-ttu-id="d2655-183">Vann, förlorad, avböjd, upphör att gälla</span><span class="sxs-lookup"><span data-stu-id="d2655-183">Won, Lost, Declined, Expired</span></span> |

### <a name="request-example"></a><span data-ttu-id="d2655-184">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="d2655-184">Request example</span></span>

```http
POST https://api.partner.microsoft.com/v1.0/engagements/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "name": "Test Cosell Invite_20",
    "status": "New",
    "substatus": "Pending",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
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
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="d2655-185">REST-svar</span><span class="sxs-lookup"><span data-stu-id="d2655-185">REST Response</span></span>

<span data-ttu-id="d2655-186">Om det lyckas returnerar den här metoden den ifyllda [hänvisnings](referral-resources.md) resursen i svars texten.</span><span class="sxs-lookup"><span data-stu-id="d2655-186">If successful, this method returns the populated [Referral](referral-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d2655-187">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="d2655-187">Response success and error codes</span></span>

<span data-ttu-id="d2655-188">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="d2655-188">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d2655-189">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="d2655-189">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d2655-190">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d2655-190">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d2655-191">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="d2655-191">Response example</span></span>

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "name": "Test Cosell Invite_20",
    "externalReferenceId": null,
    "createdDateTime": "2019-02-23T02:05:23.2931817Z",
    "updatedDateTime": "2019-02-23T02:05:23.2931817Z",
    "expirationDateTime": null,
    "status": "Active",
    "substatus": "Accepted",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "eTag": "\"00006d10-0000-0000-0000-5c70aa630000\"",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
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

## <a name="create-a-shared-referral"></a><span data-ttu-id="d2655-192">Skapa en delad hänvisning</span><span class="sxs-lookup"><span data-stu-id="d2655-192">Create a shared referral</span></span>

<span data-ttu-id="d2655-193">Det finns två steg för att skapa en hänvisning till den **delade** [hänvisnings typen](referral-resources.md#referraltype).</span><span class="sxs-lookup"><span data-stu-id="d2655-193">There are two steps to create a referral of the **Shared** [referral type](referral-resources.md#referraltype).</span></span>

1. [<span data-ttu-id="d2655-194">Skapa din delade hänvisning</span><span class="sxs-lookup"><span data-stu-id="d2655-194">Create your shared referral</span></span>](#create-your-referral)
2. [<span data-ttu-id="d2655-195">Skapa en ansluten hänvisning för den andra parten</span><span class="sxs-lookup"><span data-stu-id="d2655-195">Create a connected referral for the second party</span></span>](#create-a-connected-referral)

<span data-ttu-id="d2655-196">Följande flödes diagram illustrerar de här två stegen i skapa en delad referens.</span><span class="sxs-lookup"><span data-stu-id="d2655-196">The following flow chart illustrates these two steps in creating a shared referral.</span></span>

![Flödes diagram som visar en delad hänvisning med 2 hänvisningar som är anslutna via Microsoft partner-API: et](../images/SharedReferral.png)

### <a name="create-your-referral"></a><span data-ttu-id="d2655-198">Skapa din hänvisning</span><span class="sxs-lookup"><span data-stu-id="d2655-198">Create your referral</span></span>

1. <span data-ttu-id="d2655-199">Skapa en hänvisning med [ReferralType](referral-resources.md#referraltype) inställt på delad.</span><span class="sxs-lookup"><span data-stu-id="d2655-199">Create a referral with [ReferralType](referral-resources.md#referraltype) set to shared.</span></span>
2. <span data-ttu-id="d2655-200">Kopiera **engagementId** från retur svaret.</span><span class="sxs-lookup"><span data-stu-id="d2655-200">Copy the **engagementId** from the return response.</span></span>

<span data-ttu-id="d2655-201">[ReferralTarget](referral-resources.md#target) -exempel för hänvisning</span><span class="sxs-lookup"><span data-stu-id="d2655-201">[ReferralTarget](referral-resources.md#target) sample for referral</span></span>

```json
"target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-ABC-DEF"
        }
    ]
```

### <a name="create-a-connected-referral"></a><span data-ttu-id="d2655-202">Skapa en ansluten hänvisning</span><span class="sxs-lookup"><span data-stu-id="d2655-202">Create a connected referral</span></span>

1. <span data-ttu-id="d2655-203">Skapa en annan hänvisning för Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d2655-203">Create another referral for Microsoft.</span></span>
2. <span data-ttu-id="d2655-204">Inkludera **enagementId** från din hänvisning så att de är kopplade till varandra.</span><span class="sxs-lookup"><span data-stu-id="d2655-204">Include the **enagementId** from your referral so they are tied together.</span></span>

<span data-ttu-id="d2655-205">[ReferralTarget](referral-resources.md#target) -exempel för Microsoft referral</span><span class="sxs-lookup"><span data-stu-id="d2655-205">[ReferralTarget](referral-resources.md#target) sample for Microsoft referral</span></span>

```json
"target": [
        {
            "type": "BusinessProfileLocation",
            "id": "msft"
        }
    ]
```