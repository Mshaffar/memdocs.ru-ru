---
title: Создание профилей VPN
titleSuffix: Configuration Manager
description: Узнайте, как создавать профили VPN в Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 17811d0bb0b72ebee6879d5dab90e165b439081b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694252"
---
# <a name="how-to-create-vpn-profiles-in-configuration-manager"></a>Создание профилей VPN в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Configuration Manager поддерживает несколько типов VPN-подключений. Дополнительные сведения о типах подключений, доступных для различных платформ устройств, см. в разделе [Профили VPN](vpn-profiles.md).

Для сторонних подключений VPN распространите приложение VPN перед развертыванием профиля VPN. Если не развернуть приложение, пользователям будет предложено сделать это при попытке подключиться к VPN. Дополнительные сведения см. в разделе [Развертывание приложений](../../apps/deploy-use/deploy-applications.md).

## <a name="create-a-vpn-profile"></a>Создание профиля VPN

1. В рабочей области **Активы и соответствие** консоли Configuration Manager разверните узлы **Параметры соответствия** и **Доступ к ресурсам компании**, а затем выберите узел **Профили VPN**.

1. На вкладке **Главная** на ленте в группе **Создать** выберите **Создать профиль VPN**.

1. На странице **Общие** мастера создания профилей VPN укажите следующие сведения:

    - **Имя** — введите уникальное имя для указания профиля VPN в консоли.

        > [!NOTE]
        > Не используйте следующие символы в имени профиля VPN: `\/:*?<>|; `. Профиль VPN Windows не поддерживает эти специальные символы.

    - **Описание**. при необходимости введите описание, чтобы предоставить дополнительные сведения о профиле VPN.

    - **Тип профиля VPN**: выберите соответствующую платформу.

        При выборе платформы **Windows 8.1** можно также выбрать **Импортировать из файла**. Это действие импортирует сведения о профиле VPN из XML-файла. При выборе этого параметра остаются только следующие страницы мастера: **Поддерживаемые платформы** и **Импорт профиля VPN**.

1. На странице **Поддерживаемые платформы** выберите версии ОС, поддерживаемые этим профилем VPN.

1. На странице **Подключение** укажите перечисленные ниже сведения:

    - **Тип подключения**. Выберите тип VPN-подключения. Дополнительные сведения о поддерживаемых типах см. в разделе [Профили VPN](vpn-profiles.md).

    - **Список серверов**. Добавьте новый сервер для VPN-подключения. В зависимости от типа подключения можно добавить один или несколько VPN-серверов и указать сервер по умолчанию.

    - **Обходить VPN при наличии подключения к сети компании**: настройте клиенты так, чтобы они не использовали VPN-подключение, когда находятся во внутренней сети. При необходимости укажите DNS-имя, зависящее от подключения.

