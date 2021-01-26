---
title: Hänvisningsresurser
description: Hänvisnings resurser representerar ett lead direkt från en kund, Microsoft eller en annan partner.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 08438d208da57a4df40aeb609b14b6b6a6128d45
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770596"
---
# <a name="referral-resources"></a>Hänvisningsresurser

Gäller för:

- Partnercenter

Dessa resurser representerar ett lead direkt från en kund, Microsoft eller en annan partner.

## <a name="referral"></a>Hänvisnings

Representerar referensen.

| Egenskap              | Typ                                              | Description                                                                                                       |
|-----------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Id                    | sträng                                            | ID för den här hänvisningen.                                                                                         |
| EngagementId          | sträng                                            | EngagementID för den här referensen. Flera hänvisningar kan associeras med en enda EngagementID                 |
| Name                  | sträng                                            | Namnet på referensen.                 |
| ExternalReferenceId   | sträng                                            | En extern identifierare för referensen. Exempel: lagra ditt eget Dynamics 365-lead/affärs möjlighets-ID                    |
| CreatedDateTime       | sträng i UTC-datum/tid-format                    | Datumet då hänvisningen skapades.                                                                                |
| UpdatedDateTime       | sträng i UTC-datum/tid-format                    | Datumet då hänvisningen senast uppdaterades.                                                                           |
| ExpirationDateTime    | sträng i UTC-datum/tid-format                    | Datumet då hänvisningen upphör att gälla.                                                                                |
| Status                | [ReferralStatus](referral-resources.md#referralstatus)      | En [uppräkning](https://docs.microsoft.com/dotnet/api/system.enum) med värden som anger hänvisnings status. |
| Substatus          | [ReferralSubstatus](referral-resources.md#referralsubstatus)      | En [Enum](https://docs.microsoft.com/dotnet/api/system.enum) med värden som anger del status för hänvisning. |
| StatusReason          | sträng                                            | Ett beskrivande meddelande om status. Exempel: Varför förlorade hänvisningarna? |
| ReferralType          | [ReferralType](referral-resources.md#referraltype)          | Representerar referens typen.                                                                                     |
| Kvalificering         | [ReferralQualification](referral-resources.md#referralqualification)| Representerar referensens kvalitet.                                                                           |
| CustomerProfile       | [CustomerProfile](referral-resources.md#customerprofile)    | Information om kunden.                                                                                     |
| Samtycke               | [Samtycke](referral-resources.md#consent)                    | Medgivande flaggor runt delning av information med andra organisationer och gör det möjligt för dem att kontakta användare.         |
| Information               | [ReferralDetails](referral-resources.md#referraldetails)    | Kund information, noteringar, avtals värde, valuta stängnings datum.                                                                |
| Team                  | [Medlem](referral-resources.md#member)                      | Representerar användare i de organisationer som är inblandade.                                |
| InviteContext         | [InviteContext](referral-resources.md#invitecontext)        | Representerar ytterligare information som en användare kan tillhandahålla när de bjuder in en annan organisation till partner engagemang.  |
| ETag                  | sträng                                            | ETags används och krävs för samtidiga kontroller vid uppdatering av resurser. |
| Mål         | [ReferralTarget](referral-resources.md#target)        | Representerar ytterligare information som en användare kan tillhandahålla när de bjuder in en annan organisation till partner engagemang.  |

## <a name="referralstatus"></a>ReferralStatus

En [uppräkning](https://docs.microsoft.com/dotnet/api/system.enum) med värden som anger hänvisnings status.

| Värde           | Beskrivning                                                                                |
|-----------------|---------------------------------------------------------------------------------------------|
| Ingen            |                                                                                             |
| Ny             | Representerar en ny hänvisning.                                                                 |
| Aktiv          | Representerar en aktiv hänvisning.                                                             |
| Stängd          | Representerar en stängd referens.                                                              |

## <a name="referralsubstatus"></a>ReferralSubstatus

En [uppräkning](https://docs.microsoft.com/dotnet/api/system.enum) med värden som anger hänvisnings status.

| Värde           | Beskrivning                                                                                |
|-----------------|--------------------------------------------------------------------------------------------|
| Ingen            |                                                                                            |
| Väntar         | Representerar en ny hänvisning som väntar.                                                 |
| Mottaget        | Representerar en ny hänvisning som har tagits emot.                   |
| Har godkänts        | Representerar en aktiv hänvisning som har godkänts.                                                    |
| Vunna             | Representerar en stängd hänvisning som har vunnits.                                            |
| Brute            | Representerar en stängd hänvisning som har gått förlorad.                                           |
| Nekad        | Representerar en stängd referens som har nekats.                                       |
| Upphörd         | Representerar en stängd referens som har upphört att gälla.                                             |

### <a name="status--substatus-transition-states"></a>Status & över gångs status för under status

| Status                | Tillåten status över gång     | Tillåten under status                |
|-----------------------|-------------------------------|---------------------------------------|
| Ny                   | Nytt, aktivt, stängt           | Väntar, mottaget                     |
| Aktiv                | Aktiv, stängd                | Har godkänts                              |
| Stängd                | Stängd                        | Vann, förlorad, avböjd, upphör att gälla          |

## <a name="referraltype"></a>ReferralType

En [uppräkning](https://docs.microsoft.com/dotnet/api/system.enum) med värden som anger hänvisnings typen.

| Egenskap              | Beskrivning                                                                     |
|-----------------------|---------------------------------------------------------------------------------|
| Delad                | Representerar en hänvisning där alla berörda parter kommer att samar beta.  |
| Oberoende           | Representerar en hänvisning där två parter kommer att samar beta.           |

## <a name="referralqualification"></a>ReferralQualification

En [uppräkning](https://docs.microsoft.com/dotnet/api/system.enum) med värden som anger hänvisnings status.

| Värde                | Beskrivning                                                                                 |
|----------------------|---------------------------------------------------------------------------------------------|
| Ingen                 | Representerar en referens som inte har någon associerad kvalitets mått.                               |
| Direct               | Representerar en hänvisning som har skapats direkt av en kund.                         |
| MarketingQualified   | Representerar en hänvisning som har genererats via Microsoft Marketing Automation system.   |
| SalesQualified       | Representerar en hänvisning från en Microsoft-försäljnings agent.                                         |

## <a name="customerprofile"></a>CustomerProfile

Innehåller kundens kontakt uppgifter.

| Egenskap | Typ                                                   | Beskrivning                                            |
|----------|--------------------------------------------------------|--------------------------------------------------------|
| Name     | sträng                                                 | Kundens organisations namn.                        |
| Adress  | [Adress](referral-resources.md#address)                         | Adressen till kunden.                           |
| Storlek     | sträng                                                 | Antalet anställda hos kundernas organisation. |
| Team     | [Medlem](referral-resources.md#member)                           | Kontakterna för kund organisationen.            |
| Kompatibilitet      | [CustomerProfileType](referral-resources.md#customerprofiletype) | En [matris](https://docs.microsoft.com/dotnet/api/system.array) med värden som indikerar kundernas externa ID.                        |

## <a name="customerprofiletype"></a>CustomerProfileType

Innehåller de externa ID: na för kunden.

| Egenskap | Typ   | Description                                                                           |
|----------|--------|---------------------------------------------------------------------------------------|
| Duns     | sträng | [Dun & Bradstreet-nummer](https://www.dnb.com/duns-number.html) för kunden. |
| Extern | sträng | Ett kund-ID som är unikt för din organisation.                                            |

## <a name="address"></a>Adress

En adress som ska användas för kunden.

| Egenskap     | Typ   | Description                                                |
|--------------|--------|------------------------------------------------------------|
| AddressLine1 | sträng | Den första raden i adressen.                             |
| AddressLine2 | sträng | Den andra raden i adressen. Den här egenskapen är valfri. |
| City         | sträng | Staden.                                                  |
| Stat        | sträng | Status.                                                 |
| Postnummer   | sträng | Post nummer                                |
| Land      | sträng | Land/region i [ISO-format för landskod](https://docs.microsoft.com/dotnet/api/system.globalization.regioninfo.threeletterisoregionname?view=netframework-4.7.2).             |
| Region       | sträng | Regionen.                                                |

## <a name="member"></a>Medlem

Beskriver kontakt information för en viss individ.

| Egenskap    | Typ   | Description                  |
|-------------|--------|------------------------------|
| FirstName   | sträng | Kontaktens förnamn.    |
| LastName    | sträng | Kontaktens efter namn.     |
| PhoneNumber | sträng | Kontaktens telefonnummer.  |
| E-post       | sträng | Kontaktens e-postadress. |
| ContactPreference       | [ContactPreference](referral-resources.md#contactpreference) | Kontaktens preferens för att ta emot e-postaviseringar. |

## <a name="contactpreference"></a>ContactPreference

Beskriver kontakt inställningar för att ta emot e-postaviseringar.

| Egenskap    | Typ   | Description                  |
|-------------|--------|------------------------------|
| Nationell inställning   | sträng | Språk inställningen för e-postmeddelandet. [AllCultures](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_AllCultures), [NeutralCultures](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_NeutralCultures)och [SpecificCultures](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_SpecificCultures) stöds  |
| DisableNotifications    | boolesk | Inaktiverar e-postmeddelanden för användaren.     |

## <a name="consent"></a>Samtycke

Medgivande flaggor runt delning av information med andra organisationer och gör det möjligt för dem att kontakta användare.

| Egenskap                                         | Typ      | Description                                                                                |
|--------------------------------------------------|-----------|--------------------------------------------------------------------------------------------|
| ConsentToToShareInfoWithOthers                   | boolean   | Indikerar medgivande för att dela personligt identifierbar information (PII) med andra.             |
| ConsentToContact                                 | boolean   | Indikerar medgivande till kontakt användare.  |

## <a name="invitecontext"></a>InviteContext

Ytterligare information som kan delas när du bjuder in en annan organisation.

| Egenskap              | Typ                                                       | Beskrivning                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| Kommentarer                 | sträng                                                     | Ytterligare information om den mottagande organisationen.                |
| InvitedBy | [InvitedBy](referral-resources.md#invitedby)                                     | Organisations-ID som skickade hänvisningen.                                   |

## <a name="invitedby"></a>InvitedBy

Ytterligare information som kan delas när du bjuder in en annan organisation.

| Egenskap              | Typ                                                       | Description                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| Organisations-ID        | sträng                                                     | Organisations-ID som skickade hänvisningen.                |
| OrganizationName      | sträng                                                     | Organisations namnet som skickade hänvisningen.                                   |

## <a name="referraldetails"></a>ReferralDetails

Representerar hänvisnings informationen.

| Egenskap              | Typ                                                       | Beskrivning                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| Kommentarer                 | sträng                                                     | Ytterligare information om den mottagande organisationen.                |
| DealValue             | decimal                                                    | Referensens värde.                                    |
| Valuta              | sträng                                                    | [Valuta symbolen för ISO 4217](https://docs.microsoft.com/dotnet/api/system.globalization.regioninfo.isocurrencysymbol?view=netframework-4.7.2)                                   |
| ClosingDateTime       | sträng i UTC-datum/tid-format                         | Datum då kunden ska stängas av.                           |
| Krav          | [ReferralRequirements](referral-resources.md#referralrequirements)   | Bransch, produkter, service typ och lösningar som kunden är intresse rad av.|

## <a name="referralrequirements"></a>ReferralRequirements

Innehåller kund kraven.

| Egenskap        | Typ                                                         | Description                                          |
|-----------------|--------------------------------------------------------------|------------------------------------------------------|
| Branscher      | [Tag](referral-resources.md#tag)                                       | De branscher kunden är intresse rad av.        |
| Produkter        | [Tag](referral-resources.md#tag)                                       | De produkter kunden är intresse rad av.          |
| Tjänster        | [Tag](referral-resources.md#tag)                                       | De tjänster kunden är intresse rad av.          |
| Lösningar       | [SolutionTag](referral-resources.md#solutiontag)                       | De lösningar som kunden är intresse rad av.                             |

## <a name="solutiontag"></a>SolutionTag

Innehåller lösnings information.

| Egenskap        | Typ                                         | Description                                          |
|-----------------|----------------------------------------------|------------------------------------------------------|
| Id              | sträng                                       | ID för lösningen.        |
| Name            | sträng                                       | Lösningens namn.          |
| SolutionType    | [SolutionType](referral-resources.md#solutiontype)     | Typ av lösning.          |

## <a name="solutiontype"></a>SolutionType

En [uppräkning](https://docs.microsoft.com/dotnet/api/system.enum) med värden som visar lösnings typen.

| Egenskap        | Beskrivning                                                     |
|-----------------|-----------------------------------------------------------------|
| Ingen            |                                                                  |
| Kategori        |  Utnyttjar fördefinierade lösnings namn.                            |
| Name            |  Möjlighet att referera till lösningar från Microsoft-katalogen. |

## <a name="target"></a>Mål

Beskriver referens målet.

| Egenskap                  | Typ                                                  | Description                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| Id                        | sträng                                                | ID för referens målet. |
| Typ                      | [ReferralTargetType](referral-resources.md#targettype) | Typ av referens mål |

## <a name="targettype"></a>TargetType

En [uppräkning](https://docs.microsoft.com/dotnet/api/system.enum) med värden som visar lösnings typen.

| Egenskap        | Beskrivning                                                     |
|-----------------|-----------------------------------------------------------------|
| Ingen            |                                                                  |
| BusinessProfileLocation         |  Profil plats från partner företags profil.                            |
| SolutionProfile            |  Partnerns lösnings profil. |

## <a name="tag"></a>Tagg

Beskriver taggen.

| Egenskap                  | Typ                                                  | Description                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| Id                        | sträng                                                | ID för den här taggen.                                          |

### <a name="products"></a>Produkter

| Värde        |
|-----------------|
|Azure|
|EnterpriseMobilityAndSecurity|
|Exchange|
|DeveloperTools|
|Dynamics365Business|
|Dynamics365Enterprise|
|DynamicsAX, GP, NAV, SL|
|Microsoft365|
|Office|
|Power BI|
|Project|
|SharePoint|
|SkypeForBusiness|
|Surface|
|SurfaceHub|
|SQL|
|Teams|
|Visio|
|Windows|
|Yammer|

### <a name="services"></a>Tjänster

| Värde        |
|-----------------|
|ConsultingAndProfessional|
|CustomSolution (ISV)|
|DeploymentOrMigration|
|Maskinvara|
|Integrering|
|IPServices (ISV)|
|LearningAndCertification|
|Licensiering|
|ManagedServices|
|ProjectServices|

### <a name="industries"></a>Branscher

| Värde        |
|-----------------|
|Jordbruk, skogsbruk, & fiske|
|Kommunikation & Media|
|Education|
|Ekonomiska tjänster|
|Myndigheter|
|Sjukvård|
|Hotell- och restaurangbranschen|
|Tillverkningsindustrin|
|Power &-verktyg|
|Allmän säkerhet och nationell säkerhet|
|Butiks & konsument varor|
|Tjänster|
|Res & transport|
|Distribution av grossist &|

### <a name="solutions"></a>Lösningar

| Värde        |
|-----------------|
|AdvancedAnalytics|
|ApplicationIntegration|
|ArtificialIntelligence|
|AzureSecurityOperationManagement|
    |AzureStack|
    |BackupDisasterRecovery|
    |BigData|
    |Blockkedja|
    |Chattrobot|
    |CloudDatabaseMigration|
    |CloudMigration|
    |CloudVoice|
    |CognitiveServices|
    |CompetitiveDatabaseMigration|
    |Containers|
    |DataWarehouse|
    |DatabaseonLinux|
    |DevelopmentandTest|
    |DevOps|
    |DigitalMedia|
    |Dynamics365forCustomerService|
    |Dynamics365forFieldService|
    |Dynamics365forFinanceOperations|
    |Dynamics365forRetail|
    |Dynamics365forSales|
    |Dynamics365forTalent|
    |DynamicsonAzure|
    |EnterpriseBusinessIntelligence|
    |Spel|
    |HighPerformanceComputing|
    |HybridStorage|
    |IdentityandAccessManagement|
    |InformationManagement|
    |InternetofThings|
    |MachineLearning|
    |Microserviceapplications|
    |MobileApplications|
    |MySQLPostgresMigrationtoAzure|
    |Nätverk|
    |NoSQLMigration|
    |RedhatonAzure|
    |RegulatoryComplianceGDPR|
    |SAPonAzure|
    |ServerlessComputing|
    |SharepointonAzure|
    |SQLServerUpgrade|
    |ThreatProtection|
    |Webutveckling|

### <a name="customer-size"></a>Kund storlek

| Värde        |
|-----------------|
|    1to50employees|
|    51to500employees|
|    Morethan500employees|
|    1to9employees|
|    10to50employees|
|    51to250employees|
|    251to1000employees|
|    1001to5000employees|
|    5001to10000employees|
|    10001to20000employees|
|    Morethan20000employees|
