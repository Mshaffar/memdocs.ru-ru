---
title: Техническая версия 1708
titleSuffix: Configuration Manager
description: Сведения о функциях, доступных в Technical Preview для Configuration Manager, версия 1708.
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3c061ceb-3bdb-4d4f-8c60-344964bd416b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ab5cc83cc8e7bb51477d84a50f18d4f6b73f286d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705162"
---
# <a name="capabilities-in-technical-preview-1708-for-configuration-manager"></a>Возможности в Technical Preview 1708 для Configuration Manager

*Область применения: Configuration Manager (ветвь Technical Preview)*

Эта статья содержит сведения о функциях, доступных в версии 1708 Technical Preview для Configuration Manager. Этот выпуск можно установить для обновления и добавления новых возможностей в ознакомительную техническую версию сайта Configuration Manager. Перед установкой этой версии прочтите статью [Technical Preview для Configuration Manager](../../core/get-started/technical-preview.md). В ней приведены общие требования и ограничения на использование ознакомительной технической версии, а также сведения о том, как выполнять обновления и оставлять отзывы о функциях этого выпуска.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Известные проблемы в этой версии Technical Preview:**
- **Если сервер сайта находится в пассивном режиме, происходит сбой обновления до предварительной версии 1708**. Если вы запустили предварительную версию 1706 или 1707 и [сервер первичного сайта находится в пассивном режиме](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), удалите сервер сайта в пассивном режиме, чтобы обновить сайт предварительной версии до версии 1708. Вы можете повторно установить сервер сайта в пассивном режиме, после того как на сайте заработает версия 1708.

  Удаление сервера сайта в пассивном режиме
  1. Откройте консоль и выберите **Администрирование** > **Обзор** > **Конфигурация сайта** > **Серверы и роли системы сайта**. Затем выберите сервер сайта в пассивном режиме.
  2. На панели **Системные роли сайта** щелкните правой кнопкой мыши роль **Сервер сайта** и нажмите кнопку **Удалить роль**.
  3. Щелкните правой кнопкой мыши сервер сайта в пассивном режиме, а затем выберите **Удалить**.
  4. Удалив сервер сайта на активном сервере первичного сайта, перезапустите службу **CONFIGURATION_MANAGER_UPDATE**.




**Ниже перечислены новые возможности, доступные в этой версии.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Улучшения для указания параметров скрипта при развертывании скриптов PowerShell из Configuration Manager
<!-- 1236459 -->

Начиная с Configuration Manager 1706 можно [создавать и запускать скрипты PowerShell из консоли Configuration Manager](../../apps/deploy-use/create-deploy-scripts.md).

В [технической предварительной версии 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) мы расширили эту возможность, чтобы позволить Configuration Manager считывать параметры скрипта.

В этой технической предварительной версии мы расширили возможность параметров обнаруживать, какие параметры являются обязательными, а какие — дополнительными, и предлагаем вам ввести их.

### <a name="try-it-out"></a>Попробуйте!

1. Выполните следующие указания, чтобы научиться [создавать и запускать сценарии PowerShell из консоли Configuration Manager](../../apps/deploy-use/create-deploy-scripts.md).
2. На новой странице **Параметры сценария** **мастера создания сценариев** выберите параметр и измените его значения.
В мастере отображаются обязательные и дополнительные параметры.
4. При завершении редактирования параметров завершите работу мастера.

При запуске сценарий будет использовать настроенные вами значения параметров. Если обязательный параметр не настроен, пользователю будет предложено указать его при запуске скрипта.

## <a name="management-insights"></a>Аналитика управления
<!-- 1353967 -->
Теперь вы можете получить аналитические сведения о текущем состоянии среды на основе анализа данных в базе данных сайта. Аналитические сведения позволяют лучше понять среду и предпринять соответствующие действия. Изучите аналитику управления в консоли Configuration Manager в области **Администрирование** > **Management Insights** (Аналитика управления) > **All Insights** (Вся аналитика). В этом выпуске доступна следующая аналитика:

- **Приложения без развертываний**. Список приложений без активных развертываний в среде. Эти сведения помогут найти и удалить ненужные приложения, чтобы сократить список приложений, отображаемых в консоли.
- **Пустые коллекции**. Список коллекций без элементов в среде. Эти коллекции можно удалить, чтобы, например, сократить список коллекций, отображаемых при развертывании объектов.


