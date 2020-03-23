---
title: Краткое руководство — бесплатная пробная версия Microsoft Intune
titleSuffix: ''
description: В этом кратком руководстве вы создадите бесплатную пробную подписку, ознакомитесь с поддерживаемыми конфигурациями и требованиями к сети, а также при необходимости настроите доменное имя.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/16/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 195931c0-8208-43bd-b0af-b1f8e469a32c
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 83107121b05b2126e4c6b2b377baf57ee069f917
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79343990"
---
# <a name="quickstart-try-microsoft-intune-for-free"></a>Краткое руководство. Бесплатная пробная версия Microsoft Intune

Microsoft Intune помогает вам защищать корпоративные данные ваших сотрудников, управляя устройствами и приложениями. В этом кратком руководстве вы создадите бесплатную подписку, чтобы опробовать Intune в тестовой среде.

Intune предоставляет надежную облачную службу для управления мобильными устройствами (MDM) и мобильными приложениями (MAM), администрирование которой осуществляется в Центре администрирования Microsoft Endpoint Manager. Благодаря Intune обеспечиваются правильная настройка корпоративных ресурсов сотрудников (данных, устройств и приложений), доступ к ним и их обновление в соответствии с политиками и требованиями организации.

## <a name="prerequisites"></a>Предварительные условия
Перед настройкой Microsoft Intune изучите следующие требования.

- [Поддерживаемые операционные системы и браузеры](supported-devices-browsers.md)
- [Требования к конфигурации сети и ее пропускная способность](network-bandwidth-use.md)

## <a name="sign-up-for-a-microsoft-intune-free-trial"></a>Регистрация для использования бесплатной пробной версии Microsoft Intune

Пробная версия Intune предоставляется бесплатно на 30 дней. Если уже есть рабочая или учебная учетная запись, выполните **вход** под этой учетной записью и добавить в свою подписку Intune. Если же нет, **зарегистрируйте** новую учетную запись для использования Intune в своей организации.

> [!IMPORTANT]
> Зарегистрировав новую учетную запись, вы не сможете объединить ее с уже существующей рабочей или учебной учетной записью.

