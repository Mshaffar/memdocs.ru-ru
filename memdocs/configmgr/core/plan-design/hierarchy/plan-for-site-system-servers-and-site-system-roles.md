---
title: Планирование ролей системы сайта
titleSuffix: Configuration Manager
description: Планирование серверов системы сайта и ролей системы сайта при планировании иерархии Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3fb8c54920c10f8d3601a939c3c7b442c95e1dcf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706502"
---
# <a name="plan-for-site-system-servers-and-site-system-roles-in-configuration-manager"></a>Планирование серверов системы сайта и ролей системы сайта в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Каждый устанавливаемый сайт Configuration Manager включает в себя сервер сайта, который является **сервером системы сайта**. Сайт может также включать дополнительные серверы системы сайта на компьютерах, расположенных удаленно от сервера сайта. Серверы системы сайта (сервер сайта или удаленный сервер системы сайта) поддерживают **роли системы сайта**.  

## <a name="site-system-servers"></a><a name="bkmk_siteservers"></a> Серверы системы сайта  

Если на компьютере установить роль системы сайта, то такой компьютер становится сервером системы сайта. На каждом сайте вы можете установить один или несколько дополнительных серверов системы сайта. Вы можете не устанавливать дополнительные серверы системы сайта и выполнять все роли системы сайта непосредственно на компьютере сервера сайта. Каждый сервер системы сайта поддерживает одну или несколько ролей системы сайта. Дополнительные серверы помогают расширить возможности и емкость сайта, распределяя процессорную нагрузку, которую создают роли системы сайта на сервере.  

Планируя добавление сервера системы сайта, убедитесь, что сервер отвечает требованиям предполагаемого использования. Вы также можете добавить его в сетевое расположение, которое имеет достаточную пропускную способность для взаимодействия с ожидаемыми конечными точками. Эти конечные точки включают в себя сервер сайта, ресурсы домена, облачное расположение, серверы системы сайта и клиенты.  


## <a name="site-system-roles"></a><a name="bkmk_planroles"></a> Site system roles  

Установите роли системы сайта на сервере для предоставления сайту дополнительных возможностей. Примеры:  

- дополнительные точки управления для поддержки сайтом большего числа устройств (в пределах доступных ресурсов сайта);  

- дополнительные точки распространения для расширения инфраструктуры содержимого и повышения производительности распространения содержимого для устройств;  

- одна или несколько ролей системы сайта, определяемых конкретными компонентами. Например, точка обновления программного обеспечения позволяет управлять обновлениями программного обеспечения для управляемых устройств. Точка служб отчетов позволяет создавать отчеты для отслеживания и анализа сведений о среде.  

Разные сайты Configuration Manager могут поддерживать разные наборы ролей системы сайта. Поддерживаемые наборы ролей системы сайта зависят от типа сайта. (Эти типы включают в себя сайт центра администрирования, первичный сайт или вторичный сайт.) Топология иерархии может ограничивать размещение некоторых ролей на определенных типах сайтов. Например, точка подключения службы поддерживается только на сайте верхнего уровня иерархии. Он может быть сайтом центра администрирования или автономным первичным сайтом. Эта роль не поддерживается на дочернем первичном сайте или на вторичных сайтах.  

После установки сайта можно переместить расположение некоторых ролей системы сайта из их расположений по умолчанию на сервере сайта на другой сервер. Например, роли точки управления или точки распространения по умолчанию устанавливаются на сервере первичного или вторичного сайта. Вы также можете установить дополнительные экземпляры некоторых ролей системы сайта, чтобы расширить возможности сайта и удовлетворить бизнес-требования. Некоторые роли обязательны, другие — устанавливаются по мере необходимости.  

### <a name="configuration-manager-site-server"></a>Сервер сайта Configuration Manager

Эта роль определяет сервер, на котором запускается программа установки Configuration Manager для установки сайта, или сервер, на котором устанавливается вторичный сайт. Эту роль нельзя переместить или удалить до удаления сайта.  

### <a name="configuration-manager-site-system"></a>Система сайта Configuration Manager

