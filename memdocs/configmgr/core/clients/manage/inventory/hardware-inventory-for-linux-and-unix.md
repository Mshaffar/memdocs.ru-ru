---
title: Инвентаризация оборудования для Linux и UNIX
titleSuffix: Configuration Manager
description: См. руководство по инвентаризации оборудования для Linux и UNIX в Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1bdfb8c6d528c12581f05f86111a1a76d2259faa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695432"
---
# <a name="hardware-inventory-for-linux-and-unix-in-configuration-manager"></a>Инвентаризация оборудования для Linux и UNIX в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

> [!Important]  
> Начиная с версии 1902, Configuration Manager не поддерживает клиенты Linux и UNIX. 
> 
> Вы можете управлять серверами Linux с помощью портала управления Microsoft Azure. Решения Azure располагают расширенной поддержкой Linux, которая в большинстве случаев превышает функциональные возможности Configuration Manager, включая полное управление исправлениями для Linux.

Клиент Configuration Manager для Linux и UNIX поддерживает инвентаризацию оборудования. После сбора данных инвентаризации оборудования можно запустить просмотр инвентаризации в обозревателе ресурсов или отчетах Configuration Manager и использовать эти сведения для создания запросов и коллекций, которые позволяют выполнять следующие операции:  

- Развертывание программного обеспечения  

- Принудительное применение периодов обслуживания  

- Развертывание настраиваемых параметров клиента  

Функция инвентаризации оборудования для серверов Linux и UNIX использует сервер на основе модели CIM. CIM-сервер запускается в виде службы программного обеспечения (или управляющей программы) и предоставляет инфраструктуру управления, которая основана на стандартах Distributed Management Task Force (DMTF). CIM-сервер предоставляет функциональные возможности, схожие с возможностями CIM инструментария управления Windows (WMI), которые доступны на компьютерах под управлением Windows.  

Начиная с накопительного пакета обновления 1, клиент для Linux и UNIX использует **omiserver** с открытым исходным кодом версии 1.0.6 из **Open Group**. (До накопительного пакета обновления 1 клиент использовал **nanowbem** в качестве CIM-сервера.)  

