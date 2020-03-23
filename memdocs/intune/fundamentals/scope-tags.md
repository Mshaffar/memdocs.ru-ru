---
title: Использование управления доступом на основе ролей (RBAC) и тегов области для распределенных ИТ в Intune | Документация Майкрософт
description: Используйте теги области для фильтрации профилей конфигурации по определенным ролям.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/06/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.technology: ''
ms.assetid: a21d3039-f2ed-4f43-b6fa-d00c071edbc4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f79b3fb2c8ef11478388bebf57b0885061be529f
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79356353"
---
# <a name="use-role-based-access-control-rbac-and-scope-tags-for-distributed-it"></a>Использование управления доступом на основе ролей (RBAC) и тегов области для распределенных ИТ

Чтобы гарантировать, что администраторы будут иметь правильные права доступа и видимости для нужных объектов Intune, можно использовать управление доступом на основе ролей и теги области. Роли определяют, какой доступ имеют администраторы, и к каким объектам. Теги области определяют, какие объекты доступны администраторам для просмотра.

Предположим, что администратору региональных офисов в Сиэтле назначена роль "Диспетчер политик и профилей". Требуется, чтобы этот администратор мог просматривать и регулировать только профили и политики, которые применяются к устройствам в Сиэтле. Чтобы настроить этот доступ, выполните следующие действия.

1. Создайте тег области Seattle.
2. Создайте назначение роли для роли "Диспетчер политик и профилей": 
    - Участники (группы) = группа безопасности с именем "Seattle IT admins". Все администраторы в этой группе будут иметь разрешение на управление для политик и профилей у пользователей или устройств в области (группах).
    - Область (группы) = группа безопасности с именем "Seattle users". Всех пользователи и устройства в этой группе могут иметь профили и политики, которые управляются администраторами из числа участников (групп). 
    - Область (теги) = Seattle. Администраторы, представляющие участников (группы), могут видеть объекты Intune, которые также имеют тег области Seattle.
3. Добавьте тег области Seattle для политик и профилей, возможность доступа к которым должны иметь администраторы, представляющие участников (группы).
4. Добавьте тег области Seattle для устройств, которые должны быть видимыми для администраторов в участниках (группах). 

## <a name="default-scope-tag"></a>Тег области по умолчанию
Тег области по умолчанию автоматически добавляется ко всем объектам без тегов, поддерживающим теги области.

Эта функция тега области по умолчанию похожа на функцию областей безопасности в Microsoft Endpoint Configuration Manager. 

## <a name="to-create-a-scope-tag"></a>Создание тега области

1. В [Центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) выберите **Администрирование клиента** > **Роли** > **Область (теги)**  > **Создать**.
2. На странице **Основы** введите **имя** и **описание** (необязательно). Нажмите кнопку **Далее**.
3. На странице **Назначения** выберите группы, содержащие устройства, которым необходимо назначить этот тег области. Нажмите кнопку **Далее**.
4. На странице **Проверка и создание** выберите **Создать**.

## <a name="to-assign-a-scope-tag-to-a-role"></a>Назначение тега области для роли

1. В [Центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) выберите **Администрирование клиента** > **Роли** > **Все роли** > выберите роль > **Назначения** > **Назначить**.
2. На странице **Основные** укажите **Имя назначения** и **Описание**. Нажмите кнопку **Далее**.
3. На странице **Группы администраторов** нажмите **Выбрать группы для включения** и выберите группы, которые должны быть включены в это назначение. Пользователи в этой группе будут иметь разрешение на управление для пользователей или устройств в области (группах). Нажмите кнопку **Далее**.

    ![Снимок экрана: выбор групп участников.](./media/scope-tags/select-member-groups.png)

4. На странице **Группы области** выберите для пункта **Назначить** один из следующих вариантов.
    - **Выбранные группы**: выберите группы, содержащие пользователей или устройства, которыми требуется управлять. Все пользователи и устройства в выбранных группах будут управляться пользователями в группах администраторов.
    - **Все пользователи**. Все пользователи могут управляться пользователями в группах администраторов.
    - **Все устройства**. Все устройства могут управляться пользователями в группах администраторов.
    - **Все пользователи и все устройства**. Все пользователи и устройства могут управляться пользователями в группах администраторов.

5. Нажмите кнопку **Далее**.
6. На странице **Теги области** выберите теги, которые вы хотите добавить в эту роль. Пользователи в группах администраторов будут иметь доступ к объектам Intune с тем же тегом области. Одной роли можно назначить не более 100 тегов области.
7. Выберите **Далее**, чтобы перейти на страницу **Проверка и создание**, и нажмите **Создать**.

## <a name="assign-scope-tags-to-other-objects"></a>Назначение тегов области другим объектам

Для объектов, поддерживающих теги области, они обычно отображаются в разделе **Свойства**. Например, чтобы назначить тег области профилю конфигурации, выполните следующие действия.

1. В [Центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) выберите **Устройства** > **Профили конфигурации** > выберите профиль.

2. Выберите **Свойства** > **Область (теги)**  > **Изменить** > **Выбрать теги область** > выберите теги, которые вы хотите добавить в профиль. Одному объекту можно назначить не более 100 тегов области.
4. Нажмите **Выбрать** > **Проверка и сохранение**.

## <a name="scope-tag-details"></a>Сведения о тегах области
При работе с тегами области помните следующее: 

- Теги области можно назначить типу объекта Intune, если клиент может иметь несколько версий этого объекта (например, назначения ролей или приложения).
  Следующие объекты Intune являются исключениями из этого правила и в настоящее время не поддерживают теги области:
    - Профили Windows ESP
    - Категории устройств
    - Ограничения на регистрацию
    - Идентификаторы корпоративных устройств
    - Устройства Autopilot
    - Места соответствия устройств
    - Устройства Jamf
- Приложения VPP и электронные книги, связанные с токеном VPP, наследуют теги области, назначенные соответствующему токену VPP.
- Устройства Программы регистрации устройств (DEP) и профили DEP, связанные с токеном DEP, наследуют теги области, назначенные соответствующему токену DEP.
- Когда администратор создает объект в Intune, все области тегов, назначенных этому администратору, автоматически будут назначены новому объекту.
- Intune RBAC не применяется к ролям Azure Active Directory. Таким образом, роли администраторов службы Intune и глобальные администраторы имеют полный административный доступ к Intune независимо от того, какие теги области они имеют.
- Если у назначения роли нет тега области, ИТ-администратор может просматривать все объекты на основе разрешений ИТ-администраторов. Если у администраторов нет тегов области, как правило, у них есть все теги области.
- Можно назначить только тег области, который есть у вас в назначении роли.
- Вы можете выбирать только целевые группы, которые перечислены в областях (группах) в вашем назначении ролей.
- Если у вас есть тег области, назначенный вашей роли, вы не можете удалить все теги области объекта Intune. Требуется по крайней мере один тег области.

## <a name="next-steps"></a>Дальнейшие шаги

Узнайте, как действуют теги области, если [назначено несколько ролей](role-based-access-control.md#multiple-role-assignments).
Управление вашими [ролями](role-based-access-control.md) и [профилями](../configuration/device-profile-assign.md).

