---
title: Настройка Check Point SandBlast MTD
titleSuffix: Microsoft Intune
description: Здесь приведены сведения об интеграции Intune с Check Point SandBlast Mobile Threat Defense для управления доступом к корпоративным ресурсам с мобильных устройств.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 706a4228-9bdf-41e0-b8d1-64c923dd2d2b
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: e9c1450af064caa1f7572da0ab4753e9db68484c
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989257"
---
# <a name="check-point-sandblast-mobile-threat-defense-connector-with-intune"></a>Соединитель Check Point SandBlast Mobile Threat Defense для Intune

Вы можете управлять доступом к корпоративным ресурсам с мобильных устройств посредством условного доступа на основании оценки рисков, проведенной Check Point SandBlast Mobile, — решением для защиты от угроз на мобильных устройствах, интегрированным с Microsoft Intune. Оценка рисков основана на данных телеметрии, собранных с устройств, на которых установлено приложение Check Point SandBlast Mobile.

Вы можете настроить политики условного доступа на основе оценки рисков Check Point SandBlast Mobile, реализуемой с помощью политик соответствия устройств Intune. Эти политики также можно использовать для разрешения или запрета доступа несовместимых устройств к ресурсам организации на основании обнаруженных угроз.

> [!NOTE]
> Этот поставщик защиты от мобильных угроз не поддерживается для незарегистрированных устройств.

## <a name="supported-platforms"></a>Поддерживаемые платформы

- **Android 4.1 и более поздней версии**.

- **iOS 8 и более поздние версии**

## <a name="pre-requisites"></a>Предварительные требования

- Azure Active Directory Premium

- Подписка Microsoft Intune

- Подписка на Check Point SandBlast Mobile Threat Defense
  - Дополнительные сведения см. на [веб-сайте CheckPoint SandBlast](https://www.checkpoint.com/).

## <a name="how-do-intune-and-check-point-sandblast-mobile-help-protect-your-company-resources"></a>Как Intune и Check Point SandBlast Mobile помогают защитить ресурсы вашей организации?

Мобильное приложение Check Point SandBlast Mobile для Android или iOS/iPadOS регистрирует сведения о файловой системе и сетевом стеке, а также данные телеметрии устройства и приложений (при наличии) и отправляет их в облачную службу Check Point SandBlast для вычисления риска в отношении угроз для мобильного устройства.

Политика соответствия устройств Intune включает правило Check Point SandBlast Mobile для защиты мобильных устройств от угроз, основанное на оценке рисков Check Point SandBlast. При включении этого правила Intune оценивает соответствие устройства заданной политике. Если устройство определяется как несоответствующее, его доступ к таким ресурсам, как Exchange Online и SharePoint Online, блокируется. Пользователи заблокированных устройств получают от мобильного приложения Check Point SandBlast Mobile рекомендации по устранению проблемы и восстановлению доступа к корпоративным ресурсам.

Далее приведены некоторые распространенные сценарии.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Управление доступом на основании оценки угроз от вредоносных приложений

При обнаружении на устройствах вредоносного ПО можно заблокировать до устранения угрозы следующие функции.

- Подключение к корпоративной электронной почте

- Синхронизация корпоративных файлов с помощью приложения OneDrive для работы

- Доступ к приложениям организации

*Блокировка при обнаружении вредоносных программ:*

> [!div class="mx-imgBorder"]
> ![Блокировка Check Point MTD при обнаружении вредоносных программ](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-2.PNG)

*Доступ предоставлен после устранения угрозы:*

> [!div class="mx-imgBorder"]
> ![Предоставлен доступ Check Point MTD](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-3.PNG)

### <a name="control-access-based-on-threat-to-network"></a>Управление доступом на основе угроз для сети

Обнаружение угроз типа **злоумышленник в середине** и защита доступа к сетям Wi-Fi на основе рисков для устройств.

*Блокировка доступа к сети через Wi-Fi:*

> [!div class="mx-imgBorder"]
> ![Блокировка Check Point MTD доступа к сети через Wi-Fi](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-4.PNG)

*Доступ предоставлен после устранения угрозы:*

> [!div class="mx-imgBorder"]
> ![Предоставлен доступ Check Point MTD к сети Wi-Fi](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-5.PNG)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Управление доступом к SharePoint Online на основании оценки угрозы для сети

Обнаружение угроз типа **злоумышленник в середине** и предотвращение синхронизации корпоративных файлов на основе риска для устройств.

*Блокирование SharePoint Online при обнаружении сетевых угроз:*

> [!div class="mx-imgBorder"]
> ![Блокировка Check Point MTD доступа к SharePoint Online](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-6.PNG)

*Доступ предоставлен после устранения угрозы:*

> [!div class="mx-imgBorder"]
> ![Предоставлен доступ Check Point MTD к SharePoint Online](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-7.PNG)

<!-- ### Control access on unenrolled devices based on threats from malicious apps

When the Check Point Sandblast Mobile Threat Defense solution considers a device to be infected:
> [!div class="mx-imgBorder"]
> ![App protection policy blocks due to detected malware](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-block.png)

Access is granted on remediation:

> [!div class="mx-imgBorder"]
> ![Access is granted on remediation for App protection policy](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Дальнейшие действия

- [Интеграция CheckPoint SandBlast с Intune](checkpoint-sandblast-mobile-mtd-connector-integration.md)

- [Настройка приложения CheckPoint SandBlast Mobile](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Создание политики соответствия требованиям CheckPoint SandBlast Mobile](mtd-device-compliance-policy-create.md)

- [Включение соединителя CheckPoint SandBlast Mobile MTD](mtd-connector-enable.md)