Эта роль назначается любому компьютеру, на котором устанавливается сайт или роль системы сайта. Эту роль нельзя переместить или удалить, пока с компьютера не будет удалена последняя роль системы сайта.  

### <a name="configuration-manager-component-site-system-role"></a>Роль системы сайта компонента Configuration Manager

Эта роль идентифицирует систему сайта, в которой запущен экземпляр службы **SMS Executive**. Она требуется для поддержки других ролей, таких как точки управления. Эту роль нельзя переместить или удалить, пока с компьютера не будет удалена последняя соответствующая роль системы сайта.  

### <a name="configuration-manager-site-database-server"></a>Сервер базы данных сайта Configuration Manager

Сайт назначает эту роль серверам системы сайта, на которых хранится экземпляр базы данных для сайта. Вы можете переместить эту роль на новый сервер, только запустив программу установки, чтобы настроить для сайта использование другого экземпляра сервера SQL Server для размещения базы данных сайта.  

### <a name="sms-provider"></a>Поставщик SMS

Сайт назначает эту роль каждому компьютеру, на котором размещается экземпляр поставщика SMS. Поставщик — это интерфейс между консолью Configuration Manager и базой данных сайта. По умолчанию эта роль автоматически устанавливается на сервере сайта центра администрирования и первичных сайтах. Вы можете установить дополнительные экземпляры на каждом сайте, чтобы предоставить доступ к сайту пользователям с правами администратора или обеспечить избыточность.  

Чтобы установить дополнительные поставщики, запустите программу установки Configuration Manager для [управления поставщиком SMS](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider). Затем установите дополнительные поставщики на дополнительных компьютерах. На каждом компьютере можно установить только один экземпляр поставщика SMS. Этот компьютер должен располагаться в том же домене, что и сервер сайта.  

### <a name="application-catalog-web-service-point"></a>Точка веб-службы каталога приложений

