---
title: Взаимодействие при развертывании ОС
titleSuffix: Configuration Manager
description: Описание проблем с взаимодействием, которые возникают, если на сайтах Configuration Manager в рамках одной иерархии используются разные версии.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5931c43f0f8513ea1819e00f4eac7ecfd35dc717
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708082"
---
# <a name="plan-for-os-deployment-interoperability"></a>Планирование взаимодействия при развертывании ОС

*Область применения: Configuration Manager (Current Branch)*

Если на сайтах Configuration Manager в рамках одной иерархии используются разные версии, некоторые возможности Configuration Manager становятся недоступными. Обычно функциональные возможности более новой версии Configuration Manager недоступны на сайтах или в клиентах с предыдущими версиями. Дополнительные сведения см. в статье [Взаимодействие различных версий Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  


## <a name="objects"></a>Объекты

Учитывайте следующие объекты при обновлении сайта верхнего уровня в иерархии, а также других сайтов в иерархии Configuration Manager с предыдущими версиями:  

### <a name="client-installation-package"></a>Пакет установки клиента  

- Источник пакета установки клиента по умолчанию автоматически обновляется. Все точки распространения в иерархии обновляются с помощью нового пакета установки клиента. Такая ситуация возникает даже в точках распространения на сайтах в иерархии, которые используют более раннюю версию.  

- Новые версии клиентов невозможно назначить сайтам, которые еще не обновлены до новой версии. Назначение блокируется в точке управления.  

### <a name="boot-images"></a>загрузочные образы,  

- При обновлении сайта верхнего уровня до последней версии Configuration Manager автоматически обновляются образы загрузки по умолчанию (x86 и x64). Обновление использует Windows ADK для Windows 10, включая среду предустановки Windows 10. Файлы, связанные с образами загрузки по умолчанию, обновляются с использованием файлов самой последней версии Configuration Manager. Сайт не обновляет пользовательские образы загрузки автоматически. Необходимо будет вручную обновить пользовательские образы загрузки, включая старые версии среды предустановки Windows.  

- Если иерархия сайта содержит сайты с разными версиями Configuration Manager, избегайте использования динамических носителей. Используйте носитель на основе сайта для связи с точкой управления. После обновления всех сайтов до одной версии Configuration Manager можно снова использовать динамический носитель.

- Убедитесь, что последние версии образов загрузки Configuration Manager включают ваши настройки. Затем обновите все точки распространения на сайтах новых версий до последней версии новых образов загрузки.  

### <a name="user-state-migration-tool-usmt"></a>Средство миграции пользовательской среды (USMT)  

При обновлении сайта верхнего уровня до последней версии Configuration Manager пакет USMT по умолчанию автоматически обновляется до последней версии. Автоматическое обновление пользовательских пакетов USMT не выполняется. Эти пакеты потребуется обновить вручную.  

### <a name="new-task-sequence-steps"></a>Новые шаги последовательности задач  

Периодически вместе с новыми версиями Configuration Manager вносятся новые шаги последовательности задач. При развертывании последовательности задач с новым шагом на старых клиентах этот шаг завершается ошибкой. Перед развертыванием последовательности задач с новым шагом убедитесь, что клиенты в целевой коллекции обновлены до новой версии.  

### <a name="os-deployment-media"></a>Носитель развертывания ОС  

Когда сайт обновляется до новой версии, необходимо обновить все носители, используя новый пакет клиента Configuration Manager. К ним относятся такие типы носителей, как носитель для снятия образа, загрузочный, предварительно подготовленный и автономный носитель.

### <a name="third-party-extensions-to-os-deployment"></a>Сторонние расширения для развертывания операционной системы  

Если у вас есть сторонние расширения для развертывания ОС и используются разные версии сайтов Configuration Manager или клиентов Configuration Manager, могут возникать проблемы с расширениями.  


## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Самая последняя версия сайтов Configuration Manager в смешанной иерархии  

При обновлении сайта до последней версии Configuration Manager последовательности задач, ссылающиеся на пакет установки клиента по умолчанию, автоматически развертывают последнюю версию клиента Configuration Manager.

Последовательности задач, которые ссылаются на настраиваемый пакет установки клиента, по-прежнему развертывают ту версию клиента, которая содержится в этом пакете. Пользовательские пакеты, скорее всего, включают более раннюю версию клиента Configuration Manager. Чтобы избежать сбоев при развертывании последовательности задач, обновите все пользовательские пакеты установки клиента до последней версии.

При настройке последовательности задач для использования пользовательского пакета установки клиента, выполните одно из следующих действий:

- измените шаг последовательности задач для использования последней версии Configuration Manager в пакете установки клиента;
- измените пользовательский пакет для использования последнего источника установки клиента Configuration Manager.

> [!IMPORTANT]  
> Не развертывайте последовательности задач, которые ссылаются на пакет установки клиента Configuration Manager последней версии, для клиентов на сайте Configuration Manager более старой версии. Когда клиенты, назначенные более старому сайту Configuration Manager, обновляются до последней версии клиента Configuration Manager, Configuration Manager блокирует назначение более старому сайту Configuration Manager. Эти клиенты больше не назначены какому-либо сайту. Пока вы вручную не назначите клиент сайту Configuration Manager последней версии или не переустановите клиент старой версии Configuration Manager на компьютере, эти клиенты будут неуправляемыми.


## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Более старые версии Configuration Manager в смешанной иерархии  

При обновлении сайта центра администрирования до последней версии Configuration Manager убедитесь, что развертываемая последовательность задач развертывания операционной системы не оставляет эти клиенты в неуправляемом состоянии. Например, если развертывание выполняется на клиентах, назначенных старому сайту Configuration Manager, который еще не обновлен до последней версии Configuration Manager.

Создайте копию последовательности задач, которая используется для развертывания на клиентах на сайте последней версии Configuration Manager. Затем измените последовательность задач, чтобы ее можно было развернуть на клиентах на сайте со старой версией Configuration Manager. Настройте последовательность задач так, чтобы она ссылалась на настраиваемый пакет установки клиента, который использует более старую версию источника установки клиента Configuration Manager. Если у вас нет настраиваемого пакета установки клиента, который бы ссылался на источник установки клиента Configuration Manager более старой версии, создайте его вручную.  

> [!Important]  
> Начиная с версии 1902 нельзя развернуть пакет или последовательность задач на версии клиента 5.7730 или более ранней. Чтобы обойти это ограничение, обновите клиент до более поздней версии.<!-- SCCMDocs-pr issue #3493 -->