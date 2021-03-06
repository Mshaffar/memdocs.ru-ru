---
title: Краткое руководство. Регистрация устройства Windows 10 Desktop в Microsoft Intune
description: Краткое руководство. Использование корпоративного портала для регистрации устройств Windows 10 Desktop в Microsoft Intune
services: microsoft-intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/30/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 658a7655-a6df-4dbe-b56c-22c7fc60e706
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4f70c8487d9cb30b2a7cced63e6e019541f73704
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327052"
---
# <a name="quickstart-enroll-your-windows-10-device"></a>Краткое руководство. Регистрация устройства Windows 10

В этом кратком руководстве вы возьмете на себя роль пользователя Intune и зарегистрируете устройство Windows 10 в Microsoft Intune. Затем вы вернетесь в Intune и подтвердите зарегистрированное устройство.

Регистрация устройств в Microsoft Intune позволяет устройствам Windows 10 получить доступ к защищенным данным организации, включая электронную почту, файлы и другие ресурсы. Это справедливо как для устройств с ОС Windows 10 Desktop, так и для устройств с ОС Windows 10 Mobile. Регистрация устройств позволяет защитить доступ как для вас, так и для вашей организации, и помогает отделить рабочие данные от персональных.

> [!TIP]
> Узнайте, что происходит при [регистрации устройства в Intune](../user-help/what-happens-if-you-install-the-company-portal-app-and-enroll-your-device-in-intune-windows.md) и что это означает для [сведений на устройстве](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md).

Если у вас нет подписки Intune, [зарегистрируйтесь для получения бесплатной пробной учетной записи](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Предварительные условия

- Подписка Microsoft Intune: [зарегистрируйтесь для получения бесплатной пробной учетной записи](../fundamentals/free-trial-sign-up.md).
- Для выполнения этого краткого руководства необходимо выполнить процедуру [настройки автоматической регистрации в Intune](quickstart-setup-auto-enrollment.md).

## <a name="confirm-your-windows-10-desktop-version"></a>Проверка версии Windows 10 Desktop

Перед регистрацией устройства Windows 10 Desktop необходимо проверить версию Windows.

1. Щелкните правой кнопкой мыши значок **Пуск** Windows и выберите **Параметры**, чтобы просмотреть параметры Windows.

   ![Снимок экрана: "Параметры Windows" — "Система"](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-01.png)

2. Выберите **Система** > **О системе**. 

   ![Снимок экрана: параметры системы](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-02.png)

    > [!TIP]
    > Также можно ввести фразу "О компьютере" в **строке поиска**, а затем выбрать **О компьютере**.

3. В окне **Параметры** вы увидите список **Характеристики Windows**. В этом списке найдите пункт **Версия**.

4. Убедитесь, что значение **версии** Windows 10 — **1607 или выше**.

    > [!IMPORTANT]
    > Действия, описанные в этом кратком руководстве, предназначены для версии Windows 10 **1607 или более поздней**. Если ваша версия — **1511 или ниже**, перейдите к [этой процедуре](../user-help/enroll-windows-10-device.md).  

## <a name="enroll-windows-10-desktop"></a>Регистрация Windows 10 Desktop

1. Перейдите в раздел "Параметры Windows" и выберите **Учетные записи**.

   ![Снимок экрана: "Параметры системы" — "Учетные записи"](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-03.png)

2. Выберите **Доступ к рабочей или учебной учетной записи** > **Подключить**.

    ![Доступ к рабочей или учебной учетной записи](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-04.png)

3. Выполните вход в Intune через рабочую или учебную учетную запись и выберите **Далее**. Если вы выполнили краткое руководство по [созданию пользователя и назначению лицензии](../fundamentals/quickstart-create-user.md), вы можете войти с помощью созданной вами учетной записи пользователя.

    > [!NOTE]
    > Если вы настроили имя домена ".onmicrosoft.com", в адресе учетной записи будет часть **.onmicrosoft.com**. 

   ![Введите рабочую или учебную учетную запись](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-05.png)

    Появится сообщение о том, что устройство регистрируется в вашей компании или учебном заведении.

4. При появлении страницы **Новые функции готовы к использованию!** нажмите кнопку **Готово**. Все готово.

5. Добавленная учетная запись будет отображаться в разделе параметров **Доступ к рабочей или учебной записи** на устройстве Windows Desktop.

   ![Снимок экрана: добавленная учетная запись](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-06.png)

    Если вы выполнили описанные выше действия, но по-прежнему не можете получить доступ к рабочей или учебной учетной записи электронной почты и файлам, выполните инструкции из раздела [Устранение неполадок при появлении элемента "Доступ к учетной записи места работы или учебного заведения"](../user-help/troubleshoot-your-windows-10-device-windows.md#troubleshooting-steps-to-follow-if-you-see-access-work-or-school).

## <a name="confirm-your-device-enrollment-in-intune"></a>Проверка регистрации устройства в Intune

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) в качестве глобального администратора или администратора службы Intune.
2. Выберите **Устройства** > **Все устройства**, чтобы просмотреть зарегистрированные устройства в Intune.
3. Убедитесь, что появилось дополнительное устройство, зарегистрированное в Intune.

   ![Снимок экрана: устройства, зарегистрированные в Intune](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-07.png)

## <a name="clean-up-resources"></a>Очистка ресурсов

Сведения об отмене регистрации устройства Windows см. в разделе [Удаление устройства Windows из системы управления](../user-help/unenroll-your-device-from-intune-windows.md).

## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве вы узнали, как зарегистрировать устройство Windows 10 в Intune. Вы также можете изучить другие способы регистрации устройств на всех платформах. Дополнительные сведения об использовании устройств с помощью Intune см. в разделе [Использование управляемых устройств для выполнения задач](../user-help/use-managed-devices-to-get-work-done.md).

Чтобы выполнить эту серию кратких руководств по Intune, переходите к следующему руководству.

> [!div class="nextstepaction"]
> [Краткое руководство по настройке требуемой длины пароля для устройств Android](../protect/quickstart-set-password-length-android.md)
