---
title: Процесс адаптации Intune
titleSuffix: Microsoft Intune
description: В этой статье содержатся все сведения, которые необходимо учитывать при адаптации чисто облачного решения Microsoft Intune в своей среде.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ac7bd764-5365-4920-8fd0-ea57d5ebe039
ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8396a9713e5ce4b6001aefb55485a908f0e605dd
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "79357666"
---
# <a name="implement-your-microsoft-intune-plan"></a>План внедрения Microsoft Intune

На этапе адаптации вы внедряете Intune в свою рабочую среду. Процесс внедрения состоит из установки и настройки Intune и внешних зависимостей (при необходимости) с учетом ваших [требований к вариантам использования](planning-guide-requirements.md).

Следующий раздел содержит обзор процесса внедрения Intune, включающего в себя требования и высокоуровневые задачи.

## <a name="intune-requirements"></a>Требования для Intune

Основные требования к автономной версии Intune:

- Подписка на Enterprise Mobility + Security (EMS)/Intune

- Подписка Office 365 (для приложений Office и приложений под управлением политики защиты приложений)

- Сертификат APNs Apple (для включения управления платформой устройств iOS/iPadOS)

- Azure AD Connect (для синхронизации службы каталогов)

- Локальный соединитель Intune для Exchange (обеспечивает условный доступ для локальной организации Exchange, если это необходимо)

- Intune Certificate Connector (для развертывания сертификата SCEP, если это необходимо)

>[!TIP]
> Полный список устройств, которыми можно управлять с помощью Intune, см. в списке [поддерживаемых устройств](supported-devices-browsers.md).

## <a name="intune-implementation-process"></a>Процесс внедрения Intune

Мы определили 13 отдельных задач по развертыванию Intune. В зависимости от требований, существующей инфраструктуры и стратегии управления устройствами в вашей организации некоторые из этих задач могут быть уже выполнены. Какие-то задачи могут не касаться вашего плана.

### <a name="task-1-get-an-intune-subscription"></a>Задача 1. Получение подписки Intune

Как указано в предыдущем разделе о требованиях Intune, необходима подписка на EMS или Intune. Если у вашей организации нет такой подписки, обратитесь в корпорацию Майкрософт или службу учетных записей Майкрософт и сообщите, что хотите приобрести Enterprise Mobility + Security (EMS) или Intune.

