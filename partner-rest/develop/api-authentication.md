---
title: Autentisering för partner-API
description: Konfigurera dina autentiseringsinställningar så att de använder partner-API med Azure AD för autentisering.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: c5810678dccc2be1c3c084c901299961d6ba7820
ms.sourcegitcommit: 3c165938f544ff226cbe11ca21ed5aa00448d9b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "97770616"
---
# <a name="partner-api-authentication"></a><span data-ttu-id="96b96-103">Autentisering för partner-API</span><span class="sxs-lookup"><span data-stu-id="96b96-103">Partner API authentication</span></span>

<span data-ttu-id="96b96-104">Gäller för:</span><span class="sxs-lookup"><span data-stu-id="96b96-104">Applies to:</span></span>

- <span data-ttu-id="96b96-105">Partner-API</span><span class="sxs-lookup"><span data-stu-id="96b96-105">Partner API</span></span>

<span data-ttu-id="96b96-106">Partner-API: et använder Azure Active Directory (Azure AD) för autentisering.</span><span class="sxs-lookup"><span data-stu-id="96b96-106">The Partner API utilizes Azure Active Directory (Azure AD) for authentication.</span></span> <span data-ttu-id="96b96-107">När du interagerar med partner-API: et måste du konfigurera ett Azure AD-program på rätt sätt och få en åtkomsttoken.</span><span class="sxs-lookup"><span data-stu-id="96b96-107">When you interact with the Partner API, you must correctly configure an Azure AD application and obtain an access token.</span></span> <span data-ttu-id="96b96-108">Du kan få åtkomst-token för [program-och användar åtkomst](#application-and-user-access) eller [endast program åtkomst](#application-only-access).</span><span class="sxs-lookup"><span data-stu-id="96b96-108">You can obtain access tokens for [application and user access](#application-and-user-access) or [application-only access](#application-only-access).</span></span>

## <a name="application-and-user-access"></a><span data-ttu-id="96b96-109">Åtkomst till program och användare</span><span class="sxs-lookup"><span data-stu-id="96b96-109">Application and user access</span></span>

<span data-ttu-id="96b96-110">Den här metoden rekommenderas för att ställa in **program-och användar åtkomst** till API: et.</span><span class="sxs-lookup"><span data-stu-id="96b96-110">This method is recommended to set up **application and user access** to the API.</span></span>

1. <span data-ttu-id="96b96-111">Logga in på [Azure-portalen](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="96b96-111">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="96b96-112">Välj tjänsten **Azure Active Directory** .</span><span class="sxs-lookup"><span data-stu-id="96b96-112">Choose the **Azure Active Directory** service.</span></span>
3. <span data-ttu-id="96b96-113">Välj **Appregistreringar** och välj sedan **ny program registrering**.</span><span class="sxs-lookup"><span data-stu-id="96b96-113">Choose **App registrations**, then choose **New application registration**.</span></span>
4. <span data-ttu-id="96b96-114">Skapa ditt nya program.</span><span class="sxs-lookup"><span data-stu-id="96b96-114">Create your new application.</span></span> <span data-ttu-id="96b96-115">För **program typ** väljer du **intern**.</span><span class="sxs-lookup"><span data-stu-id="96b96-115">For **Application type**, select **Native**.</span></span> <span data-ttu-id="96b96-116">Ange ett namn och en URL och välj sedan **skapa**.</span><span class="sxs-lookup"><span data-stu-id="96b96-116">Provide a name and URL, then select **Create**.</span></span>
5. <span data-ttu-id="96b96-117">Välj **API-behörigheter** för programmet.</span><span class="sxs-lookup"><span data-stu-id="96b96-117">Choose **API permissions** for the application.</span></span> <span data-ttu-id="96b96-118">På skärmen **begär API-behörigheter** väljer du **Lägg till en behörighet** och väljer sedan de **API: er som min organisation använder**</span><span class="sxs-lookup"><span data-stu-id="96b96-118">On the **Request API permissions** screen, choose **Add a permission**, then choose **APIs my organization uses**</span></span>
6. <span data-ttu-id="96b96-119">Sök efter *Microsoft partner* (*Microsoft dev Center*) API ( `4990cffe-04e8-4e8b-808a-1175604b879f` ).</span><span class="sxs-lookup"><span data-stu-id="96b96-119">Search for the *Microsoft Partner* (*Microsoft Dev Center*) API (`4990cffe-04e8-4e8b-808a-1175604b879f`).</span></span>

    ![Skärm bild av skärmen begär API-behörigheter med en sökning efter Microsoft partner-API: et](../images/SearchGatewayApi.png)

7. <span data-ttu-id="96b96-121">Ange **delegerade behörigheter** till **partner Center**.</span><span class="sxs-lookup"><span data-stu-id="96b96-121">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Skärm bild av skärmen delegerade behörigheter för konfiguration av Microsoft partner-API](../images/SelectUserPermission.png)
    
8. <span data-ttu-id="96b96-123">Sök efter *Microsoft partner* (*Microsoft Partner Center*) API ( `fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd` ).</span><span class="sxs-lookup"><span data-stu-id="96b96-123">Search for the *Microsoft Partner* (*Microsoft Partner Center*) API (`fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd`).</span></span>

    ![Skärm bild av skärmen begär API-behörigheter med en sökning för Microsoft Partner Center API](../images/SearchPCApi.png)
    
9. <span data-ttu-id="96b96-125">Välj **Microsoft Partner Center** och markera **user_impersonation**.</span><span class="sxs-lookup"><span data-stu-id="96b96-125">Select **Microsoft Partner Center** and check **user_impersonation**.</span></span>

10. <span data-ttu-id="96b96-126">Ange **delegerade behörigheter** till **partner Center**.</span><span class="sxs-lookup"><span data-stu-id="96b96-126">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Skärm bild av skärmen delegerade behörigheter för konfiguration av Microsoft Partner Center API](../images/SelectPCUserPermission.png)

