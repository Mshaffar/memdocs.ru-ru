---
title: Общие сведения о развертывании операционной системы
titleSuffix: Configuration Manager
description: Ознакомьтесь с основными понятиями, прежде чем приступать к развертыванию операционных систем в среде Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d9a1c545-8301-492c-832f-2c108ff93c77
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d53ab2221e3ee936f9b09592a7c7b383b200c928
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703872"
---
# <a name="introduction-to-operating-system-deployment-in-configuration-manager"></a>Общие сведения о развертывании операционных систем в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Configuration Manager можно использовать для развертывания операционных систем разными способами. Используйте сведения в этом разделе, чтобы понять, как осуществить развертывание операционных систем и автоматизацию задач. 

##  <a name="the-operating-system-deployment-process"></a><a name="BKMK_OSDeploymentProcess"></a> Процесс развертывания операционной системы  
 Configuration Manager обеспечивает несколько способов развертывания операционной системы. Независимо от используемого метода развертывания потребуется выполнить несколько обязательных действий:  

-   определение драйверов устройств Windows, необходимых для запуска развертываемого образа загрузки или образа операционной системы;  

-   определение загрузочного образа, который требуется использовать для запуска конечного компьютера  

-   использование последовательности задач для записи образа операционной системы, который требуется развернуть; кроме того, можно использовать образ операционной системы по умолчанию;  

-   передача загрузочного образа, образа операционной системы и другого связанного содержимого на точку распространения;  

-   создание последовательности задач с шагами для развертывания образа загрузки и образа операционной системы;  

-   развертывание последовательности задач в коллекции компьютеров;  

-   мониторинг развертывания.  

##  <a name="operating-system-deployment-scenarios"></a><a name="BKMK_OSDScenarios"></a> Сценарии развертывания операционной системы  
 Существует множество сценариев развертывания операционной системы в Configuration Manager, которые можно выбрать в зависимости от среды и цели установки операционной системы.  Можно, например, секционировать и отформатировать существующий компьютер с использованием новой версии Windows или обновить Windows до более последней версии. Для определения метода развертывания, соответствующего вашим потребностям, см. статью [Сценарии развертывания операционных систем предприятия](../deploy-use/scenarios-to-deploy-enterprise-operating-systems.md).  Вы можете выбирать следующие сценарии развертывания операционной системы:  

-   [Обновление Windows до последней версии](../deploy-use/upgrade-windows-to-the-latest-version.md)  

-   [Обновление существующего компьютера до новой версии Windows](../deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Установка новой версии Windows на новом компьютере (без операционной системы)](../deploy-use/install-new-windows-version-new-computer-bare-metal.md)  

