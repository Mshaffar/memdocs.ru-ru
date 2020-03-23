---
title: Похоже, для устройства Android включено шифрование | Документация Майкрософт
description: Разрешение состояния шифрования на корпоративном портале и в приложении Microsoft Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/14/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ba593c08-1a78-4013-8525-b45a948772ec
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 4fd08ba190654db5678766e34e3340330dcf3ca8
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79346096"
---
# <a name="device-encrypted-but-apps-say-otherwise"></a>Устройство зашифровано, однако в приложениях указано иное

Если на корпоративном портале или в приложении Microsoft Intune указано, что устройство не зашифровано, однако вы уверены, что оно зашифровано, попробуйте выполнить действия, описанные в этой статье.  

## <a name="add-a-startup-pin"></a>Добавление ПИН-кода запуска

Для защиты некоторых устройств Android необходимо создать ПИН-код запуска. Этот параметр находится в приложении **Параметры** на устройстве. Имя и расположение параметра могут отличаться. Например, на устройстве Samsung Galaxy S7 этот параметр называется **Безопасный запуск**. Чтобы включить его и создать секретный код, выберите **Параметры** > **Блокировка экрана и безопасность** > **Безопасный запуск**.  

## <a name="encrypt-the-entire-device"></a>Зашифруйте все устройство.

Сведения в данном разделе применимы только к приложению корпоративного портала. На некоторых устройствах доступна возможность шифрования всего устройства или только используемого пространства. Выберите вариант шифрования всего устройства. Если выбрано шифрование только используемого пространства:

1. [Удалите это устройство с Корпоративного портала.](unenroll-your-device-from-intune-android.md)
2. Расшифруйте используемое пространство.  
3. Зашифруйте все устройство.  
4. Повторно зарегистрируйте устройство.  

## <a name="downgrade-your-version-of-android"></a>Переход на более раннюю версию Android

Сведения в данном разделе применимы только к приложению корпоративного портала. Если устройство позволяет вернуться к Android версии 6.0 и выше, сделайте это. При понижении версии устройства существует риск потери данных. В противном случае рекомендуем обратиться в службу поддержки вашей компании для решения этой проблемы. Контактные данные вашей службы поддержки см. на [веб-сайте Корпоративного портала](https://go.microsoft.com/fwlink/?linkid=2010980).  

## <a name="specific-manufacturer-issues"></a>Проблемы, связанные с конкретным производителем

На некоторых устройствах с Android версии 7.0 и выше способы шифрования не соответствуют определенным стандартам платформы Android. Эти методы шифрования ставят информацию на устройстве под угрозу. В результате такие устройства не поддерживаются.

Список поддерживаемых устройств Android, который постоянно пополняется, см. в статье [Поддерживаемые операционные системы и браузеры в Intune](https://docs.microsoft.com/intune/fundamentals/supported-devices-browsers#supported-samsung-knox-standard-devices). Если устройство отсутствует в списке, обратитесь к изготовителю устройства или в службу поддержки.

> [!Note]
> Корпорация Майкрософт активно сотрудничает с производителями для устранения проблем, выявляемых по результатам тестирования или обращений пользователей. При поступлении новой информации содержимое этой статьи будет обновляться.

## <a name="update-devices"></a>Обновление устройств

Если вы не обновили устройство до последней версии Android, перейдите на устройстве в приложение **Параметры** и выберите **Обновить**.  

## <a name="next-steps"></a>Дальнейшие шаги

По-прежнему нужна помощь? Обратитесь в службу поддержки вашей компании (см. контактные данные на [веб-сайте корпоративного портала](https://go.microsoft.com/fwlink/?linkid=2010980)) или отправьте письмо <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with enrolling my Android device&body=Describe the issue you're experiencing here.">команде разработчиков Майкрософт для Android</a>.  