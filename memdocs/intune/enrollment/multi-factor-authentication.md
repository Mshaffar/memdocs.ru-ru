---
title: Настройка обязательной многофакторной проверки подлинности для регистрации устройств в Intune
titleSuffix: Microsoft Intune
description: Как настроить обязательную многофакторную проверку подлинности в Azure AD для регистрации устройств в Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 94280c73-c05c-4e72-b0dd-a7cb997782f9
ROBOTS: ''
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2ec03d186b0b5d64b5b867cf413f477d9ded79e9
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79345108"
---
# <a name="require-multi-factor-authentication-for-intune-device-enrollments"></a>Настройка обязательной многофакторной проверки подлинности для регистрации устройств в Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune использует многофакторную идентификацию (MFA) Azure Active Directory (AD) при регистрации устройств для защиты корпоративных ресурсов.

В MFA используются любые два (или более) из следующих способов проверки подлинности:

- что-то, что вы знаете (обычно пароль или ПИН-код);
- что-то, что у вас есть (доверенное устройство, которое сложно продублировать, например телефон);
- что-то ваше (биометрические данные, например отпечаток пальца).

MFA поддерживается на устройствах под управлением iOS, iPadOS, Android, Windows 8.1 и более поздних версий, а также Windows Phone 8.1 и Windows 10 Mobile или более поздних версий.

При включении MFA конечные пользователи должны указать два вида учетных данных для регистрации устройства.

## <a name="configure-intune-to-require-multi-factor-authentication-at-device-enrollment"></a>Настройка в Intune обязательной многофакторной проверки подлинности при регистрации устройств

Если требуется многофакторная проверка подлинности при регистрации устройства, выполните следующие действия.

>[!Important]
>Для реализации этой политики пользователям необходимо назначить план Azure Active Directory Premium P1 или более высокого уровня.

>[!Important]
>Не устанавливайте **правила доступа на основе устройств** для регистрации в Microsoft Intune.

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), выберите **Устройства** > **Условный доступ**. Узел условного доступа, доступ к которому осуществляется из *Intune*, является тем же узлом, доступ к которому осуществляется из *Azure AD*.
2. Выберите **Создать политику**.
3. В поле **Новая** введите описательное имя для политики.
4. В разделе **Назначения** выберите **Пользователи и группы**. 
5. В разделе **Пользователи и группы** выберите **Выбрать пользователей или группы** и установите флажок **Пользователи и группы**. Затем выберите пользователей или группы, которые будут получать эту политику, и нажмите кнопку **Готово**.
6. В разделе **Назначения** выберите **Облачные приложения**.
7. На вкладке **Включить** раздела **Облачные приложения** выберите **Выбрать приложения**, затем — **Выбрать** > **Регистрация в Microsoft Intune**, после чего нажмите кнопку **Готово**. Выбирая **Соглашение о регистрации Microsoft Intune**, условный доступ MFA применяется только к регистрации устройства (одноразовый запрос MFA).
8. В разделе **Назначения** не нужно настраивать никакие параметры для MFA в поле **Условия**.
9. В разделе **Элементы управления доступом** выберите **Предоставление**.
10. В разделе **Предоставление** выберите **Предоставить доступ**, а затем — **Требовать многофакторную идентификацию**. Не выбирайте параметр **Требовать, чтобы устройство было отмечено как соответствующее**, так как устройство может быть проверено на соответствие только после его регистрации. Затем выберите **Выбрать**.
11. В разделе **Новая политика** выберите **Включить политику** > **Включить**, а затем щелкните **создать**.



## <a name="next-steps"></a>Дальнейшие шаги

Когда конечный пользователь регистрирует свое устройство, он должен пройти проверку подлинности с использованием второй формы идентификации, например ПИН-кода, телефона или биометрических данных.