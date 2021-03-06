---
title: Управление устройствами в Microsoft 365
description: В состав Microsoft 365 корпоративный входит служба Microsoft Intune. Как Intune обеспечивает управление мобильными устройствами и мобильными приложениями для вашей организации? Изучите распространенные сценарии и используйте Intune для развертывания Microsoft 365 в вашей среде.
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/13/2019
ms.topic: overview
audience: microsoft-business
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.technology: ''
ms.assetid: 0649d310-43a7-4b01-85d2-da255d03e1da
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: microsoft-intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 44f9446299bb20bd73890a67ec33c3d8e7a36e48
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988148"
---
# <a name="device-management-overview"></a>Общие сведения об управлении устройствами

Основная задача любого администратора заключается в обеспечении безопасности и защиты ресурсов и данных администрации. Эта задача реализует *управление устройствами*. В распоряжении пользователей находится множество устройств, на которых они открывают и совместно используют личные файлы, посещают веб-сайты, устанавливают приложения и игры. Те же самые пользователи также являются сотрудниками и учащимися. Они хотят использовать свои устройства для доступа к рабочим и учебным ресурсам, например к электронной почте и OneNote.

Управление устройствами позволяет организации защитить свои ресурсы и данные при использовании различных устройств.

Используя поставщик управления устройствами, организации предоставляют доступ к конфиденциальной информации только авторизованным пользователям и устройствам. Кроме того, пользователи устройств могут легко обращаться к рабочим данным со своих телефонов, так как они знают, что устройства соответствуют требованиям безопасности организации. В каждой организации может возникнуть вопрос: **что нужно использовать для защиты ресурсов?**

Ответ — [Microsoft Intune](what-is-intune.md). Intune предлагает функции управления мобильными устройствами (MDM) и управления мобильными приложениями (MAM). Решения MDM и MAM предназначены для выполнения следующих ключевых задач.

- Поддержка разнообразных мобильных сред и безопасное управление устройствами с iOS, iPadOS, Android, Windows и macOS.
- Обеспечение соответствия устройств и приложений требованиям безопасности в организации.
- Создание политик для защиты данных организации на корпоративных и личных устройствах.
- Использование единого мобильного решения для применения этих политик и управление устройствами, приложениями, пользователями и группами.
- Защита данных организации при помощи управления обращением к ним и их совместным использованием.

Intune входит в состав Microsoft Azure, Microsoft 365, а также интегрируется с Azure Active Directory (Azure AD). Azure AD помогает контролировать лиц, имеющих права доступа, а также ресурсы, к которым они обращаются.

## <a name="microsoft-intune"></a>Microsoft Intune

Многие организации, например Майкрософт, используют Intune для обеспечения безопасности защищаемых данных, к которым пользователи получают доступ с корпоративных и личных мобильных устройств. Intune включает в себя такие возможности, как политики конфигурации устройств и приложений, политики обновления программного обеспечения и состояния установки (диаграммы, таблицы и отчеты), для защиты и отслеживания доступа к данным.

Зачастую у пользователей есть несколько устройств, работающих на разных платформах. Например, сотрудник может использовать Surface Pro для выполнения рабочих задач и мобильное устройство Android в личных целях. И он также может обращаться с этих нескольких устройств к ресурсам организации, таким как Microsoft Outlook и SharePoint.

Intune позволяет управлять несколькими устройствами, выделенными каждому сотруднику, и различными платформами, которые поддерживаются на каждом устройстве, включая iOS, iPadOS, macOS, Android и Windows. Intune разделяет параметры и политики по признаку платформы устройства. Это облегчает управление и просмотр устройств для определенной платформы.

**[Распространенные сценарии](common-scenarios.md)** — это отличный ресурс, позволяющий найти ответы на общие вопросы при работе с мобильными устройствами в Intune. Вы найдете сценарии на следующие темы.  

- Защита электронной почты с помощью локальной службы Exchange
- Безопасный доступ к Office 365
- Использование личных устройств для доступа к ресурсам организации

Дополнительные сведения об Intune см. в статье [Что такое Intune](what-is-intune.md).

## <a name="integration-with-secure-and-protect-services"></a>Интеграция со службами безопасности и защиты

Основной задачей любого решения для управления устройствами является обеспечение безопасности и защиты. Для ее реализации Intune отлично интегрируется с другими службами. Пример.

