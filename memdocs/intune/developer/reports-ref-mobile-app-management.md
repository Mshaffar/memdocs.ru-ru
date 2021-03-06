---
title: Управление мобильными приложениями (MAM)
titleSuffix: Microsoft Intune
description: Справочник по категории "Управление мобильными приложениями" коллекций сущностей в API хранилища данных Intune.
keywords: Хранилище данных Intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/03/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 084F11AD-F7BA-45A4-8424-45E6E4564930
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 428ee1ce93b4f6fe21c4b0180a9df222f3e23e09
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "79359759"
---
# <a name="reference-for-mobile-app-management-mam-entities"></a>Справочник по сущностям управления мобильными приложениями (MAM)

Категория **Управление мобильными приложениями** содержит сущности для мобильных приложений, например:

- Apps
- Экземпляры
- Состояние отметки
- Состояние работоспособности
- Состояние политики
- Состояние регистрации
- Типы платформ

## <a name="mamapplications"></a>mamApplications

Сущность **mamApplication** выводит список бизнес-приложений, управляемых системой управления мобильными приложениями (MAM) без регистрации в организации.

| Свойство | Описание | Пример |
|---------|------------|--------|
| mamApplicationKey |Уникальный идентификатор приложения MAM. | 432 |
| mamApplicationName |Имя приложения MAM. |Пример имени приложения MAM |
| mamApplicationId |Идентификатор приложения MAM. | 123 |
| isDeleted |Указывает, обновлена ли запись приложения MAM. <br>True — приложение MAM имеет новую запись с обновленными полями в этой таблице. <br>False — последняя запись для этого приложения MAM. |Истина/ложь |
| startDateInclusiveUTC |Дата и время (в формате UTC) создания этого приложения MAM в хранилище данных. |23/11/2016 12:00:00 |
| deletedDateUTC |Дата и время (в формате UTC), когда значение IsDeleted изменилось на True. |23/11/2016 12:00:00 |
| rowLastModifiedDateTimeUTC |Дата и время (в формате UTC) последнего изменения этого приложения MAM в хранилище данных. |23/11/2016 12:00:00 |


## <a name="mamapplicationinstances"></a>mamApplicationInstances

Сущность **mamApplicationInstance** выводит список приложений, управляемых системой MAM, в виде единственных экземпляров для пользователя на устройство. Все указанные в сущности пользователи и устройства защищены, так как им назначена по меньшей мере одна политика MAM.


|          Свойство          |                                                                                                  Описание                                                                                                  |               Пример                |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
|   applicationInstanceKey   |                                                               Уникальный идентификатор для экземпляра приложения MAM в хранилище данных — суррогатный ключ.                                                                |                 123                  |
|           userId           |                                                                              Идентификатор пользователя, установившего это приложение MAM.                                                                              | b66bc706-ffff-7437-0340-032819502773 |
|   applicationInstanceId    |                                              Уникальный идентификатор экземпляра приложения MAM — аналогичен ApplicationInstanceKey, но является естественным ключом.                                              | b66bc706-ffff-7437-0340-032819502773 |
| mamApplicationId | Идентификатор приложения MAM, для которого был создан этот экземпляр приложения.   | 23/11/2016 12:00:00   |
|     applicationVersion     |                                                                                     Версия этого приложения MAM.                                                                                      |                  2                   |
|        createdDate         |                                                                 Дата создания записи для этого экземпляра приложения MAM. Может иметь значение NULL.                                                                 |        23/11/2016 12:00:00        |
|          Платформа          |                                                                          Платформа устройства, на котором установлено это приложение MAM.                                                                           |                  2                   |
|      platformVersion       |                                                                      Версия платформы устройства, на котором установлено это приложение MAM.                                                                       |                 2.2                  |
|         sdkVersion         |                                                                            Версия пакета SDK для MAM, с помощью которого было упаковано это приложение MAM.                                                                            |                 3,2                  |
| mamDeviceId | Идентификатор устройства, с которым связан экземпляр приложения MAM.   | 23/11/2016 12:00:00   |
| mamDeviceType | Тип устройства, с которым связан экземпляр приложения MAM.   | 23/11/2016 12:00:00   |
| mamDeviceName | Имя устройства, с которым связан экземпляр приложения MAM.   | 23/11/2016 12:00:00   |
|         isDeleted          | Указывает, обновлена ли запись этого экземпляра приложения MAM. <br>True — этот экземпляр приложения MAM имеет новую запись с обновленными полями в этой таблице. <br>False — последняя запись для этого экземпляра приложения MAM. |              Истина/ложь              |
|   startDateInclusiveUtc    |                                                              Дата и время (в формате UTC) создания этого экземпляра приложения MAM в хранилище данных.                                                               |        23/11/2016 12:00:00        |
|       deletedDateUtc       |                                                                             Дата и время (в формате UTC), когда значение IsDeleted изменилось на True.                                                                              |        23/11/2016 12:00:00        |
| rowLastModifiedDateTimeUtc |                                                           Дата и время (в формате UTC) последнего изменения этого экземпляра приложения MAM в хранилище данных.                                                            |        23/11/2016 12:00:00        |


