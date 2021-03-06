---
title: Новая версия 1610
titleSuffix: Configuration Manager
description: Сведения об изменениях и о новых возможностях, появившихся в Configuration Manager версии 1610.
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b3e1a2feaddb7384d76790249152c89dfa8ee2d3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904803"
---
# <a name="what39s-new-in-version-1610-of-configuration-manager"></a>Новые возможности в Configuration Manager версии 1610

*Область применения: Configuration Manager (Current Branch)*

Обновление 1610 для Configuration Manager (Current Branch) доступно в виде обновления в консоли для ранее установленных сайтов, работающих под управлением версии 1511, 1602 или 1606.


> [!TIP]  
> Чтобы установить новый сайт, необходимо использовать базовую версию Configuration Manager.  
>
> Дополнительные сведения    
> - [Установка новых сайтов](../../servers/deploy/install/installing-sites.md)  
> - [Установка обновлений на сайтах](../../servers/manage/updates.md)  
> - [Базовые и обновленные версии](../../servers/manage/updates.md#bkmk_Baselines)

В следующих разделах содержатся сведения об изменениях и новых возможностях, появившихся в Configuration Manager версии 1610.  


## <a name="in-console-monitoring-of-update-installation-status"></a>Мониторинг состояния установки обновления в консоли  
Начиная с версии 1610 в процесс установки пакета обновления и мониторинга установки в консоли добавился новый этап **После установки**. Этот этап включает получение сведений о состоянии таких задач, как перезапуск основных служб, и инициализация мониторинга репликации. (Этот этап недоступен в консоли, пока сайт не будет обновлен до версии 1610.) Дополнительные сведения о состоянии установки обновлений см. в разделе [Установка обновлений в консоли](../../servers/manage/install-in-console-updates.md#bkmk_install).


## <a name="exclude-clients-from-automatic-upgrade"></a>Исключение клиентов из автоматического обновления
Клиенты Windows можно исключить из обновления до новых версий клиентского программного обеспечения. Для этого необходимо включить клиентские компьютеры в коллекцию, исключаемую из обновления. Клиенты в исключаемой коллекции игнорируют запросы на обновление клиентского программного обеспечения.  Дополнительные сведения см. в разделе [Исключение клиентов Windows из обновления](../../clients/manage/upgrade/exclude-clients-windows.md).


## <a name="improvements-for-boundary-groups"></a>Усовершенствования для групп границ
В версии 1610 представлены важные изменения, касающиеся групп границ и их работы с точками распространения. Эти изменения могут упростить процесс разработки инфраструктуры содержимого, предоставляя повышенный уровень контроля над способами и случаями отката клиентов в целях поиска дополнительных точек распространения в качестве расположений источников содержимого. К таким точкам относятся локальные и облачные точки распространения.
Эти усовершенствования приходят на смену понятиям и принципам работы, которые могут быть вам знакомы на данный момент (например, настройка точек распространения как быстрых или медленных). Новая модель должна быть проще в настройке и обслуживании. Кроме того, эти изменения закладывают основу для будущих преобразований, которые улучшат другие роли системы сайта, связываемые с группами границ.

Во время обновления до версии 1610 конфигурации текущей группы границ преобразуются в соответствии с новой моделью так, чтобы эти изменения не затрагивали существующие конфигурации распространения содержимого.

Дополнительные сведения см. в разделе [Группы границ](../../servers/deploy/configure/boundary-groups.md).


## <a name="peer-cache-for-content-distribution-to-clients"></a>Одноранговый кэш для распространения содержимого на клиентах
Начиная с версии 1610 **одноранговый кэш** клиента помогает управлять развертыванием содержимого на клиентах в удаленных расположениях. Одноранговый кэш — это встроенное решение Configuration Manager, позволяющее клиентам использовать содержимое совместно с другими клиентами непосредственно из своего локального кэша.

После развертывания клиентских параметров, включающих одноранговый кэш в коллекции, члены этой коллекции могут выступать в качестве источника однорангового содержимого для других клиентов в той же группе границ.

Чтобы получить представление об использовании источников содержимого однорангового кэша в среде, можно также использовать новую панель мониторинга **Клиентские источники данных**.

> [!TIP]  
> В версии 1610 одноранговый кэш и панель мониторинга "Источники данных клиента" находятся на стадии предварительного выпуска. Сведения об их включении см. в разделе [Использование функций предварительной версии из обновлений](../../servers/manage/install-in-console-updates.md#bkmk_prerelease).

Дополнительные сведения см. в разделах [Одноранговый кэш для клиентов Configuration Manager](../hierarchy/client-peer-cache.md) и [Панель мониторинга "Клиентские источники данных"](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Одновременный перенос нескольких общих точек распространения
При использовании команды **Переназначить точку распространения** Configuration Manager теперь может параллельно выполнять переназначение 50 общих точек распространения. До этой версии переназначаемые точки распространения обрабатывались по одной. Дополнительные сведения см. в разделе [Одновременный перенос нескольких общих точек распространения](../../migration/planning-a-content-deployment-migration-strategy.md#migrate-multiple-shared-distribution-points-at-the-same-time).

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>Облачный шлюз управления для управления клиентами через Интернет

Облачный шлюз управления обеспечивает простой способ управления клиентами Configuration Manager в Интернете. Служба облачного шлюза управления, которая развертывается в Microsoft Azure и требует подписки Azure, подключается к локальной инфраструктуре Configuration Manager с помощью новой роли "Точка подключения к облачному шлюзу управления". После завершения развертывания и настройки службы клиенты могут взаимодействовать с локальными ролями системы сайта Configuration Manager вне зависимости от наличия подключения к внутренней частной сети или к Интернету. Дополнительные сведения и сравнение облачного шлюза управления с управлением клиентами через Интернет см. в разделе [Управление клиентами в Интернете](../../clients/manage/manage-clients-internet.md).

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Улучшения для политики обновления выпуска Windows 10
В этом выпуске этот тип политики содержит следующие усовершенствования:

- Теперь политику обновления выпусков можно использовать на ПК с ОС Windows 10, где запущен клиент Configuration Manager, а также на ПК с Windows 10, зарегистрированных в Microsoft Intune.
- Вы можете обновить Windows 10 Профессиональная до любой из указанных в мастере платформ, которые совместимы с оборудованием.

## <a name="manage-hardware-identifiers"></a>Управление идентификаторами оборудования
Теперь можно предоставить список идентификаторов оборудования, которые Configuration Manager должен игнорировать при загрузке PXE и регистрации клиентов. Это позволяет решить две распространенные проблемы.

1. Многие устройства, такие как Surface Pro 3, не имеют встроенного порта Ethernet. Для установления проводного подключения в целях развертывания операционной системы, как правило, используется адаптер USB–Ethernet. Однако такие адаптеры часто используются совместно, так как это удобно и стоимость их может быть высокой. Так как MAC-адрес адаптера используется для идентификации устройства, повторное использование адаптера может создавать проблемы, если администратор не предпримет дополнительных мер между развертываниями. Теперь в версии 1610 Configuration Manager можно исключить MAC-адрес такого адаптера, чтобы его легко можно было использовать повторно.
2. Хотя предполагается, что идентификатор SMBIOS является уникальным идентификатором оборудования, некоторые специальные устройства имеют повторяющиеся идентификаторы. Хотя такая ситуация встречается не так часто, как сценарий использования адаптера USB–Ethernet, с помощью списка исключаемых идентификаторов оборудования можно решить эту проблему.

Подробные сведения см. в разделе [Управление повторяющимися идентификаторами оборудования](../../clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers).

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Усовершенствования интеграции Магазина Windows для бизнеса с Configuration Manager
Изменения в этом выпуске:
- Ранее можно было развертывать только бесплатные приложения из Магазина Windows для бизнеса. Теперь Configuration Manager также поддерживает развертывание платных лицензированных веб-приложений (только для зарегистрированных устройств Intune).
- Вы можете запускать немедленную синхронизацию между Магазином Windows для бизнеса и Configuration Manager.
- Теперь можно изменить секретный ключ клиента, полученный из Azure Active Directory.
- Можно удалить подписку на магазин.

Дополнительные сведения см. в статье [Управление приложениями из Магазина Windows для бизнеса с помощью Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).


## <a name="policy-sync-for-intune-enrolled-devices"></a>Синхронизация политики для устройств, зарегистрированных в Intune
Теперь вы можете запросить синхронизацию политики для зарегистрированного в Intune устройства из консоли Configuration Manager вместо того, чтобы запрашивать синхронизацию в приложении корпоративного портала на самом устройстве. Сведения о состоянии запроса синхронизации доступны в новом столбце **Состояние удаленной синхронизации** в представлениях устройств. Они также отображаются в разделе "Данные обнаружения" диалогового окна **Свойства** для каждого устройства.


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>Используйте параметры соответствия для настройки параметров Защитника Windows
Вы можете настроить параметры клиента Защитника Windows на зарегистрированных в Intune компьютерах с Windows 10 с помощью элементов конфигурации в консоли Configuration Manager.
Подробные сведения см. в подразделе **Защитник Windows** раздела [Создание элементов конфигурации для устройств Windows 8.1 и Windows 10, управляемых без использования клиента Configuration Manager](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).



## <a name="general-improvements-to-software-center"></a>Общие усовершенствования в центре программного обеспечения
- Теперь пользователи могут запрашивать приложения как из центра программного обеспечения, так и из каталога приложений.
- Усовершенствования, помогающие пользователям понять, какое программное обеспечение является новым и важным.

## <a name="new-columns-in-device-collection-views"></a>Новые столбцы в представлениях коллекции устройств
В представлениях коллекции устройств теперь могут выводиться столбцы **IMEI** и **Серийный номер** (для устройств iOS).

## <a name="customizable-branding-for-software-center-dialogs"></a>Настраиваемая фирменная символика для диалоговых окон центра программного обеспечения
В Configuration Manager версии 1602 была представлена настраиваемая фирменная символика для центра программного обеспечения. В версии 1610 фирменная символика используется для всех связанных диалоговых окон. В результате пользователи центра программного обеспечения получают возможность более согласованного взаимодействия.

Настраиваемая фирменная символика для центра программного обеспечения применяется согласно указанным далее правилам.

- Если роль сервера сайта "Точка веб-сайта каталога приложений" не установлена, то в центре программного обеспечения отображается название организации, указанное в параметре клиента **Агент компьютера** > **Название организации, которое отображается в центре программного обеспечения**. Инструкции см. в статье [Настройка параметров клиента](../../clients/deploy/configure-client-settings.md).

- Если роль сервера сайта "Точка веб-сайта каталога приложений" установлена, то в центре программного обеспечения отобразятся название организации и цвет, которые указаны в свойствах роли сервера сайта "Точка веб-сайта каталога приложений". Дополнительные сведения см. в статье [Параметры конфигурации для точки веб-сайта каталога приложений](../../servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).

- Если подписка Microsoft Intune настроена и подключена к среде Configuration Manager, то в центре программного обеспечения отображаются название организации, цвет и логотип компании, указанные в свойствах подписки Intune.


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>Льготный период принудительного применения для обязательных приложений и развертывания обновлений программного обеспечения
В некоторых случаях может потребоваться предоставить пользователям больше времени на установку обязательных развертываний приложений или обновлений программного обеспечения (по сравнению с настроенными крайними сроками). Например, это может быть необходимо, если компьютер был отключен в течение длительного времени и требует установки большого числа приложений или обновлений. Например, если пользователь только что вернулся из отпуска, ему может потребоваться значительное время, чтобы дождаться завершения установки просроченных развертываний приложений. Чтобы решить эту проблему, теперь можно определять льготный период применения, развернув параметры клиента Configuration Manager в коллекции. 

Чтобы настроить льготный период, выполните указанные далее действия.
1. На странице **Агент компьютера** параметров клиента настройте новое свойство **Льготный период для принудительного применения после крайнего срока развертывания (ч)** со значением в диапазоне от **1** до **120** часов.
2. В новом обязательном развертывании приложения или в окне свойств существующего развертывания на странице **Планирование** установите флажок **Отложить применение этого развертывания в соответствии с пользовательскими предпочтениями вплоть до окончания льготного периода, определенного в настройках клиента**. Льготный период применения будет действовать для всех развертываний, для которых установлен этот флажок и которые предназначены для устройств с развернутым параметром клиента.

Если настроить льготный период применения и установить флажок, по достижении крайнего срока установки приложения оно будет установлено в первом нерабочем периоде, настроенном пользователем, в течение такого льготного периода. Тем не менее, пользователь может открыть Центр программного обеспечения и установить приложение в любой момент по мере необходимости. По истечении льготного периода режим принудительного применения возвращается к нормальному поведению для просроченных развертываний. Аналогичные параметры были добавлены в мастер развертывания обновлений программного обеспечения, мастер правил автоматического развертывания и на страницы свойств.



## <a name="improved-functionality-in-dialog-boxes-about-required-software"></a>Улучшенные возможности в диалоговых окнах, связанных с обязательным программным обеспечением
Когда пользователь получает необходимое программное обеспечение, он может установить для параметра **Отложить и напомнить снова через:** значение, выбрав нужный вариант в раскрывающемся списке. 
- **Позднее**. Указывает, что вывод уведомлений запланирован на основе параметров уведомлений, настроенных в окне параметров агента клиента.
- **Фиксированное время**. Указывает, что запланировано повторное отображение уведомления через установленный период времени (например, 30 минут).

![Страница "Агент компьютера " в параметрах агента клиента](media/client-notification-settings.png)

Максимальное значение времени переноса зависит от значений уведомлений, настроенных в параметрах агента клиента. Например, если для параметра **Крайний срок развертывания более 24 часов, напоминать пользователю каждые (в часах)** на странице агента компьютера задано 10 часов, а до наступления крайнего срока более 24 часов, то пользователю будет доступен набор параметров переноса со значениями до 10 часов, но никак не больше. По мере приближения крайнего срока будет доступно меньше вариантов согласно соответствующим параметрам агента клиента для каждого компонента временной шкалы развертывания.

Кроме того, для развертывания с высоким уровнем риска, такого как последовательность задач для развертывания операционной системы, уведомление конечных пользователей осуществляется более активно. Вместо временных уведомлений на панели задач, информирующих о необходимости обслуживания важного программного обеспечения, на экране компьютера отображается диалоговое окно, аналогичное показанному далее.

![Диалоговое окно "Необходимое программное обеспечение"](media/client-toast-notification.png)


Дополнительные сведения
- [Параметры для управления развертываниями с высоким риском](../../servers/manage/settings-to-manage-high-risk-deployments.md)
- [Настройка параметров клиента](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>Панель мониторинга "Обновления программного обеспечения"
С помощью новой панели мониторинга "Обновления программного обеспечения" можно просматривать текущее состояние соответствия устройств требованиям в организации и быстро анализировать данные, чтоб определять устройства, находящиеся под угрозой. Чтобы открыть эту панель мониторинга, выберите **Наблюдение** > **Обзор** > **Безопасность** > **Панель мониторинга обновлений программного обеспечения**.

Подробные сведения см. в разделе [Мониторинг обновлений программного обеспечения](../../../sum/deploy-use/monitor-software-updates.md).


## <a name="improvements-to-the-application-request-process"></a>Усовершенствования процесса запроса приложений
После утверждения приложения к установке вы можете впоследствии отклонить запрос, нажав кнопку **Отклонить** в консоли Configuration Manager. Ранее эта кнопка была неактивна после утверждения.

Это действие не приводит к удалению приложения с устройств. Однако оно блокирует установку новых копий приложения пользователями из центра программного обеспечения.

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Фильтрация по размеру содержимого в правилах автоматического развертывания
Теперь можно выполнять фильтрацию по размеру содержимого для обновлений программного обеспечения в правилах автоматического развертывания. Например, чтобы скачивать только обновления программного обеспечения, размер которых не превышает 2 МБ, можно задать для фильтра **Размер содержимого (КБ)** значение **< 2048**. Этот фильтр препятствует автоматическому скачиванию больших обновлений программного обеспечения, что позволяет более эффективно поддерживать упрощенное обслуживание старых версий Windows при ограниченной пропускной способности сети. Дополнительные сведения см. в разделе:
- [Configuration Manager и упрощенное обслуживание более старых версий ОС Windows](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-and-simplified-windows-servicing-on-down/ba-p/274056)
- [Автоматическое развертывание обновлений программного обеспечения](../../../sum/deploy-use/automatically-deploy-software-updates.md)

Чтобы настроить значение в поле **Размер содержимого (КБ)** , выполните одно из указанных ниже действий.
- При создании правила автоматического развертывания в мастере создания правил автоматического развертывания перейдите на страницу **Обновления программного обеспечения**.
- В окне свойств существующего правила автоматического развертывания перейдите на вкладку **Обновления программного обеспечения**.

## <a name="office-365-client-management-dashboard"></a>Панель мониторинга для управления клиентом Office 365
Панель мониторинга для управления клиентом Office 365 теперь доступна в консоли Configuration Manager. Чтобы открыть эту панель мониторинга, последовательно выберите **Библиотека программного обеспечения** > **Обзор** > **Управление клиентом Office 365**.

На панели мониторинга отображаются следующие диаграммы:

- Число клиентов Office 365
- Версии клиентов Office 365
- Языки клиентов Office 365
- Ветви клиентов Office 365     

Подробные сведения см. в разделе [Управление обновлениями Office 365 профессиональный плюс](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Этапы последовательности задач для управления преобразованием BIOS в UEFI
Последовательность задач развертывания операционной системы можно настроить с использованием новой переменной TSUEFIDrive таким образом, чтобы на шаге **Перезагрузить компьютер** выполнялась подготовка раздела FAT32 на жестком диске для перехода на UEFI. Далее приводится пример создания шагов последовательности задач для подготовки жесткого диска к преобразованию BIOS в UEFI. Подробные сведения см. в разделе [Этапы последовательности задач для управления преобразованием BIOS в UEFI](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md).

##  <a name="improvements-to-the-task-sequence-step-prepare-configmgr-client-for-capture"></a>Улучшения этапа последовательности задач Prepare ConfigMgr Client for Capture  
Теперь на шаге "Подготовка клиента Configuration Manager перед снятием образа" полностью удаляется клиент, а не только основные сведения. Когда последовательность задач развертывает записанный образ операционной системы, она каждый раз будет устанавливать новый клиент Configuration Manager. Подробные сведения см. в разделе [Шаги последовательности задач](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture).



## <a name="intune-compliance-policy-charts"></a>Диаграммы политики соответствия Intune
Теперь можно быстро просмотреть общее состояние соответствия устройств и основные причины несоответствия. Это можно сделать с помощью новых диаграмм в рабочей области **Наблюдение** в консоли Configuration Manager. Чтобы перейти к подробному списку устройств, относящихся к определенной категории, щелкните раздел диаграммы. Дополнительные сведения см. в разделе [Мониторинг политики соответствия](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>Интеграция с Lookout в гибридных развертываниях для защиты устройств iOS и Android
Майкрософт интегрируется с решением мобильной защиты от угроз Lookout для защиты мобильных устройств iOS и Android путем обнаружения вредоносных программ, опасных приложений и многого другого на устройствах. Решение Lookout помогает определить настраиваемый уровень угроз. Можно создать правило политики соответствия в Configuration Manager, чтобы определить соответствие устройств на основе оценки рисков в Lookout. Используя политики условного доступа, вы можете разрешить или заблокировать доступ к ресурсам организации на основе состояния соответствия устройства.

Пользователям не соответствующих политике устройств iOS будет предложено зарегистрироваться. Для доступа к корпоративным данным им потребуется установить приложение Lookout for Work на устройствах, активировать приложение и устранить угрозы в приложении Lookout for Work.


## <a name="new-compliance-settings-for-configuration-items"></a>Новые параметры соответствия для элементов конфигурации
Имеется множество новых параметров, которые можно использовать в элементах конфигурации для различных платформ устройств. Это параметры, ранее существовавшие в Microsoft Intune в изолированной конфигурации. Теперь они доступны при использовании Intune с Configuration Manager.
Подробнее см. в разделе [Элементы конфигурации для устройств, управляемых без использования клиента Configuration Manager](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).

### <a name="new-settings-for-android-devices"></a>Новые параметры для устройств Android
#### <a name="password-settings"></a>Параметры пароля
- **Запоминать историю паролей**
- **Разрешить разблокировку по отпечатку пальца**

#### <a name="security-settings"></a>Параметры безопасности
- **Обязательное использование шифрования на картах памяти**
- **Разрешить снимок экрана**
- **Разрешить отправку диагностических данных**

#### <a name="browser-settings"></a>Параметры браузера
- **Разрешить веб-браузер**
- **Разрешить автозаполнение**
- **Разрешить блокирование всплывающих окон**
- **Разрешить файлы cookie**
- **Разрешить выполнение активных сценариев**

#### <a name="app-settings"></a>Параметры приложения
- **Разрешить использование магазина Google Play**

#### <a name="device-capability-settings"></a>Параметры возможностей устройств
- **Разрешить съемные носители**
- **Разрешить модем Wi-Fi**
- **Разрешить геолокацию**
- **Разрешить NFC**
- **Разрешить Bluetooth**
- **Разрешить голосовой роуминг**
- **Разрешить передачу данных в роуминге**
- **Разрешить обмен SMS и MMS**
- **Разрешить использование голосового помощника**
- **Разрешить голосовой набор**
- **Разрешить копирование и вставку**

### <a name="new-settings-for-ios-devices"></a>Новые параметры для устройств iOS
#### <a name="password-settings"></a>Параметры пароля
- **Число обязательных сложных символов в пароле**
- **Разрешить простые пароли**
- **Время бездействия (в минутах), по истечении которого требуется ввод пароля**
- **Запоминать историю паролей**

### <a name="new-settings-for-mac-os-x-devices"></a>Новые параметры для устройств Mac OS X
#### <a name="password-settings"></a>Параметры пароля
- **Число обязательных сложных символов в пароле**
- **Разрешить простые пароли**
- **Запоминать историю паролей**
- **Время бездействия (в минутах), по истечении которого включается экранная заставка**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Новые параметры для устройств Windows 10 Desktop и Mobile
#### <a name="password-settings"></a>Параметры пароля
- **Минимальное число наборов символов**
- **Запоминать историю паролей**
- **Требовать пароль при возвращении устройства из состояния простоя**

#### <a name="security-settings"></a>Параметры безопасности
- **Требовать шифрование на мобильном устройстве**
- **Разрешить отмену регистрации вручную**

#### <a name="device-capability-settings"></a>Параметры возможностей устройств
- **Разрешить VPN через сотовую сеть**
- **Разрешить роуминг VPN через сотовую сеть**
- **Разрешить сброс по телефону**
- **Разрешить USB-подключение**
- **Разрешить использование Кортаны**
- **Разрешить уведомления центра поддержки**

### <a name="new-settings-for-windows-10-team-devices"></a>Новые параметры для устройств Windows 10 для совместной работы
#### <a name="device-settings"></a>Параметры устройства
- **Включить Azure Operational Insights**
- **Включить беспроводную проекцию Miracast**
- **Выберите информацию о собрании, отображаемую на экране приветствия**
- **URL-адрес фонового изображения экрана блокировки**

### <a name="new-settings-for-windows-81-devices"></a>Новые параметры для устройств Windows 8.1
#### <a name="applicability-settings"></a>Параметры применимости
- **Применить все конфигурации к Windows 10**

#### <a name="password-settings"></a>Параметры пароля
- **Требуемый тип пароля**
- **Минимальное число наборов символов**
- **Минимальная длина пароля**
- **Допустимое число неудачных попыток входа, после которых устройство будет очищено**
- **Время бездействия перед отключением экрана (в минутах)**
- **Срок действия пароля (в днях)**
- **Запоминать историю паролей**
- **Запретить использование предыдущих паролей**
- **Разрешить графический пароль и ПИН-код**

#### <a name="browser-settings"></a>Параметры браузера
- **Разрешить автоматическое обнаружение сети интрасети**

### <a name="new-settings-for-windows-phone-81-devices"></a>Новые параметры для устройств Windows Phone 8.1
#### <a name="applicability-settings"></a>Параметры применимости
- **Применить все конфигурации к Windows 10**

#### <a name="password-settings"></a>Параметры пароля
- **Минимальное число наборов символов**
- **Разрешить простые пароли**
- **Запоминать историю паролей**

#### <a name="device-capability-settings"></a>Параметры возможностей устройств
- **Разрешить автоматическое подключение к бесплатным точкам подключения Wi-Fi**
