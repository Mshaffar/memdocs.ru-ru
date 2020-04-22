---
title: Планирование развертывания клиентов на компьютерах Mac
titleSuffix: Configuration Manager
description: Планирование развертывания клиентов на компьютерах Mac в Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d15ae3f-de42-461f-a907-c43873da22d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f231e0681b2a202696b6c719966abf818a9c8e27
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693722"
---
# <a name="planning-for-client-deployment-to-mac-computers-in-configuration-manager"></a>Планирование развертывания клиентов на компьютерах Mac в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Клиент Configuration Manager можно установить на компьютерах Mac с операционной системой Mac OS X для использования перечисленных ниже возможностей управления.  

- **Инвентаризация оборудования**  

   Средство инвентаризации оборудования Configuration Manager можно использовать для сбора информации об оборудовании компьютеров Mac и установленных на них приложениях. Затем эту информацию можно просмотреть с помощью обозревателя ресурсов в консоли Configuration Manager и использовать для создания коллекций, запросов и отчетов. Дополнительные сведения см. в статье [Использование обозревателя ресурсов для просмотра данных инвентаризации оборудования](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

   Configuration Manager собирает следующие сведения об оборудовании на компьютерах Mac:  

  -   Процессор  

  -   Компьютерная система  

  -   Диск  

  -   Раздел диска  

  -   Сетевой адаптер  

  -   Операционная система  

  -   Служба  

  -   Процесс  

  -   Установленное ПО  

  -   Продукт компьютерной системы  

  -   USB-контроллер  

  -   USB-устройство  

  -   Устройство чтения компакт-дисков  

  -   Видеоконтроллер  

  -   Настольный монитор  

  -   Переносная батарея  

  -   Физическая память  

  -   Принтер  

  > [!IMPORTANT]  
  >  Данные об оборудовании, собираемые на компьютерах Mac в процессе инвентаризации оборудования, расширить нельзя.  

- **Параметры соответствия**  

   Параметры соответствия Configuration Manager можно использовать для просмотра состояния соответствия и исправления предпочитаемых параметров Mac OS X (PLIST). Например, можно настроить принудительное применение параметра, который устанавливает домашнюю страницу веб-браузера Safari, или же обеспечить включение брандмауэра Apple. Вы также можете использовать сценарии оболочки для отслеживания и исправления параметров Mac OS X.  

- **Управление приложениями**  

   Configuration Manager позволяет развертывать программное обеспечение на компьютерах Mac. На компьютеры Mac можно развертывать программное обеспечение в следующих форматах:  

  -   образ диска Apple (DMG);  

  -   метафайл пакета (MPKG);  

  -   пакет установщика Mac OS X (PKG);  

  -   приложение Mac OS X (APP).  

  При установке клиента Configuration Manager на компьютерах Mac нельзя использовать следующие возможности управления, поддерживаемые клиентом Configuration Manager на компьютерах Windows:  

- Принудительная установка клиента  

- Развертывание операционной системы  

- Обновления программного обеспечения  

  > [!NOTE]  
  >  Можно использовать реализованные в Configuration Manager средства управления приложениями для развертывания обязательных обновлений ПО Mac OS X на компьютерах Mac. Кроме того, можно использовать параметры соответствия для проверки наличия на компьютерах обязательных обновлений программного обеспечения.  

- Периоды обслуживания  

- Удаленное управление  

- Исключение брандмауэра Windows для прокси-сервера пробуждения  

- Проверка и исправление состояния клиента  

  Дополнительные сведения об установке и настройке клиента Configuration Manager для Mac см. в разделе [Развертывание клиентов на компьютерах Mac](../../../../core/clients/deploy/deploy-clients-to-macs.md).