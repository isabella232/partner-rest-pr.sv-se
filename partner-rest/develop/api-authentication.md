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
# <a name="partner-api-authentication"></a>Autentisering för partner-API

Gäller för:

- Partner-API

Partner-API: et använder Azure Active Directory (Azure AD) för autentisering. När du interagerar med partner-API: et måste du konfigurera ett Azure AD-program på rätt sätt och få en åtkomsttoken. Du kan få åtkomst-token för [program-och användar åtkomst](#application-and-user-access) eller [endast program åtkomst](#application-only-access).

## <a name="application-and-user-access"></a>Åtkomst till program och användare

Den här metoden rekommenderas för att ställa in **program-och användar åtkomst** till API: et.

1. Logga in på [Azure-portalen](https://portal.azure.com/).
2. Välj tjänsten **Azure Active Directory** .
3. Välj **Appregistreringar** och välj sedan **ny program registrering**.
4. Skapa ditt nya program. För **program typ** väljer du **intern**. Ange ett namn och en URL och välj sedan **skapa**.
5. Välj **API-behörigheter** för programmet. På skärmen **begär API-behörigheter** väljer du **Lägg till en behörighet** och väljer sedan de **API: er som min organisation använder**
6. Sök efter *Microsoft partner* (*Microsoft dev Center*) API ( `4990cffe-04e8-4e8b-808a-1175604b879f` ).

    ![Skärm bild av skärmen begär API-behörigheter med en sökning efter Microsoft partner-API: et](../images/SearchGatewayApi.png)

7. Ange **delegerade behörigheter** till **partner Center**.

    ![Skärm bild av skärmen delegerade behörigheter för konfiguration av Microsoft partner-API](../images/SelectUserPermission.png)
    
8. Sök efter *Microsoft partner* (*Microsoft Partner Center*) API ( `fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd` ).

    ![Skärm bild av skärmen begär API-behörigheter med en sökning för Microsoft Partner Center API](../images/SearchPCApi.png)
    
9. Välj **Microsoft Partner Center** och markera **user_impersonation**.

10. Ange **delegerade behörigheter** till **partner Center**.

    ![Skärm bild av skärmen delegerade behörigheter för konfiguration av Microsoft Partner Center API](../images/SelectPCUserPermission.png)

## <a name="application-only-access"></a>Endast program åtkomst

Den här metoden rekommenderas för konfiguration av **program åtkomst** till API: erna.

> [!IMPORTANT]
> Du måste ange program-ID, program nyckel och katalog-ID från ditt Azure AD-program.

1. Logga in på [Azure-portalen](https://portal.azure.com/).
2. Välj tjänsten **Azure Active Directory** .
3. Välj **Appregistreringar** och välj sedan **ny program registrering**.
4. Skapa ditt nya program. För **program typ** väljer du **webbapp/API**. Ange ett program **namn** och en **URL**. Välj sedan **Skapa**.
5. Välj **API-behörigheter** för programmet. Välj **Lägg till en behörighet** och välj sedan de **API: er som används i organisationen**
6. Sök efter *Microsoft partner* (*Microsoft dev Center*) API ( `4990cffe-04e8-4e8b-808a-1175604b879f` ).

    ![Skärm bild av skärmen begär API-behörigheter med en sökning efter Microsoft partner-API: et](../images/SearchGatewayApi.png)

7. Ange **delegerade behörigheter** till **partner Center**.

    ![Skärm bild av skärmen delegerade behörigheter för konfiguration av Microsoft partner-API](../images/SelectUserPermission.png)

8. För det program som du har registrerat väljer du **Egenskaper** och sedan **Kopiera program-ID**.
9. Välj **Inställningar** och välj sedan **certifikat & hemligheter**. Välj **ny klient hemlighet** och ange **förfallo datum**  till **aldrig förfaller**. Välj sedan **Spara**.
10. På menyn **nycklar** väljer **du kopiera värdet nyckel**. Spara en kopia av det här värdet.

> [!WARNING]
> Se till att spara en kopia av nyckelvärdet för den nyckel som du har skapat. Du måste använda detta nyckel värde senare för att hämta en token.

## <a name="partner-consent"></a>Partner medgivande

I hanterings portalen för Azure väljer du **företags program**. Sök efter programmet som du skapade i föregående avsnitt och välj det programmet. Välj **behörigheter** och välj sedan **bevilja administratörs medgivande för partner konto**.