## <a name="mamcheckins"></a>mamCheckins

Сущность **mamCheckin** представляет данные, собранные во время отметки экземпляра приложения MAM в службе Intune. 

> [!Note]  
> Если экземпляр приложения отмечается несколько раз в день, хранилище данных сохраняет одну отметку.

| Свойство | Описание | Пример |
|---------|------------|--------|
| dateKey |Ключ даты, когда в хранилище данных была записана отметка приложения MAM. | 20160703 |
| applicationInstanceKey |Ключ экземпляра приложения, связанный с этой отметкой приложения MAM. | 123 |
| userKey |Ключ пользователя, связанный с этой отметкой приложения MAM. | 4323 |
| mamApplicationKey |Ключ приложения, связанный с регистрацией приложения MAM. | 432 |
| deviceHealthKey |Ключ DeviceHealth, связанный с этой отметкой приложения MAM. | 321 |
| PlatformKey |Представляет платформу устройства, связанного с этой отметкой приложения MAM. |123 |
| effectiveAppliedPolicyKey |Представляет эффективную действующую политику, связанную с этим отметившимся приложением MAM. Эффективная действующая политика получается путем объединения всех политик, которые относятся к конкретному приложению и пользователю. | 322 |
| pastCheckInDate |Дата и время последней отметки этого приложения MAM. Может иметь значение NULL. |23/11/2016 12:00:00 |


## <a name="mamdevicehealth"></a>mamDeviceHealth

Сущность **MamDeviceHealth** представляет устройства, для которых развернуты политики управления мобильными приложениями (MAM), даже если на устройствах снята защита.

| Свойство | Описание | Пример |
|---------|------------|--------|
| deviceHealthKey |Уникальный идентификатор для устройства и его работоспособности в хранилище данных — суррогатный ключ. |123 |
| DeviceHealth |Уникальный идентификатор для устройства и его работоспособности — аналогичен DeviceHealthKey, но является естественным ключом. |b66bc706-ffff-7777-0340-032819502773 |
| DeviceHealthName |Представляет состояние устройства. <br>Not available — информация об этом устройстве отсутствует. <br>Healthy — устройство не подвергалось взлому ОС. <br>Unhealthy — устройство подвергалось взлому ОС. |Not Available Healthy Unhealthy |
| rowLastModifiedDateTimeUtc |Дата и время (в формате UTC) последнего изменения работоспособности этого устройства MAM в хранилище данных. |23/11/2016 12:00:00 |

## <a name="mameffectivepolicies"></a>mamEffectivePolicies

Сущность **MamEffectivePolicy** выводит список всех эффективных политик MAM, действующих в вашей организации. Эффективная действующая политика получается путем объединения всех политик, которые относятся к конкретному приложению и пользователю.

| Свойство | Описание | Пример |
|---------|------------|--------|
| effectivePolicyKey |Уникальный идентификатор действующей политики MAM в хранилище данных. |2 |
| realPolicyKey |Уникальный идентификатор политики MAM, созданной ИТ-специалистом |1 |
| RowCreatedDateTimeUtc |Дата и время (в формате UTC) создания этой эффективной политики MAM в хранилище данных |23/11/2016 12:00:00 |

## <a name="mamplatforms"></a>MamPlatforms

Сущность **MamPlatform** выводит список имен и типов платформ, где было установлено приложение MAM.


|          Свойство          |                                    Описание                                    |                         Пример                         |
|----------------------------|-----------------------------------------------------------------------------------|---------------------------------------------------------|
|        PlatformKey         |     Уникальный идентификатор платформы в хранилище данных — суррогатный ключ.      |                           123                           |
|          Платформа          | Уникальный идентификатор платформы — аналогичен PlatformKey, но является естественным ключом. |                           123                           |
|        PlatformName        |                                   Имя платформы                                   | Недоступно <br>Нет <br>Windows <br>iOS <br>Android. |
| rowLastModifiedDateTimeUtc | Дата и время (в формате UTC) последнего изменения этой платформы в хранилище данных.  |                 23/11/2016 12:00:00                  |

