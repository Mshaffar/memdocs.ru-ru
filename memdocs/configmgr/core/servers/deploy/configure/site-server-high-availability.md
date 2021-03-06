---
title: Высокая доступность сервера сайта
titleSuffix: Configuration Manager
description: Сведения о настройке высокой доступности для сервера сайта Configuration Manager путем добавления сервера сайта в пассивном режиме.
ms.date: 02/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6dcef836-c0d1-40af-ad30-cd8d864b09a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 395504f5ccc3635f580bca739f1c4b7273861123
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700902"
---
# <a name="site-server-high-availability-in-configuration-manager"></a>Высокая доступность сервера сайта в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

<!--1128774-->

Сложилось так, что можно добавить избыточность к большей части ролей в Configuration Manager, развернув несколько экземпляров этих ролей в вашей среде. Исключением выступает лишь сам сервер сайта. Высокий уровень доступности для роли сервера сайта — это решение на основе Configuration Manager, которое предусматривает установку дополнительного сервера сайта в *пассивном* режиме. Сайт центра администрирования и первичные дочерние сайты теперь могут использовать сервер дополнительного сайта в пассивном режиме. Сервер сайта в пассивном режиме может работать локально или в облаке Azure.

Преимущества функции:

- избыточность и высокий уровень доступности роли сервера сайта;  
- упрощенная замена оборудования или изменение операционной системы сервера сайта;  
- упрощенное перемещение сервера сайта в Azure IaaS.  

Сервер сайта в пассивном режиме — это дополнение к существующему серверу сайта, который работает в *активном* режиме. Сервер сайта в пассивном режиме готов к использованию в любой момент, когда это необходимо. Включите этот дополнительный сервер сайта в общую концепцию по обеспечению [высокой доступности](high-availability-options.md) службы Configuration Manager.  

Сервер сайта в пассивном режиме:

- использует ту же базу данных сайта, что и сервер сайта в активном режиме;
- не записывает данные в базу данных сайта, пока находится в пассивном режиме;
- использует ту же библиотеку содержимого, что и сервер сайта в активном режиме.

Чтобы активировать сервер сайта в пассивном режиме, нужно вручную *повысить его уровень*. При этом сервер сайта в активном режиме переводится в пассивный режим. Все роли системы сайта, которые существуют на исходном активном сервере, останутся доступными, пока доступен соответствующий компьютер. Переключение активного и пассивного режимов выполняется только для роли сервера сайта.