- Дополнительные сведения о том, [как приобрести Microsoft Intune](https://www.microsoft.com/cloud-platform/microsoft-intune-pricing).

### <a name="task-2-add-office-365-subscription"></a>Задача 2. Добавление подписки Office 365

Этот шаг не является обязательным. Подписка на Office 365 необходима в том случае, если вы планируете использовать Exchange Online и управлять мобильными приложениями Office с помощью политик защиты приложений. Если у вашей организации нет такой подписки, обратитесь в корпорацию Майкрософт или службу технической поддержки учетных записей Майкрософт и сообщите, что хотите приобрести Office 365.

- Дополнительные сведения о том, [как приобрести Office 365](https://products.office.com/business/compare-office-365-for-business-plans).

### <a name="task-3-add-users-groups-in-azure-ad"></a>Задача 3. Добавление групп пользователей в Azure AD

В зависимости от ваших требований и сценариев использования Intune может понадобиться добавление пользователей или групп безопасности в Active Directory или Azure Active Directory. Просмотрите текущих пользователей и группы безопасности в Active Directory или Azure Active Directory и определите, полностью ли они соответствуют вашим потребностям. Новых пользователей и группы безопасности рекомендуем добавлять в Active Directory и синхронизировать с Azure Active Directory с помощью Azure AD Connect.

- Дополнительные сведения о том, [как добавить пользователей или групп в Intune](users-add.md).
<!---why not send them to the AAD connect topic? Question out to Andre: https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect--->


### <a name="task-4-assign-intune-and-office-365-user-licenses"></a>Задача 4. Назначение пользовательских лицензий Intune и Office 365

Всем пользователям, которых затронет развертывание EMS/Intune и Office 365, необходимо назначить лицензию. Назначить лицензии EMS/Intune и Office 365 можно на портале Центра администрирования Microsoft 365.

- Дополнительные сведения о том, [как назначить лицензии Intune](licenses-assign.md).

### <a name="task-5-set-mobile-device-management-authority-to-intune"></a>Задача 5. Задание Intune в качестве центра управления мобильными устройствами

Перед началом установки, настройки, регистрации устройств и управления ими с помощью Intune следует задать Intune в качестве центра управления устройствами.

- Дополнительные сведения о том, как задать центр управления устройствами, см. [здесь](mdm-authority-set.md).

### <a name="task-6-enable-device-platforms"></a>Задача 6. Включение платформ устройств

По умолчанию большинство платформ устройств, кроме устройств Apple (iOS/iPadOS и Mac), включены. Прежде чем можно будет регистрировать устройства iOS/iPadOS в Intune и управлять ими, требуется включить эту платформу устройств. Для этого необходимо создать сертификат MDM Push и добавить его в Intune.

- Дополнительные сведения о включение устройств Apple для регистрации см. [здесь](../enrollment/apple-mdm-push-certificate-get.md).

### <a name="task-7-add-and-deploy-terms-and-conditions-policies"></a>Задача 7. Добавление и развертывание политик условий

Intune поддерживает политики условий. Добавьте нужные политики условий и разверните их в целевых группах с учетом требований и вариантов использования для развертывания Intune.

- Дополнительные сведения о том, [как добавить и развернуть политики условий](../enrollment/terms-and-conditions-create.md).

### <a name="task-8-add-and-deploy-configuration-policies"></a>Задача 8. Добавление и развертывание политик конфигурации

Intune поддерживает два типа политик конфигурации — общие и настраиваемые. Добавьте нужные политики конфигурации и разверните их в целевых группах с учетом требований и вариантов использования для развертывания Intune.

- Дополнительные сведения о том, [как добавить и развернуть политики конфигурации](../configuration/device-profiles.md).

### <a name="task-9-add-and-deploy-resource-profiles"></a>Задача 9. Добавление и развертывание профилей ресурсов

Intune поддерживает профили электронной почты, Wi-Fi и VPN. Добавьте нужные профили и разверните их в целевых группах с учетом требований и вариантов использования для развертывания Intune.

- Дополнительные сведения о том, как обеспечить доступ к ресурсам организации с помощью Intune, см. [здесь](../configuration/device-profiles.md).

### <a name="task-10-add-and-deploy-apps"></a>Задача 10. Добавление и развертывание приложений

Intune поддерживает развертывание веб-приложений, бизнес-приложений и приложений, опубликованных в магазине. Кроме того, приложениями с интегрированным пакетом SDK Intune можно управлять, сопоставив их с политиками защиты приложений. Добавьте нужные приложения и разверните их в целевых группах с учетом требований и вариантов использования для развертывания Intune.

- Дополнительные сведения о добавлении и развертывании приложений см. [здесь](../apps/app-management.md).

### <a name="task-11-add-and-deploy-compliance-policies"></a>Задача 11. Добавление и развертывание политик соответствия

Intune поддерживает политики соответствия. Добавьте нужные политики соответствия и разверните их в целевых группах с учетом требований и вариантов использования для развертывания Intune.

- Дополнительные сведения о [политиках соответствия требованиям](../protect/device-compliance-get-started.md).

### <a name="task-12-enable-conditional-access-policies"></a>Задача 12. Включение политик условного доступа

Intune поддерживает условный доступ к Exchange Online и локальной организации Exchange, SharePoint Online, Skype для бизнеса Online и Dynamics CRM Online. Включите и настройте нужные политики условного доступа с учетом требований и вариантов использования для развертывания Intune.

- Дополнительные сведения об [условном доступе](../protect/conditional-access.md).

### <a name="task-13-enroll-devices"></a>Задача 13. регистрации устройств;

Intune поддерживает платформы настольных и мобильных устройств Windows, iOS/iPadOS, Mac OS, Android. Зарегистрируйте нужные платформы мобильных устройств с учетом требований и вариантов использования для развертывания Intune.

- Дополнительные сведения о том, [как зарегистрировать устройства](../enrollment/device-enrollment.md).


## <a name="next-steps"></a>Дальнейшие шаги
Рекомендации по тестированию и проверке развертывания Intune см. [здесь](planning-guide-test-validation.md).
