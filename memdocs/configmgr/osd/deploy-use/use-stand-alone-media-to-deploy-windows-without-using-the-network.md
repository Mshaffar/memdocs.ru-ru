---
title: Использование автономного носителя для развертывания Windows
titleSuffix: Configuration Manager
description: Узнайте, как использовать автономный носитель в Configuration Manager для развертывания Windows при ограниченной пропускной способности для установки или обновления ПО или обновления ПО и компьютеров.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a840636ae1be0d8d38819d0465be1211ff6d2f60
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709042"
---
# <a name="use-stand-alone-media-to-deploy-windows-without-using-the-network"></a>Применение автономного носителя для развертывания Windows без использования сети

*Область применения: Configuration Manager (Current Branch)*

Автономный носитель в Configuration Manager содержит все необходимые данные для развертывания операционной системы на компьютере. Сюда входит образ загрузки, образ операционной системы и последовательность задач для установки операционной системы, включая приложения, драйверы и т. п. Развертывание с автономного носителя позволяет выполнять развертывание операционной системы в следующих ситуациях:  

-   в средах, где копирование образа операционной системы или других крупных пакетов по сети, является непрактичным;  

-   в средах без подключения к сети или с низкой пропускной способностью сети.  

Автономный носитель можно использовать в следующих сценариях развертывания операционной системы:  

- [Обновление существующего компьютера до новой версии Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Установка новой версии Windows на новом компьютере (без операционной системы)](install-new-windows-version-new-computer-bare-metal.md)  

- [Обновление Windows до последней версии](upgrade-windows-to-the-latest-version.md)  

  Выполните шаги, указанные для одного из сценариев развертывания операционной системы, а затем используйте следующие разделы для подготовки и создания автономного носителя.  

## <a name="task-sequence-actions-not-supported-when-using-stand-alone-media"></a>Неподдерживаемые действия последовательности задач при использовании автономного носителя  
 Если вы выполнили шаги одного из поддерживаемых сценариев развертывания операционной системы, последовательность задач для развертывания или обновления операционной системы уже создана, а все соответствующее содержимое уже передано на точку распространения. При использовании автономного носителя в последовательности задач не поддерживаются следующие действия:  

-   автоматическое применение драйверов в последовательности задач. Автоматическое применение драйверов устройств из каталога драйверов не поддерживается, однако определенный набор драйверов можно сделать доступным в программе установки Windows, выбрав шаг «Применить пакет драйверов»;  

-   установку обновлений программного обеспечения;  

-   установку программного обеспечения перед развертыванием операционной системы;  

-   связывание пользователей с конечным компьютером (поддержка сопоставления пользователей и устройств).  

-   динамическую установку пакетов через задачу установки пакетов;  

-   динамическую установку приложений через задачу установки приложений.  

> [!NOTE]  
>  Если последовательность задач для развертывания операционной системы включает шаг [Установить пакет](../understand/task-sequence-steps.md#BKMK_InstallPackage) и вы создаете автономный носитель на сайте центра администрирования, может возникнуть ошибка. Сайт центра администрирования не имеет политик конфигурации клиентов, необходимых для включения агента распространения программного обеспечения при выполнении последовательности задач. В файле журнала CreateTsMedia.log может возникнуть следующая ошибка:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>   
>  Для автономного носителя, включающего шаг **Установить пакет**, необходимо проводить создание на первичном сайте с включенным агентом распространения ПО или добавить шаг [Выполнить из командной строки](../understand/task-sequence-steps.md#BKMK_RunCommandLine) после шага [Настроить Windows и Configuration Manager](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) и перед первым шагом **Установить пакет** в последовательности задач. Шаг **Выполнить из командной строки** выполняет команду WMIC, чтобы включить программу агент распространения ПО до первого шага "Установить пакет". Можно использовать следующий шаг **Выполнить из командной строки** :  
>   
>  **Командная строка**: **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  

## <a name="configure-deployment-settings"></a>Настройка параметров развертывания  
 При использовании автономного носителя для запуска процесса развертывания операционной системы необходимо настроить развертывание на предоставление носителю доступа к операционной системе. Такую настройку можно выполнить на странице **Параметры развертывания** мастера развертывания программного обеспечения или на вкладке **Параметры развертывания** в свойствах развертывания.  Для параметра **Сделать доступной для** настройте одно из следующих значений:  

-   **Клиенты Configuration Manager, носители и PXE**  

-   **Только носители и PXE**  

-   **Только носители и PXE (скрытые)**  

## <a name="create-the-stand-alone-media"></a>Создание автономного носителя  
 Вы можете указать, является ли автономный носитель USB-устройством флэш-памяти либо набором компакт-дисков или DVD-дисков. Компьютер, на котором запускается носитель, должен поддерживать использование выбранного носителя в качестве загрузочного диска. Дополнительные сведения см. в разделе [Создание автономного носителя](create-stand-alone-media.md).  

## <a name="install-the-operating-system-from-stand-alone-media"></a>Установка операционной системы с автономного носителя  
 Вставьте автономный носитель в загрузочный дисковод компьютера и затем включите питание для установки операционной системы.  