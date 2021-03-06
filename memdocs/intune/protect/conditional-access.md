---
title: Условный доступ с помощью Microsoft Intune
titleSuffix: Microsoft Intune
description: Узнайте, как определить условия, которым должны отвечать пользователи, устройства и приложения для доступа к корпоративным ресурсам в Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/06/2018
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a1973f38-ea55-43eb-a151-505fb34a8afb
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8f7f4bf735ee5145bdad269a0ea6a6016d0ad97e
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83985960"
---
# <a name="learn-about-conditional-access-and-intune"></a>Дополнительные сведения об условном доступе и Intune

Условный доступ — это способ управления устройствами и приложениями, которые могут подключаться к вашей электронной почте и ресурсам компании. 

Enterprise Mobility + Security (EMS) не является изолированным продуктом. Это решение, которое принимает участие во всех службах и продуктах, входящих в состав EMS. Условный доступ обеспечивает детализированное управление доступом для эффективной защиты корпоративных данных, гарантируя при этом максимально продуктивную работу пользователей на любом устройстве и из любого места.

Вы можете определить условия, ограничивающие доступ к вашим корпоративным данным на основе расположения, состояния устройства и пользователя, а также конфиденциальности приложения.

> [!NOTE]
> Условный доступ также расширяет возможности [служб Office 365](https://docs.microsoft.com/office365/enterprise/office-365-client-support-conditional-access).

![Схема условного доступа](./media/conditional-access/ca-diagram-1.png)

## <a name="use-conditional-access-with-intune"></a>Условный доступ с помощью Intune

Условный доступ — это функция Azure Active Directory, которая входит в лицензию Azure Active Directory Premium. Intune расширяет эту возможность, добавляя в решение средства для обеспечения соответствия мобильных устройств и для управления мобильными приложениями. 

![Intune и условный доступ при использовании EMS](./media/conditional-access/intune-with-ca-1.png)

Способы использования условного доступа с помощью Intune:

- **Условный доступ на основе информации об устройстве**

  - Условный доступ для локальной организации Exchange

  - Условный доступ на основе управления доступом к сети

  - Условный доступ на основе сведений о рисках для устройства

  - Условный доступ для ПК под управлением Windows

    - Корпоративные устройства

    - Принеси свое устройство (BYOD)

- **Условный доступ на основе приложений**

## <a name="next-steps"></a>Дальнейшие действия

[Каковы стандартные способы использования условного доступа с помощью Intune?](conditional-access-intune-common-ways-use.md)
