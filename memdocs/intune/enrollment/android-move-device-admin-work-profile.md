---
title: Перевод устройств Android с управления администратором устройств на управление рабочими профилями
titleSuffix: Microsoft Intune
description: Перевод устройств Android с управления администратором устройств на управление рабочими профилями в Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f16c39ff0af44918099863be5d23ec9fe564493
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "80624915"
---
# <a name="move-android-devices-from-device-administrator-to-work-profile-management"></a>Перевод устройств Android с управления администратором устройств на управление рабочими профилями

Чтобы помочь пользователям перевести свои устройства Android с управления администратором устройств на управление рабочими профилями, используйте параметр соответствия **Block devices managed with device administrator** (Блокировать устройства, управляемые администратором устройств). При включении этого параметра устройство перестает соответствовать требованиям, если им управляет администратор устройств. 

Когда пользователь заметит, что его устройство не соответствует требованиям по этой причине, он может коснуться кнопки **Разрешить**, чтобы выполнить следующие действия на основе контрольного списка:
1. Отмена регистрации в управлении администраторами устройств
2. Регистрация в управлении рабочими профилями.
3. Решение проблем с совместимостью. 

## <a name="prerequisites"></a>Предварительные условия

- Пользователям следует использовать [устройства Android под управлением администратора устройств](android-enroll-device-administrator.md) с установленным приложением "Корпоративный портал" для Android версии 5.0.4720.0 или более поздней.
- Настройте управление рабочими профилями Android, [подключив учетную запись клиента Intune к учетной записи Android для бизнеса](connect-intune-android-enterprise.md).
- [Настройте регистрацию рабочих профилей Android для бизнеса](android-work-profile-enroll.md) для группы пользователей, которые переводятся на использование рабочего профиля Android.
- Рекомендуем увеличить пределы устройств пользователей. Возможно, при отмене управления администратором устройств соответствующие записи устройств будут удалены не сразу. Чтобы обеспечить резерв на этот период, возможно, вам понадобится увеличить предел устройств. Так пользователи смогут зарегистрировать свои устройства в управлении рабочими профилями.
  - [Настройте параметры устройств Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings), задав подходящее максимальное число устройств на пользователя.
  - Измените [предел устройств Intune](enrollment-restrictions-set.md#create-a-device-limit-restriction), задав значение параметра "Предел устройств". 

## <a name="create-device-compliance-policy"></a>Создание политики соответствия устройств

1. В [центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) выберите элементы **Устройства** > **Политики соответствия** > **Политики** > **Создать политику**.

    ![Создание политики](./media/android-move-device-admin-work-profile/create-policy.png)

2. На странице **Создать политику** задайте для параметра **Платформа** значение **Администратор устройств Android** > **Создать**.
3. На странице **Основные сведения** введите **имя** и **описание** > **Далее**.

    ![Страница "Основные сведения"](./media/android-move-device-admin-work-profile/basics.png)
    
4. На странице **Параметры соответствия** в разделе **Работоспособность устройств** установите для параметра **Block devices managed with device administrator** (Блокировать устройства, управляемые администратором устройств) значение **Да** > **Далее**.

    ![Блокировка устройств](./media/android-move-device-admin-work-profile/block-devices.png)

5. На странице **Расположения** при необходимости можно добавить расположения > **Далее**.
6. На странице **Действия при несоответствии** можно задать действие **Отправить сообщение электронной почты пользователю**.

    ![Отправка сообщения](./media/android-move-device-admin-work-profile/send-email.png)


    В текст отправляемых пользователям сообщений можно включить приведенный ниже URL-адрес. По этому URL-адресу запустится приложение "Корпоративный портал" для Android на странице **Обновить параметры устройства**. На этой странице приведены инструкции по переходу на управление рабочими профилями.
    - `https://portal.manage.microsoft.com/UpdateSettings.aspx`.
    - Для государственных организаций США можно использовать эту ссылку: `https://portal.manage.microsoft.us/UpdateSettings.aspx`.
  
    > [!NOTE]
    > - Разумеется, в сообщениях вы можете использовать понятные для пользователя гипертекстовые ссылки. Но не используйте средства сокращения URL-адресов, так как полученные с их помощью ссылки могут не работать.
    > - Если приложение "Корпоративный портал" для Android открыто и работает в фоновом режиме, возможно, по ссылке пользователь будет перенаправлен к последней странице, которую он открывал.
    > - Пользователи должны коснуться ссылки на устройстве Android. Если они вставят ссылку в браузер, Корпоративный портал Android не запустится. 

    Нажмите кнопку **Далее**.

7. На странице **Теги области** выберите теги области, которые необходимо включить.
8. На странице **Назначения** назначьте политику группе, в которой есть устройства под управлением администратора устройств > **Далее**.
9. На странице **Проверка и создание** подтвердите все параметры, а затем выберите **Создать**.

## <a name="troubleshooting"></a>Диагностика

С помощью [инструкций по переходу на новую схему управления устройством](../user-help/move-to-new-device-management-setup.md) пользователи могут отменить управление администраторами устройств и настроить управление рабочими профилями для своих устройств. Пользователям следует использовать [устройства Android под управлением администратора устройств](android-enroll-device-administrator.md) с установленным приложением "Корпоративный портал" для Android версии 5.0.4720.0 или более поздней.

### <a name="user-sees-an-error-after-tapping-resolve"></a>Для пользователя отображается сообщение об ошибке после касания кнопки "Разрешить"
Если для пользователя отображается сообщение об ошибке после касания кнопки **Разрешить**, это, скорее всего, вызвано одной из следующих причин:
- Регистрация рабочих профилей настроена неправильно (не подключена учетная запись Android для бизнеса или заданы ограничения регистрации, из-за которых регистрация рабочих профилей заблокирована).
- Устройство работает под управлением ОС Android 4.4 или более ранней версии, которая не поддерживает регистрацию рабочих профилей. 
- Производитель устройства не поддерживает регистрацию рабочих профилей для этой модели устройства.

### <a name="resolve-button-doesnt-appear-on-the-users-device"></a>Кнопка "Разрешить" не отображается на устройстве пользователя
Кнопка **Разрешить** не отображается на устройстве пользователя, если пользователь пытается перевести его на управление администратором устройств, после того как к этому устройству была применена описанная выше политика соответствия устройств.

Чтобы появилась кнопка **Разрешить**, пользователю нужно отложить настройку и перезапустить процесс, начиная с уведомления.

Во избежание такой ситуации используйте ограничения регистрации, чтобы заблокировать регистрацию для управления администратором устройств.

### <a name="user-sees-an-error-after-tapping-url-to-update-device-settings-page"></a>Для пользователя отображается сообщение об ошибке после касания URL-адреса на странице "Обновить параметры устройства"
При переходе по URL-адресу, ведущему к странице **Обновить параметры устройства** приложения "Корпоративный портал" для Android, для пользователей может отображаться страница ошибки в браузере. Эта ошибка может быть вызвана одной из следующих причин:
- устройство не является устройством Android;
- на устройстве Android не установлено приложение "Корпоративный портал";
- на устройстве установлено приложение "Корпоративный портал" для Android более ранней версии, чем 5.0.4720.0;
- устройство работает на базе ОС Android 6 или более ранней версии. 

## <a name="next-steps"></a>Дальнейшие действия
[См. поток конечного пользователя](../user-help/move-to-new-device-management-setup.md)
[Управление устройствами с рабочим профилем Android в Intune](android-enterprise-overview.md)