1. Перейдите на страницу [пробной версии Microsoft Intune](https://go.microsoft.com/fwlink/?linkid=2019088) и заполните форму.

    ![Снимок экрана веб-страницы для регистрации пробной учетной записи Microsoft Intune](./media/free-trial-sign-up/account-sign-up-site-full-browser.png)

    Если большая часть ваших ИТ-операций и пользователей поддерживают региональные параметры, отличные от ваших, эти параметры можно задать в раскрывающемся списке **Страна или регион**. Azure использует сведения о регионе для предоставления соответствующих услуг. Этот параметр невозможно будет изменить позднее.

2. Создайте учетную запись, указав название организации, за которым следует **.onmicrosoft.com**. 

    ![Снимок экрана: ввод новых учетных данных для пробной учетной записи Intune](./media/free-trial-sign-up/account-sign-up-site-user-id.png)

    Если у вашей организации есть личный домен, который вы хотите использовать без **.onmicrosoft.com**, вы можете внести это изменение в Центре администрирования Microsoft 365, как описано далее в этой статье.

3. По завершении регистрации просмотрите сведения о новой учетной записи.

    ![Изображение со сведениями об учетной записи](./media/free-trial-sign-up/intune-end-of-sign-up-process.png) 

## <a name="sign-in-to-intune-in-the-microsoft-endpoint-manager"></a>Вход в Intune с помощью Microsoft Endpoint Manager

Если вы еще не вошли на портал, выполните следующие действия:

1. Откройте новое окно браузера и введите в адресной строке **https://devicemanagement.microsoft.com** . 
2. Используйте идентификатор пользователя, приведенный в шагах выше, чтобы войти в систему ( *yourID@yourdomain* .onmicrosoft.com).

    ![Изображение страницы входа на портал](./media/free-trial-sign-up/azure-portal-signin.png)

При регистрации для использования пробной версии на электронный адрес, указанный в процессе регистрации, отправляется сообщение с информацией об учетной записи. Оно является подтверждением активации пробной версии.

> [!TIP]
> При работе с Microsoft Endpoint Manager вы можете добиться лучших результатов, работая с браузером в обычном, а не защищенном режиме.

## <a name="confirm-the-mdm-authority-in-intune"></a>Подтверждение центра MDM в Intune

По умолчанию центр MDM задается при создании бесплатной пробной версии. Вы можете подтвердить, что центр MDM задан, выполнив указанные ниже действия:

1. Если вы еще не выполнили вход, войдите в Microsoft Endpoint Manager.
2. Щелкните **Администрирование клиента**.
3. Просмотрите сведения о клиенте. В качестве **центра MDM** необходимо использовать **Microsoft Intune**.

Если после входа в Microsoft Endpoint Manager вы видите оранжевый баннер, указывающий, что центр MDM не настроен, вы можете активировать его прямо сейчас. Параметр центра управления мобильными устройствами (MDM) определяет способ администрирования устройств. Необходимо настроить центр MDM, чтобы пользователи могли регистрировать устройства для управления.

### <a name="to-set-the-mdm-authority-to-intune-follow-these-steps"></a>Чтобы изменить центр MDM на Intune, выполните указанные ниже действия.

1. Откройте новое окно браузера и введите в адресной строке **https://portal.azure.com** . 
2. Выберите **Все службы** > **Microsoft Intune**.
3. Нажмите на баннер, указывающий, что вы не включили управление устройствами. Если вы не видите баннер, нажмите **Регистрация устройств**. Откроется колонка **Выберите центр MDM**, если вы еще не включили управление устройствами.

    > [!NOTE]
    > Если вы задали центр MDM, соответствующее значение будет отображаться в колонке **Регистрация устройства**. Оранжевый баннер отображается только в том случае, если вы еще не установили центр MDM. 

    ![Изображение колонки "Выбор центра MDM"](./media/free-trial-sign-up/choose-mdm-authority.png) 

4. Если центр MDM не задан, в разделе **Выбор центра MDM** укажите **Центр MDM в Intune**.

Сведения о настройке центра MDM см. в разделе [Настройка центра управления мобильными устройствами](mdm-authority-set.md).

## <a name="configure-your-custom-domain-name-optional"></a>Настройка личного доменного имени

Как было сказано выше, если у организации есть личный домен, который вы хотите использовать без **.onmicrosoft.com**, домен можно изменить в Центре администрирования Microsoft 365. Добавление, проверка и настройка имени личного домена осуществляются следующим образом.  

> [!IMPORTANT]
> Нельзя переименовать или удалить *исходное* доменное имя **onmicrosoft.com**. Однако вам доступно добавление, проверка и переименование *личных* доменных имен, используемых в Intune и позволяющих идентифицировать вашу организацию. Дополнительные сведения см. в разделе [Настройка имени домена](custom-domain-name-configure.md).

1. Откройте [Центр администрирования Microsoft 365](https://admin.microsoft.com) и войдите под учетной записью администратора.

2. В области навигации выберите **Настройка** > **Домены** > **Добавить домен**.

3. Введите личное доменное имя. Нажмите кнопку **Далее**.

   ![Снимок экрана Центра администрирования Microsoft 365: добавление домена](./media/free-trial-sign-up/domain-custom-add.png)

4. Подтвердите владение доменом, указанным в предыдущем шаге. 
    
    Если выбрать **отправить код по почте**, сообщение электронной почты будет отправлено зарегистрированному контактному лицу, связанному с вашим доменом. Получив сообщение, скопируйте код и введите его в поле **Введите код проверки**. Если код проверки верный, домен будет добавлен в ваш клиент. Отображаемый адрес электронной почты может быть незнакомым. Некоторые регистраторы скрывают действительный адрес электронной почты. Адрес электронной почты также может отличаться от адреса, указанного при регистрации домена.

   ![Снимок экрана Центра администрирования Microsoft 365: проверка домена](./media/free-trial-sign-up/domain-custom-verify.png)

   > [!NOTE]
   > Сведения о подтверждении записи типа TXT см. в статье [Создание записи DNS для любого поставщика услуг размещения DNS для Office 365](https://support.office.com/article/Create-DNS-records-at-any-DNS-hosting-provider-for-Office-365-7B7B075D-79F9-4E37-8A9E-FB60C1D95166).

## <a name="admin-experiences"></a>Интерфейс администратора

Есть два портала, которые вы будете использовать наиболее часто:
- Центр администрирования Microsoft Endpoint Manager ([https://devicemanagement.microsoft.com/](https://devicemanagement.microsoft.com/)) — здесь можно просматривать [возможности Intune](what-is-intune.md). Это место, где администратор будет работать с Intune.
- Центр администрирования Microsoft 365 ([https://admin.microsoft.com](https://admin.microsoft.com)) позволяет вам добавлять пользователей и управлять ими, если для этого не используется Azure Active Directory. Здесь также можно управлять и другими функциями учетной записи, включая выставление счетов и предоставление поддержки.

## <a name="next-steps"></a>Дальнейшие шаги

В этом кратком руководстве вы создали бесплатную подписку, чтобы опробовать Intune в тестовой среде. Для получения дополнительных сведений о настройке Intune см. [эту статью](setup-steps.md).

Чтобы выполнить эту серию кратких руководств по Intune, переходите к следующему руководству.

> [!div class="nextstepaction"]
> [Краткое руководство. Создание пользователя и назначение ему лицензии](quickstart-create-user.md)