Подразделение Microsoft Core Services Engineering and Operations использовало эту функцию для переноса сайта центра администрирования в Microsoft Azure. Дополнительные сведения см. в статье [Migrating System Center Configuration Manager on-premises infrastructure to Microsoft Azure](https://www.microsoft.com/itshowcase/Article/Content/1065/Migrating-System-Center-Configuration-Manager-onpremises-infrastructure-to-Microsoft-Azure) (Перенос локальной инфраструктуры System Center Configuration Manager в Microsoft Azure).

## <a name="prerequisites"></a>Предварительные условия

- Библиотека содержимого сайта должна находиться в удаленной сетевой папке. Обоим серверам сайта нужны разрешения "Полный доступ" для этой общей папки и ее содержимого. Дополнительные сведения см. в разделе [Настройка библиотеки удаленного содержимого на сервере сайта](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote).<!--1357525-->  

  - Учетной записи компьютера сервера сайта необходимы разрешения на **полный доступ** для сетевого пути, по которому перемещается библиотека содержимого. Это разрешение применяется к общей папке и файловой системе. В удаленной системе компоненты не установлены.

  - Сервер сайта не может иметь роль точки распространения. Точка распространения также использует библиотеку содержимого, и эта роль не поддерживает библиотеку удаленного содержимого. После перемещения библиотеки содержимого роль точки распространения невозможно добавить на сервер сайта.  

- Сервер сайта в пассивном режиме может работать локально или в облаке Azure.  

    > [!NOTE]
    > Облачный сервер сайта в пассивном режиме использует инфраструктуру как услугу (IaaS) Azure. Дополнительные сведения см. в следующих статьях:
    >
    >   - [Виртуальные машины Azure (для облачной инфраструктуры)](../../../understand/use-cloud-services.md#azure-virtual-machines-for-cloud-based-infrastructure)
    >   - [Часто задаваемые вопросы по Configuration Manager в Azure](../../../understand/configuration-manager-on-azure.md)  

- Оба сервера сайта должны быть присоединены к одному и тому же домену Active Directory.  

- Configuration Manager поддерживает серверы сайта в пассивном режиме в иерархии. Сайт центра администрирования и первичные дочерние сайты теперь могут использовать сервер дополнительного сайта в пассивном режиме.<!-- 3607755 -->  

- На обоих серверах сайта необходимо использовать одну и ту же базу данных сайта.  

  - База данных может находиться удаленно от каждого сервера сайта. Начиная с версии 1810 процесс установки Configuration Manager более не блокирует установку роли сервера сайта на компьютере с ролью Windows для отказоустойчивой кластеризации. Эта роль требуется для SQL Always On, в связи с чем ранее было невозможно размещать базу данных сайта на сервере сайта. Благодаря этому изменению вы можете создать сайт с высоким уровнем доступности с меньшим количеством серверов за счет использования SQL Always On и сервера сайта в пассивном режиме.<!-- SCCMDocs issue 1074 -->  

  - Сервер SQL Server, на котором размещена эта база данных сайта, может использовать экземпляр по умолчанию, именованный экземпляр, [кластер SQL Server](use-a-sql-server-cluster-for-the-site-database.md) или [группу доступности AlwaysOn SQL Server](sql-server-alwayson-for-a-highly-available-site-database.md).  

  - Обоим серверам сайта нужны роли безопасности **sysadmin** в экземпляре SQL Server, где размещается база данных сайта. На исходном сервере сайта уже должны быть эти роли, поэтому добавьте их для нового сервера сайта. Например, следующий скрипт SQL добавляет эти роли для нового сервера сайта **VM2** в домене Contoso:  

    ```SQL
    USE [master]
    GO
    CREATE LOGIN [contoso\vm2$] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
    GO
    ALTER SERVER ROLE [sysadmin] ADD MEMBER [contoso\vm2$]
    GO
    ```

  - Обоим серверам сайта требуется доступ к базе данных сайта в экземпляре SQL Server. На исходном сервере сайта уже должен быть этот доступ, поэтому добавьте его для нового сервера сайта. Например, следующий скрипт SQL добавляет имя входа в базу данных **CM_ABC** для сервера сайта **VM2** в домене Contoso:  

    ```SQL
    USE [CM_ABC]
    GO
    CREATE USER [contoso\vm2$] FOR LOGIN [contoso\vm2$] WITH DEFAULT_SCHEMA=[dbo]
    GO
    ```

  - Для сервера сайта в пассивном режиме настраивается та же база данных сайта, что и для сервера сайта в активном режиме. Сервер сайта в пассивном режиме только считывает данные из базы данных. Он не осуществляет запись в базу данных до повышения уровня для переключения в активный режим.  

- Особенности сервера сайта в пассивном режиме:  

  - должен соответствовать всем обязательным условиям для установки первичного сайта, например .NET Framework, удаленное разностное сжатие и Windows ADK (полный список см. в разделе [Предварительные требования к сайту и системе сайта для Configuration Manager](../../../plan-design/configs/site-and-site-system-prerequisites.md));<!-- SCCMDocs issue 765 -->  

    > [!NOTE]
    > Обязательно установите SQL Server Native Client. В противном случае средство проверки готовности к установке сообщит об отсутствии разрешений для SQL Server во время установки Configuration Manager.<!-- SCCMDocs#2290 -->

  - его учетная запись компьютера должна входить в группу "Локальные администраторы" на сервере сайта в активном режиме;<!--516036-->

  - для его установки должны использоваться исходные файлы той же версии, что и для сервера сайта в активном режиме;  

  - перед установкой сервера сайта в роли пассивного режима на нем не должна выполняться роль системы сайта с любого установленного на нем сайта.  

- Оба сервера сайта могут использовать разные версии ОС или пакетов обновления при условии, что они [поддерживаются Configuration Manager](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).  

- Не размещайте роль точки подключения службы на сервере сайта, настроенном для обеспечения высокого уровня доступности. Если она в данный момент находится на исходном сервере сайта, удалите ее и установите на другом сервере системы сайта. Дополнительные сведения см. в статье [Точки подключения службы](about-the-service-connection-point.md).  

- Разрешения, которые должны быть у [учетной записи установки системы сайта](../../../plan-design/hierarchy/accounts.md#site-system-installation-account):  

  - По умолчанию многие клиенты используют учетную запись компьютера сервера сайта для установки новых систем сайта. В таком случае нужно добавить учетную запись компьютера сервера сайта в локальную группу **Администраторы** в удаленной системе сайта. Если эта конфигурация используется в среде, обязательно добавьте учетную запись компьютера нового сервера сайта в эту локальную группу во всех удаленных системах сайта. Например, на всех удаленных точках распространения.  

  - Более безопасная и рекомендуемая конфигурация — использование учетной записи службы для установки системы сайта. Наиболее безопасная конфигурация — использование локальной учетной записи службы. Если эта конфигурация используется в среде, изменений не требуется.  

## <a name="limitations"></a>Ограничения

- Для каждого сайта поддерживается только один сервер сайта в пассивном режиме.  

- Сервер сайта в пассивном режиме не поддерживается на вторичном сайте.<!--SCCMDocs issue 680-->  

    > [!NOTE]  
    > Вторичные сайты по-прежнему поддерживаются на первичном сайте с высокодоступными серверами сайта.

- Повышение уровня сервера сайта в пассивном режиме до активного режима выполняется вручную. Автоматическая отработка отказа не применяется.  

- Роли системы сайта невозможно установить на новом сервере сайта до перевода его в пассивный режим.  

    > [!NOTE]
    > После установки сервера сайта в пассивном режиме при необходимости можно добавить дополнительные роли. Например, точку управления на первичном сайте.

- Для таких ролей, как точка формирования отчетов, использующих базу данных, следует разместить эту базу данных на сервере, являющемся удаленным для обоих серверов сайта.  

- Консоль Configuration Manager не устанавливается автоматически на сервере сайта в пассивном режиме.  

## <a name="add-a-site-server-in-passive-mode"></a>Добавление сервера сайта в пассивном режиме

Дополнительные сведения об общей процедуре добавления ролей см. в разделе [Установка ролей системы сайта](install-site-system-roles.md).

1. В консоли Configuration Manager перейдите в рабочую область **Администрирование**, разверните узел **Конфигурация сайта**, выберите узел **Сайты**, а затем щелкните **Создать сервер системы сайта** на ленте.

2. На странице **Общие** мастера создания сервера системы сайта укажите сервер для размещения сервера сайта в пассивном режиме. Вы не сможете установить сервер сайта в пассивном режиме, если на выбранном сервере размещены роли системы сайта.  

3. На странице **Выбор системной роли** выберите только **Сервер сайта в пассивном режиме**.  

    > [!NOTE]  
    > На этой странице мастер выполняет следующие проверки необходимых условий:
    >
    > - Выбранный сервер не является сервером вторичного сайта
    > - Выбранный сервер не является сервером сайта в пассивном режиме
    > - Библиотека содержимого сайта находится в удаленном расположении  
    >  
    > Если эти проверки необходимых условий не пройдены, вы не сможете продвинуться дальше этой страницы мастера.  

4. На странице **Сервер сайта в пассивном режиме** укажите следующие сведения для запуска программы установки и установки роли сервера сайта на указанном сервере:

     - Выберите один из следующих вариантов.  

         - **Копировать исходные файлы установки с сервера сайта по сети в активном режиме**: этот параметр создает сжатый пакет и отправляет его на новый сервер сайта.  

         - **Использовать исходные файлы в следующем расположении на сервере сайта в пассивном режиме**: например локальный путь, по которому вы уже скопировали исходные файлы. Убедитесь, что это содержимое имеет ту же версию, что и сервер сайта в активном режиме.  

         - (*Рекомендуется*) **Использовать исходные файлы в следующей сетевой папке**: укажите путь непосредственно к содержимому папки **CD.Latest** с сервера сайта в активном режиме. Например, `\\Server\SMS_ABC\CD.Latest`, где "*Server*" — имя сервера сайта в активном режиме, а "*ABC*" — это код сайта.  

     - Укажите локальный путь, по которому следует установить Configuration Manager на новом сервере сайта. Пример: `C:\Program Files\Configuration Manager`  

5. Завершите работу мастера. Теперь Configuration Manager установит сервер сайта в пассивном режиме на указанном сервере.

Чтобы получить подробные сведения о состоянии установки, перейдите в рабочую область **Мониторинг** в консоли и выберите узел **Состояние сервера сайта**. Для сервера сайта в пассивном режиме здесь отображается состояние **Установка**. Для получения более подробных сведений выберите сервер и нажмите кнопку **Показать состояние**. Это действие открывает окно "Состояние установки сервера сайта". По завершении процесса для обоих серверов отображается состояние **ОК**.

Дополнительные сведения о процессе установки см. в разделе [Блок-схема настройки сервера сайта в пассивном режиме](passive-site-server-flowchart.md).

После добавления сервера сайта в пассивном режиме просмотрите оба сервера сайта на вкладке **Узлы** узла **Сайты** в консоли.

Все компоненты сервера сайта Configuration Manager на сервере сайта в пассивном режиме находятся в состоянии ожидания. Службы Windows продолжают работать.

## <a name="site-server-promotion"></a>Повышение уровня сервера сайта  

Как и в случае с резервным копированием и восстановлением, спланируйте процесс изменения серверов сайта и отработайте его на практике. При планировании повышения уровня учтите следующие аспекты:  

- Отработайте на практике плановое повышение уровня, когда оба сервера сайта работают. Кроме того, отработайте на практике внеплановую отработку отказа, принудительно отключив сервер сайта в активном режиме или завершив его работу.  

- Определите свои рабочие процедуры во время отработки отказа и сведения, которые требуется передать другим администраторам Configuration Manager.  

- Перед плановым повышением уровня:  

  - проверьте общее состояние сайта и его компонентов; убедитесь, что все компоненты вашей среды находятся в работоспособном состоянии;  

  - проверьте состояние содержимого для любых пакетов, активно реплицируемых между сайтами;  

  - Проверьте состояние вторичного сайта и репликацию сайта.

  - Не начинайте любые новые задания по распространению содержимого или обслуживания на серверах дочерних или вторичных сайтов.

    > [!NOTE]
    > Если во время отработки отказа выполняется репликация файлов или базы данных между сайтами, новый сервер сайта может не получить реплицируемое содержимое. В этом случае повторно распространите содержимое программного обеспечения после активации нового сервера сайта.<!--515436--> Для репликации базы данных может потребоваться повторная инициализация вторичного сайта после отработки отказа.<!-- SCCMDocs issue 808 -->

  - Сократите или удалите другие действия, запланированные на одно и то же время. Например, не планируйте повышение уровня сервера сайта сразу после обновления сайта до новой версии. Обновление сайта включает другие задачи, которые могут конфликтовать с повышением уровня сервера сайта.

    > [!TIP]
    > Ниже приведен пример того, как другие действия могут конфликтовать с повышением уровня сервера сайта.
    >
    > - Понедельник: обновление сайта до последней версии. Включение автоматического обновления клиента с помощью пилотного развертывания клиента.
    > - Вторник: повышение уровня сервера сайта в пассивном режиме до активного сервера сайта.
    >
    > К среде или четвергу это действие может привести к обновлению *всех* клиентов, а не только лишь пилотной коллекции. Такое поведение может привести к значительному повышению объема использования сети и непредвиденной нагрузке на точки распространения.<!-- SCCMDocs-pr#4794 -->

### <a name="process-to-promote-the-site-server-in-passive-mode-to-active-mode"></a>Процедура повышения уровня сервера сайта в пассивном режиме до активного режима

Этот раздел описывает, как повысить уровень сервера сайта в пассивном режиме до активного режима. Чтобы обратиться к сайту и внести это изменение, требуется доступ к экземпляру поставщика SMS. Дополнительные сведения см. в разделе [Использование нескольких поставщиков SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md#BKMK_MultiSMSProv).  

> [!IMPORTANT]  
> Если все экземпляры поставщика SMS находятся в автономном режиме, вы не сможете подключиться к сайту из-за отсутствия поставщика. При добавлении сервера сайта в пассивном режиме программа установки устанавливает на этом сервере экземпляр поставщика SMS.<!-- SCCMDocs#1613 -->
>
> Консоль Configuration Manager запрашивает список доступных поставщиков SMS из инструментария WMI на сервере сайта. Когда на сайте установлено несколько поставщиков SMS, он случайным образом назначает каждому новому запросу на подключение один из установленных поставщиков SMS. Указать определенное расположение поставщика SMS для конкретного сеанса подключения невозможно. Если консоли не удается подключиться к сайту из-за того, что текущий сервер сайта находится в автономном режиме, укажите другой сервер сайта в окне "Подключение к сайту".  

1. В консоли Configuration Manager перейдите в рабочую область **Администрирование**, разверните узел **Конфигурация сайта** и выберите узел **Сайты**. Выберите сайт, а затем перейдите на вкладку **Узлы**. Выберите сервер сайта в пассивном режиме, а затем щелкните **Перевести в активный режим** на ленте. Нажмите кнопку **Да**, чтобы подтвердить и продолжить.
  
2. Обновите узел консоли. Столбец **Состояние** для сервера, уровень которого вы повышаете, отображается на вкладке **Узлы** в виде **Идет перевод**.  

3. Когда повышение уровня завершается, в столбце **Состояние** отображается **ОК** как для нового сервера сайта в активном режиме, так и для нового сервера сайта в пассивном режиме. В столбце **Имя сервера** для сайта теперь отображается имя нового сервера сайта в активном режиме.

Чтобы получить подробные сведения о состоянии, перейдите в рабочую область **Мониторинг** и выберите узел **Состояние сервера сайта**. Столбец **Режим** обозначает, какой сервер является *активным* или *пассивным*. При повышении уровня сервера из пассивного режима до активного режима вам нужно указать сервер сайта, уровень которого вы повышаете, и выбрать на ленте элемент **Показать состояние**. При этом открывается окно с состоянием повышения уровня для сервера сайта с подробной информацией о процессе.

Когда сервер сайта переключается из активного режима в пассивный, изменения распространяются только на роль системы сайта. Все остальные роли, установленные на этом компьютере, остаются активными и доступными для клиентов.

Дополнительные сведения о процессе *планового* повышения уровня см. в разделе [Блок-схема планового повышения уровня сервера сайта](promote-site-server-flowchart.md).

### <a name="unplanned-failover"></a>Внеплановая отработка отказа

Если текущий сервер сайта в активном режиме находится в автономном режиме, сервер сайта для повышения уровня в течение 30 минут пытается связаться с текущим сервером сайта в активном режиме. Если до истечения этого периода автономный сервер снова подключается к сети, он успешно уведомляется и изменение продолжается корректно. В противном случае сервер сайта для повышения уровня принудительно изменяет конфигурацию сайта, чтобы сделать его активным. Если автономный сервер подключается к сети по истечении этого времени, он сначала проверяет текущее состояние в базе данных сайта. Затем он понижает свой уровень до сервера сайта в пассивном режиме.

В течение этого 30-минутного периода ожидания у сайта нет сервера сайта в активном режиме. Клиенты продолжают взаимодействовать с клиентскими ролями, такими как точки управления, точки обновления программного обеспечения и точки распространения. Пользователи могут устанавливать программное обеспечение, которое уже развернуто. Администрирование сайта в этот период невозможно. Дополнительные сведения см. в разделе [Последствия сбоев в работе сайта](../../manage/site-failure-impacts.md).  

Если автономный сервер сайта поврежден настолько, что не может возобновить работу, удалите его из консоли. Затем создайте сервер сайта в пассивном режиме, чтобы восстановить службу высокой доступности.

Дополнительные сведения о процессе *внеплановой* отработки отказа см. в разделе [Блок-схема внепланового повышения уровня сервера сайта](promote-site-server-unplanned-flowchart.md).

### <a name="additional-tasks-after-site-server-promotion"></a>Дополнительные задачи после повышения уровня сервера сайта  

После переключения серверов сайта не требуется выполнять большинство других задач, которые необходимы при [восстановлении сайта](../../manage/recover-sites.md#post-recovery-tasks). Например, не нужно сбрасывать пароли или повторно подключать подписку Microsoft Intune.

При необходимости в вашей среде могут потребоваться следующие действия:  

- В случае импорта PKI-сертификатов для точек распространения повторно импортируйте сертификат для затронутых серверов. Дополнительные сведения см. в разделе [Повторное создание сертификатов для точек распространения](../../manage/recover-sites.md#regenerate-the-certificates-for-distribution-points).  

- В случае интеграции Configuration Manager с Microsoft Store для бизнеса перенастройте это подключение. Дополнительные сведения см. в разделе [Управление приложениями, приобретенными в Microsoft Store для бизнеса](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).  

## <a name="daily-monitoring"></a>Ежедневный мониторинг

При наличии сервера сайта в пассивном режиме его мониторинг следует осуществлять ежедневно. Убедитесь, что он находится в состоянии ОК и готов к использованию. В консоли Configuration Manager перейдите в рабочую область **Мониторинг** и выберите узел **Состояние сервера сайта**. Просмотрите оба сервера сайта и их текущее состояние. Также просмотрите состояние в рабочей области **Администрирование**. Разверните узел **Конфигурация сайта** и выберите узел **Сайты**. Выберите сайт, а затем перейдите на вкладку **Узлы**.

> [!NOTE]
> При обновлении сайта до новой версии Configuration Manager также обновляется сервер сайта в пассивном режиме. <!-- SCCMDocs-pr#4293 -->