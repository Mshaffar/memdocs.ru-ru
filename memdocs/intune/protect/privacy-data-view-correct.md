---
title: Просмотр и изменение персональных данных
titleSuffix: Microsoft Intune
description: Сведения о просмотре и изменении персональных данных.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1ba77bc7-505e-4eca-a49e-dcdaa75d0043
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6cddd94400874c508a31b11b22fa4417798e2da
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "80084771"
---
# <a name="view-and-correct-personal-data"></a>Просмотр и изменение персональных данных

Администраторы Intune могут просматривать некоторые персональные данные с учетом своих разрешений доступа, но только конечные пользователи могут изменять персональные данные на своем устройстве.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]


## <a name="view-personal-data"></a>Просмотр персональных данных

Администраторы могут просматривать персональные данные конечных пользователей в различных колонках пользовательского интерфейса Intune. В следующих статьях описано, к какой информации администраторам предоставляется и не предоставляется доступ:
- [Просмотр сведений об устройстве в Intune](../remote-actions/device-inventory.md) — описано, как просмотреть сведения об устройстве пользователя.
- [Отслеживание сведений о приложении и его назначений](../apps/apps-monitor.md) — описано, как просмотреть подробные сведения о приложениях, установленных на устройстве пользователя.
- [Какие сведения становятся доступными для моей организации при регистрации устройства?](https://docs.microsoft.com/mem/intune/user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune) — описаны сведения, к которым организации предоставляется и не предоставляется доступ на просмотр. Рекомендуется четко пояснить пользователям, какие сведения вы будете собирать и по какой причине. Эта статья может стать первым шагом к достижению подобной прозрачности.

### <a name="who-can-view-the-data"></a>Кто может просматривать данные?

Корпорация Майкрософт для управления доступом к данным клиентов прибегает к строгому контролю, предоставляя самый низкий, необходимый для выполнения ключевых задач, уровень доступа и отзывая его, когда он больше не нужен. 

Вы можете защитить и контролировать доступ к персональным данным конечных пользователей с помощью управления доступом на основе ролей (RBAC). Дополнительные сведения см. в разделе [Управление доступом на основе ролей с помощью Microsoft Intune](../fundamentals/role-based-access-control.md).

Дополнительные сведения о методах корпорации Майкрософт по работе с данными см. в [заявлении о конфиденциальности Microsoft Online Services](https://go.microsoft.com/fwlink/p/?linkid=131004&clcid=0x409). 

## <a name="correct-end-user-personal-data"></a>Исправление персональных данных конечных пользователей

Администраторы не могут изменять сведения, относящиеся к конкретному устройству или приложению. Если конечный пользователь хочет исправить любые персональные данные (например, имя устройства), он должен сделать это непосредственно на своем устройстве. Такие изменения синхронизируются при следующем подключении к Intune.


## <a name="next-steps"></a>Дальнейшие действия

Сведения об [аудите, экспорте и удалении](privacy-data-audit-export-delete.md) персональных данных в Intune.