-   [Замена существующего компьютера и перенос параметров](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="methods-to-deploy-operating-systems"></a><a name="BKMK_OSDMethods"></a> Методы, используемые для развертывания операционной системы  
 Предусмотрено несколько способов развертывания операционных систем на клиентских компьютерах Configuration Manager.  

- **Развертывания, запускаемые по сети (PXE)** . Развертывания, запускаемые по сети с помощью протокола PXE, позволяют клиентским компьютерам запрашивать развертывание по сети. Этот метод развертывания подразумевает отправку образа операционной системы и загрузочного образа среды предустановки Windows на точку распространения, поддерживающую прием запросов на загрузку PXE. Дополнительные сведения см. в статье [Use PXE to deploy Windows over the network with Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md) (Использование PXE для развертывания Windows по сети с помощью Configuration Manager).  

- **Сделать операционные системы доступными в Центре программного обеспечения**. Можно развернуть операционную систему и сделать ее доступной в Центре программного обеспечения. Клиенты Configuration Manager могут запускать установку операционной системы из центра программного обеспечения. Дополнительные сведения см. в статье [Замена существующего компьютера и перенос параметров](../deploy-use/replace-an-existing-computer-and-transfer-settings.md).  

- **Многоадресные развертывания**. Многоадресные развертывания экономят пропускную способность сети за счет одновременной отправки данных нескольким клиентам, а не отправки копии данных каждому клиенту по отдельному каналу. Этот метод развертывания подразумевает, что образ операционной системы отправляется в точку распространения. Она в свою очередь выполняет одновременное развертывание образа при получении соответствующего запроса от клиентов. Дополнительные сведения см. в разделе [Использование многоадресной рассылки для развертывания Windows по сети](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

- **Развертывание с загрузочного носителя**. Развертывание с загрузочного носителя позволяет выполнить развертывание операционной системы при запуске конечного компьютера. При запуске конечного компьютера он получает последовательность задач, образ операционной системы и прочее необходимое содержимое из сети. Поскольку контент не размещается на носителе, его можно обновить без повторного создания носителя. Дополнительные сведения см. в разделе [Создание загрузочного носителя](../deploy-use/create-bootable-media.md).  

- **Развертывание с автономного носителя**. Развертывание с автономного носителя позволяет выполнять развертывание операционной системы в следующих ситуациях:  

  - в средах, где копирование образа операционной системы или других крупных пакетов по сети, является непрактичным;  

  - в средах без подключения к сети или с низкой пропускной способностью сети.  

    Дополнительные сведения см. в статье [Создание автономного носителя](../deploy-use/create-stand-alone-media.md).  

- **Развертывания с помощью предварительно подготовленного носителя**. Развертывания с помощью предварительно подготовленного носителя позволяют выполнить развертывание операционной системы на компьютере, подготовка которого еще не завершена. Предварительно подготовленный носитель представляет собой WIM-файл, который может быть установлен на компьютер без операционной системы производителем или в центре подготовки организации без подключения к среде Configuration Manager.  

   Затем в среде Configuration Manager с помощью загрузочного образа, расположенного на носителе, компьютер подключится к точке управления сайта, чтобы получить доступные последовательности задач, которые завершат процесс скачивания. Этот метод развертывания позволяет сократить уровень трафика в сети, так как загрузочный образ и образ операционной системы уже находятся на конечном компьютере. Вы можете указать приложения, пакеты и пакеты драйверов, включаемые в предварительно подготовленный носитель. Дополнительные сведения см. в разделе [Создание предварительно подготовленного носителя](../deploy-use/create-prestaged-media.md).  

##  <a name="boot-images"></a><a name="BKMK_BootImages"></a> загрузочные образы,  
 Образ загрузки в Configuration Manager представляет собой образ среды предустановки Windows (WinPE), используемый во время развертывания операционной системы. Образы загрузки используются для запуска компьютера в среде WinPE — миниатюрной операционной системе с ограниченным набором компонентов и служб, которые подготавливают конечный компьютер к установке Windows. Configuration Manager предоставляет два загрузочных образа: один для поддержки 32-разрядных (x86) платформ, а второй — для 64-разрядных (x64) платформ. Они считаются образами загрузки по умолчанию. Образы загрузки, которые вы создаете и добавляете в Configuration Manager, считаются пользовательскими. Образы загрузки по умолчанию могут быть автоматически заменены при обновлении Configuration Manager. Дополнительные сведения об образах загрузки см. в разделе [Управление загрузочными образами](../get-started/manage-boot-images.md).  

##  <a name="operating--system-images"></a><a name="BKMK_OSImages"></a> Образы операционной системы  
 Образы операционных систем в Configuration Manager — это WIM-файлы, которые представляют собой сжатые наборы эталонных файлов и папок, необходимых для успешной установки и настройки операционной системы на компьютере. Для всех сценариев развертывания операционной системы необходимо выбрать образ операционной системы. Вы можете использовать образ операционной системы по умолчанию или создать такой образ на настроенном компьютере-образце. Дополнительные сведения см. в разделе [Управление образами операционных систем](../get-started/manage-operating-system-images.md).  

##  <a name="operating-system-upgrade-packages"></a><a name="BKMK_OSUpgradePackages"></a> пакеты обновления операционной системы;  
 Пакеты обновления операционной системы используются для обновления операционной системы и представляют собой развертывания операционных систем, запускаемые программой установки. Пакеты обновления операционной системы импортируются в Configuration Manager с DVD-диска или подключенного ISO-файла. Дополнительные сведения см. в разделе [Управление пакетами обновления операционной системы](../get-started/manage-operating-system-upgrade-packages.md).  

##  <a name="media-to-deploy-operating-systems"></a><a name="BKMK_OSDMedia"></a> Носители, используемые для развертывания операционной системы  
 Для развертывания операционных систем можно создавать различные типы носителей. К ним относятся носители для записи, которые используются для записи образов операционных систем, а также автономные, предварительно подготовленные и загрузочные носители, которые используются для развертывания операционной системы. Используя носитель, можно выполнить развертывание операционных систем на компьютерах, не подключенных к сети, или в случае низкой пропускной способности подключения к сайту Configuration Manager. Дополнительные сведения об использовании носителей см. в разделе [Создание носителя последовательности задач](../deploy-use/create-task-sequence-media.md).  

##  <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a> Драйверы устройств  
 Драйверы устройств можно установить на конечных компьютерах, не включая их в развертываемый образ операционной системы. Configuration Manager предоставляет каталог драйверов, содержащий ссылки на все драйверы устройств, импортируемые в Configuration Manager. Каталог драйверов размещается в рабочей области **Библиотека программного обеспечения** и состоит из двух узлов: **Драйверы** и **Пакеты драйверов**. Узел **Драйверы** содержит список всех драйверов, импортированных в каталог драйверов. Этот узел можно использовать для поиска сведений обо всех импортированных драйверах, для изменения принадлежности драйвера пакету драйверов или загрузочному образу, включения и отключения драйвера и выполнения других действий. Дополнительные сведения см. в разделе [Управление драйверами](../get-started/manage-drivers.md).  

##  <a name="save-and-restore-user-state"></a><a name="BKMK_OSDUserState"></a> Сохранение и восстановление пользовательской среды  
 При развертывании операционной системы можно сохранить пользовательскую среду конечного компьютера, выполнить развертывание операционной системы, а затем восстановить пользовательскую среду в новой ОС. Эта процедура, как правило, используется при установке операционной системы на клиентском компьютере Configuration Manager.  

 Данные о пользовательской среде собираются и сохраняются с помощью последовательностей задач. Собранные данные о пользовательской среде можно сохранить одним из следующих способов.  

- Данные пользовательской среды можно сохранить удаленно, настроив точку миграции состояния. Последовательность задач записи отправляет данные на точку миграции состояния. Затем после развертывания операционной системы последовательность задач восстановления получает данные и восстанавливает пользовательскую среду на конечном компьютере.  

- Данные пользовательской среды можно сохранить локально, указав конкретное расположение. В этом случае последовательность задач записи копирует данные пользователя в определенное расположение на конечном компьютере. После развертывания операционной системы последовательность задач восстановления получает данные пользователя из этого расположения.  

- Можно указать жесткие связи, которые будут использоваться для восстановления данных пользователей в исходное расположение. В этом случае данные пользовательской среды остаются на диске, тогда как старая операционная система с него удаляется. После развертывания новой операционной системы последовательность задач восстановления использует жесткие связи для восстановления данных пользовательской среды в исходное расположение.  

  Дополнительные сведения см. в разделе [Управление пользовательской средой](../get-started/manage-user-state.md).  

##  <a name="deploy-to-unknown-computers"></a><a name="BKMK_UnknownComputer"></a> Развертывание на неизвестные компьютеры  
 Операционные системы можно развертывать на компьютерах, не управляемых средствами Configuration Manager. База данных Configuration Manager не содержит записей об этих компьютерах. Такие компьютеры называются неизвестными. К неизвестным компьютерам относятся следующие:  

- компьютеры, на которых не установлен клиент Configuration Manager;  

- компьютеры, которые не импортированы в Configuration Manager;  

- компьютеры, которые не обнаружены Configuration Manager.  

  Дополнительные сведения см. в разделе [Подготовка развертываний на неизвестные компьютеры](../get-started/prepare-for-unknown-computer-deployments.md).  

##  <a name="associate-users-with-a-computer"></a><a name="BKMK_UDA"></a> Сопоставление пользователей с компьютером  
 При развертывании операционной системы можно связать пользователей с конечными компьютерами, чтобы обеспечить поддержку сопоставления пользователей и устройств. Связывая пользователя с конечным компьютером, администратор может впоследствии выполнять действия, выбирая компьютер, связанный с данным пользователем, например, развертывать приложение на компьютере для определенного пользователя. Однако в случае развертывания операционной системы нельзя развернуть ее на компьютере для конкретного пользователя. Дополнительные сведения см. в разделе [Связывание пользователей с конечным компьютером](../get-started/associate-users-with-a-destination-computer.md).  

##  <a name="use-task-sequences-to-automate-steps"></a><a name="BKMK_TaskSequences"></a> Использование последовательностей задач для автоматизации шагов  
 Можно создавать последовательности задач, выполняющие различные задачи в среде Configuration Manager. Действия последовательности задач определяются в отдельных шагах последовательности. При выполнении последовательности задач действия каждого шага выполняются на уровне командной строки без необходимости участия пользователя. Последовательности задач можно использовать в следующих целях:  

-   [Создание последовательности задач для установки операционной системы](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)  

-   [Создание последовательности задач для развертывания операционных систем](../deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)  

-   [Создание последовательности задач для записи операционной системы](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)  

-   [Создание последовательности задач для записи и восстановления пользовательского состояния](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)  

-   [Создание настраиваемой последовательности задач](../deploy-use/create-a-custom-task-sequence.md)  
