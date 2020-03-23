---
title: Ограничение возможностей устройств с помощью политики в Microsoft Intune — Azure | Документация Майкрософт
description: Добавление профиля устройства для ограничения функций на устройствах Android, macOS, iOS, iPadOS, Windows Phone и Windows 10 в Microsoft Intune
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28cf0b8bffc06a0b5a56165c1e9eeab780c453c7
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79361826"
---
# <a name="configure-device-restriction-settings-in-microsoft-intune"></a>Настройка параметров ограничений устройств в Microsoft Intune



Intune включает политики ограничения устройств, которые помогают администраторам контролировать устройства Android, iOS/iPadOS, macOS и Windows. Эти ограничения позволяют контролировать широкий спектр параметров и функций для защиты ресурсов организации. Например, администраторы могут:

- разрешить или блокировать использование камеры устройства;
- управлять доступом к Google Play, магазинам приложений, просмотру документов и играм;
- блокировать встроенные приложения или создать список разрешенных или запрещенных приложений;
- разрешить или запретить резервное копирование файлов в облачные учетные записи и учетные записи хранения;
- установить минимальную длину пароля и заблокировать простые пароли.

Эти функции настраиваются администратором и доступны в Intune. Intune использует "профили конфигурации" для создания и настройки этих параметров для вашей организации. После добавления этих компонентов в профиль вы сможете отправлять или развертывать профиль в устройства в своей организации.

В этой статье описано, как создать профиль ограничения для устройств. Также можно увидеть все доступные настройки для разных платформ.

## <a name="create-the-profile"></a>Создание профиля

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Устройства** > **Профили конфигурации** > **Создать профиль**.
3. Укажите следующие свойства.

    - **Имя** — Введите описательное имя для политики. Назначьте имена политикам, чтобы их можно было легко найти в последствии. Например, хорошее имя политики — **iOS/iPadOS: Блокировать камеру на устройствах**.
    - **Описание**. Введите описание политики. Этот параметр является необязательным, но мы рекомендуем его использовать.
    - **Платформа**. Выберите платформу устройств. Доступны следующие параметры:  

        - **Android**
        - **Android для бизнеса**
        - **iOS/iPadOS**
        - **macOS**
        - **Windows Phone 8.1**
        - **Windows 8.1 и более поздние версии**
        - **Windows 10 и более поздних версий**.

    - **Тип профиля**. Выберите **Ограничения устройств**.

        Если вы хотите создать профиль ограничений для устройств Windows 10 для совместной работы, например Surface Hub, выберите **Ограничения для устройств (Windows 10 для совместной работы)** .

4. Доступные для настройки параметры различаются в зависимости от выбранной платформы. Выберите платформу для настройки дополнительных параметров:

    - [Параметры Android](device-restrictions-android.md)
    - [Параметры Android для бизнеса](device-restrictions-android-for-work.md)
    - [Параметры iOS/iPadOS](device-restrictions-ios.md)
    - [Параметры macOS](device-restrictions-macos.md)
    - [Параметры Windows Phone 8.1](device-restrictions-windows-phone-8-1.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Параметры Windows 10](device-restrictions-windows-10.md)
    - [Параметры Windows 10 для совместной работы](device-restrictions-windows-10-teams.md)
    - [Параметры Windows Holographic for Business](device-restrictions-windows-holographic.md)

5. По завершении нажмите **ОК** > **Создать**, чтобы сохранить изменения.

Созданный профиль отобразится в списке профилей.

## <a name="next-steps"></a>Дальнейшие шаги

Созданный профиль готов к назначению. Далее [назначьте профиль](device-profile-assign.md) и [отслеживайте его состояние](device-profile-monitor.md).

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/device-restrictions-configure/disable-android-camera.png)

-->