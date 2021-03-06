---
title: Возможности технической версии 1701
titleSuffix: Configuration Manager
description: Сведения о функциях, доступных в Technical Preview для Configuration Manager, версия 1701.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: f100d28b3fd4ce0d310ddb2f0b4e777c72f72881
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076209"
---
# <a name="capabilities-in-technical-preview-1701-for-configuration-manager"></a>Возможности в Technical Preview 1701 для Configuration Manager

*Область применения: Configuration Manager (ветвь Technical Preview)*



В этой статье содержатся сведения о функциях, доступных в версии 1701 Technical Preview для Configuration Manager. Этот выпуск можно установить для обновления и добавления новых возможностей в ознакомительную техническую версию сайта Configuration Manager. Перед установкой этой версии прочтите вводную статью [Technical Preview для Configuration Manager](../../core/get-started/technical-preview.md), чтобы ознакомиться с общими требованиями и ограничениями на использование ознакомительной технической версии, а также узнать, как выполнять обновления и оставлять отзывы о возможностях этого выпуска.    


**Ниже перечислены новые возможности, доступные в этой версии.**  

## <a name="boundary-groups-improvements-for-software-update-points"></a>Улучшения групп границ для точек обновления программного обеспечения
Начиная с этой предварительной версии группы границ используются для связывания клиентов с точками обновления программного обеспечения. Это изменение внесено в рамках продолжающейся работы над реализацией возможностей по использованию групп границ для управления дополнительными ролями системы сайта.  Изменения в отношении использования групп границ были впервые реализованы в Technical Preview 1609 и версии 1610 Current Branch.  

В этой предварительной версии новые возможности групп границ позволяют управлять тем, какие точки обновления программного обеспечения может использовать клиент, аналогично тому, как раньше можно было управлять используемой точкой распространения.  

- Вы можете настроить группы границ, чтобы установить связь с одним или несколькими серверами, на которых размещается точка обновления программного обеспечения.
- Клиенты, ищущие новую точку обновления ПО, будут пытаться использовать точку, связанную с текущей группой границ.
- Если клиенту не удается связаться с текущей точкой обновления ПО и найти точку обновления ПО в текущей группе границ, он прибегает к механизму отката, расширяющему пул доступных точек обновления ПО.    

Дополнительные сведения о группах границ см. в разделе [Группы границ](../servers/deploy/configure/boundary-groups.md) документации по Current Branch.

Но в этой предварительной версии группы границ для точек обновления программного обеспечения реализованы лишь частично. Вы можете добавить точки обновления ПО и настроить соседние группы границ, содержащие такие точки, но период отката для точек обновления ПО пока не поддерживается, и клиенты приступают к процедуре отката только через два часа.

Ниже описывается схема работы точек обновления ПО в этой версии Technical Preview.  

- **Новые клиенты используют группы границ для выбора точек обновления программного обеспечения**. Клиент, установленный после установки версии 1701, выбирает точку обновления ПО из связанной с ним группы границ.

  Такая схема работы отличается от использовавшейся ранее, когда клиент случайным образом выбирал точку обновления ПО из списка совместно используемых точек в лесу клиентов.   

- **Ранее установленные клиенты по-прежнему используют текущую точку обновления ПО, пока не произведут откат для поиска новой точки.**
  Клиенты, которые были установлены ранее и уже имеют точку обновления ПО, продолжат использовать ее, пока не будет выполнен откат. Это относится и к точкам обновления ПО, которые не связаны с текущей группой границ клиента. Они не пытаются мгновенно найти и использовать точку обновления ПО из текущей группы границ.

  Клиент, у которого уже есть точка обновления ПО, использует новую схему работы только после того, как ему не удается связаться с текущей точкой обновления ПО и он приступает к процедуре отката.
  Такой отложенный переход к новой схеме работе является преднамеренным. Связан он с тем, что смена точки обновления ПО может привести к интенсивному использованию пропускной способности сети, когда клиент синхронизирует данные с новой точкой обновления ПО. Такая задержка позволяет избежать перегрузки сети, которая возникла бы в случае, если все клиенты переключились бы на новые точки обновления ПО одновременно.

- **Конфигурации периода отката**. Конфигурации периода времени, через который клиенты начинают откат для поиска новой точки обновления ПО, не поддерживаются в этой версии Technical Preview. Это касается параметров **Время отката (в минутах)** и **Никогда не выполнять откат**, которые можно настроить для других связей групп границ.

  Вместо этого клиенты по-прежнему пытаются подключиться к текущей точке обновления ПО в течение двух часов, прежде чем начинать процедуру отката для поиска новой доступной точки обновления ПО.

  Когда клиент все же прибегает к откату, он использует конфигурации групп границ для отката, чтобы создать пул доступных точек обновления ПО. Этот пул включает в себя все точки обновления ПО из *текущей группы границ* клиента, *соседних групп границ*, а также из *группы границ по умолчанию для сайта*.

- **Настройка группы границ по умолчанию для сайта**.  
  Рассмотрите возможность добавления точки обновления ПО в группу *Default-Site-Boundary-Group&lt;код_сайта>* . Таким образом клиенты, не входящие в другую группу границ, не смогут выполнить откат для поиска точки обновления ПО.


