---
title: Блокировка устройств с помощью Microsoft Intune в Azure | Документация Майкрософт
description: Используйте действие удаленной блокировки в Microsoft Intune, чтобы заблокировать устройство, защищенное с помощью ПИН-кода или пароля.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3b67f285-229d-4a0f-ae34-0402a20b4518
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 29b30d46fc5998c69059c743c3f469e198cee1ef
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "80325136"
---
# <a name="remotely-lock-devices-with-intune"></a>Удаленная блокировка устройств с помощью Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Действие устройства **Удаленная блокировка** позволяет заблокировать устройство. Чтобы разблокировать устройство, владельцу устройства необходимо ввести секретный код. Удаленно заблокировать можно устройства, для которых задан ПИН-код или пароль. Устройства без ПИН-кода или пароля нельзя заблокировать удаленно.

## <a name="supported-platforms"></a>Поддерживаемые платформы

**Удаленная блокировка** поддерживается на указанных ниже платформах.

- Android
- Киоски с Android для бизнеса
- Устройства с рабочим профилем Android для бизнеса
- iOS
- macOS
- Windows 10 Mobile
- Windows Phone 8.1 и более поздней версии

**Удаленная блокировка** не поддерживается для следующих систем:
- Windows 10 Desktop

> [!NOTE]
> Для устройств с macOS необходимо задать ПИН-код восстановления из шести цифр. При блокировке устройства в разделе **Обзор устройства** отображается ПИН-код, пока не будет отправлено другое действие устройства.

## <a name="remote-lock-a-device"></a>Удаленная блокировка устройства

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Выберите **Устройства** > **Все устройства**.
4. Выберите нужное устройство в списке устройств, а затем укажите действие **Удаленная блокировка**.

## <a name="next-steps"></a>Дальнейшие действия

- Чтобы отобразились сведения о состоянии действия, выберите **Microsoft Intune** > **Устройства** > **Действия устройства**. 
- Дополнительные действия по управлению устройствами см. в статье о [доступных действиях](device-management.md).
