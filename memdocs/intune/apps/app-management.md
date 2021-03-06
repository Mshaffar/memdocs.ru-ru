---
title: Что такое управление приложениями с помощью Microsoft Intune
titleSuffix: ''
description: Узнайте о возможностях управления клиентскими приложениями в зависимости от платформы для Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/31/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1975a2dc-3a14-4cb9-9afb-e2ba01a1c51b
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: aef549cc01ba0e45d61c16eb8489f8926f92276b
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990522"
---
# <a name="what-is-microsoft-intune-app-management"></a>Что такое управление приложениями с помощью Microsoft Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Как ИТ-администратор, вы можете использовать Microsoft Intune для управления клиентскими приложениями, которые используют сотрудники организации. Эта функция дополняет возможности управления устройствами и защиты данных. Одна из основных задач администратора — убедиться в том, что пользователи имеют доступ к приложениям, необходимым им для работы. Это может быть сложной задачей, так как:
- существует множество платформ устройств и типов приложений;
- может потребоваться управлять приложениями и на устройствах организации, и на личных устройствах пользователей;
- необходимо обеспечить безопасность сети и данных.

Кроме того, может потребоваться назначать приложения и управлять ими на устройствах, которые не зарегистрированы в Intune.

## <a name="mobile-application-management-mam-basics"></a>Основные сведения об управлении мобильными приложениями (MAM)

[Управление мобильными приложениями (MAM) в Intune](app-lifecycle.md) — это набор функций управления, позволяющих публиковать, отправлять, настраивать, защищать, отслеживать и обновлять мобильные приложения для пользователей.

