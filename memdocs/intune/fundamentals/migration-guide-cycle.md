---
title: Как выполняется типичный цикл миграции Intune
titleSuffix: Microsoft Intune
description: В этой статье объясняется, как выполняется цикл миграции Microsoft Intune, и приводятся примеры выполнения циклов миграции.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3688b724-9521-4210-bf4d-bcf47d8d4ca0
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7d5a9c1fab01393f45c877165230ae68118b1113
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79358225"
---
# <a name="typical-migration-cycle"></a>Типичный цикл миграции

Чаще всего миграция Intune в организации начинается с небольшого пилотного проекта с выделением подмножества пользователей в ИТ-отделе. Кроме того, для определения периода миграции в организации может потребоваться обсудить такие факторы, как готовность группы к изменениям, число пользователей, сложность, требования, расположение и бизнес-риски.

Ниже приведен пример расписания для целевых групп.

  | **Целевые группы миграции** | **Период 1** | **Период 2** | **Период 3** | **Период 4** | **...**
|:---:|:---:|:---:|:---:|:---:|:---:|
| Ограниченная пилотная группа в ИТ-организации (50 пользователей) | Объявление плана | Указание относительно регистрации | Установка крайнего срока | Применение условного доступа |  |                                                        
| Расширенная пилотная группа в ИТ-организации (200 пользователей) |  | Объявление плана | Указание относительно регистрации | Установка крайнего срока | Применение условного доступа |
| Первый этап миграции, технические специалисты (2000) |  |  | Объявление плана | Указание относительно регистрации | Установка крайнего срока |
| Второй этап миграции, восточная часть США |  |  |  | Объявление плана | Указание относительно регистрации |
| Все регионы |  |  |  |  | Объявление плана |

## <a name="customer-migration-case-study"></a>Пример миграции у клиента

### <a name="adatum-corporation"></a>Adatum Corporation

Узнайте, [как проходил процесс миграции со стороннего поставщика MDM в Intune в Adatum Corporation](https://gallery.technet.microsoft.com/Intune-migration-guide-893a95e3?redir=0).

## <a name="monitoring-migration"></a>Мониторинг миграции

Intune предлагает несколько способов мониторинга миграции:

* Представления группы пользователей Intune.

* Набор встроенных отчетов.

* Оповещения в консоли.

Проверяйте количество пользователей, зарегистрировавших устройства, в конце каждого этапа миграции. Это даст вам следующие возможности:

- Оценка эффективности плана распространения сведений.

- Оценка того, как повлияло применение политики условного доступа.


## <a name="post-migration"></a>После миграции

После миграции в Intune снимите с учета предыдущий поставщик MDM и отменить подписку на службу. Кроме того, удалите все ненужные требования к инфраструктуре, следуя указаниям поставщика MDM.