## <a name="application-only-access"></a><span data-ttu-id="96b96-128">Endast program åtkomst</span><span class="sxs-lookup"><span data-stu-id="96b96-128">Application-only access</span></span>

<span data-ttu-id="96b96-129">Den här metoden rekommenderas för konfiguration av **program åtkomst** till API: erna.</span><span class="sxs-lookup"><span data-stu-id="96b96-129">This method is recommended for **application-only access** setup to the APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96b96-130">Du måste ange program-ID, program nyckel och katalog-ID från ditt Azure AD-program.</span><span class="sxs-lookup"><span data-stu-id="96b96-130">You must provide the application ID, application key, and directory ID from your Azure AD application.</span></span>

1. <span data-ttu-id="96b96-131">Logga in på [Azure-portalen](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="96b96-131">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="96b96-132">Välj tjänsten **Azure Active Directory** .</span><span class="sxs-lookup"><span data-stu-id="96b96-132">Select the **Azure Active Directory** service.</span></span>
3. <span data-ttu-id="96b96-133">Välj **Appregistreringar** och välj sedan **ny program registrering**.</span><span class="sxs-lookup"><span data-stu-id="96b96-133">Choose **App registrations**, then select **New application registration**.</span></span>
4. <span data-ttu-id="96b96-134">Skapa ditt nya program.</span><span class="sxs-lookup"><span data-stu-id="96b96-134">Create your new application.</span></span> <span data-ttu-id="96b96-135">För **program typ** väljer du **webbapp/API**.</span><span class="sxs-lookup"><span data-stu-id="96b96-135">For **Application type**, choose **Web app/API**.</span></span> <span data-ttu-id="96b96-136">Ange ett program **namn** och en **URL**.</span><span class="sxs-lookup"><span data-stu-id="96b96-136">Enter a an application **name** and **URL**.</span></span> <span data-ttu-id="96b96-137">Välj sedan **Skapa**.</span><span class="sxs-lookup"><span data-stu-id="96b96-137">Then choose **Create**.</span></span>
5. <span data-ttu-id="96b96-138">Välj **API-behörigheter** för programmet.</span><span class="sxs-lookup"><span data-stu-id="96b96-138">Choose **API permissions** for the application.</span></span> <span data-ttu-id="96b96-139">Välj **Lägg till en behörighet** och välj sedan de **API: er som används i organisationen**</span><span class="sxs-lookup"><span data-stu-id="96b96-139">Choose **Add a permission**, then choose **APIs my organization uses**</span></span>
6. <span data-ttu-id="96b96-140">Sök efter *Microsoft partner* (*Microsoft dev Center*) API ( `4990cffe-04e8-4e8b-808a-1175604b879f` ).</span><span class="sxs-lookup"><span data-stu-id="96b96-140">Search for the *Microsoft Partner* (*Microsoft Dev Center*) API (`4990cffe-04e8-4e8b-808a-1175604b879f`).</span></span>

    ![Skärm bild av skärmen begär API-behörigheter med en sökning efter Microsoft partner-API: et](../images/SearchGatewayApi.png)

7. <span data-ttu-id="96b96-142">Ange **delegerade behörigheter** till **partner Center**.</span><span class="sxs-lookup"><span data-stu-id="96b96-142">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Skärm bild av skärmen delegerade behörigheter för konfiguration av Microsoft partner-API](../images/SelectUserPermission.png)

