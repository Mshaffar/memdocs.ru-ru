---
title: Создание профилей Wi-Fi
titleSuffix: Configuration Manager
description: Сведения о том, как использовать профили Wi-Fi в Configuration Manager, чтобы развернуть параметры беспроводной сети для пользователей вашей организации.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 21dffd1201b04846a9fffcdc7cc917465daa5905
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690232"
---
# <a name="create-wi-fi-profiles"></a>Создание профилей Wi-Fi

*Область применения: Configuration Manager (Current Branch)*

Используйте профили Wi-Fi в Configuration Manager, чтобы развернуть параметры беспроводной сети для пользователей вашей организации. Развертывание этих параметров позволяет упростить подключение к Wi-Fi для пользователей.  

Например, имеется сеть Wi-Fi, возможность подключения к которой необходимо обеспечить для всех ноутбуков Windows. Создайте профиль Wi-Fi, содержащий параметры, которые необходимы для подключения к беспроводной сети. Затем разверните профиль для всех пользователей, имеющих ноутбуке Windows в иерархии. Пользователи этих устройств увидят локальную сеть в списке беспроводных сетей и смогут легко подключиться к ней.  

Профили Wi-Fi можно настроить для следующих версий ОС:

- Windows 8.1 32- или 64-разрядная версия

- Windows RT 8.1

- Windows 10 или Windows 10 Mobile

Вы также можете использовать Configuration Manager для развертывания параметров беспроводной сети на мобильных устройствах с помощью локального управления мобильными устройствами (MDM). Дополнительные общие сведения см. разделе [Что такое локальное управление мобильными устройствами](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

При создании профиля Wi-Fi можно указать большое количество параметров безопасности, в том числе сертификаты для проверки сервера и проверки подлинности клиента, подготовленные с помощью профилей сертификатов в Configuration Manager. Дополнительные сведения о профилях сертификатов см. в статье [Профили сертификатов](introduction-to-certificate-profiles.md).

## <a name="create-a-wi-fi-profile"></a>Создание профиля Wi-Fi

1. В рабочей области **Активы и соответствие** консоли Configuration Manager разверните узлы **Параметры соответствия** и **Доступ к ресурсам компании**, а затем выберите узел **Профили Wi-Fi**.

1. На вкладке **Главная** в группе **Создать** щелкните **Создать профиль Wi-Fi**.

1. На странице **Общие** мастера создания профилей Wi-Fi укажите перечисленные ниже сведения.

    - **Имя** — введите уникальное имя для указания профиля в консоли.

    - **Описание**. при необходимости добавьте описание, чтобы предоставить дополнительные сведения для профиля Wi-Fi.

    - **Импортировать существующий профиль Wi-Fi из файла**. Выберите этот параметр, чтобы использовать параметры из другого профиля Wi-Fi. При выборе этого параметра останется только две страницы мастера: **Импорт профиля Wi-Fi** и **Поддерживаемые платформы**.

        > [!IMPORTANT]
        > Убедитесь, что импортируемый профиль Wi-Fi содержит допустимый XML-код для профиля Wi-Fi. Configuration Manager не проверяет профиль при импорте файла.

    - **Степень важности несоответствия для отчетов**: выберите один из следующих уровней серьезности, о которых сообщает устройство, если оно оценивает профиль Wi-Fi как несоответствующий. Например, если установка профиля завершается сбоем, это означает несоответствие.

        - **Нет**: компьютеры, для которых не выполняется данное правило соответствия, не передают сведения о серьезности сбоя для отчетов Configuration Manager.

        - **Сведения**.

        - **Предупреждение**

        - **Критическая**.

        - **Критическая с событием**. Компьютеры, не выполняющие правило соответствия, сообщают степень серьезности сбоя типа **Критическая** в отчетах Configuration Manager. Устройства также заносят в журнал событий приложений состояние несоответствия в виде события Windows.

1. На странице **Профиль Wi-Fi** в мастере укажите перечисленные ниже сведения:

    - **Имя сети**. укажите имя, которое будет отображаться устройствами в качестве сетевого имени.

        > [!IMPORTANT]
        > Configuration Manager не поддерживает использование в имени сети таких символов, как апостроф (`'`) и запятая (`,`).

    - **SSID**. укажите идентификатор беспроводной сети с учетом регистра.

    - **Подключаться автоматически, если эта сеть находится в диапазоне**
    - **Искать другие беспроводные сети при подключении к этой сети**
    - **Подключаться, если сеть не ведет вещание своего имени (SSID)**

1. На странице **Настройка безопасности** укажите следующие сведения.

    > [!IMPORTANT]
    > При создании профиля Wi-Fi для [локального управления мобильными устройствами](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) текущая ветвь Configuration Manager поддерживает только следующие конфигурации безопасности Wi-Fi:  
    >
    > - Типы безопасности: **WPA2 Enterprise** или **WPA2 Personal**  
    > - Типы шифрования: **AES** или **TKIP**  
    > - Типы EAP: **Смарт-карта или другой сертификат** либо **PEAP**  

    - **Тип безопасности**. Выберите протокол безопасности, используемый беспроводной сетью, или пункт **Без проверки подлинности (открытая)** для незащищенных сетей.

    - **Шифрование**. если тип безопасности поддерживает шифрование, задайте метод шифрования для беспроводной сети.

    - **Тип EAP**. выберите протокол проверки подлинности для выбранного метода шифрования.

        > [!NOTE]
        > Только для устройств Windows Phone: типы EAP **LEAP** и **EAP-FAST** не поддерживаются.

        Нажмите **Настройка**, чтобы настроить свойства для выбранного типа EAP. Этот параметр недоступен для некоторых выбранных типов EAP.

        > [!IMPORTANT]
        > Окно конфигурации типа EAP приводится из Windows. Убедитесь, что консоль Configuration Manager запущена на компьютере, который поддерживает выбранный тип EAP.

    - **Запоминать учетные данные пользователя при каждом входе в систему**. выберите этот параметр для сохранения учетных данных пользователей, чтобы пользователи не вводили учетные данные беспроводной сети при каждом входе в Windows.

1. На странице **Дополнительные параметры** в мастере укажите дополнительные параметры для профиля Wi-Fi. В зависимости от параметров, выбранных на странице мастера **Настройка безопасности**, дополнительные параметры могут быть недоступны или отличаться от указанных. Например, режим проверки подлинности или параметры единого входа.

1. Если в беспроводной сети используется прокси-сервер, на странице **Параметры прокси-сервера** выберите параметр **Настроить параметры прокси-сервера для этого профиля Wi-Fi**. Затем укажите сведения о конфигурации для прокси-сервера.

1. На странице **Поддерживаемые платформы** выберите версии ОС, в которых применяется этот профиль Wi-Fi.

1. Завершите работу мастера.

## <a name="next-step"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Развертывание профилей Wi-Fi](deploy-wifi-vpn-email-cert-profiles.md)