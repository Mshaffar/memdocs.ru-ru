---
title: Управление устройствами с помощью Exchange
titleSuffix: Configuration Manager
description: Управление мобильными устройствами с помощью коннектора Exchange Server в Configuration Manager.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 08d92d5c09331d675dc679a374e1bbf81633748e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724808"
---
# <a name="device-management-with-exchange-and-configuration-manager"></a>Управление устройствами с помощью Exchange и Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Если у вас есть мобильные устройства, которые подключаются к Exchange Server через протокол ActiveSync, можно использовать коннектор Exchange Server в Configuration Manager для управления этими устройствами. Соединитель работает как с локальным сервером Exchange Server, так и с Exchange Online. Используйте консоль Configuration Manager для настройки функций управления мобильными устройствами Exchange. Например, удаленная очистка устройств и управление параметрами для нескольких серверов Exchange.

![Логическая схема коннектора Exchange Server с Configuration Manager](media/configmgr-with-exchange.png)  

При управлении мобильными устройствами с помощью этого соединителя он не устанавливает клиент Configuration Manager или не регистрирует устройства с помощью MDM. Функции управления Exchange Server ограничены в сравнении с другими параметрами. Например, невозможно установить программное обеспечение или использовать элементы конфигурации для настройки этих устройств. Дополнительные сведения см. [в статье Выбор решения для управления устройствами для Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md).  

## <a name="policies"></a>Политики

При использовании соединителя Configuration Manager настраивает параметры на мобильных устройствах. Устройства не используют политики почтовых ящиков Exchange ActiveSync по умолчанию. Определите параметры, которые вы хотите использовать в следующих группах:

- **Общие**
- **Пароль**
- **Управление электронной почтой**
- **Безопасность**
- **Приложение**

Например, в группе **пароль** можно настроить следующие параметры.

- Требуется ли для мобильных устройств пароль
- Минимальная длина пароля
- Сложность пароля
- Разрешено ли восстановление пароля

Если в группе настроен хотя бы один параметр, Configuration Manager будет управлять всеми параметрами в группе для мобильных устройств. Если вы не настраиваете какой-либо параметр в группе, Exchange продолжит управлять этими параметрами для мобильных устройств. Все политики почтовых ящиков Exchange ActiveSync, настроенные на сервере Exchange Server и назначенные пользователям, по-прежнему применяются.

## <a name="access-rules-and-remote-actions"></a>Правила доступа и удаленные действия

Можно также настроить коннектор Exchange Server для управления правилами доступа к Exchange. Эти правила доступа включают разрешение, блокировку или карантин мобильных устройств. Вы можете выполнять удаленную очистку мобильных устройств с помощью консоли Configuration Manager, а пользователи могут выполнять удаленную очистку своих мобильных устройств с помощью каталога приложений.

Мобильное устройство пользователя автоматически отображается в каталоге приложений при управлении им, а сервер Exchange — в локальной среде. Чтобы мобильное устройство отображалось в каталоге приложений при использовании Exchange Online, вручную настройте сопоставление пользователей и устройств. Дополнительные сведения см. в статье [Связывание пользователей и устройств с помощью сопоставления пользователей и устройств](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

> [!TIP]  
> При передаче мобильного устройства другому пользователю, прежде чем новый владелец настроит свою учетную запись Exchange на устройстве, удалите мобильное устройство из консоли Configuration Manager.

## <a name="prerequisites"></a>Предварительные условия

> [!IMPORTANT]  
> Перед установкой этого соединителя убедитесь, что Configuration Manager поддерживает вашу версию Exchange. Дополнительные сведения см. в разделе [Поддерживаемые конфигурации — коннектор Exchange Server](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_ExSrvConOS).  

### <a name="permissions-to-configure-the-connector"></a>Разрешения для настройки соединителя

Для настройки коннектора Exchange Server в Configuration Manager необходимы следующие разрешения безопасности:

- Для добавления, изменения и удаления коннектора Exchange Server: разрешение **Изменение** для объекта **Сайт** .  

- Для настройки параметров мобильного устройства: разрешение **Изменение политики коннектора** для объекта **Сайт** .  

Например, встроенная роль **полного администратора** включает в себя необходимые разрешения.  

### <a name="permissions-to-manage-mobile-devices"></a>Разрешения для управления мобильными устройствами

Для управления мобильными устройствами необходимы следующие разрешения безопасности.  

- Для очистки мобильного устройства: разрешение **Удалить ресурс** для объекта **Коллекция** .  

- Для отмены команды очистки: разрешение **Изменить ресурс** для объекта **Коллекция** .  

- Разрешение и блокировка мобильных устройств: разрешение **Изменить ресурс** для объекта **Коллекция** .  

Например, встроенная роль **администратора операций** включает эти необходимые разрешения.

Дополнительные сведения см. в разделе [Настройка ролевого администрирования](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Установка и Настройка соединителя Exchange](install-configure-exchange-connector.md)
