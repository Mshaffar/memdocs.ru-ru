---
title: Последствия сбоев в работе сайта
titleSuffix: Configuration Manager
description: Сведения о влиянии различных сбоев на сайте Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6f0e08f8-f2e1-4823-90f6-7b1f4341eb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf56aee2e9f73ea8c3c69737c749f2a599e1ac37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708572"
---
# <a name="site-failure-impacts-in-configuration-manager"></a>Последствия сбоев в работе сайта в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Сервер сайта и любые другие системы сайта могут давать сбои и не выполнять функций, которые они регулярно выполняют. Если на одном компьютере установлено несколько систем сайта и у компьютера происходит сбой, недоступными становятся одновременно все эти службы.

Процесс планирования должен включать изучение влияния на службу, предоставляемую организации. Так как каждая из систем отвечает за отдельный набор функций, последствия сбоя для сайта зависят от роли системы сайта, в которой произошел сбой. 

Используйте [возможности высокой доступности](../deploy/configure/high-availability-options.md), чтобы уменьшить влияние сбоя на любую отдельную систему. Кроме того, запланируйте и отработайте на практике стратегию [резервного копирования и восстановления](backup-and-recovery.md), чтобы сократить время недоступности службы.

Следующие разделы описывают последствия неработоспособности указанной системы сайта:


### <a name="site-server"></a>Сервер сайтов

- Администрирование сайта невозможно. Вы не можете подключить консоль к сайту.  

- Точка управления будет собирать сведения о клиентах и сохранять их в кэше, пока работа сервера сайта не будет восстановлена.  

- Пользователи могут запускать существующие развертывания, а клиенты — скачивать содержимое из точек распространения.  


### <a name="site-database"></a>База данных сайта

- Администрирование сайта невозможно.  

- Если клиент Configuration Manager уже имеет назначение политик с новыми политиками и точка управления кэшировала содержимое политики, клиент может запросить содержимое политики и получить ответ с ним. Однако сайт не может обслуживать запросы на новые назначения политик.  

- Клиенты будут иметь возможность запускать развертывания только тогда, когда они уже получили политику, а соответствующие исходные файлы сохранены в локальном кэше клиента.  


### <a name="management-point"></a>Точка управления

- Хотя вы можете создавать развертывания, клиенты не получат их, пока не заработает точка управления.  

- Клиенты продолжают собирать данные инвентаризации, сведения о контроле использования программных продуктов и сведения о состоянии. Они сохраняют эти данные локально, пока не будет доступна точка управления.  

- Клиенты будут иметь возможность запускать развертывания только тогда, когда они уже получили политику, а соответствующие исходные файлы сохранены в локальном кэше клиента.  


### <a name="distribution-point"></a>Точка распространения

- Клиенты Configuration Manager могут запускать развертывания только в том случае, если соответствующие исходные файлы скачаны локально или доступны в одноранговом источнике.