8. <span data-ttu-id="96b96-144">För det program som du har registrerat väljer du **Egenskaper** och sedan **Kopiera program-ID**.</span><span class="sxs-lookup"><span data-stu-id="96b96-144">For the application you registered, choose **Properties** and then select **copy the Application ID**.</span></span>
9. <span data-ttu-id="96b96-145">Välj **Inställningar** och välj sedan **certifikat & hemligheter**.</span><span class="sxs-lookup"><span data-stu-id="96b96-145">Choose **Settings**, then choose **Certificates & Secrets**.</span></span> <span data-ttu-id="96b96-146">Välj **ny klient hemlighet** och ange **förfallo datum**  till **aldrig förfaller**.</span><span class="sxs-lookup"><span data-stu-id="96b96-146">Choose **New Client Secret** and set the **Expiration**  to **Never expires**.</span></span> <span data-ttu-id="96b96-147">Välj sedan **Spara**.</span><span class="sxs-lookup"><span data-stu-id="96b96-147">Then choose **Save**.</span></span>
10. <span data-ttu-id="96b96-148">På menyn **nycklar** väljer **du kopiera värdet nyckel**.</span><span class="sxs-lookup"><span data-stu-id="96b96-148">On the **Keys** menu, choose **Copy the key value**.</span></span> <span data-ttu-id="96b96-149">Spara en kopia av det här värdet.</span><span class="sxs-lookup"><span data-stu-id="96b96-149">Save a copy of this value.</span></span>

> [!WARNING]
> <span data-ttu-id="96b96-150">Se till att spara en kopia av nyckelvärdet för den nyckel som du har skapat.</span><span class="sxs-lookup"><span data-stu-id="96b96-150">Be sure to save a copy of the key value for the key you created.</span></span> <span data-ttu-id="96b96-151">Du måste använda detta nyckel värde senare för att hämta en token.</span><span class="sxs-lookup"><span data-stu-id="96b96-151">You will need to use this key value later to obtain a token.</span></span>

## <a name="partner-consent"></a><span data-ttu-id="96b96-152">Partner medgivande</span><span class="sxs-lookup"><span data-stu-id="96b96-152">Partner consent</span></span>

<span data-ttu-id="96b96-153">I hanterings portalen för Azure väljer du **företags program**.</span><span class="sxs-lookup"><span data-stu-id="96b96-153">In the Azure management portal, select **Enterprise applications**.</span></span> <span data-ttu-id="96b96-154">Sök efter programmet som du skapade i föregående avsnitt och välj det programmet.</span><span class="sxs-lookup"><span data-stu-id="96b96-154">Search for the application you created in the previous section, and select that application.</span></span> <span data-ttu-id="96b96-155">Välj **behörigheter** och välj sedan **bevilja administratörs medgivande för partner konto**.</span><span class="sxs-lookup"><span data-stu-id="96b96-155">Select **Permissions** , then select **Grant Admin Consent for Partner Account**.</span></span>
