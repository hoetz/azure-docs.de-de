---
title: Wiederherstellen oder dauerhaftes Löschen eines kürzlich gelöschten Benutzers in Azure Active Directory | Microsoft-Dokumentation
description: Vorgehensweise beim Wiederherstellen eines gelöschten Benutzers, Anzeigen von wiederherstellbaren Benutzern und endgültigen Löschen eines Benutzers in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: ''
ms.devlang: ''
ms.topic: article
ms.date: 03/28/2018
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: it-pro
ms.openlocfilehash: 9eea61cc1b735c6505df87526cd526a9a4a6eed8
ms.sourcegitcommit: 34e0b4a7427f9d2a74164a18c3063c8be967b194
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="restore-a-deleted-user-in-azure-active-directory"></a>Wiederherstellen eines gelöschten Benutzers in Azure Active Directory

Dieser Artikel enthält Anweisungen zum Wiederherstellen oder endgültigen Löschen eines zuvor gelöschten Benutzers. Wenn Sie einen Benutzer in Azure Active Directory (Azure AD) löschen, wird der gelöschte Benutzer nach dem Löschdatum 30 Tage lang beibehalten. Während dieses Zeitraums können der Benutzer und seine Eigenschaften wiederhergestellt werden. 

> [!wARNING]
> Der Benutzer kann nach dem dauerhaften Löschen nicht wiederhergestellt werden.


## <a name="how-to-restore-a-recently-deleted-user"></a>Wiederherstellen eines kürzlich gelöschten Benutzers
Wenn ein Benutzer vor Kurzem gelöscht wurde, werden alle Verzeichnisinformationen beibehalten. Wenn der Benutzer wiederhergestellt wird, werden diese Informationen ebenfalls wiederhergestellt.

1. Wählen Sie im [Azure AD Admin Center](https://aad.portal.azure.com) **Benutzer und Gruppen** &gt; **Alle Benutzer** aus. 
2. Filtern Sie die Seite unter **Anzeigen**, um **Kürzlich gelöschte Benutzer** anzuzeigen. 
3. Wählen Sie mindestens einen kürzlich gelöschten Benutzer aus.
4. Wählen Sie **Benutzer wiederherstellen** aus.

## <a name="how-to-permanently-delete-a-recently-deleted-user"></a>Dauerhaftes Löschen eines kürzlich gelöschten Benutzers

1. Wählen Sie im [Azure AD Admin Center](https://aad.portal.azure.com) **Benutzer und Gruppen** &gt; **Alle Benutzer** aus. 
2. Filtern Sie die Seite unter **Anzeigen**, um **Kürzlich gelöschte Benutzer** anzuzeigen. 
3. Wählen Sie mindestens einen kürzlich gelöschten Benutzer aus.
4. Wählen Sie **Endgültig löschen** aus.

## <a name="required-permissions"></a>Erforderliche Berechtigungen
Die folgenden Berechtigungen sind zum Wiederherstellen eines Benutzers ausreichend.

Rolle  | Berechtigungen 
--------- | ---------
Unternehmensadministrator<p>Partnersupport der Ebene 1<p>Partnersupport der Ebene 2<p>Benutzerkontoadministrator | Kann gelöschte Benutzer wiederherstellen 
Unternehmensadministrator<p>Partnersupport der Ebene 1<p>Partnersupport der Ebene 2<p>Benutzerkontoadministrator | Kann Benutzer endgültig löschen

## <a name="next-steps"></a>Nächste Schritte
Diese Artikel enthalten zusätzliche Informationen zur Benutzerverwaltung in Azure Active Directory.

* [Schnellstart: Hinzufügen oder Löschen von Benutzern in Azure Active Directory](add-users-azure-active-directory.md)
* [Verwalten von Benutzerprofilen](active-directory-users-profile-azure-portal.md)
* [Hinzufügen von Gastbenutzern aus einem anderen Verzeichnis](active-directory-b2b-what-is-azure-ad-b2b.md) 
* [Zuweisen eines Benutzers zu einer Rolle in Azure AD](active-directory-users-assign-role-azure-portal.md)