Для управления точками обновления ПО для групп границ используйте [процедуры из документации по Current Branch](../servers/deploy/configure/boundary-group-procedures.md), но помните, что настроенные вами периоды отката пока не используются для точек обновления ПО.


## <a name="hardware-inventory-collects-uefi-information"></a>Функция инвентаризации оборудования собирает сведения о UEFI
Доступны новый класс (**SMS_Firmware**) и свойство (**UEFI**) инвентаризации оборудования, помогающие определить, запускается ли компьютер в режиме UEFI. Когда компьютер запускается в режиме UEFI, свойство **UEFI** принимает значение **TRUE**. Это поведение включено в функции инвентаризации оборудования по умолчанию. Дополнительные сведения об инвентаризации оборудования см. в разделе [Настройка инвентаризации оборудования](../clients/manage/inventory/configure-hardware-inventory.md).

## <a name="improvements-to-operating-system-deployment"></a>Усовершенствования развертывания операционной системы
Мы внесли указанные ниже усовершенствования в процедуру развертывания операционной системы, многие из которых являются результатом ваших отзывов.
- [**Поддержка дополнительных приложений для выполнения последовательности задач установки приложений**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t). Мы увеличили максимальное число приложений до 99, которые устанавливаются на шаге последовательности задач **Установка приложений**. Ранее максимальное число приложений было равно 9.
- [**Выбор нескольких приложений на шаге последовательности задач установки приложений**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step). Когда вы добавляете приложения на шаг установки приложений в редакторе последовательности задач, можно выбрать несколько приложений в области **Выбор приложения для установки**.
- [**Срок действия автономного носителя**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media). При создании автономного носителя доступны новые необязательные параметры, позволяющие задать начальную и конечную даты срока действия носителя. По умолчанию эти параметры отключены. Перед запуском автономного носителя даты сравниваются с системным временем. Если системное время ранее времени начала или позднее времени окончания, автономный носитель не запускается. Эти параметры также доступны при использовании командлета PowerShell New-CMStandaloneMedia.
- [**Поддержка дополнительного содержимого для автономных носителей**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic). Теперь поддерживается дополнительное содержимое в автономном носителе. Вы можете выбрать дополнительные пакеты, пакеты драйверов и приложения для промежуточного хранения на носителе, помимо другого содержимого, на которое ссылается последовательность задач. Ранее на автономном носителе могло находиться только промежуточное содержимое, на которое ссылалась последовательность задач.
- [**Настраиваемое время ожидания для шага последовательности задач автоматического применения драйверов**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout). Стали доступны новые переменные последовательности задач для настройки значения времени ожидания при создании HTTP-запросов к каталогу в шаге "Автоматическое применение драйвера" последовательности задач. Доступны следующие переменные и значения по умолчанию (в секундах):
   - SMSTSDriverRequestResolveTimeOut; значение по умолчанию — 60
   - SMSTSDriverRequestConnectTimeOut; значение по умолчанию — 60
   - SMSTSDriverRequestSendTimeOut; значение по умолчанию — 60
   - SMSTSDriverRequestReceiveTimeOut; значение по умолчанию — 480
- [**Теперь идентификационный номер пакета отображается на шагах последовательности задач**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste). Для любого шага последовательности задач, ссылающегося на пакет, пакет драйверов, образ операционной системы, образ загрузки или пакет обновления операционной системы, теперь отображается идентификатор пакета соответствующего объекта. Если шаг последовательности задач ссылается на приложение, отображается идентификатор объекта.
- **Отслеживание Windows 10 ADK по версии сборки**. Комплект Windows 10 ADK теперь отслеживается по версии сборки для более надежной поддержки процедуры настройки образов загрузки Windows 10. Например, если сайт использует Windows ADK для Windows 10 версии 1607, в консоли можно настроить только образы загрузки версии 10.0.14393. Подробные сведения о настройке версией WinPE см. в разделе [Настройка загрузочных образов](../../osd/get-started/customize-boot-images.md).
- **Исходный путь к образу загрузки по умолчанию теперь нельзя изменять**. Управление образами загрузки по умолчанию осуществляется с помощью Configuration Manager, и исходный путь к образу загрузки по умолчанию больше нельзя изменить в консоли Configuration Manager или с помощью пакета SDK для Configuration Manager. Вы по-прежнему можете настроить исходный путь для пользовательских образов загрузки.

## <a name="host-software-updates-on-cloud-based-distribution-points"></a>Размещение обновлений программного обеспечения в облачных точках распространения
Начиная с этой предварительной версии облачную точку распространения можно использовать для размещения пакета обновления программного обеспечения. Но, так как можно настроить клиенты для скачивания обновлений ПО непосредственно из Центра обновления Майкрософт, следует учесть дополнительные затраты, связанные с развертыванием пакета обновления ПО в облачной точке распространения.

Сведения об использовании облачных точек распространения см. в разделе [Использование облачной точки распространения](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) в документации по Configuration Manager (Current Branch).