- **Microsoft 365** является ключевым компонентом для упрощения распространенных ИТ-задач. В центре администрирования Microsoft 365 ведется создание пользователей и управление группами. Вы также получаете доступ к другим службам, таким как Intune, Azure AD и многие другие.

  Например, в Microsoft 365 можно создать группу устройств с iOS или iPadOS. Затем с помощью Intune отправить политики в группу устройств iOS или iPadOS, поддерживающих функции iOS и iPadOS, такие как доступ к магазину приложений, использование AirDrop, резервное копирование в iCloud, использование веб-фильтра Apple и многое другое.

- **Защитник Windows** предоставляет множество функций безопасности для защиты устройств Windows 10. Используя Intune вместе с Защитником Windows, вы можете:

  - включить [SmartScreen Защитника Windows](../protect/endpoint-protection-windows-10.md) для поиска подозрительной активности в файлах и приложениях на мобильных устройствах;
  - Используйте [Advanced Threat Protection в Microsoft Defender](../protect/advanced-threat-protection.md) для предотвращения нарушений безопасности на мобильных устройствах. Также помогите ограничить последствия брешей в системе безопасности путем блокирования пользователей к корпоративным ресурсам.

- **Условный доступ** — это функция Azure Active Directory, которая легко интегрируется с Intune. С помощью [условного доступа](../protect/conditional-access.md) доступ к электронной почте, SharePoint и другим приложениям предоставляется только соответствующим устройствам.

## <a name="choose-the-device-management-solution-thats-right-for-you"></a>Выбор оптимального решения по управлению устройствами

Существует несколько подходов к решению вопроса об управлении устройствами. Во-первых, для управления различными аспектами устройств можно использовать все встроенные возможности Intune. Этот подход называется **управлением мобильными устройствами (MDM)** . В этом случае пользователи регистрируют свои устройства и взаимодействуют с Intune с помощью сертификатов. ИТ-администратор может отправлять приложения на устройства, ограничивать устройства определенной операционной системой, блокировать личные устройства и многое другое. Если устройство будет потеряно или украдено, с него можно удалить все данные.

Второй подход заключается в управлении приложениями на устройствах. Этот подход называется **управлением мобильными приложениями (MAM)** . В этом случае пользователи обращаются к ресурсам организации со своих личных устройств. При открытии приложения, например электронной почты или SharePoint, пользователям предлагается пройти дополнительную проверку подлинности. Если устройство будет потеряно или украдено, вы можете удалить все данные организации из приложений Microsoft Intune.

Также можно использовать сочетание [MDM и MAM](byod-technology-decisions.md).

При настройке Intune для управления устройствами можно выбрать только портал Azure или комбинацию Intune и Microsoft 365. [Перенос управления мобильными устройствами в Intune на портале Azure](https://www.microsoft.com/itshowcase/Article/Content/1042/Migrating-mobile-device-management-to-Intune-in-the-Azure-portal) — это пример использования ИТ в Майкрософт. Мы рассмотрим, как ИТ-отдел Майкрософт использовал современный подход к управлению устройствами, и узнаем про сделанные выводы.

## <a name="simplify-it-tasks-using-the-device-management-admin-center"></a>Упрощение ИТ-задач с помощью центра администрирования "Управление устройствами"

[Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) — это централизованное средство для выполнения и администрирования задач для мобильных устройств. В этой рабочей области находятся службы, используемые для управления устройствами, включая Intune и Azure Active Directory, а также для управления клиентскими приложениями.

В центре администрирования "Управление устройствами" можно выполнять приведенные ниже задачи.

- [Регистрация устройств](../enrollment/device-enrollment.md)
- [Задание соответствия устройства требованиям](../protect/device-compliance-get-started.md)
- [Управление устройствами](../remote-actions/device-management.md)
- [Управление приложениями](../apps/app-management.md)  
- [Электронные книги по iOS](../apps/vpp-ebooks-ios.md)  
- [Установка локального соединителя Exchange](../protect/exchange-connector-install.md)  
- [Управление ролями](role-based-access-control.md)  
- Управление обновлениями программного обеспечения
  - [Управление обновлениями Windows 10](../protect/windows-update-for-business-configure.md)  
  - [Управление обновлениями iOS и iPadOS](../protect/software-updates-ios.md)  
- [Azure Active Directory](https://docs.microsoft.com/azure/active-directory)  
- [Управление пользователями](https://docs.microsoft.com/azure/active-directory/fundamentals/add-users-azure-active-directory)
- [Управление группами и членами](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups)
- [Устранение проблем](help-desk-operators.md)

## <a name="next-steps"></a>Дальнейшие действия

Когда вы будете готовы начать работу с решением MDM и MAM, настроить Intune, зарегистрировать устройства и приступить к созданию политик, см. сведения в статье [Управление мобильными устройствами для Microsoft 365](https://docs.microsoft.com/microsoft-365/enterprise/mobility-infrastructure).