CIM-сервер устанавливается в составе клиента для Linux и UNIX. Клиент для Linux и UNIX взаимодействует напрямую с CIM-сервером и не использует интерфейс WS-MAN сервера CIM. Во время установки клиента порт WS-MAN на CIM-сервере отключен. Корпорация Майкрософт разработала CIM-сервер с открытым исходным кодом, доступный в рамках проекта Open Management Infrastructure (OMI). Дополнительные сведения о проекте Open Management Infrastructure см. на веб-сайте [The Open Group](https://www.opengroup.org/) .  

Инвентаризации оборудования на серверах UNIX и Linux работает путем сопоставления существующих свойств и классов WMI Win32 с эквивалентными свойствами и классами для серверов Linux и UNIX. Это взаимно-однозначное сопоставление классов и свойств позволяет функции инвентаризации оборудования Linux и UNIX интегрироваться с Configuration Manager. Данные инвентаризации с серверов Linux и UNIX отображаются вместе с данными инвентаризации с компьютеров с ОС Windows в консоли и отчетах Configuration Manager. Такое поведение обеспечивает согласованное управление разнородными данными.  

> [!TIP]  
>  Вы можете использовать значение **Caption** класса **Operating System** для определения различных ОС Linux и UNIX в запросах и коллекциях.  

##  <a name="configuring-hardware-inventory-for-linux-and-unix-servers"></a><a name="BKMK_ConfigHardwareforLnU"></a> Настройка инвентаризации оборудования для Linux и UNIX  
 При настройке инвентаризации оборудования вы можете использовать параметры клиента по умолчанию или создать настраиваемые параметры для устройства. При использовании настраиваемых параметров клиентского устройства можно настроить классы и свойства, которые требуется собирать только с ваших серверов Linux и UNIX. Вы также можете задать настраиваемые расписания, определяющие график сбора полных и изменившихся данных инвентаризации с серверов Linux и UNIX.  

 Клиент для Linux и UNIX поддерживает следующие классы инвентаризации оборудования, доступные на серверах UNIX и Linux:  

- Win32_BIOS  

- Win32_ComputerSystem  

- Win32_DiskDrive  

- Win32_DiskPartition  

- Win32_NetworkAdapter  

- Win32_NetworkAdapterConfiguration  

- Win32_OperatingSystem  

- Win32_Process  

- Win32_Service  

- Win32Reg_AddRemovePrograms  

- SMS_LogicalDisk  

- SMS_Processor  

Не все свойства для этих классов инвентаризации включены для компьютеров Linux и UNIX в Configuration Manager.  

##  <a name="operations-for-hardware-inventory"></a><a name="BKMK_OperationsforHardwareforLnU"></a> Операции для инвентаризации оборудования  
 После сбора данных инвентаризации оборудования с серверов Linux и UNIX эту информацию можно просматривать и использовать точно так же, как и данные инвентаризации, собираемые с других компьютеров:  

- Используйте обозреватель ресурсов для просмотра подробных сведений о данных инвентаризации оборудования, собранных с серверов Linux и UNIX.  

- Создавайте запросы на основе определенных конфигураций оборудования.  

- Создавайте коллекции на базе запросов, которые основываются на определенных конфигурациях оборудования.  

- Запускайте отчеты, в которых отображаются определенные сведения о конфигурациях оборудования.  

Инвентаризация оборудования на сервере UNIX или Linux выполняется по расписанию, настроенному в параметрах клиента. По умолчанию это раз в семь дней. Клиент для Linux и UNIX поддерживает как циклы сбора полных данных инвентаризации, так и циклы сбора изменившихся данных инвентаризации.  

Вы также можете принудительно заставить клиента на сервере UNIX или Linux выполнить инвентаризацию оборудования. Чтобы осуществить инвентаризацию оборудования, используйте на клиенте **корневые** учетные данные для выполнения следующей команды и запуска цикла инвентаризации оборудования: `/opt/microsoft/configmgr/bin/ccmexec -rs hinv`.  

Действия для инвентаризации оборудования вносятся в файл журнала клиента **scxcm.log**.  

##  <a name="how-to-use-open-management-infrastructure-to-create-custom-hardware-inventory"></a><a name="BKMK_CustomHINVforLinux"></a> Использование Open Management Infrastructure для создания настраиваемой инвентаризации оборудования  
 Клиент для Linux и UNIX поддерживает настраиваемую инвентаризацию оборудования, которую можно создать с помощью Open Management Infrastructure (OMI). Для этого сделайте следующее:  

1.  Создание поставщика настраиваемой инвентаризации с помощью источника OMI  

2.  Настройка компьютеров на использование нового поставщика для вывода отчетов об инвентаризации  

3.  Обеспечение поддержки нового поставщика в Configuration Manager  

###  <a name="create-a-custom-hardware-inventory-provider-for-linux-and-unix-computers"></a><a name="BKMK_LinuxProvider"></a> Создание поставщика настраиваемой инвентаризации оборудования для компьютеров Linux и UNIX:  
 Чтобы создать поставщик настраиваемой инвентаризации оборудования для клиента Configuration Manager для Linux и UNIX, используйте **OMI Source — v.1.0.6** и следуйте инструкциям из руководства по началу работы с OMI. Этот процесс включает создание MOF-файла, который определяет схему нового поставщика. Впоследствии этот MOF-файл импортируется в Configuration Manager для обеспечения поддержки нового класса настраиваемой инвентаризации.  

 Как OMI Source - v.1.0.6, так и руководство по началу работы с OMI можно скачать с веб-сайта [The Open Group](https://github.com/microsoft/omi/blob/master/README.md) . Эти файлы можно найти на вкладке **документов** на странице веб-сайта OpenGroup.org [Open Management Infrastructure (OMI)](https://go.microsoft.com/fwlink/p/?LinkId=286805).  

###  <a name="configure-each-computer-that-runs-linux-or-unix-with-the-custom-hardware-inventory-provider"></a><a name="BKMK_AddProvidertoLinux"></a> Настройте на каждом компьютере, работающем под управлением UNIX или Linux, поставщик инвентаризации оборудования:  
 После создания поставщика настраиваемой инвентаризации необходимо скопировать и затем зарегистрировать файл библиотеки поставщика на каждом компьютере, где имеются данные инвентаризации, которые требуется собрать.  

1.  Скопируйте библиотеку поставщика на каждый компьютер Linux и UNIX, с которого требуется собирать данные инвентаризации. Имя библиотеки поставщика выглядит примерно так: **XYZ_MyProvider.so**.  

2.  Затем зарегистрируйте библиотеку поставщика на каждом компьютере Linux и UNIX с помощью сервера OMI. Сервер OMI устанавливается на компьютере при установке клиента Configuration Manager для Linux и UNIX, однако регистрировать настраиваемых поставщиков необходимо вручную. Для регистрации поставщика используйте следующую команду: `/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so`  

3.  После регистрации нового поставщика проверьте его поставщик с помощью средства **omicli** . Клиент **omicli** устанавливается на каждом компьютере Linux и UNIX при установке клиента Configuration Manager для Linux и UNIX. Например, выполните следующую команду на компьютере (где **XYZ_MyProvider** — имя созданного поставщика): **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     Сведения о **omicli** и тестировании настраиваемых поставщиков см. в руководстве по началу работы с OMI.  

> [!TIP]  
>  Используйте распространение программного обеспечения для развертывания настраиваемых поставщиков и регистрации пользовательских поставщиков на каждом клиентском компьютере Linux и UNIX.  

###  <a name="enable-the-new-inventory-class-in-configuration-manager"></a><a name="BKMK_AddLinuxProvidertoCM"></a> Включите новый класс инвентаризации в Configuration Manager:  
 Чтобы с помощью Configuration Manager можно было создавать отчеты о данных инвентаризации, полученных от нового поставщика с компьютеров Linux и UNIX, необходимо импортировать MOF-файл, определяющий схему настраиваемого поставщика.  

 Инструкции по импорту настраиваемого MOF-файла в Configuration Manager см. в разделе [Настройка инвентаризации оборудования](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  