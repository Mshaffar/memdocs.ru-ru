---
title: Параметры ограничений Microsoft Intune для применения к устройствам Windows Phone 8.1
titleSuffix: ''
description: Сведения о параметрах Intune, с помощью которых можно управлять параметрами и работой устройств Windows Phone 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 285144e42f2a029bf2d24b96493c54922727d6dc
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "80407644"
---
# <a name="microsoft-intune-windows-phone-81-device-restriction-settings"></a>Параметры ограничений для устройств с Windows Phone 8.1 в Microsoft Intune

В этой статье описаны все параметры ограничений устройств в Microsoft Intune, которые можно настроить для устройств под управлением Windows Phone 8.1.

## <a name="general"></a>Общие

- **Камера**. Значение **Блокировать** запрещает доступ к камере на устройстве. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.

  Intune управляет доступом только к камере устройства. У него нет доступа к изображениям или видео.

- **Копирование и вставка**. Значение **Блокировать** запрещает копирование и вставку между приложениями на устройстве. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Съемные носители**. Значение **Блокировать** запрещает использование внешних запоминающих устройств на устройствах, например SD-карты. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Географическое положение**. Значение **Блокировать** предотвращает включение службы определения местоположения на устройствах. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Учетная запись Майкрософт**. Значение **Блокировать** запрещает пользователям связывание учетных записей Майкрософт с устройством. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Снимок экрана**. Значение **Блокировать** запрещает получение снимков экрана на устройствах. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Передача диагностических данных**. Значение **Блокировать** запрещает отправку с устройств данных телеметрии о диагностике и использовании в корпорацию Майкрософт. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Синхронизация настраиваемых учетных записей электронной почты**. Значение **Блокировать** запрещает устройствам подключаться к учетным записям электронной почты, отличным от Майкрософт. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.

## <a name="password"></a>Пароль

- **Пароль**. При значении **Требовать** пользователь должен ввести пароль для доступа к устройству. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. Применяется только к локальным учетным записям. Пароли учетных записей домена по-прежнему настраиваются Active Directory (AD) и Azure AD.
  - **Требуемый тип пароля**. Выберите тип пароля. Доступны следующие параметры:
    - **По умолчанию для устройства**. Пароль может содержать числа и буквы.
    - **Буквенно-цифровой**. Пароль должен содержать сочетание букв и цифр.
    - **Числовой**. Пароль должен состоять только из цифр.
  - **Минимальная длина пароля**. Введите минимальное число обязательных символов (4–16). Например, введите `6`, чтобы требовать по крайней мере шесть символов в пароле.
  - **Простые пароли**. Значение **Блокировать** запрещает пользователям создавать простые пароли, например `1234` или `1111`. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
  - **Число неудачных попыток входа перед очисткой устройства**. Введите число попыток ввода пароля до очистки устройств.
  - **Максимальное время бездействия (в минутах), по истечении которого экран блокируется**. Введите период бездействия устройства, по истечении которого экран автоматически блокируется. Например, введите значение `5`, чтобы блокировать устройства после 5 минут бездействия. Если задано значение **Не настроено** или значение не указано, Intune не изменяет или не обновляет этот параметр.
  - **Срок действия пароля (в днях)** . Задайте время, по истечении которого требуется сменить пароль для устройства (от 1 до 255). Например, чтобы изменить пароль через 90 дней, введите `90`. Если значение не указано, Intune не изменяет или не обновляет этот параметр.
  - **Запретить использование предыдущих паролей**. Введите число предыдущих паролей, которые нельзя использовать повторно (1–24). Значение `5` означает, что в качестве нового пароля пользователь не может установить свой текущий или любой из четырех предыдущих паролей. Если значение не указано, Intune не изменяет или не обновляет этот параметр.
- **Шифрование**. Значение **Требовать** делает обязательным шифрование на устройстве, включая файлы. Не все устройства поддерживают шифрование. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. Чтобы настроить этот параметр и правильно сообщить о соответствии требованиям, также настройте следующие элементы:
  - **Требовать пароль**. Задайте значение **Требовать**.
  - **Требуемый тип пароля**. Установите как минимум значение **Числовой**.
  - **Минимальная длина пароля**. Установите как минимум значение `4`.

## <a name="app-store"></a>Магазин App Store

- **App Store**. **Блокировать** — запрещает пользователям доступ к магазину приложений. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.

## <a name="restricted-apps"></a>Ограниченные приложения

В списке ограниченных приложений можно настроить один из следующих списков.

- **Заблокированные приложения**. Указывает приложения, не управляемые Intune, которые пользователям запрещено устанавливать и запускать.
- **Разрешенные приложения**. Указывает приложения, которые пользователям разрешено устанавливать. Приложения под управлением Intune автоматически разрешены.

Чтобы настроить список, щелкните **Добавить**, затем укажите выбранное имя, при необходимости издателя приложения и URL-адрес для приложения в магазине приложений.

### <a name="how-to-specify-the-url-to-an-app-in-the-store"></a>Как указать URL-адрес для приложений в магазине

URL-адрес приложения в списке разрешенных и заблокированных приложений необходимо указывать в следующем формате:

На странице [Магазин Windows Phone](https://www.microsoft.com/store/apps/windows-phone) найдите приложение, которое вы хотите использовать.

Откройте страницу приложения и скопируйте URL-адрес в буфер обмена. После этого его можно использовать как URL-адрес в списке разрешенных приложений или в списке заблокированных приложений.

Пример: выполните поиск в магазине по запросу "Приложение Skype". Используется URL-адрес вида `http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51`.

### <a name="additional-options"></a>Дополнительные параметры

Вы также можете щелкнуть **Импорт**, чтобы заполнить список из CSV-файла в формате <*URL-адрес приложения*>, <*имя приложения*>, <*издатель приложения*>, или **Экспорт**, чтобы создать CSV-файл, содержащий список ограниченных приложений в том же формате.

## <a name="browser"></a>Браузер

- **Веб-браузер**. Значение **Блокировать** отключает встроенный веб-браузер на устройствах. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.

## <a name="cellular-and-connectivity"></a>Сотовая сеть и подключение

- **Wi-Fi**. Значение **Блокировать** отключает функции Wi-Fi на устройствах. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Модем Wi-Fi**. Значение **Блокировать** запрещает использование модема Wi-Fi на устройствах. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Автоматически подключаться к хот-спотам Wi-Fi**. Разрешает устройствам автоматически подключаться к бесплатным хот-спотам Wi-Fi и автоматически принимать любые условия использования.
- **Обнаружение хот-спотов Wi-Fi**. Значение **Блокировать** запрещает устройствам отправлять сведения о подключениях к хот-спотам Wi-Fi. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **NFC**. Значение **Блокировать** отключает операции, которые используют NFC на устройствах, поддерживающих эту технологию. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Bluetooth**. Значение **Блокировать** запрещает пользователю включать Bluetooth. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.

## <a name="next-steps"></a>Дальнейшие шаги

Общие сведения о профиле ограничений устройства см. в разделе [Настройка параметров ограничений устройств в Microsoft Intune](device-restrictions-configure.md).
