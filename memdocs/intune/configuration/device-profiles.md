---
title: Функции и параметры устройств в Microsoft Intune — Azure | Документация Майкрософт
description: Общие сведения о различных профилях устройств Microsoft Intune. Узнайте о функциях, ограничениях, электронной почте, Wi-Fi, VPN, образовании, сертификатах, обновлении Windows 10, BitLocker и Microsoft Defender, Windows Information Protection, административных шаблонах и пользовательских параметрах устройства в центре администрирования Microsoft Endpoint Manager. Используйте эти профили для управления и защиты данных и устройств в вашей компании.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: karthib
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: ade4842564188c457af94a22fe49d3d18d791ebb
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79361878"
---
# <a name="apply-features-and-settings-on-your-devices-using-device-profiles-in-microsoft-intune"></a>Применение параметров и функций на устройствах с помощью профилей устройств в Microsoft Intune

Microsoft Intune включает параметры и функции, которые можно включать или отключать на различных устройствах в вашей организации. Эти параметры и компоненты добавляются в "профили конфигурации". Вы можете создавать профили для различных устройств и платформ, включая iOS/iPadOS, Android и Windows. Затем используйте Intune, чтобы применить или назначить профиль устройствам.

Используйте эти профили конфигурации для выполнения различных задач в составе решения по управлению мобильными устройствами (MDM). Примеры профилей:

- На устройствах с Windows 10 используйте шаблон профиля, который блокирует элементы управления ActiveX в Internet Explorer.
- На устройствах с iOS/iPadOS и macOS разрешите пользователям работу с принтерами AirPrint в вашей организации.
- Разрешение или запрет на использование BlueTooth на устройстве.
- Создание профиля Wi-Fi или VPN, предоставляющего различным устройствам доступ к корпоративной сети.
- Управление обновлениями программного обеспечения, включая их установку.
- Запуск устройства Android как выделенного киоска, где можно запускать одно приложение или несколько.

В этой статье описываются различные типы профилей, которые вы можете создать. С помощью этих профилей можно включать или отключать некоторые функции на устройствах.

## <a name="administrative-templates"></a>Административные шаблоны

[Административные шаблоны](administrative-templates-windows.md) включают сотни параметров, которые можно настроить: Internet Explorer, OneDrive, удаленный рабочий стол, Word, Excel, прочие программы Office.

Эти шаблоны предоставляют администраторам упрощенное представление параметров, аналогичное групповой политике, но они являются полностью облачными.

Эта функция поддерживает:

- Windows 10 и более поздней версии

## <a name="certificates"></a>Сертификаты

[Сертификаты](../protect/certificates-configure.md) — настройка доверенных сертификатов, сертификатов SCEP и PKCS, которые можно назначить устройствам. Эти сертификаты можно использовать для проверки подлинности Wi-Fi, VPN и профилей электронной почты.

Эта функция поддерживает: 

- Android
- Android для бизнеса
- iOS/iPadOS
- MacOS
- Windows Phone 8.1
- Windows 8.1
- Windows 10 и более поздней версии

## <a name="custom-profile"></a>Пользовательский профиль

[Настраиваемые параметры](custom-settings-configure.md) позволяют администраторам использовать параметры устройства, не встроенные в Intune. На устройствах Android можно ввести значения OMA-URI. Для устройств iOS/iPadOS можно импортировать файл конфигурации, созданный в Apple Configurator.

Эта функция поддерживает:

- Android
- Android для бизнеса
- iOS/iPadOS
- MacOS
- Windows Phone 8.1

## <a name="delivery-optimization"></a>Оптимизация доставки

[Оптимизация доставки](delivery-optimization-windows.md) повышает удобство работы при доставке обновлений программного обеспечения. Эти параметры заменяют параметры **Обновления программного обеспечения** > **Круг обновления Windows 10** .

Используйте эти параметры для управления тем, как обновления программного обеспечения скачиваются на устройства в вашей организации. Например, вы можете разрешить пользователям получать необходимые им обновления или получать обновления с помощью облачных служб оптимизации доставки в профиле устройства.

Эта функция поддерживает:

- Windows 10 и более поздней версии

## <a name="device-features"></a>Возможности устройств

[Возможности устройств](device-features-configure.md) позволяют управлять возможностями устройств с iOS/iPadOS и macOS, например AirPrint, уведомлениями и сообщениями на экране блокировки.

Эта функция поддерживает:

- iOS/iPadOS
- MacOS

## <a name="device-firmware-configuration-interface"></a>Интерфейс конфигурации встроенного ПО устройства

[Интерфейс конфигурации встроенного ПО устройства](device-firmware-configuration-interface-windows.md) (DFCI) позволяет администраторам включать и отключать параметры UEFI (BIOS) с помощью Intune. Используйте эти параметры для повышения безопасности на уровне встроенного ПО, которое обычно более устойчиво к атакам злоумышленников.

Эта функция поддерживает:

- Windows 10 версии 1809 и более поздней в поддерживаемом встроенном ПО

## <a name="device-restrictions"></a>Ограничения устройств

