---
title: Подготовка к регистрации устройств Android в Intune
titleSuffix: Microsoft Intune
description: Сведения о том, как зарегистрировать устройства Android в Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 7/23/2019
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f276d98c-b077-452a-8835-41919d674db5
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a0739b27d5b2b6bb21809b2a9f109c894765ea7e
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988559"
---
# <a name="enroll-android-devices"></a>Регистрация устройств Android

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Администратор Intune может зарегистрировать устройства Android следующим образом:
- В Android для бизнеса доступно несколько вариантов регистрации, предлагающих пользователям самые актуальные и безопасные функции.
    - [**Android для бизнеса — рабочий профиль**](android-work-profile-enroll.md). Личные устройства, которым предоставлено разрешение на доступ к корпоративным данным. Администраторы могут управлять рабочими учетными записями, приложениями и данными. Персональные данные на устройстве хранятся отдельно от рабочих данных, и администраторы не могут управлять личными параметрами или данными. 
    - [**Выделенные устройства Android для бизнеса**](android-kiosk-enroll.md). Корпоративные однофункциональные устройства, например для цифровых подписей, печати билетов или управления складскими запасами. Администраторы ограничивают работу устройства, разрешая использовать ограниченный набор приложений и веб-ссылок. Пользователи не могут добавлять другие приложения или выполнять другие операции на устройстве.
    - [**Полностью управляемая среда Android Enterprise**](android-fully-managed-enroll.md). Корпоративные устройства одного пользователя, применяемые исключительно для работы, но не для личного использования. Администраторы могут управлять всем устройством и принудительно применять элементы управления политики для рабочих профилей. 
- [**Как администратор вы можете управлять устройствами Android**](android-enroll-device-administrator.md), в том числе устройствами Samsung Knox Standard и [Zebra](../configuration/android-zebra-mx-overview.md). 

## <a name="prerequisites"></a>Предварительные условия

Чтобы подготовиться к управлению мобильными устройствами, нужно установить **Microsoft Intune** в качестве службы управления мобильными устройствами (MDM). Инструкции см. в статье [Установка центра управления мобильными устройствами](../fundamentals/mdm-authority-set.md). Этот параметр указывается только один раз при первой настройке Intune для управления мобильными устройствами.

Для устройств, изготовленных компанией Zebra Technologies, может потребоваться предоставить для Корпоративного портала дополнительные разрешения в зависимости от возможностей конкретного устройства. Дополнительные сведения см. в статье о [расширениях Mobility на устройствах Zebra](../configuration/android-zebra-mx-overview.md).

Для устройств Samsung Knox Standard имеются [другие предварительные требования](android-samsung-knox-mobile-enroll.md).

## <a name="next-steps"></a>Дальнейшие шаги

- [Настройка регистрации устройств с рабочим профилем Android](android-work-profile-enroll.md)
- [Настройка регистрации в Intune выделенных устройств с Android для бизнеса](android-kiosk-enroll.md)
- [Настройка регистрации полностью управляемых устройств Android для бизнеса в Intune (предварительная версия)](android-fully-managed-enroll.md)
- [Регистрация с использованием функции администратора устройства Android](android-enroll-device-administrator.md)