## <a name="validate-device-health-attestation-data-via-management-points"></a>Проверка данных подтверждения работоспособности устройства посредством точек управления

Начиная с этой предварительной версии можно настроить точки управления для проверки данных подтверждения работоспособности, предоставляемых облачной или локальной службой подтверждения работоспособности. На новой вкладке **Дополнительные параметры** в диалоговом окне **Свойства компонента точки управления** можно **добавить**, **изменить** или **удалить** **URL-адрес локальной службы подтверждения работоспособности устройств**. Кроме того, вы можете задать **настраиваемые параметры устройств** для агента клиента так, чтобы **использовалась локальная служба подтверждения работоспособности**.  Если выбрать для этого параметра значение **Да**, данные будут передаваться в локальную точку управления, а не в облачную службу.

### <a name="try-it-out"></a>Попробуйте!

- **Включение локальной службы подтверждения работоспособности устройств в точке управления**<br>  В консоли Configuration Manager перейдите к точке управления и откройте диалоговое окно **Свойства компонента точки управления**, после чего перейдите на вкладку **Дополнительные параметры**. Нажмите кнопку **Добавить** и укажите локальный URL-адрес (например, https://10.10.10.10) для **URL-адресов локальной службы подтверждения работоспособности устройств**.
- **Включение передачи данных подтверждения работоспособности в локальную точку управления для агента клиента**<br>В консоли Configuration Manager последовательно выберите **Администрирование** > **Параметры клиента** и дважды щелкните узел **Настраиваемые параметры устройств** или создайте его. Выберите **Агент компьютера** и задайте для параметра **Использовать локальную службу подтверждения работоспособности** значение **Да**. Если для параметра **Включить взаимодействие со службой подтверждения работоспособности устройств** задано значение **Да**, а для параметра **Использовать локальную службу подтверждения работоспособности** — значение **Нет**, точка управления будет использовать облачную службу подтверждения работоспособности устройств.

## <a name="use-the-oms-connector-for-microsoft-azure-government-cloud"></a>Использование соединителя OMS для облака Microsoft Azure для государственных организаций
Начиная с этой версии Technical Preview можно использовать соединитель Microsoft Operations Management Suite (OMS) для подключения к рабочей области OMS, находящейся в облаке Microsoft Azure для государственных организаций.  

Для этого нужно изменить файл конфигурации так, чтобы он указывал на облако для государственных организаций, а затем установить соединитель OMS.

### <a name="set-up-an-oms-connector-to-microsoft-azure-government-cloud"></a>Настройка соединителя OMS для облака Microsoft Azure для государственных организаций
1. На любом компьютере, на котором установлена консоль Configuration Manager, измените следующий файл конфигурации так, чтобы он указывал на облако для государственных организаций.  ***&lt;Путь установки Configuration Manager >\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

   **Изменения:**

   Измените значение параметра *FairFaxArmResourceID* на <https://management.usgovcloudapi.net/">

   - **Исходный параметр:** &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
     &lt;value>&lt;/value>   
     &lt;/setting>

   - **Параметр после изменения:**      
     &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value><https://management.usgovcloudapi.net/&lt;/value>>  
     &lt;/setting>

   Измените значение параметра *FairFaxAuthorityResource* на "<https://login.microsoftonline.com/>"

   - **Исходный параметр:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
     &lt;value>&lt;/value>

   - **Измененный параметр:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
     &lt;value><https://login.microsoftonline.com/&lt;/value>>

2. Сохранив файл с внесенными изменениями, перезапустите консоль Configuration Manager на этом же компьютере, а затем установите соединитель OMS с ее помощью. Чтобы установить соединитель, используйте сведения из раздела [Синхронизация данных Configuration Manager с Microsoft Operations Management Suite](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm) и выберите **рабочую область Operations Management Suite** в облаке Microsoft Azure для государственных организаций.

3. После установки соединителя OMS подключение к облаку для государственных организаций будет доступно при использовании консоли, подключенной к сайту.

## <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>В мастерах создания для гибридного управления мобильными устройствами указывать версии Android и iOS более не нужно.

Начиная с этого Technical Preview для гибридного управления мобильными устройствами (MDM), больше не нужно указывать конкретные версии Android и iOS при создании политик и профилей для устройств, управляемых Intune. Вместо этого вы можете выбрать устройство одного из следующих типов:

- Android
- Samsung KNOX Standard 4.0 и более поздней версии
- iPhone
- iPad

Это изменение затронет мастера создания следующих элементов:

- элементы конфигурации,
- Политики соответствия требованиям
- Профили сертификатов
- Профили электронной почты
- Профили VPN
- Профили Wi-Fi

Теперь гибридные развертывания быстрее обеспечат поддержку новых версий Android и iOS. Для этого более не нужен новый выпуск или расширение Configuration Manager. Как только в Intune появится поддержка новой версии, пользователи смогут установить ее на мобильные устройства.

Чтобы не возникали проблемы при обновлении с предыдущих версий Configuration Manager, выбор версии мобильной операционной системы останется доступен на страницах свойств этих элементов. Если вам по-прежнему нужна конкретная версия, можно создать элемент и указать целевую версию на странице свойств.