[Ограничения устройств](device-restrictions-configure.md) позволяют управлять безопасностью, оборудованием, общим доступом к данным и другими параметрами на устройствах. Например, можно создать профиль ограничения устройства, который запрещает доступ к камере пользователям устройств с iOS/iPadOS. 

Эта функция поддерживает:

- Android
- Android для бизнеса
- iOS/iPadOS
- MacOS
- Windows 10 и более поздней версии
- Windows 10 для совместной работы

## <a name="domain-join"></a>Присоединение к домену

Во время [присоединения к домену](domain-join-configure.md) настраиваются локальные сведения о домене Active Directory. Эти сведения развертываются на гибридных устройствах, присоединенных к Azure AD, при подготовке с помощью Windows Autopilot и Intune. Этот профиль указывает домен и подразделение, к которым должны быть присоединены устройства.

Эта функция поддерживает:

- Windows 10 и более поздней версии

## <a name="edition-upgrade"></a>Обновление выпусков

[Обновления выпуска Windows 10](edition-upgrade-configure-windows-10.md) — автоматическое обновление устройств, работающих под управлением одной из версий Windows 10.

Эта функция поддерживает:

- Windows 10 и более поздней версии

## <a name="education"></a>Образование

[Параметры образования — Windows 10](education-settings-configure.md) — настройка параметров для [приложения Windows Take a Test](https://education.microsoft.com/gettrained/win10takeatest). После настройки этих параметров никакие другие приложения не смогут работать на устройстве до завершения теста.

[Параметры образования — iOS/iPadOS](../fundamentals/education-settings-configure-ios-shared.md) — приложение iOS/iPadOS Класс помогает преподавателям руководить обучением и управлять устройствами учащихся в классе. Устройства iPad можно настроить так, чтобы несколько учащихся могли пользоваться одним устройством.

## <a name="email"></a>Электронная почта

Профиль [параметров электронной почты](email-settings-configure.md) позволяет создавать, назначать и отслеживать параметры электронной почты Exchange ActiveSync на устройствах. Этот профиль обеспечивают согласованность, сокращение числа обращений в службу поддержки, а также предоставляет пользователям доступ к электронной почте компании с личных устройств без дополнительных настроек. 

Эта функция поддерживает: 

- Android
- Android для бизнеса
- iOS/iPadOS
- Windows Phone 8.1
- Windows 10 и более поздней версии

## <a name="endpoint-protection"></a>Защита конечных точек

[Параметры защиты конечных точек для Windows 10](../protect/endpoint-protection-windows-10.md) — настройка параметров BitLocker и защитника Майкрософт для устройств Windows 10.

Сведения о внедрении Advanced Threat Protection в Microsoft Defender (WDATP) с помощью Microsoft Intune см. в статье [Настройка конечных точек с помощью средств управления мобильными устройствами (MDM)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-mdm).

Эта функция поддерживает:

- Windows 10 и более поздней версии

## <a name="esim-cellular---public-preview"></a>Сотовая связь eSIM (общедоступная предварительная версия)

[Профили сотовой связи eSIM](esim-device-configuration.md) позволяют администраторам настраивать тарифные планы сотовой сети на управляемых устройствах для доступа к Интернету и данным. После получения кодов активации от оператора мобильной связи можно использовать Intune для импорта этих кодов, а затем назначить их для устройств, поддерживающих eSIM.

Эта функция поддерживает:

- Windows 10 Fall Creators Update и более поздние версии

## <a name="extensions"></a>Расширения

[Расширения ядра](kernel-extensions-overview-macos.md) позволяют администраторам добавлять функции или программы на уровне ядра на устройствах macOS. Настройте эти параметры, чтобы доверять всем расширениям конкретного разработчика или партнера, или разрешить конкретные расширения ядра.

Эта функция поддерживает:

- MacOS

## <a name="identity-protection"></a>Защита идентификации

[Защита идентификации](../protect/identity-protection-configure.md) управляет возможностью использования Windows Hello для бизнеса на устройствах с Windows 10 и Windows 10 Mobile. Настройте эти параметры, чтобы предоставить Windows Hello для бизнеса для пользователей и устройств, а также указать требования к ПИН-кодам и жестам для устройств.  

Эта функция поддерживает:  

- Windows 10 и более поздней версии
- Windows Holographic for Business  

## <a name="kiosk"></a>Киоск

Профиль [параметров киоска](kiosk-settings.md) настраивает выполнение одного или нескольких приложений на устройстве. Для киоска можно также настроить другие компоненты, включая меню "Пуск" и веб-браузер.

Эта функция поддерживает:

- Windows 10 и более поздней версии

Этот профиль также можно использовать в качестве ограничений для устройств [Android](device-restrictions-android.md#kiosk), [Android для бизнеса](device-restrictions-android-for-work.md#dedicated-device-settings) и [iOS/iPadOS](device-restrictions-ios.md#kiosk).

## <a name="oemconfig"></a>OEMConfig

[OEMConfig](android-oem-configuration-overview.md) — это стандарт, который позволяет OEM (производителям оригинального оборудования) и EMM (управлению мобильностью предприятия) создавать и поддерживать специфичные для OEM-производителя функции стандартным способом на устройствах Android для бизнеса. С помощью OEMConfig OEM создает схему, которая определяет специфичные для OEM функции управления, и встраивает ее в приложение, загруженное в Google Play. Intune считывает схему из приложения, позволяя администраторам Intune настраивать параметры в схеме.

Эта функция поддерживает:

- Android для бизнеса (OEMConfig)

## <a name="powershell-scripts"></a>Сценарии PowerShell

[Сценарии PowerShell на устройствах с Windows 10](../apps/intune-management-extension.md) использует расширение управления Intune для отправки скриптов PowerShell в Intune, а затем выполняет эти сценарии на устройствах. Также ознакомьтесь с требованиями к использованию расширения, добавлением их в Intune и другими важными сведениями.


Эта функция поддерживает:

- Windows 10 и более поздней версии
- Windows Holographic for Business

## <a name="shared-multi-user-device"></a>Общие устройства для множества пользователей

[Windows 10](shared-user-device-settings-windows.md) и [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md) включают параметры для управления устройствами с несколькими пользователями, также известными как общие устройства или общие ПК. При входе пользователя на устройстве можно выбрать, может ли пользователь изменять параметры спящего режима или сохранять файлы на устройстве. В другом примере можно создать профиль, который удаляет неактивные учетные данные с устройств Windows HoloLens для экономии места.

Эти параметры общего устройства для нескольких пользователей позволяют администратору управлять некоторыми функциями устройства и контролировать эти общие устройства с помощью Intune.

Эта функция поддерживает:

- Windows 10 и более поздней версии
- Windows Holographic for Business

## <a name="update-policies"></a>Политики обновления

В статье [Политики обновления iOS/iPadOS](../protect/software-updates-ios.md) показано, как создавать и назначать политики iOS/iPadOS для установки обновлений программного обеспечения на устройствах iOS/iPadOS. Кроме того, можно просмотреть состояние установки.

Политики обновления на устройствах Windows см. в разделе [Оптимизация доставки](delivery-optimization-windows.md). 

Эта функция поддерживает:

- iOS/iPadOS

## <a name="vpn"></a>VPN

[Параметры VPN](vpn-settings-configure.md) — назначение профилей VPN для пользователей и устройств в организации и обеспечение простого и безопасного подключения к сети. 

Виртуальная частная сеть (VPN) предоставляет пользователям безопасный удаленный доступ к сети компании. Устройства используют профиль VPN-подключения для установления подключения к VPN-серверу. 

Эта функция поддерживает: 

- Android
- Android для бизнеса
- iOS/iPadOS
- MacOS
- Windows Phone 8.1
- Windows 8.1
- Windows 10 и более поздней версии

## <a name="wi-fi"></a>Wi-Fi

[Параметры Wi-Fi](wi-fi-settings-configure.md) — параметры беспроводной сети для пользователей и устройств. При назначении профиля Wi-Fi пользователи получают доступ к корпоративной сети Wi-Fi, не настраивая ее самостоятельно. 

Эта функция поддерживает: 

- Android
- Android для бизнеса
- iOS/iPadOS
- MacOS
- Windows 8.1 (только импорт)
- Windows 10 и более поздней версии

## <a name="windows-information-protection-profile"></a>Профиль Windows Information Protection

[Windows Information Protection](../protect/windows-information-protection-configure.md) позволяет предотвратить утечку данных, не влияя при этом на работу сотрудника. Кроме того, эта политика защищает от случайной утечки данных корпоративные приложения и данные на рабочих устройствах, принадлежащих организации или сотрудникам. При использовании Windows Information Protection не требуется вносить изменения в вашу среду или другие приложения.

Эта функция поддерживает:

- Windows 10 и более поздней версии

## <a name="zebra-mobility-extensions-mx"></a>Zebra Mobility Extensions (MX)

[Zebra Mobility Extensions (MX)](android-zebra-mx-overview.md) позволяет администраторам использовать устройства Zebra и управлять ими в Intune. Создайте профили StageNow со своими настройками, а затем с помощью Intune назначьте и разверните эти профили на устройствах Zebra. [Журналы StageNow и распространенные проблемы](android-zebra-mx-logs-troubleshoot.md) — это отличный ресурс для устранения неполадок в профилях и просмотра потенциальных проблем при использовании StageNow.

Эта функция поддерживает:

- Android (расширения мобильности)

## <a name="manage-and-troubleshoot"></a>Управление и устранение неполадок

[Управление профилями](device-profile-monitor.md) используется для проверки состояния устройств и назначенных профилей. Оно также помогает разрешать конфликты путем просмотра параметров, которые вызывают конфликт, и профилей, содержащих эти параметры. В [этой статье](device-profile-troubleshoot.md) описаны общие проблемы и решения, которые помогут администраторам работать с профилями. В ней описано, что происходит при удалении профиля, что вызывает отправку уведомлений на устройства и многое другое.

## <a name="next-steps"></a>Дальнейшие шаги

Выберите платформу и приступайте к работе.