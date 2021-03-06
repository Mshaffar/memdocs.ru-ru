---
title: Идентификаторы пакета iOS и iPadOS для встроенных приложений в Microsoft Intune — Azure | Документация Майкрософт
titleSuffix: ''
description: Ознакомьтесь со списком идентификаторов пакетов для встроенных приложений iOS и iPadOS. Используйте эти идентификаторы пакетов, чтобы явно разрешить приложения в профилях и политиках конфигурации устройств в Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c7de0b978c24f28988c62854a249505a0598db95
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "80084078"
---
# <a name="bundle-ids-for-built-in-ios-and-ipados-apps-you-can-use-in-intune"></a>Идентификаторы пакетов для встроенных приложений iOS и iPadOS, которые можно использовать в Intune

При настройке функций на устройствах iOS и iPadOS можно также добавить встроенные приложения на этих устройствах. В этой статье перечислены идентификаторы пакета некоторых стандартных встроенных приложений iOS и iPadOS. Чтобы найти идентификаторы наборов других приложений, обратитесь к поставщику программного обеспечения. См. список [идентификаторов пакета iOS и iPadOS](https://support.apple.com/guide/mdm/ios-bundle-ids-mdm90f60c1ce/web) от Apple (веб-сайт Apple).

## <a name="bundle-ids"></a>Идентификаторы пакета

| Идентификатор пакета                   | имя приложения;     | Publisher |
|-----------------------------|--------------|-----------|
| com.apple.AppStore          | Магазин App Store    | Apple     |
| com.apple.store.Jolly       | Магазин Apple Store  | Apple     |
| com.apple.calculator        | "Калькулятор"   | Apple     |
| com.apple.mobilecal         | "Календарь"     | Apple     |
| com.apple.camera            | Камера       | Apple     |
| com.apple.mobiletimer       | "Часы"        | Apple     |
| com.apple.clips             | Clips        | Apple     |
| com.apple.compass           | "Компас"      | Apple     |
| com.apple.MobileAddressBook | Контакты     | Apple     |
| com.apple.facetime          | FaceTime     | Apple     |
| com.apple.DocumentsApp      | Файлы        | Apple     |
| com.apple.mobileme.fmf1     | "Найти друзей" | Apple     |
| com.apple.mobileme.fmip1    | "Найти iPhone"  | Apple     |
| com.apple.gamecenter        | Game Center  | Apple     |
| com.apple.mobilegarageband  | GarageBand   | Apple     |
| com.apple.Health            | "Здоровье"       | Apple     |
| com.apple.Home              | Корневая         | Apple     |
| com.apple.iBooks            | iBooks       | Apple     |
| com.apple.iMovie            | iMovie       | Apple     |
| com.apple.itunesconnect.mobile | iTunes Connect | Apple |
| com.apple.MobileStore       | Магазин iTunes | Apple     |
| com.apple.itunesu           | iTunes U     | Apple     |
| com.apple.Keynote           | Keynote      | Apple     |
| com.apple.mobilemail        | Mail         | Apple     |
| com.apple.Maps              | "Карты"         | Apple     |
| com.apple.measure           | Measure      | Apple     |
| com.apple.MobileSMS         | "Сообщения"     | Apple     |
| com.apple.Music             | "Музыка"        | Apple     |
| com.apple.news              | News         | Apple     |
| com.apple.mobilenotes       | Заметки        | Apple     |
| com.apple.Numbers           | Числа      | Apple     |
| com.apple.Pages             | Pages        | Apple     |
| com.apple.mobilephone       | Телефон        | Apple     |
| com.apple.Photo-Booth       | Photo Booth  | Apple     |
| com.apple.mobileslideshow   | "Фото"       | Apple     |
| com.apple.podcasts          | "Подкасты"     | Apple     |
| com.apple.reminders         | "Напоминания"    | Apple     |
| com.apple.mobilesafari      | Safari       | Apple     |
| com.apple.Preferences       | Параметры     | Apple     |
| com.apple.shortcuts         | Ярлыки    | Apple     |
| com.apple.SiriViewService   | Siri         | Apple     |
| com.apple.stocks            | "Акции"       | Apple     |
| com.apple.tips              | "Советы"         | Apple     |
| com.apple.tv                | TV           | Apple     |
| com.apple.videos            | Видеоролики       | Apple     |
| com.apple.VoiceMemos        | VoiceMemos   | Apple     |
| com.apple.Passbook          | Wallet       | Apple     |
| com.apple.Bridge            | Watch        | Apple     |
| com.apple.weather           | "Погода"      | Apple     |

## <a name="next-steps"></a>Дальнейшие действия

Используйте эти идентификаторы пакета, чтобы настроить [функции устройства](ios-device-features-settings.md), а также чтобы [разрешить или ограничить некоторые параметры](device-restrictions-ios.md) на устройствах iOS и iPadOS.