> [!Important]
> Пользовательский интерфейс Silverlight каталога приложений не поддерживается в текущей ветви версии 1806. Начиная с версии 1906, обновленные клиенты автоматически используют точку управления для развертываний приложений, доступных пользователю. Но вы не можете устанавливать новые роли каталога приложений. Поддержка ролей каталога приложений прекращена в версии 1910.  
>
> Дополнительные сведения см. в следующих статьях:
>
> - [Настройка центра программного обеспечения](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Удаленные и устаревшие компоненты](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Роль системы сайта, которая предоставляет сведения о программном обеспечении из библиотеки программного обеспечения на веб-сайт каталога приложений. Несмотря на то что эта роль поддерживается только на первичных сайтах, можно установить несколько экземпляров этой роли на сайте или на нескольких сайтах в той же иерархии.  

### <a name="application-catalog-website-point"></a>Точка веб-сайта каталога приложений

> [!Important]
> Пользовательский интерфейс Silverlight каталога приложений не поддерживается в текущей ветви версии 1806. Начиная с версии 1906, обновленные клиенты автоматически используют точку управления для развертываний приложений, доступных пользователю. Но вы не можете устанавливать новые роли каталога приложений. Поддержка ролей каталога приложений прекращена в версии 1910.  
>
> Дополнительные сведения см. в следующих статьях:
>
> - [Настройка центра программного обеспечения](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Удаленные и устаревшие компоненты](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Роль системы сайта, которая предоставляет пользователям список программного обеспечения, доступного в каталоге приложений. Несмотря на то что эта роль поддерживается только на первичных сайтах, можно установить несколько экземпляров этой роли на сайте или на нескольких сайтах в той же иерархии.  

### <a name="asset-intelligence-synchronization-point"></a>точка синхронизации каталога аналитики активов;

Роль системы сайта, которая подключается к службам Майкрософт для скачивания сведений о каталоге аналитики активов. Эта роль также передает продукты без категории для их последующего включения в каталог корпорацией Майкрософт. Иерархия поддерживает только один экземпляр этой роли, размещенный на сайте верхнего уровня в иерархии. При расширении автономного первичного сайта в более крупную иерархию необходимо удалить эту роль основного сайта. Затем установите ее на сайте центра администрирования.

Дополнительные сведения см. в статье [Аналитика активов в Configuration Manager](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

### <a name="certificate-registration-point"></a>Точка регистрации сертификатов

Роль системы сайта, взаимодействующая с сервером, на котором выполняется служба регистрации сертификатов для сетевых устройств (NDES). Эта роль необходима для управления запросами сертификатов устройств, использующих протокол SCEP. Эта роль поддерживается только на первичных сайтах и на сайте центра администрирования.

Несмотря на то что одна точка регистрации сертификатов может обеспечить функционирование всей иерархии, можно установить несколько экземпляров этой роли на сайте или на нескольких сайтах в той же иерархии. Эта конфигурация упрощает распределение нагрузки. Если в иерархии имеется несколько экземпляров, клиенты назначаются одной из точек регистрации сертификатов случайным образом.  

Каждой точке регистрации сертификатов требуется доступ к отдельному экземпляру NDES. Несколько точек регистрации сертификатов нельзя настроить для использования одного и того же экземпляра NDES. Кроме того, не устанавливайте точку регистрации сертификатов на том же сервере, на котором запущена служба NDES.  

### <a name="cloud-management-gateway-connection-point"></a>Точка подключения шлюза управления облачными клиентами

Это роль системы сайта для взаимодействия со [шлюзом управления облаком](../../clients/manage/cmg/plan-cloud-management-gateway.md).  

### <a name="data-warehouse-service-point"></a>Точка обслуживания хранилища данных

Точка обслуживания хранилища данных позволяет длительно хранить исторические данные в среде Configuration Manager и создавать отчеты на их основе. Дополнительные сведения см. в статье [Хранилище данных](../../servers/manage/data-warehouse.md).  

### <a name="distribution-point"></a>Точка распространения

Роль системы сайта, которая содержит исходные файлы, скачиваемые клиентами, например:

- Содержимое приложения
- Пакеты программного обеспечения
- Обновления программного обеспечения
- Образы ОС
- загрузочные образы,  

По умолчанию эта роль устанавливается на сервере сайта при установке нового первичного или вторичного сайта. Она не поддерживается на сайте центра администрирования. Вы можете установить несколько экземпляров этой роли на поддерживаемом сайте или на нескольких сайтах в той же иерархии. Дополнительные сведения см. в статьях [Основные принципы управления содержимым](fundamental-concepts-for-content-management.md) и [Управление содержимым и инфраструктурой содержимого](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="endpoint-protection-point"></a>Точка Endpoint Protection

Роль системы сайта, используемая Configuration Manager для принятия условий лицензионного соглашения Endpoint Protection и настройки членства по умолчанию в службе Cloud Protection. Иерархия поддерживает только один экземпляр этой роли, размещенный на сайте верхнего уровня. При расширении автономного первичного сайта в более крупную иерархию удалите эту роль с первичного сайта, а затем установите ее на сайте центра администрирования. Дополнительные сведения см. в статье [Endpoint Protection в Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

### <a name="enrollment-point"></a>Точка регистрации

Роль системы сайта, которая использует PKI-сертификаты Configuration Manager для регистрации мобильных устройств и компьютеров macOS. Несмотря на то что эта роль поддерживается только на первичных сайтах, можно установить несколько экземпляров этой роли на сайте или на нескольких сайтах в той же иерархии.  

Если пользователь регистрирует мобильные устройства с помощью Configuration Manager и учетная запись Active Directory пользователя находится в лесу, который не имеет отношений доверия с лесом сервера сайта, установите точку регистрации в лесу пользователя. После этого Configuration Manager сможет проверить подлинность пользователя.  

### <a name="enrollment-proxy-point"></a>Прокси-точка регистрации.

Роль системы сайта, которая управляет запросами на регистрацию Configuration Manager от мобильных устройств и компьютеров macOS. Несмотря на то что эта роль поддерживается только на первичных сайтах, можно установить несколько экземпляров этой роли на сайте или на нескольких сайтах в той же иерархии.  

Если обеспечивается поддержка мобильных устройств в Интернете, установите одну прокси-точку регистрации в сети периметра и еще одну в интрасети.

### <a name="exchange-server-connector"></a>Соединитель Exchange Server

Сведения об этой роли см. в статье [Управление мобильными устройствами с помощью Configuration Manager и Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="fallback-status-point"></a>Резервная точка состояния

Роль системы сайта, помогающая отслеживать установку клиента. Она позволяет определять, какими клиентами невозможно управлять из-за отсутствия связи с точкой управления. Хотя эта роль поддерживается только на первичных сайтах, можно установить несколько экземпляров этой роли на одном сайте и нескольких сайтах в той же иерархии.

### <a name="management-point"></a>Точка управления

Роль системы сайта, которая предоставляет клиентам сведения о политике и расположении служб. Она также принимает данные конфигурации от клиентов.  

По умолчанию эта роль устанавливается на сервере сайта при установке нового первичного или вторичного сайта. Первичные сайты поддерживают несколько экземпляров этой роли. Вторичные сайты поддерживают одну точку управления. Эта роль на вторичном сайте, также называемая прокси-точкой управления, предоставляет локальную точку контакта для клиентов с целью получения политик компьютера и пользователя.  

Настройте для точек управления поддержку протокола HTTP или HTTPS. Они также могут поддерживать мобильные устройства, которыми вы управляете с помощью локального управления мобильными устройствами (MDM) в Configuration Manager. Чтобы снизить процессорную нагрузку на сервер базы данных сайта, которую создают точки управления при обработке запросов от клиентов, используйте [реплики базы данных для точек управления](../../servers/deploy/configure/database-replicas-for-management-points.md).  

### <a name="reporting-services-point"></a>Точка служб отчетов

Роль системы сайта, которая интегрируется со службами SQL Server Reporting Services для создания отчетов и управления ими в Configuration Manager. Эта роль поддерживается на первичных сайтах и на сайте центра администрирования, кроме того, вы можете установить несколько экземпляров этой роли на поддерживаемом сайте. Дополнительные сведения см. в разделе [Планирование отчетов](../../servers/manage/planning-for-reporting.md).  

### <a name="service-connection-point"></a>Точка подключения службы

Роль системы сайта, которая отправляет данные по использованию с сайта и требуется для того, чтобы обновления для Configuration Manager стали доступными в консоли. Иерархия поддерживает только один экземпляр этой роли, размещенный на сайте верхнего уровня в иерархии. При расширении автономного первичного сайта в более крупную иерархию удалите эту роль с первичного сайта, а затем установите ее на сайте центра администрирования. Дополнительные сведения см. в статье [Точки подключения службы](../../servers/deploy/configure/about-the-service-connection-point.md).  

### <a name="software-update-point"></a>Точка обновления программного обеспечения

Роль системы сайта, которая интегрируется со службами Windows Server Update Services (WSUS) для предоставления обновлений программного обеспечения клиентам Configuration Manager. Эта роль поддерживается на всех сайтах.  

- Установите эту роль системы сайта на сайте центра администрирования для синхронизации со службами WSUS.  

- Настройте каждый экземпляр этой роли на дочерних первичных сайтах для синхронизации с сайтом центра администрирования.  

- Если данные передаются по сети слишком медленно, рекомендуется установить точку обновления программного обеспечения на вторичных сайтах.  

Дополнительные сведения см. в статье [Планирование обновлений программного обеспечения](../../../sum/plan-design/plan-for-software-updates.md).  

### <a name="state-migration-point"></a>точка миграции состояния,

Эта роль системы сайта хранит данные по состоянию пользователей при переводе компьютера на новую операционную систему. Эта роль поддерживается на первичных и вторичных сайтах. Вы можете установить несколько экземпляров этой роли на одном или нескольких сайтах в той же иерархии. Дополнительные сведения о сохранении состояния пользователей при развертывании ОС см. в статье [Управление пользовательской средой](../../../osd/get-started/manage-user-state.md).  


## <a name="next-steps"></a>Дальнейшие шаги

Для некоторых ролей системы сайта Configuration Manager требуется подключение к Интернету. Если в среде требуется подключение к Интернету для использования прокси-сервера, настройте эти роли системы сайта для использования прокси-сервера. Дополнительные сведения см. в статье [Поддержка прокси-сервера](../network/proxy-server-support.md).  