## <a name="restart-computers-from-the-configuration-manager-console"></a>Перезагрузка компьютеров из консоли Configuration Manager   
<!-- 1356283 -->
Начиная с этого выпуска консоль Configuration Manager можно использовать для определения клиентских устройств, которые требуют перезапуска, а затем использовать действие уведомления клиента для их перезапуска.

Для определения устройств, которые ожидают перезагрузки, перейдите к **Assets and Compliance** (Ресурсы и соответствие) > **Устройства** и выберите коллекцию с устройствами, которым может потребоваться перезагрузка. После выбора коллекции можно просмотреть состояние каждого устройства в области сведений в новом столбце с именем **Ожидается перезагрузка**. Каждое устройство имеет значение **Да** или **Нет**.

Чтобы создать клиентское уведомление для перезапуска устройства, сделайте следующее:
1. Найдите устройство, которое необходимо перезапустить, в узле устройств консоли.
2. Щелкните устройство правой кнопкой мыши, выберите **Уведомление клиента**, а затем — **Перезагрузка**. Откроется окно со сведениями о перезапуске. Нажмите кнопку **ОК**, чтобы подтвердить запрос на перезапуск.

При получении уведомления клиентом открывается окно уведомления **Центр программного обеспечения**, чтобы сообщить пользователю о перезапуске. По умолчанию перезагрузка происходит через 90 минут. Время перезапуска можно изменить, настроив [параметры клиента](../clients/deploy/configure-client-settings.md). Параметры поведения при перезапуске находятся на вкладке [Перезагрузка компьютера](../clients/deploy/about-client-settings.md#computer-restart) параметров по умолчанию.


### <a name="try-it-out"></a>Попробуйте!
Попробуйте выполнить следующие задачи, а затем отправьте нам **отзыв** с помощью вкладки на ленте **Главная**, чтобы сообщить о результатах.
1. Разверните приложение или обновите устройство, которое требует перезагрузки устройства для завершения установки.
2. Найдите устройство в узле консоли **Assets and Compliance** (Ресурсы и соответствие)  > **Устройства**. Убедитесь, что в колонке **Ожидается перезагрузка** отображается значение **Да**. Для отображения состояния "Ожидается перезагрузка" в консоли может потребоваться до 20 минут.
3. Наблюдайте за устройством, чтобы подтвердить открытие уведомления центра программного обеспечения и успешный перезапуск устройства.


## <a name="software-center-customization"></a>Настройка центра программного обеспечения
<!-- 1351224 -->
Вы можете добавить элементы фирменной символики и указать видимость вкладок в центре программного обеспечения, а также добавить имя компании для центра программного обеспечения, установить цветовую тему конфигурации центра программного обеспечения, логотип компании и задать видимые вкладки для клиентских устройств.

### <a name="customize-software-center"></a>Настройка центра программного обеспечения

Чтобы изменить центр программного обеспечения, сделайте следующее:

1. В консоли **Configuration Manager** последовательно выберите **Администрирование** > **Параметры клиента**. Щелкните необходимый экземпляр параметров клиента.
2. На вкладке **Главная** в группе **Свойства** нажмите кнопку **Свойства**.
3. В диалоговом окне **Параметры по умолчанию** выберите **Центр программного обеспечения**.
4. Выберите **Да** для **Select new settings to specify company information** (Выбрать новые параметры для указания сведений о компании), чтобы включить параметры настройки центра программного обеспечения.
5. Введите **название компании**.
6. Выберите **цветовую схему для центра программного обеспечения**.
7. Щелкните **Обзор**, чтобы перейти к своему логотипу для центра программного обеспечения. Логотип должен быть в формате JPEG или PNG, иметь максимальное разрешение 400 x 100 пикселей и размер не более 750 КБ.
8. Выберите **Да**, чтобы сделать вкладки видимыми в центре программного обеспечения для клиентских устройств. Должна быть видима хотя бы одна вкладка:

    -  Включите вкладку "Приложения".
    -  Включите вкладку "Обновления".
    -  Включите вкладку "Операционные системы".
    -  Включите вкладку "Состояние установки".
    -  Включите вкладку Device compliance (Соответствие устройств).
    -  Включите вкладку "Параметры".

### <a name="next-steps"></a>Дальнейшие шаги

Дополнительные сведения об управлении приложениями Configuration Manager см. в статье [Общие сведения об управлении приложениями](../../apps/understand/introduction-to-application-management.md).