---
title: Hantera leads-och samförsäljnings möjligheter via programmering i Partner Center
description: 'I det här avsnittet beskrivs hur partner kan använda partner-API: er för att hantera leads och samförsäljnings möjligheter via programmering.'
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0da725c9b2459a6c5631b7cc7e21b46e9a7191b8
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770639"
---
# <a name="programmatically-manage-leads-and-co-sell-opportunities-in-partner-center"></a><span data-ttu-id="38788-103">Hantera leads-och samförsäljnings möjligheter via programmering i Partner Center</span><span class="sxs-lookup"><span data-stu-id="38788-103">Programmatically manage leads and co-sell opportunities in Partner Center</span></span>

<span data-ttu-id="38788-104">Den här artikeln hjälper dig att förstå hur du program mässigt hanterar de leads som du får från sidan Microsoft Solution Provider och samförsäljnings möjligheter som du får från Microsoft-säljare eller andra partner.</span><span class="sxs-lookup"><span data-stu-id="38788-104">This article will help you understand how you can programmatically manage the leads that you receive from Microsoft solution provider page and the co-sell opportunities that you receive from Microsoft sales representative or other partners.</span></span> <span data-ttu-id="38788-105">Du kan också använda dessa API: er för att program mässigt dela ditt företags försäljnings förlopp eller bjuda in Microsoft-säljare för att samar beta med potentiella affärs möjligheter.</span><span class="sxs-lookup"><span data-stu-id="38788-105">You can also use these api's to programmatically share your company's sales pipeline or invite Microsoft sales representatives to collaborate on potential opportunities.</span></span> 

## <a name="manage-leads-and-opportunities"></a><span data-ttu-id="38788-106">Hantera leads och affärs möjligheter</span><span class="sxs-lookup"><span data-stu-id="38788-106">Manage leads and opportunities</span></span>

- <span data-ttu-id="38788-107">[Hämta listan över leads och affärs möjligheter](get-a-list-of-referrals.md) – hämtar listan över leads från Microsoft Solution Provider-sidan och samförsäljnings möjligheter från Microsoft-säljare eller andra partner.</span><span class="sxs-lookup"><span data-stu-id="38788-107">[Get the list of leads and opportunities](get-a-list-of-referrals.md) - Gets the list of leads from Microsoft solution provider page and co-sell opportunities from Microsoft sellers or other partners.</span></span> <span data-ttu-id="38788-108">Detta innehåller även en lista med affärs möjligheter som har skapats av din organisation.</span><span class="sxs-lookup"><span data-stu-id="38788-108">This will also contain the list of opportunities created by your organization.</span></span>
- <span data-ttu-id="38788-109">[Hämta ett lead eller en affärs möjlighet efter ID](get-a-referral-by-Id.md) – hämtar ett lead eller en affärs möjlighet efter ID.</span><span class="sxs-lookup"><span data-stu-id="38788-109">[Get a lead or opportunity by Id](get-a-referral-by-Id.md) - Gets a lead or opportunity by Id.</span></span>
- <span data-ttu-id="38788-110">[Uppdatera ett lead eller en affärs möjlighet](patch-a-referral.md) – gör att du kan uppdatera lead-eller affärs möjlighets information som avtals värde, uppskattat stängnings datum eller hantera försäljnings stegen med annan information.</span><span class="sxs-lookup"><span data-stu-id="38788-110">[Update a lead or opportunity](patch-a-referral.md) - Allows you to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.</span></span>
- <span data-ttu-id="38788-111">[Skapa en ny affärs möjlighet](create-a-referral.md) – gör att du kan skapa en ny affärs möjlighet eller privat kund avtal.</span><span class="sxs-lookup"><span data-stu-id="38788-111">[Create a new opportunity](create-a-referral.md) - Enables you to create a new co-sell opportunity or private deal.</span></span>
- [<span data-ttu-id="38788-112">Hänvisningsresurser</span><span class="sxs-lookup"><span data-stu-id="38788-112">Referral resources</span></span>](referral-resources.md)

> [!Note]
> <span data-ttu-id="38788-113">Leads som tas emot från Microsofts kommersiella marknads plats (Azure Marketplace och AppSource) kan inte hanteras med API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="38788-113">Leads received from the Microsoft commercial marketplace (Azure Marketplace and AppSource) cannot be managed using Partner Center api's.</span></span>