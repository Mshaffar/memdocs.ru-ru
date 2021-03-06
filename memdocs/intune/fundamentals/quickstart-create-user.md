---
title: Краткое руководство. Создание пользователя в Intune
description: Краткое руководство. Создание пользователя в Intune.
services: microsoft-intune
author: ErikjeMS
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.topic: quickstart
ms.date: 01/17/2020
ms.author: erikje
ms.manager: dougeby
ms.assetid: 820fcb18-0927-4ebd-be79-dce92b51c261
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: cf5c76e276722fb9bab2b5d6fac511f0b22ae1f2
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "79356717"
---
# <a name="quickstart-create-a-user-in-intune-and-assign-the-user-a-license"></a>Краткое руководство. Создание пользователя в Intune и назначение ему лицензии

В этом кратком руководстве описано, как создать пользователя и назначить ему лицензию в Intune. При работе с Intune каждый пользователь, которому будет предоставлен доступ к корпоративным данным, должен иметь свою учетную запись. Позже администраторы Intune могут включить для таких пользователей возможность управления доступом.

## <a name="prerequisites"></a>Предварительные условия

- Подписка Microsoft Intune. [Зарегистрируйтесь для получения бесплатной пробной учетной записи](../fundamentals/free-trial-sign-up.md).

## <a name="sign-in-to-intune-in-microsoft-endpoint-manager"></a>Вход в Intune с помощью Microsoft Endpoint Manager

Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) в качестве [глобального администратора или администратора службы Intune](users-add.md#types-of-administrators). Если вы создали подписку на пробную версию Intune, учетная запись, с помощью которой вы создали подписку, является глобальным администратором.

## <a name="create-a-user"></a>Создание пользователя

Для регистрации в системе управления устройствами Intune пользователю нужна учетная запись. Чтобы создать пользователя, сделайте следующее:

1. В Microsoft Endpoint Manager выберите **Пользователи**>**Все пользователи**>**Новый пользователь**:  ![Выбор параметра "Новый пользователь" в Microsoft Endpoint Manager](./media/quickstart-create-user/create-user.png)
2. В поле **Имя** введите имя, например *Dewey Kellum*:  ![Добавление сведений о пользователе](./media/quickstart-create-user/create-user-02.png)
3. В поле **Имя пользователя** введите идентификатор пользователя, например Dewey@contoso.onmicrosoft.com.

    > [!NOTE]
    > Если вы еще не настроили доменное имя клиента, используйте имя проверенного домена, который использовался для создания подписки Intune (или [бесплатной пробной версии](free-trial-sign-up.md#sign-up-for-a-microsoft-intune-free-trial)). 

4. Выберите **Показать пароль** и запомните автоматически созданный пароль, который потребуется для входа на тестовое устройство.
5. Щелкните **Создать**.

## <a name="assign-a-license-to-the-user"></a>Назначение лицензии пользователю

Создав пользователя, назначьте ему лицензию Intune в [Центре администрирования Microsoft 365](https://go.microsoft.com/fwlink/p/?LinkId=698854). Если не назначить пользователю лицензию, он не сможет регистрировать свои устройства в Intune.

Чтобы назначить лицензию Intune пользователю, сделайте следующее:

1. Войдите в [Центр администрирования Microsoft 365](https://go.microsoft.com/fwlink/p/?LinkId=698854) с теми же учетными данными, с которыми входили в Intune.
2. Выберите **Пользователи** > **Активные пользователи**, а затем выберите только что созданного пользователя.
3. Выберите вкладку **Лицензии и приложения**.
4. В разделе **Выберите расположение** выберите расположение для пользователя, если оно еще не задано.
2. Установите флажок **Intune** в разделе **Лицензии**. Вы можете выбрать другую лицензию, если она включает Intune. Отображаемое [название продукта](https://docs.microsoft.com/azure/active-directory/users-groups-roles/licensing-service-plan-reference) используется в качестве плана обслуживания в управлении Azure.

    ![Выбор расположения и лицензии Intune](./media/quickstart-create-user/create-user-03.png)

   > [!NOTE]
   > Этот параметр использует одну из ваших лицензий для пользователя. При использовании пробной версии затем нужно переназначить эту лицензию для реального пользователя в реальной среде.

6. Выберите **Сохранить изменения**.

Будет отображаться, что новый активный пользователь Intune использует лицензию **Intune**.

## <a name="clean-up-resources"></a>Очистка ресурсов

Если этот пользователь больше не нужен, вы можете удалить его, перейдя в [Центр администрирования Microsoft 365](https://go.microsoft.com/fwlink/p/?LinkId=698854) и выбрав **Пользователи** > *выберите этого пользователя* > *щелкните значок "Удалить пользователя"*  > **Удалить пользователя** > **Закрыть**.

   ![Щелкните значок "Удалить"](./media/quickstart-create-user/create-user-04.png)

## <a name="next-steps"></a>Дальнейшие шаги

В этом кратком руководстве вы создали пользователя и назначили ему лицензию в Intune. Дополнительные сведения о добавлении пользователей в Intune см. в разделе [Добавление пользователей и предоставление административных разрешений для Intune](users-add.md).

Чтобы продолжить эту серию кратких руководств по Intune, перейдите к следующему руководству:

> [!div class="nextstepaction"]
> [Краткое руководство. Создание группы для управления пользователями](quickstart-create-group.md)