MAM позволяет управлять данными Организации и защищать их в приложении. С помощью **MAM без регистрации** (MAM-WE) вы можете управлять рабочими или учебными приложениями, которые содержат конфиденциальные данные, практически с любого [устройства](app-management.md#app-management-capabilities-by-platform), включая личные устройства в рамках сценария **BYOD**. Intune MAM позволяет управлять многими бизнес-приложениями, включая программы Microsoft Office. См. официальный список общедоступных [защищенных приложений Microsoft Intune](apps-supported-intune-apps.md).

Intune MAM поддерживает две конфигурации.
- **Intune MDM и MAM.** ИТ-администраторы могут управлять приложениями только с помощью MAM и политик защиты приложений на устройствах, зарегистрированных с использованием управления мобильными устройствами Intune (MDM). Для управления приложениями с помощью MDM и MAM следует использовать консоль Intune, которую можно найти на портале Azure по адресу https://portal.azure.com.
- **MAM без регистрации устройства** (MAM-WE). Позволяет ИТ-администраторам управлять приложениями с помощью MAM и политик защиты приложений на устройствах, не зарегистрированных с использованием Intune MDM. Это означает, что приложениями можно управлять в Intune на устройствах, зарегистрированных с использованием сторонних поставщиков EMM. Для управления приложениями с помощью MAM-WE следует использовать консоль Intune, которую можно найти на портале Azure по адресу https://portal.azure.com. Кроме того, приложениями можно управлять в Intune на устройствах, зарегистрированных с использованием сторонних поставщиков EMM (Enterprise Mobility Management) или вовсе не зарегистрированных в MDM. Дополнительные сведения о BYOD и EMS Microsoft см. в статье [Технические решения при реализации концепции BYOD с помощью Microsoft Enterprise Mobility + Security (EMS)](../fundamentals/byod-technology-decisions.md).

## <a name="app-management-capabilities-by-platform"></a>Возможности управления приложениями в зависимости от платформы

Intune предлагает широкий набор возможностей, позволяющих получить и запустить нужные приложения на требуемых устройствах. В таблице ниже перечислены возможности управления приложениями.

|  | Android/Android Enterprise | iOS/iPadOS | MacOS | быть под управлением ОС Windows 10; | Windows Phone 8.1 |
|-------------------------------------------------------------------------------------|---------|-----|-------|------------|-------------------|
| Добавление и назначение приложений устройствам и пользователям | Да | Да | Да | Да | Да |
| Назначение приложений устройствам, не зарегистрированным в Intune | Да | Да | Нет | Нет | Нет |
| Использование политик конфигурации приложений для управления их работой при запуске | Да | Да | Нет | Нет | Нет |
| Использование политик подготовки мобильных приложений для обновления приложений с истекшим сроком действия | Нет | Да | Нет | Нет | Нет |
| Использование политик защиты приложений для обеспечения безопасности корпоративных данных | Да | Да | Нет | Нет <sup>1</sup> | Нет |
| Удаление только корпоративных данных из установленного приложения (выборочная очистка приложений) | Да | Да | Нет | Да | Да |
| Мониторинг назначения приложений | Да | Да | Да | Да | Да |
| Назначение и отслеживание приложений, приобретенных в магазине по программе Volume Purchase | Нет | Нет | Нет | Да | Нет |
| Обязательная установка приложений на устройствах <sup>2</sup> | Да | Да | Да | Да | Да |
| Необязательная установка на устройствах из Корпоративного портала (доступная установка) | Да <sup>3</sup> | Да | Да | Да | Да |
| Установка ярлыка приложения в Интернете (веб-ссылка) | Да <sup>4</sup> | Да | Да | Да | Да |
| Собственные приложения (бизнес-приложения) | Да | Да | Да | Да | Нет |
| Приложения из магазина | Да | Да | Нет | Да | Да |
| Обновление приложений | Да | Да | Нет | Да | Да |

<sup>1</sup> Рассмотрите возможность использования [Windows Information Protection](../protect/windows-information-protection-configure.md) для защиты приложений на устройствах под управлением Windows 10.<br>
<sup>2</sup> Поддерживается только для устройств под управлением Intune.<br>
<sup>3</sup> Intune поддерживает доступные приложения из управляемого Google Play Маркета на устройствах Android для бизнеса.<br>
<sup>4</sup> Intune не обеспечивает установку ярлыка приложения в качестве веб-ссылки на стандартных устройствах Android для бизнеса. Однако поддержка веб-ссылок предоставляется для [выделенных устройств Android для бизнеса с несколькими приложениями](../configuration/device-restrictions-android-for-work.md#dedicated-devices). 


## <a name="get-started"></a>Начало работы

Большинство сведений, связанных с приложениями, находятся в рабочей нагрузке **Приложения**, к которой можно получить доступ следующим образом:

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Выберите **Приложения**.

    ![Панель рабочей нагрузки приложений](./media/app-management/apps-workload.png)

В рабочей нагрузке приложений содержатся ссылки для доступа к общим сведениям и функциональным возможностям приложения. 

В верхней части меню навигации рабочей нагрузки приложения представлены часто используемые сведения о приложении:
- **Обзор**. Выберите этот параметр, чтобы просмотреть имя клиента, центр MDM, расположение клиента, состояние учетной записи, состояние установки приложения и состояние политики защиты приложений.
- **Все приложения**: Выберите этот параметр, чтобы отобразить список всех доступных приложений. На этой странице можно добавить дополнительные приложения. Кроме того, можно просмотреть состояние каждого приложения, а также определить, назначено ли каждое из них. Дополнительные сведения см. в разделах [Добавление приложений](apps-add.md) и [Назначение приложений](apps-deploy.md).
- **Мониторинг приложений**
    - **Лицензии приложений**. В этом разделе можно просматривать, назначать и отслеживать приложения, приобретенные по программе Volume Purchase Program в магазинах приложений. Дополнительные сведения см. в разделах [Приложения iOS, приобретенные по программе корпоративных закупок Apple Volume Purchase Program](vpp-apps-ios.md) и [Магазин Microsoft Store для бизнес-приложений, приобретаемых по программе корпоративного лицензирования](windows-store-for-business.md).
    - **Обнаруженные приложения**. Здесь отображаются приложения, назначенные Intune или установленные на устройстве. Дополнительные сведения см. в статье [Intune discovered apps](app-discovered-apps.md) (Обнаруженные Intune приложения).
    - **Состояние установки приложения**. Здесь отображается состояние созданного назначения приложения. Дополнительные сведения см. в разделе [Отслеживание сведений о приложении и его назначениях с помощью Microsoft Intune](apps-monitor.md#device-and-user-status-graphs).
    - **Состояние защиты приложений**. Здесь отображается состояние политики защиты приложения для выбранного пользователя.
- **По платформе**. Выберите платформы, чтобы просмотреть доступные приложения по платформам.
    - Windows
    - iOS
    - MacOS
    - Android
- **Политика**.
    - **Политики защиты приложений**. Позволяют связать параметры с приложением для защиты используемых корпоративных данных. Например, можно ограничить возможности приложения взаимодействовать с другими приложениями или требовать ввода ПИН-кода для доступа к корпоративному приложению. Дополнительные сведения см. в статье [Политики защиты приложений](app-protection-policies.md).
    - **Политики конфигурации приложений**. Используйте их для предоставления параметров, которые могут быть необходимы, когда пользователь работает с приложением. Дополнительные сведения см. в статьях [Политики конфигурации приложений](app-configuration-policies-use-ios.md), [Политики конфигурации приложений iOS](app-configuration-policies-use-ios.md) и [Политики конфигурации приложений Android](app-configuration-policies-overview.md).
    - **Профили подготовки приложений iOS**. Приложения iOS содержат профиль подготовки и код, подписанный сертификатом. Если срок действия сертификата истек, вы не сможете запустить приложение. Intune предоставляет средства для упреждающего назначения новой политики профиля подготовки на устройствах с приложениями, срок действия которых вскоре истекает. Дополнительные сведения см. в статье [Предотвращение истечения срока действия приложений iOS с помощью профилей подготовки приложений](app-provisioning-profile-ios.md).
    - **Дополнительные политики режима S**. Выберите этот параметр, чтобы авторизовать дополнительные приложения для запуска на управляемых устройствах с режимом S. Дополнительные сведения см. в разделе [Дополнительные политики режима S](apps-win32-s-mode.md).
    - **Наборы политик**. Выберите этот параметр, чтобы создать назначаемую коллекцию приложений, политик и других созданных вами объектов управления. Дополнительные сведения см. в статье [Наборы политик](../fundamentals/policy-sets.md).
- **Другие**.   
    - **Выборочная очистка приложений**. Этот параметр позволяет удалить только корпоративные данные с выбранного устройства пользователя. Дополнительные сведения см. разделе [Выборочная очистка приложений](apps-selective-wipe.md).
    - **Категории приложений**. Добавляйте, закрепляйте и удаляйте имена категорий приложений.
    - **Электронные книги**. Некоторые магазины приложений позволяют приобретать сразу несколько лицензий, если приложение или книги планируется использовать в организации. Дополнительные сведения см. в статье [Управление приложениями и книгами, приобретенными по программе корпоративных закупок, с помощью Microsoft Intune](vpp-apps.md).
- **Справка и поддержка**. Устраняйте неполадки, подавайте запросы на поддержку или просматривайте сведения о состоянии Intune. Дополнительные сведения см. в разделе [Устранение неполадок](../fundamentals/help-desk-operators.md).

### <a name="try-the-interactive-guide"></a>Попробуйте интерактивное руководство
Интерактивное руководство [Управление мобильными и настольными приложениями и их защита с помощью Microsoft Endpoint Manager](https://mslearn.cloudguides.com/en-us/guides/Manage%20and%20protect%20mobile%20and%20desktop%20applications%20with%20Microsoft%20Endpoint%20Manager) описывает, как в центре администрирования Microsoft Endpoint Manager можно управлять устройствами, развернутыми в Intune, обеспечивать соответствие политикам и защищать данные организации.</br></br>

> [!VIDEO https://mslearn.cloudguides.com/en-us/guides/Manage%20and%20protect%20mobile%20and%20desktop%20applications%20with%20Microsoft%20Endpoint%20Manager]

## <a name="additional-information"></a>Дополнительные сведения
Следующие элементы в консоли предоставляют функциональные возможности, связанные с приложением:
- **Microsoft Store для бизнеса**. В этом разделе можно настроить интеграцию с Microsoft Store для бизнеса. После этого вы сможете синхронизировать приобретенные приложения с Intune, назначать их и отслеживать использование лицензий. Дополнительные сведения см. в статье [Магазин Microsoft Store для бизнес-приложений, приобретаемых по программе корпоративного лицензирования](windows-store-for-business.md).
- **Сертификат Windows Корпоративная**. Примените сертификат подписи кода, используемый для распространения бизнес-приложений на управляемых устройствах Windows, или просмотрите сведения о его состоянии.
- **Сертификат Windows Symantec**. Примените сертификат подписи кода Symantec, который необходим для распространения APPX-файлов XAP и WP8.x на устройствах Windows 10 Mobile, или просмотрите сведения о его состоянии.
- **Ключи загрузки неопубликованных приложений Windows**. Добавьте ключ загрузки неопубликованных приложений Windows, чтобы установить приложение непосредственно на устройствах вместо его публикации и загрузки из магазина Windows. Дополнительные сведения см. в статье [Подписывание бизнес-приложений для развертывания на устройствах Windows с помощью Intune](app-sideload-windows.md).
- **Токены VPP Apple**. Применение и просмотр лицензий Volume Purchase Program (VPP) для iOS и iPadOS. Дополнительные сведения см. в разделе [Приложения iOS/iPadOS, приобретенные по программе Volume Purchase Program (VPP)](vpp-apps-ios.md).
- **Управляемый Google Play**. Управляемый Google Play — это корпоративное хранилище приложений Google и единственный источник приложений в Android для бизнеса. Дополнительные сведения см. в статье [Назначение приложений управляемого Google Play для корпоративных устройств с Android с помощью Intune](apps-add-android-for-work.md).
- **Настройка**. Здесь можно настроить фирменную символику для Корпоративного портала. Дополнительные сведения см. в разделе [Конфигурация приложений корпоративного портала](company-portal-app.md).

Дополнительные сведения о добавлении приложений в Intune см. в [этой статье](../apps/apps-add.md).

## <a name="next-steps"></a>Дальнейшие шаги

- [Добавление веб-приложения в Microsoft Intune](apps-add.md)