1. На странице **Метод проверки подлинности** в мастере выберите метод, который поддерживается типом соединения. Настройки и доступные параметры на этой странице зависят от выбранного типа соединения. Дополнительные сведения см. в разделе [Справочник по методам проверки подлинности](#bkmk_auth).

1. Если VPN использует прокси-сервер, на странице **Параметры прокси-сервера** выберите один из параметров, соответствующий вашей среде. Затем укажите сведения о конфигурации для прокси-сервера.

1. Страница **Приложения** применяется только к профилям Windows 10. Добавьте классические и универсальные приложения, которые автоматически подключаются к этой сети VPN. Идентификатор приложения определяется типом приложения:

    - Для *классического приложения* укажите путь к файлу приложения.

    - Для *универсального приложения* укажите имя семейства пакетов (PFN). Сведения об определении имени PFN для приложения см. в разделе [Определение имени семейства пакетов для VPN для отдельного приложения](find-a-pfn-for-per-app-vpn.md).

    Кроме того, можно выбрать параметр **Только указанные приложения могут использовать эту сеть VPN**.

    > [!IMPORTANT]
    > Обеспечьте безопасность всех списков связанных приложений, компилируемых для настройки VPN для отдельных приложений. Если неавторизованный пользователь изменяет список, а вы импортируете его в список приложений VPN для отдельных приложений, вы можете разрешить доступ к VPN приложениям, которые не должны иметь такой доступ.

1. Страница **Границы** применяется только к профилям Windows 10 для настройки границ VPN. Вы можете добавить следующие параметры:

    - **Правила сетевого трафика**. Укажите, какие протоколы, локальные и удаленные порты, а также диапазоны адресов нужно включить для VPN-подключения.  

        > [!Note]
        > Если не создать правило сетевого трафика, включаются все протоколы, порты и диапазоны адресов. VPN-подключение использует только протоколы, порты и диапазоны адресов, указанные в созданном правиле или дополнительных правилах.

    - **DNS-имена и серверы**: DNS-серверы, используемые VPN-подключением после того, как устройство установит подключение.

    - **Маршруты**: сетевые маршруты, использующие VPN-подключение. Создание более чем 60 маршрутов может вызвать сбой политики.

1. Завершите работу мастера.

Новый профиль VPN отобразится в узле **Профили VPN** рабочей области **Активы и соответствие** .

## <a name="authentication-method-reference"></a><a name="bkmk_auth"></a> Справочник по методам проверки подлинности

Доступные методы проверки подлинности VPN зависят от типа подключения:

### <a name="certificates"></a>Сертификаты

Если сертификат клиента используется для проверки подлинности на сервере RADIUS (например, на сервере политики сети), в качестве альтернативного имени субъекта в сертификате задайте имя субъекта-пользователя.

Поддерживаемые типы подключений:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- Check Point Mobile VPN

### <a name="username-and-password"></a>Имя пользователя и пароль

Поддерживаемые типы подключений:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- Check Point Mobile VPN

### <a name="microsoft-eap-ttls"></a>Microsoft EAP-TTLS

Поддерживаемые типы подключений:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- PPTP
- IKEv2
- L2TP

### <a name="microsoft-protected-eap-peap"></a>Защищенный EAP от Майкрософт (PEAP)

Поддерживаемые типы подключений:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="microsoft-secured-password-eap-mschap-v2"></a>Защищенный пароль Майкрософт (EAP-MSCHAP v2)

Поддерживаемые типы подключений:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="smart-card-or-other-certificate"></a>Смарт-карта или иной сертификат

Поддерживаемые типы подключений:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="mschap-v2"></a>MSCHAP v2

Поддерживаемые типы подключений:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="use-machine-certificates"></a>Использовать сертификаты компьютера

Поддерживаемые типы подключений:

- IKEv2

### <a name="additional-authentication-options"></a>Дополнительные параметры проверки подлинности

Если версия клиента Windows это поддерживает, доступна возможность **Настроить** способ проверки подлинности. При выборе этого параметра отображается окно свойств Windows для настройки способа проверки подлинности.

В зависимости от выбранных параметров, вам может быть предложено ввести дополнительные сведения, например:

- **Запоминать учетные данные пользователя при каждом входе в систему**. Учетные данные пользователя запоминаются, чтобы пользователю не нужно было вводить их при каждом подключении.  

- **Выберите сертификат клиента для проверки подлинности клиента**. Выберите созданный ранее профиль сертификата SCEP клиента, который будет использоваться для проверки подлинности VPN-подключения. Дополнительные сведения см. в разделе [Создание профилей сертификатов PFX](create-certificate-profiles.md).

## <a name="next-steps"></a>Дальнейшие шаги

- Для сторонних подключений VPN распространите приложение VPN перед развертыванием профиля VPN. Если не развернуть приложение, пользователям будет предложено сделать это при попытке подключиться к VPN. Дополнительные сведения см. в разделе [Развертывание приложений](../../apps/deploy-use/deploy-applications.md).

- Разверните профиль VPN. Дополнительные сведения см. в разделе [Развертывание профилей](deploy-wifi-vpn-email-cert-profiles.md).