---
title: Auflisten Ihrer Anwendung im Azure Active Directory-Anwendungskatalog | Microsoft-Dokumentation
description: Auflisten einer Anwendung, die einmaliges Anmelden unterstützt, im Azure Active Directory-App-Katalog
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: ''
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/20/2018
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: e02c60d46fe709c8d418ea4743ba383147e9ddac
ms.sourcegitcommit: 34e0b4a7427f9d2a74164a18c3063c8be967b194
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="list-your-application-in-the-azure-active-directory-application-gallery"></a>Auflisten Ihrer Anwendung zum Azure Active Directory-Anwendungskatalog


##  <a name="what-is-the-azure-ad-application-gallery"></a>Was ist der Azure AD-Anwendungskatalog?

Azure Active Directory (Azure AD) ist ein cloudbasierter Identitätsdienst. Der [Azure AD-Anwendungskatalog](https://azure.microsoft.com/marketplace/active-directory/all/) ist der Azure Marketplace-App-Store, in dem alle Anwendungsconnectors für einmaliges Anmelden und die Benutzerbereitstellung veröffentlicht werden. Kunden, die Azure AD als Identitätsanbieter verwenden, finden hier die veröffentlichten SaaS-Anwendungsconnectors. IT-Administratoren fügen Connectors aus dem App-Katalog hinzu und konfigurieren und verwenden diese dann für einmaliges Anmelden und die Bereitstellung. Azure AD unterstützt alle wichtigen Verbundprotokolle für einmaliges Anmelden, einschließlich SAML 2.0, OpenID Connect, OAuth und WS-Fed.

## <a name="what-are-the-benefits-of-listing-an-application-in-the-gallery"></a>Welche Vorteile bietet eine Auflistung einer Anwendung im Katalog?

*  Kunden finden so die bestmögliche Umgebung für einmaliges Anmelden.

*  Die Konfiguration der Anwendung ist einfach und in wenigen Schritten erledigt. 

*  Eine schnelle Suche findet Ihre Anwendung im Katalog.

*  Azure AD-Kunden mit den Tarifen Free, Basic und Premium können diese Integration nutzen. 

*  Gemeinsame Kunden erhalten ausführliche Tutorials zur Konfiguration. 

*  Kunden, die SCIM verwenden, können für die gleiche App die Bereitstellung nutzen.


##  <a name="prerequisites-implement-federation-protocol"></a>Voraussetzungen: Implementieren eines Verbundprotokolls

Damit eine Anwendung im Azure AD-App-Katalog aufgelistet werden kann, müssen Sie zunächst eines der folgenden von Azure AD unterstützten Verbundprotokolle implementieren. Lesen Sie die Geschäftsbedingungen des Azure AD-App-Katalogs. 

*   **OpenID Connect:** Erstellen Sie die mehrinstanzenfähige Anwendung in Azure AD, und implementieren Sie das [Azure AD-Genehmigungsframework](active-directory-integrating-applications.md#overview-of-the-consent-framework) für Ihre Anwendung. Senden Sie die Anmeldeanforderung an einen gemeinsamen Endpunkt, damit jeder Kunde der Anwendung zustimmen kann. Sie können den Benutzerzugriff anhand der Mandanten-ID und des im Token erhaltenen UPN des Benutzers steuern. Befolgen Sie zum Integrieren Ihrer Anwendung in Azure AD die [Anweisungen für Entwickler](active-directory-authentication-scenarios.md).

*   **SAML 2.0** oder **WS-Fed**: Ihre Anwendung sollte über eine Funktion zur SAML-/WS-Fed-SSO-Integration im SP- oder IDP-Modus verfügen. Jede App, die SAML 2.0 unterstützt, kann direkt in einen Azure AD-Mandanten integriert werden. Befolgen Sie dazu die [Anweisungen zum Hinzufügen einer benutzerdefinierten Anwendung](../active-directory-saas-custom-apps.md).

*   **Kennwortbasiertes SSO:** Erstellen Sie eine Webanwendung mit HTML-Anmeldeseite, um das [kennwortbasierte einmalige Anmelden](../active-directory-appssoaccess-whatis.md) zu konfigurieren. Das kennwortbasierte einmalige Anmelden (auch als „Password Vaulting“ oder „Kennworttresor“ bezeichnet) ermöglicht es Ihnen, den Benutzerzugriff und die Kennwörter für Webanwendungen zu verwalten, die keinen Identitätsverbund unterstützen. Es ist auch für Szenarien nützlich, in denen mehrere Benutzer ein Konto gemeinsam verwenden müssen, wie z.B. bei den App-Konten für die sozialen Medien Ihrer Organisation.

##  <a name="updateremove-existing-listing"></a>Aktualisieren bzw. Entfernen vorhandener Auflistungen

Um eine bestehende Anwendung im Azure AD-App-Katalog zu aktualisieren oder zu entfernen, müssen Sie zuerst die Anfrage im [Anwendungsnetzwerkportal](https://microsoft.sharepoint.com/teams/apponboarding/Apps) stellen. Wenn Sie über ein Office 365-Konto verfügen, verwenden Sie dieses für die Anmeldung bei diesem Portal. Verwenden Sie andernfalls Ihr Microsoft-Konto (z.B. Outlook oder Hotmail) für die Anmeldung.

* Auswählen der geeigneten Option aus der folgenden Abbildung

    ![Zeitachse für Auflistung einer SAML-Anwendung in der Galerie](./media/active-directory-app-gallery-listing/updateorremove.png)

    * Wenn Sie eine vorhandene Anwendung aktualisieren möchten, wählen Sie **Vorhandene Anwendungsauflistung aktualisieren**.

    * Wenn Sie eine vorhandene Anwendung aus dem Azure AD-Katalog entfernen möchten, wählen Sie **Vorhandene Anwendungsauflistung entfernen**.

    * Wenn Sie Probleme mit dem Zugriff haben, wenden Sie sich an das [Azure AD-SSO-Integrationsteam](<mailto:SaaSApplicationIntegrations@service.microsoft.com>). 

## <a name="submit-the-request-in-the-portal"></a>Übermitteln der Anforderung im Portal

Nachdem Sie getestet haben, dass Ihre Anwendungsintegration mit Azure AD funktioniert, übermitteln Sie Ihre Anforderung für den Zugriff auf unser [Anwendungsnetzwerkportal](https://microsoft.sharepoint.com/teams/apponboarding/Apps). Wenn Sie über ein Office 365-Konto verfügen, verwenden Sie dieses für die Anmeldung bei diesem Portal. Verwenden Sie andernfalls Ihr Microsoft-Konto (z.B. Outlook oder Hotmail) für die Anmeldung.

Nach der Anmeldung wird die folgende Seite angezeigt. Geben Sie eine geschäftliche Begründung für den Zugriff in das Textfeld ein, und wählen Sie dann **Zugriff anfordern** aus. Unser Team überprüft die Details und gewährt Ihnen entsprechend Zugriff. Danach können Sie sich beim Portal anmelden und Ihre detaillierte Anforderung für die Anwendung übermitteln.

Wenn Sie Probleme mit dem Zugriff haben, wenden Sie sich an das [Azure AD-SSO-Integrationsteam](<mailto:SaaSApplicationIntegrations@service.microsoft.com>).

![Zugriffsanforderung im SharePoint-Portal](./media/active-directory-app-gallery-listing/accessrequest.png)

## <a name="timelines"></a>Zeitpläne
    
Das Auflisten einer SAML 2.0- oder WS-Fed-Anwendung im Katalog dauert etwa 7 bis 10 Werktage.

   ![Zeitachse für Auflistung einer SAML-Anwendung in der Galerie](./media/active-directory-app-gallery-listing/timeline.png)

Das Auflisten einer OpenID Connect-Anwendung im Katalog dauert etwa 2 bis 5 Werktage.

   ![Zeitachse für Auflistung einer SAML-Anwendung in der Galerie](./media/active-directory-app-gallery-listing/timeline2.png)

## <a name="escalations"></a>Eskalationen

Für Eskalationen senden Sie eine E-Mail an das [Azure AD-SSO-Integrationsteam](mailto:SaaSApplicationIntegrations@service.microsoft.com) an SaaSApplicationIntegrations@service.microsoft.com. Wir melden uns so schnell wie möglich bei Ihnen.
