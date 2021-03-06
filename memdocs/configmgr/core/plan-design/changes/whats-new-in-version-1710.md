---
title: Новая версия 1710 | Документация Майкрософт
titleSuffix: Configuration Manager
description: Сведения об изменениях и о новых возможностях, появившихся в Configuration Manager версии 1710.
ms.date: 01/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 15735b015796d2cccfa9b0a24afc8f6eb0573df1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073625"
---
# <a name="what39s-new-in-version-1710-of-configuration-manager"></a>Новые возможности в Configuration Manager версии 1710

*Область применения: Configuration Manager (Current Branch)*

Обновление 1710 для Configuration Manager (Current Branch) доступно в виде обновления в консоли для ранее установленных сайтов, работающих под управлением версии 1610, 1702 или 1706.

Помимо новых функций, этот выпуск также включает в себя дополнительные изменения, такие как исправление ошибок. Дополнительные сведения см. в статье [Сводка изменений в текущей ветви Configuration Manager, версия 1710](https://support.microsoft.com/help/4056470/summary-of-changes-in-system-center-configuration-manager-current-bran).

Также доступны следующие дополнительные обновления к этому выпуску:
- [Накопительный пакет обновления для Configuration Manager (Current Branch), версия 1710](https://support.microsoft.com/help/4057517/update-rollup-for-system-center-configuration-manager-current-branch-v)
- [Накопительный пакет обновления 2 для Configuration Manager (Current Branch), версия 1710](https://support.microsoft.com/en-us/help/4086143/update-rollup-2-for-system-center-configuration-manager-current-branch)

> [!TIP]  
> Чтобы установить новый сайт, необходимо использовать базовую версию Configuration Manager.  
>
> Дополнительные сведения    
> - [Установка новых сайтов](../../servers/deploy/install/installing-sites.md)  
> - [Установка обновлений на сайтах](../../servers/manage/updates.md)  
> - [Базовые и обновленные версии](../../servers/manage/updates.md#bkmk_Baselines)

Следующие разделы содержат сведения об изменениях и новых возможностях, появившихся в Configuration Manager версии 1710.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1710 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Инфраструктура сайта

### <a name="updates-for-peer-cache-----sms500850---"></a>Обновления для однорангового кэша  <!-- sms500850 -->
Начиная с этого выпуска, одноранговый кэш больше не считается функцией предварительной версии.  Какие-либо другие изменения для однорангового кэша в этом выпуске отсутствуют. Дополнительные сведения см. в разделе [Одноранговый кэш для клиентов Configuration Manager](../hierarchy/client-peer-cache.md).

### <a name="cloud-distribution-point-support-for-azure-government-cloud------sms491428---"></a>Поддержка облачных точек распространения для облака Azure для государственных организаций   <!-- sms491428 -->
Теперь вы можете использовать [облачные точки распространения](../hierarchy/use-a-cloud-based-distribution-point.md) в облаке Azure для государственных организаций.   

### <a name="inventory-default-unit-revision----sms503697---"></a>Пересмотр единицы измерения по умолчанию для инвентаризации <!-- sms503697 -->
Так как теперь устройства имеют жесткие диски размером в несколько гигабайт (ГБ), терабайт (ТБ) и даже больше, этот выпуск изменяет единицу измерения по умолчанию (SMS_Units), используемую во многих представлениях, с мегабайтов на гигабайты. Например, v_gs_LogicalDisk.FreeSpace теперь выдает значение в ГБ.


<!-- ## Migration  -->


## <a name="client-management"></a>Управление клиентами

### <a name="co-management-for-windows-10-devices"></a>Совместное управление для устройств Windows 10    
<!-- 1350871 -->
После выпуска предыдущих обновлений Windows 10 можно одновременно присоединять устройство Windows 10 к Active Directory (AD) как в локальной, так и в облачной среде (гибридная служба Azure AD). После выпуска с Configuration Manager версии 1710 это улучшение открывает новые возможности для совместного управления, позволяя работать с устройствами Windows 10 версии 1709 (также называется Fall Creators Update) одновременно при помощи Configuration Manager и Intune. Решение обеспечивает поэтапный переход с традиционной системы управления на современную. Дополнительные сведения см. в руководстве по [совместному управлению устройствами Windows 10](../../../comanage/overview.md).

### <a name="restart-computers-from-the-configuration-manager-console-----1356283---"></a>Перезагрузка компьютеров из консоли Configuration Manager  <!-- 1356283 -->
Начиная с этого выпуска, консоль Configuration Manager можно использовать для определения клиентских устройств, которые требуют перезапуска, а затем использовать действие уведомления клиента для их перезапуска.

См. раздел [Управление клиентами](../../clients/manage/manage-clients.md#restart-clients).


<!-- ## Compliance settings -->


## <a name="application-management"></a>Управление приложениями
### <a name="improvements-for-run-scripts------1236459---"></a>Усовершенствования для функции выполнения сценариев   <!-- 1236459 -->
Этот выпуск содержит несколько улучшений для функции **выполнения сценариев**, которая позволяет развертывать сценарии PowerShell для выполнения на управляемых устройствах. Эта функция появилась в версии 1706.

Доступные улучшения:
- использование областей безопасности для управления доступом к функции выполнения сценариев;
- мониторинг выполняемых сценариев в реальном времени.
- Параметры для сценариев отображаются в мастере создания сценариев, поддерживают проверку и определяются как обязательные или необязательные.

Дополнительные сведения об использовании этой функции см. в статье [Создание и выполнение сценариев](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="new-mobile-application-management-policy-settings"></a>Новые параметры политики управления мобильными приложениями
<!-- 1324760 -->
Для политики управления мобильными приложениями были добавлены следующие параметры:
- **Отключить синхронизацию контактов.** Запрещает приложению сохранять данные в собственном приложении "Контакты" на устройстве.
- **Отключить печать.** Запрещает приложению распечатывать рабочие или учебные данные.

### <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Центр программного обеспечения больше не искажает значки, размер которых превышает 250 x 250  
<!-- 1356194 -->

В этом выпуске центр программного обеспечения больше не будет искажать значки, размер которых превышает 250 x 250. Раньше в центре программного обеспечения эти значки выглядели нечеткими. Теперь вы можете задать значок с размером до 512 x 512 пикселей, и он будет отображаться без искажений.

Чтобы добавить значок для приложения в центре программного обеспечения, см. статью [Создание приложений](../../../apps/deploy-use/create-applications.md).

## <a name="operating-system-deployment"></a>Развертывание операционной системы
 > [!TIP]   
 > <!-- 1354281 -->
 > Начиная с этой версии 1709 Windows 10 (Fall Creators Update), Windows Media включает несколько выпусков. При настройке последовательности задач для использования пакета обновления операционной системы или образа операционной системы не забудьте выбрать [выпуск, который поддерживается в Configuration Manager](../configs/support-for-windows-10.md#windows-10-as-a-client).

### <a name="add-child-task-sequences-to-a-task-sequence"></a>Добавление дочерней последовательности задач в последовательность задач
<!-- 1261338 -->

Вы можете добавить новый шаг последовательности задач, который управляет другой последовательностью задач, что, в свою очередь, создает иерархическое отношение между последовательностями задач. Это позволяет создать дополнительные модульные последовательности задач, которые можно повторно использовать.  

Дополнительные сведения о дочерних последовательностях задач см. в статье [Дочерняя последовательность задач](../../../osd/understand/task-sequence-steps.md#child-task-sequence).

## <a name="software-center-customization"></a>Настройка центра программного обеспечения
<!-- 1351224 -->
Вы можете добавить элементы фирменной символики и указать видимость вкладок в центре программного обеспечения, а также добавить имя компании для центра программного обеспечения, установить цветовую тему конфигурации центра программного обеспечения, логотип компании и задать видимые вкладки для клиентских устройств.

Дополнительные сведения см. в разделе [Планирование и настройка управления приложениями](../../../apps/plan-design/plan-for-and-configure-application-management.md).

## <a name="software-updates"></a>Обновления программного обеспечения

### <a name="surface-driver-updates-----1098490---"></a>Обновления драйверов Surface  <!-- 1098490 -->
Начиная с этого выпуска, управление обновлением драйверов Surface больше не считается функцией предварительной версии.  


## <a name="reporting"></a>Отчеты

### <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Ограничение расширенного объема данных Windows 10 только отправкой данных, относящихся к работоспособности устройств Windows Analytics
<!-- 1356148 -->

Теперь вы можете задать для сбора данных диагностики Windows 10 уровень **Расширенный (с ограничениями)** . Этот параметр позволяет получать практические сведения об устройствах в вашей среде. При этом устройства не отправляют все данные, если задан уровень **Расширенные** в Windows 10 версии 1709 и выше.

<!-- ## Inventory  -->


## <a name="mobile-device-management"></a>Управление мобильными устройствами

### <a name="actions-for-non-compliance"></a>Действия при несоответствии 
<!--1321366 -->    
Теперь можно настроить упорядоченную по времени последовательность действий, которые применяются к устройствам, перестающим быть соответствующими. Например, вы можете отправлять сообщения электронной почты пользователям несоответствующих устройств или помечать такие устройства как несоответствующие.

### <a name="windows-10-arm64-device-support"></a>Поддержка устройств ARM64 с Windows 10
<!-- 1355000 -->

Гибридные сценарии управления мобильными устройствами (MDM) будут поддерживаться на устройствах ARM64 под управлением Windows 10, если такие устройства доступны.

### <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Улучшенный интерфейс профиля VPN в консоли Configuration Manager 
<!-- 1318232 -->

В этом выпуске мы обновили мастер профилей VPN и страницы свойств для отображения параметров для выбранной платформы.


- Каждая платформа имеет собственный рабочий процесс. Это значит, что новые профили VPN содержат только параметры, поддерживаемые платформой.
- Теперь страница **Поддерживаемые платформы** отображается после страницы **Общие**.  Платформа выбирается перед заданием значений свойств.
- Если в качестве платформы выбраны **Android**, **Android for Work** или **Windows Phone 8.1**, страница **Поддерживаемые платформы** не требуется и не отображается.
- Рабочий процесс на основе клиента Configuration Manager объединен с рабочими процессами Windows 10 на основе клиента гибридного развертывания MDM. Они поддерживают те же параметры.
- Каждый рабочий процесс платформы включает в себя только параметры для этого рабочего процесса.  Например, рабочий процесс Android содержит параметры, соответствующие Android. Параметры, соответствующие iOS или Windows 10 Mobile больше не отображаются в рабочем процессе Android.
- Страница "Автоподключение VPN" устарела и была удалена.

Эти изменения применяются к новым профилям VPN.  

Чтобы свести к минимуму риск совместимости, существующие профили VPN оставлены без изменений.  При редактировании существующего профиля параметры отображаются так же, как и при создании профиля.  

Дополнительные сведения см. в разделе [Профили VPN на мобильных устройствах](../../../protect/deploy-use/vpn-profiles.md).

### <a name="limited-support-for-cryptography-next-generation-cng-certificates----1356191---"></a>Ограниченная поддержка сертификатов Cryptography: Next Generation (CNG) <!-- 1356191 -->

Configuration Manager обеспечивает ограниченную поддержку сертификатов Cryptography: Next Generation (CNG). Клиенты Configuration Manager могут использовать PKI-сертификат для проверки подлинности клиента с закрытым ключом в поставщике хранилища ключей CNG (KSP). Благодаря поддержке поставщика хранилища ключей Configuration Manager поддерживает аппаратный закрытый ключ, например KSP доверенного платформенного модуля (TPM) для PKI-сертификатов проверки подлинности клиента.

Дополнительные сведения см. в статье [Общие сведения о сертификатах CNG](../network/cng-certificates-overview.md).

## <a name="protect-devices"></a>Защита устройств

### <a name="create-and-deploy-exploit-guard-policies"></a>Создание и развертывание политик Exploit Guard
<!-- 1355468 -->

Вы можете [создать и развернуть политики](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md), управляющие всеми четырьмя компонентами Exploit Guard в Защитнике Windows, включая уменьшение уязвимой зоны, контролируемый доступ к файлам, защиту от эксплойтов и защиту сети.

### <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Создание и развертывание политики Application Guard в Защитнике Windows
<!-- 1351960 -->

Вы можете [создать и развернуть политики Application Guard в Защитнике Windows](../../../protect/deploy-use/create-deploy-application-guard-policy.md), используя защиту конечных точек Configuration Manager.

### <a name="device-guard-policy-changes"></a>Изменения политик Device Guard
<!-- 1355092 -->
В политики Device Guard внесены следующие три изменения.

- Политики Device Guard переименованы в политики Application Control в Защитнике Windows. Например, **мастер создания политик Device Guard** теперь называется **мастер создания политик Application Control в Защитнике Windows** .
- Устройства, использующие Fall Creators Update для Windows версии 1709, не нужно перезагружать для применения политик управления приложениями в Защитнике Windows. По умолчанию перезапуск по-прежнему выполняется, но вы можете [отключить его](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md).
- Вы можете [настроить устройства для автоматического запуска программного обеспечения](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md), которому доверяет Intelligent Security Graph.





## <a name="next-steps"></a>Дальнейшие шаги
Когда вы будете готовы установить эту версию, см. статью [Обновления для Configuration Manager](../../servers/manage/updates.md).
