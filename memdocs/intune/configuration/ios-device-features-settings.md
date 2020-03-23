---
title: Настройка устройств с iOS/iPadOS в Microsoft Intune в Azure | Документация Майкрософт
description: Здесь описываются все параметры для настройки устройств с iOS и iPadOS, в том числе параметры принтеров AirPrint, макета начального экрана, уведомлений приложений, общего устройства, единого входа, а также фильтра веб-содержимого в Microsoft Intune. Чтобы настроить устройства с iOS/iPadOS и использовать эти возможности Apple в своей организации, измените параметры в профиле конфигурации устройства.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/09/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 351c6ade59d98ce620b939c5ff6238e650390a5f
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79361085"
---
# <a name="ios-and-ipados-device-settings-to-use-common-iosipados-features-in-intune"></a>Параметры устройств с iOS/iPadOS для использования распространенных возможностейiOS/iPadOS в Intune

Благодаря некоторым встроенным параметрам Intune пользователи могут применять различные возможности Apple на своих устройствах с iOS/iPadOS. Например, администратор может контролировать то, как пользователи iOS/iPadOS используют принтеры AirPrint, добавляют приложения и папки на панель закрепления, а также страницы на начальный экран, настраивают отображение уведомлений приложений и сведений о тегах ресурсов на экране блокировки, используют аутентификацию для единого входа, и может настроить проверку подлинности пользователей на основе сертификатов.

Эти возможности можно использовать для управления устройствами с iOS/iPadOS в рамках решения для управления мобильными устройствами (MDM).

В этой описаны все параметры и их назначение. Дополнительные сведения об этих функциях см. в статье [Add iOS or macOS device feature settings in Intune](device-features-configure.md) (Добавление параметров для возможностей устройств iOS или macOS в Intune).

## <a name="before-you-begin"></a>Подготовка к работе

[Создайте профиль конфигурации устройства с iOS/iPadOS](device-features-configure.md).

> [!NOTE]
> Эти параметры применяются к различным типам регистрации, при этом некоторые параметры применяются ко всем вариантам регистрации. Дополнительные сведения о различных типах регистрации см. в статье о [регистрации устройств iOS/iPadOS](../enrollment/ios-enroll.md).

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-all-enrollment-types"></a>Область применения параметров: Все типы регистрации.

> [!NOTE]
> Обязательно добавьте все принтеры в один профиль. Apple предотвращает использование нескольких профилей AirPrint для одного устройства.

- **IP-адрес**. Введите IPv4- или IPv6-адрес принтера. Если для обозначения принтеров используются имена узлов, IP-адрес можно получить, проверив связь с принтером с помощью терминала. Дополнительные сведения см. в этой статье в разделе "Получение IP-адреса и пути".
- **Путь**. Как правило, для принтеров в сети путь будет таким: `ipp/print`. Дополнительные сведения см. в этой статье в разделе "Получение IP-адреса и пути".
- **Порт**. Укажите порт прослушивания для целевого объекта AirPrint. Если это свойство не указано, AirPrint будет использовать порт по умолчанию. Доступно в iOS 11.0 и iPadOS 13.0 и их более поздних версиях.
- **TLS**. Выберите **Включить**, чтобы защитить подключения AirPrint с помощью TLS. Доступно в iOS 11.0 и iPadOS 13.0 и их более поздних версиях.

Чтобы добавить серверы AirPrint, можно:

- **Добавить** — кнопка для добавления сервера AirPrint в список. Вы можете добавить несколько серверов AirPrint.
- Вы также можете **импортировать** CSV-файл с этими данными. Или **экспортировать** файл, чтобы создать список добавленных серверов AirPrint.

### <a name="get-server-ip-address-resource-path-and-port"></a>Получение IP-адреса сервера, пути к ресурсу и порта

Чтобы добавить серверы AirPrinter, вам потребуется IP-адрес принтера, путь к ресурсу и порт. Ниже описывается, как получить эту информацию.

1. На устройстве Mac, подключенном к той же локальной сети (подсети), что и принтеры AirPrint, откройте **Терминал** (меню **/Приложения/Служебные программы**).
2. В приложении "Терминал" введите `ippfind` и нажмите клавишу ВВОД.

    Запишите сведения о принтере. Например, приложение может вернуть такой адрес: `ipp://myprinter.local.:631/ipp/port1`. Первая часть — это имя принтера. Последняя часть (`ipp/port1`) — это путь к ресурсу.

3. В приложении "Терминал" введите `ping myprinter.local` и нажмите клавишу ВВОД.

   Запишите IP-адрес. Например, приложение может вернуть такой адрес: `PING myprinter.local (10.50.25.21)`.

4. Используйте значения IP-адреса и пути к ресурсу. В этом примере IP-адрес — `10.50.25.21`, а путь к ресурсу — `/ipp/port1`.

## <a name="home-screen-layout"></a>макет начального экрана;

Данная функция применяется к:

- iOS 9.3 или более поздним версиям;
- iPadOS 13.0 и более поздние версии.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Область применения параметров: Автоматическая регистрация устройств (защищенная).

### <a name="dock"></a>Панель закрепления

С помощью параметров **панели закрепления** можно добавить до шести элементов или папок для отображения на экране iOS/iPadOS. Многие устройства позволяют добавлять меньше элементов. Например iPhone поддерживает до четырех элементов. В этом случае на экране устройства отображаются только первые четыре элемента, которые вы добавили.

На панели закрепления устройства вы можете добавить не более **шести** элементов (как приложений, так и папок).

- **Добавить**. Добавляет приложения или папки на панель закрепления на устройстве.
- **Тип** — Вы можете добавить **приложение** или **папку**.

  - **Приложение**. Выберите этот параметр, чтобы добавить приложения на панель закрепления на экране. Введите:

    - **Имя приложения**. Введите имя приложения. Это имя используется в качестве справочного в центре администрирования диспетчера конечных точек Майкрософт. Оно *не* отображается на устройствах с iOS/iPadOS.
    - **Идентификатор набора приложений**. Введите идентификатор пакета приложения. Примеры см. в перечне [идентификаторов пакетов для встроенных приложений iOS/iPadOS](bundle-ids-built-in-ios-apps.md).

  - **Папка**. Выберите этот параметр, чтобы добавить папку на панель закрепления на экране.

    Приложения, добавляемые на страницу в папке, упорядочены слева направо в том же порядке, что и в списке. Приложения, которые не поместились на одной странице, перемещаются на другую.

    - **Имя папки**. Введите имя папки. Это имя пользователи видят на своем устройстве.
    - **Список страниц**. Нажмите **Добавить**, чтобы добавить страницу, и укажите следующие свойства.

      - **Имя страницы**. Введите имя страницы. Это имя используется в качестве справочного в центре администрирования диспетчера конечных точек Майкрософт. Оно *не* отображается на устройствах с iOS/iPadOS.
      - **Имя приложения**. Введите имя приложения. Это имя используется в качестве справочного в центре администрирования диспетчера конечных точек Майкрософт. Оно *не* отображается на устройствах с iOS/iPadOS.
      - **Идентификатор набора приложений**. Введите идентификатор пакета приложения. Примеры см. в перечне [идентификаторов пакетов для встроенных приложений iOS/iPadOS](bundle-ids-built-in-ios-apps.md).

      На панель закрепления устройства можно добавить до **20** страниц.

> [!NOTE]
> При добавлении значков через команды закрепления значки начального экрана и на страницах будут заблокированы, и их невозможно будет переместить. Это может быть предусмотрено архитектурой системы iOS/iPadOS и политиками MDM Apple.

#### <a name="example"></a>Пример

В примере ниже на экране с панелью закрепления показаны только три приложения: Safari, "Почта" и "Акции". Для приложения "Почта" открыто окно свойств:

![Пример параметров закрепления для iOS/iPadOS](./media/ios-device-features-settings/FfFiUcP.png)

При назначении политики устройству iPhone панель закрепления будет выглядеть, как на рисунке ниже.

![Пример макета закрепления для iOS на iPhone](./media/ios-device-features-settings/bAgCe8F.png)

### <a name="pages"></a>Pages

Добавьте страницы, которые вы хотите отображать на начальном экране, и приложения, которые будут отображаться на каждой странице. Приложения, добавляемые на страницу, упорядочены слева направо в том ж порядке, что и в списке. Приложения, которые не поместились на одной странице, перемещаются на другую.

> [!TIP]
> Вы можете изменить порядок элементов в любом списке на начальном экране и других страницах, просто перетащив их.

На одном устройстве можно добавить не более **40** страниц.

- **Список страниц**. Нажмите **Добавить**, чтобы добавить страницу, и укажите следующие свойства.

  - **Имя страницы**. Введите имя страницы. Это имя используется в качестве справочного в центре администрирования диспетчера конечных точек Майкрософт и *не* отображается на устройствах с iOS/iPadOS.

  На одном устройстве можно добавить не более **60** элементов (как ярлыков приложений, так и папок).

  - **Добавить**. Добавляет приложения или папки на страницу на устройстве.

    - **Тип** — Вы можете добавить **приложение** или **папку**.

      - **Приложение**. Выберите этот параметр, чтобы добавить приложения на страницу экрана. Кроме того, укажите:

        - **Имя приложения**. Введите имя приложения. Это имя используется в качестве справочного в центре администрирования диспетчера конечных точек Майкрософт. Оно *не* отображается на устройствах с iOS/iPadOS.
        - **Идентификатор набора приложений**. Введите идентификатор пакета приложения. Примеры см. в перечне [идентификаторов пакетов для встроенных приложений iOS/iPadOS](bundle-ids-built-in-ios-apps.md).

      - **Папка**. Выберите этот параметр, чтобы добавить папку на панель закрепления на экране.

        Приложения, добавляемые на страницу в папке, упорядочены слева направо в том же порядке, что и в списке. Приложения, которые не поместились на одной странице, перемещаются на другую.

        - **Имя папки**. Введите имя папки. Это имя пользователи видят на своем устройстве.
        - **Добавить**. Добавляет страницы в папку. Укажите также следующие свойства.

          - **Имя страницы**. Введите имя страницы. Это имя используется в качестве справочного в центре администрирования диспетчера конечных точек Майкрософт. Оно *не* отображается на устройствах с iOS/iPadOS.
          - **Имя приложения**. Введите имя приложения. Это имя используется в качестве справочного в центре администрирования диспетчера конечных точек Майкрософт. Оно *не* отображается на устройствах с iOS/iPadOS.
          - **Идентификатор набора приложений**. Введите идентификатор пакета приложения. Примеры см. в перечне [идентификаторов пакетов для встроенных приложений iOS/iPadOS](bundle-ids-built-in-ios-apps.md).

#### <a name="example"></a>Пример

В примере ниже показано, как добавить страницу с именем **Contoso**. На странице отображаются только приложения "Найти друзей" и "Настройки". Для приложения "Настройки" открыто окно свойств:

![Пример параметров начального экрана iOS/iPadOS в Intune](./media/ios-device-features-settings/Jc2OxyX.png)

При назначении политики устройству iPhone страница будет выглядеть, как на рисунке ниже.

![Устройство iOS/iPadOS с измененным начальным экраном в Intune](./media/ios-device-features-settings/Bd37PHa.png)

## <a name="app-notifications"></a>Уведомления приложения

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Область применения параметров: Автоматическая регистрация устройств (защищенная).

- **Добавить**. Добавляет уведомления для приложений.

    ![Добавление уведомления для приложения в профиль iOS/iPadOS в Intune](./media/ios-device-features-settings/ios-macos-app-notifications.png)

  - **Идентификатор пакета приложений**. Укажите **идентификатор пакета приложений** для приложения, которое требуется добавить. Примеры см. в перечне [идентификаторов пакетов для встроенных приложений iOS/iPadOS](bundle-ids-built-in-ios-apps.md).
  - **Имя приложения**. Введите имя приложения, которое необходимо добавить. Это имя используется в качестве справочного в центре администрирования диспетчера конечных точек Майкрософт. Оно *не* отображается на устройстве.
  - **Издатель** — Укажите издателя для приложения, которое собираетесь добавить. Это имя используется в качестве справочного в центре администрирования диспетчера конечных точек Майкрософт. Оно *не* отображается на устройстве.
  - **Уведомления**. **Включите** или **отключите** для приложения параметр отправки уведомлений на устройство.
    - **Показать в центре уведомлений**. **Включите** этот параметр, чтобы разрешить приложению показывать уведомления в центре уведомлений устройства. **Отключите** этот параметр, чтобы запретить приложению показывать уведомления в центре уведомлений.
    - **Показать на экране блокировки**. **Включите** этот параметр, чтобы уведомления приложения отображались на экране блокировки устройства. **Отключите** этот параметр, чтобы уведомления приложения не отображались на экране блокировки устройства.
    - **Тип оповещения**. После разблокирования устройства выберите, как будут отображаться уведомления. Доступны следующие параметры:
      - **Нет**: Без уведомлений.
      - **Заголовок**. Вместе с уведомлением отображается краткий заголовок.
      - **Модальный**. Когда уведомление отобразится, пользователю необходимо будет вручную отменить его, чтобы продолжить работу с устройством.
    - **Значок на ярлыке приложения**. **Включите**, чтобы добавить значок на ярлык приложения. Значок означает, что приложение отправило уведомление.
    - **Звуки**. **Включите** этот параметр для воспроизведения звука при получении уведомления.

## <a name="lock-screen-message"></a>Сообщение на экране блокировки

Данная функция применяется к:

- iOS 9.3 и более поздние версии.
- iPadOS 13.0 и более поздние версии.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Область применения параметров: Автоматическая регистрация устройств (защищенная).

- **Сведения о теге ресурса**. Введите сведения о теге ресурса устройства. Например, введите `Owned by Contoso Corp` или `Serial Number: {{serialnumber}}`.

  Вводимый текст отображается на экране входа и окна блокировки устройства.

- **Примечание на экране блокировки**. Введите примечание, которое поможет вернуть устройство в случае его потери или кражи. Можно ввести любой текст. Например, можно ввести `If found, call Contoso at ...`.

  Токены устройств также можно использовать, чтобы добавить сведения об устройстве для этих полей. Например, чтобы отобразить серийный номер, введите `Serial Number: {{serialnumber}}`. На экране блокировки отображается текст вида `Serial Number 123456789ABC`. При вводе переменных не забудьте использовать фигурные скобки `{{ }}`. Раздел [Токены конфигурации приложений](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) содержит список переменных, которые можно использовать. Можно также использовать `deviceName` или любое другое значение конкретного устройства.

  > [!NOTE]
  > Переменные не проверяются в пользовательском интерфейсе и вводятся с учетом регистра. В результате профили могут сохраняться с неверными входными данными. Например, если ввести `{{DeviceID}}` вместо `{{deviceid}}`, то вместо уникального идентификатора устройства отображается литеральная строка. Убедитесь, что указаны правильные данные.

## <a name="single-sign-on"></a>Единый вход

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Область применения параметров: Регистрация устройств, автоматическая регистрация устройств (защищенная)

- **Атрибут имени пользователя из AAD.** Служба Intune ищет этот атрибут для каждого пользователя в Azure Active Directory. Затем служба Intune вставляет его в соответствующее поле (например, имя субъекта-пользователя), прежде чем создать XML для установки на устройстве. Доступны следующие параметры:

  - **Имя участника-пользователя**. Имя участника-пользователя анализируется следующим образом:

    ![Атрибут единого входа пользователя iOS или iPadOS в Intune](./media/ios-device-features-settings/User-name-attribute.png)

    Вы также можете переопределить область, введя собственный текст в поле **Область**.

    Например, компания Contoso может работать в нескольких регионах, таких как Европа, Азия и Северная Америка. Компания Contoso хочет, чтобы пользователи из Азии могли использовать единый вход и чтобы в приложении нужно было вводить имя участника-пользователя в формате `username@asia.contoso.com`. Если выбрано **имя участника-пользователя**, для каждого пользователя используется область из Azure Active Directory, например `contoso.com`. Поэтому, для пользователей в Азии, выберите **имя участника-пользователя** и введите `asia.contoso.com`. Имя участника-пользователя будет иметь вид `username@asia.contoso.com`, а не `username@contoso.com`.

  - **Идентификатор устройства в Intune**. Служба Intune автоматически выбирает идентификатор устройства.

    По умолчанию приложениям необходимо использовать только идентификатор устройства. Но если приложение использует идентификатор и область, ее можно ввести в текстовом поле Область.

    > [!NOTE]
    > Если используется идентификатор устройства, по умолчанию область следует оставлять пустой.

  - **Идентификатор устройства Azure AD**

- **Область**. Введите часть URL-адреса с доменом. Например, введите `contoso.com`.
- **Префиксы URL-адреса, для которых будет использоваться единый вход**. **Добавьте** все URL-адреса в вашей организации, для которых нужно выполнять проверку подлинности пользователей на основе единого входа.

  Когда пользователь подключается к одному из этих сайтов, устройство с iOS или iPadOS использует учетные данные единого входа. При этом пользователю не нужно вводить дополнительные учетные данные. Если включена многофакторная проверка подлинности, пользователям необходимо использовать второе средство проверки подлинности.

  > [!NOTE]
  > URL-адреса должны иметь правильный формат полных доменных имен. Компания Apple требует использовать следующий формат: `http://<yourURL.domain>`.

  Шаблоны сопоставления URL-адресов должны начинаться с префикса `http://` или `https://`. Выполняется простое сравнение строк, поэтому URL-адрес `http://www.contoso.com/` не совпадает с `http://www.contoso.com:80/`. В iOS 10.0 и iPadOS 13.0 или более поздних версий можно использовать один подстановочный знак \* для ввода всех соответствующих значений. Например, шаблону `http://*.contoso.com/` соответствует как адрес `http://store.contoso.com/`, так и `http://www.contoso.com`.

  Шаблонам `http://.com` и `https://.com` соответствуют все URL-адреса, начинающиеся с префикса HTTP и HTTPS соответственно.

- **Приложения, для которых будет использоваться единый вход**. **Добавьте** приложения на устройствах пользователей, которые могут использовать единый вход.

  Массив `AppIdentifierMatches` должен содержать строки, соответствующие идентификаторам пакетов приложений. Эти строки могут представлять собой точные совпадения (например, `com.contoso.myapp`), либо можно использовать шаблоны с подстановочным знаком \*, сопоставляемые с префиксами идентификаторов пакетов. Подстановочный знак должен находиться после точки (.). Он может использоваться только один раз в конце строки, например `com.contoso.*`. Если в строке есть подстановочный знак, доступ к учетной записи предоставляется всем приложениям, идентификаторы пакетов которых начинаются с указанного префикса.

  В поле **Имя приложения** можно указать понятное имя, помогающее определить идентификатор пакета.

- **Сертификат продления учетных данных**. Если для проверки подлинности используются сертификаты (без паролей), выберите SCEP или PFX в качестве сертификата проверки подлинности. Как правило, это тот же сертификат, который развертывается у пользователя для других профилей, включая профили VPN, Wi-Fi или электронной почты.

## <a name="web-content-filter"></a>Фильтр веб-содержимого

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Область применения параметров: Автоматическая регистрация устройств (защищенная).

- **Тип фильтра**. Выберите веб-сайты, которые нужно разрешить. Доступны следующие параметры:

  - **Настройка URL-адресов**. Воспользуйтесь встроенным фильтром веб-содержимого Apple, который ищет ненормативную лексику или выражения сексуального характера. Эта функция оценивает каждую веб-страницу во время загрузки, определяет и блокирует такое содержимое. Можно также добавить URL-адреса, которые не будут проверяться фильтром. Или заблокировать определенные URL-адреса, независимо от настроек фильтра Apple.

    - **Разрешенные URL-адреса**. **Добавьте** нужные URL-адреса в список разрешенных. Эти URL-адреса не проверяются веб-фильтром Apple.

        > [!NOTE]
        > URL-адреса, которые вы ввели, — это адреса, которые не нужно проверять веб-фильтром Apple. Эти URL-адреса не включены в список разрешенных веб-сайтов. Чтобы создать список разрешенных веб-сайтов, установите для параметра **Тип фильтра** значение **Только некоторые веб-сайты**.

    - **Заблокированные URL-адреса**. **Добавьте** URL-адреса, доступ к которым вы хотите закрыть, независимо от параметров веб-фильтра Apple.

  - **Только некоторые веб-сайты** (только для браузера Safari). Эти URL-адреса добавляются в закладки браузера Safari. Пользователю разрешено посещать **только эти** сайты. Другие сайты недоступны. Используйте этот параметр только в том случае, если вы знаете точный список URL-адресов, доступных пользователям.

    - **URL-адрес**. Введите URL-адрес веб-сайта, который вы хотите разрешить. Например, введите `https://www.contoso.com`.
    - **Путь к закладке**. Этот параметр изменен Apple. Все закладки перемещаются в папку **Approved Sites** (Утвержденные сайты). Закладки не перемещаются по пути, который вы введете.
    - **Название**. Введите описательное название закладки.

    Если не ввести URL-адреса, пользователи не смогут получить доступ ни к одному сайту, кроме`microsoft.com`, `microsoft.net` и `apple.com`. Доступ к этим URL-адреса открыт в службе Intune по умолчанию.

## <a name="single-sign-on-app-extension"></a>Расширение для приложения единого входа

Данная функция применяется к:

- iOS версии 13.0 и выше
- iPadOS версии 13.0 и выше

### <a name="settings-apply-to-all-enrollment-types"></a>Область применения параметров: Все типы регистрации.

- **Тип расширения единого входа для приложения**. Выберите тип расширения для расширения приложения единого входа. Доступны следующие параметры:

  - **Не настроено**. Расширения приложения не используются. Чтобы отключить расширение, можно переключить тип расширения единого входа для приложения на значение **Не настроено**.
  - **Перенаправление**. Используйте универсальное настраиваемое расширение приложения перенаправления для единого входа с помощью современных способов проверки подлинности. Убедитесь, что вы знаете идентификатор для расширения приложения своей организации.
  - **Учетные данные**. Используйте универсальное настраиваемое расширение учетных данных для приложения, чтобы выполнять единый вход с помощью потоков проверки подлинности с запросом и ответом. Убедитесь, что вы знаете идентификатор для расширения приложения своей организации.
  - **Kerberos.** Используйте встроенное расширение Kerberos для Apple, которое включено в iOS 13.0 и iPadOS 13.0, и их более поздние версии. Это расширение является версией расширения приложения **Учетные данные**, предназначенной для Kerberos.

  > [!TIP]
  > С помощью типов **Перенаправление** и **Учетные данные** вы добавляете свои значения конфигурации для передачи через расширение. Если вы используете тип **Учетные данные**, рассмотрите применение встроенных параметров конфигурации, предоставляемых Apple с типом **Kerberos**.

- **Идентификатор расширения** (для типов "Перенаправление" и "Учетные данные"). Введите идентификатор пакета, который определяет расширение единого входа для приложения, например `com.apple.extensiblesso`.

- **Идентификатор Team ID** (для типов "Перенаправление" и "Учетные данные"). Введите идентификатор команды для расширения единого входа для приложения. Идентификатор команды — это создаваемая Apple строка, которая состоит из 10 символов (цифр и букв), например `ABCDE12345`. Идентификатор команды — необязательный параметр.

  Дополнительные сведения см. на странице [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (Поиск идентификатора команды) — откроется веб-сайт Apple.

- **Область** (для типов "Учетные данные" и "Kerberos"). Введите имя области проверки подлинности. Имя области следует писать прописными буквами, например `CONTOSO.COM`. Как правило, имя области совпадает с именем домена DNS, но пишется только прописными буквами.

- **Домены** (для типов "Учетные данные" и "Kerberos"). Введите имена доменов или узлов для сайтов, на которых можно проходить проверку подлинности с помощью единого входа. Например, если веб-сайт — `mysite.contoso.com`, тогда `mysite` — имя узла, а `contoso.com` — доменное имя. Когда пользователи будут подключаться к любому из этих сайтов, расширение приложения будет обрабатывать запрос проверки подлинности. Эта проверка подлинности позволяет пользователям входить на сайты с помощью Face ID, Touch ID или ПИН-кода либо секретного кода Apple.

  - Все домены в расширении единого входа для приложения в Intune должны быть уникальными. Один и тот же домен нельзя указывать повторно ни в одном профиле расширения единого входа для приложения, даже если вы используете разные типы расширений единого входа.
  - В этих именах доменов не учитывается регистр.

- **URL-адреса** (только для типа "Перенаправление"). Введите префиксы URL-адресов поставщиков удостоверений, от имени которых расширение перенаправления будет выполнять единый вход. При перенаправлении пользователя по этим адресам запускается расширение приложения для выполнения единого входа.

  - Все URL-адреса в профилях расширения единого входа для приложения в Intune должны быть уникальными. Один и тот же домен нельзя указывать повторно ни в одном профиле расширения единого входа для приложения, даже если вы используете разные типы расширений единого входа.
  - URL-адреса должны начинаться с "http://" или "https://".

- **Дополнительная конфигурация** (для типов "Перенаправление" и "Учетные данные"). Введите дополнительные специализированные данные для передачи расширению приложения единого входа.
  - **Ключ**: Введите имя элемента, который необходимо добавить, например `user name`.
  - **Тип** — Введите тип данных. Доступны следующие параметры:

    - Строка
    - Логическое значение. В поле **Значение конфигурации** введите `True` или `False`.
    - Целое число. В поле **Значение конфигурации** введите число.
    
  - **Значение**. Введите данные.

  - **Добавить**. Выберите ключи конфигурации, которые необходимо добавить.

- **Использование цепочки ключей** (только для типа "Kerberos"). Выберите значение **Заблокировать**, чтобы запретить сохранение паролей в цепочке ключей. Если этот параметр заблокирован, пользователю не предлагается сохранить пароль, и при истечении срока действия билета Kerberos необходимо повторно ввести пароль. Если оставить значение **Не настроено** (по умолчанию), пароли будут сохраняться и храниться в цепочке ключей. По истечении срока действия билета пользователи не получают запрос на повторный ввод пароля.
- **Face ID, Touch ID или секретный код** (только для типа "Kerberos"). Если выбрано значение **Требовать**, для обновления билета Kerberos пользователям необходимо ввести Face ID, Touch ID или секретный код устройства. Если оставить значение **Не настроено** (по умолчанию), пользователям не нужно будет использовать биометрические данные или секретный код для обновления билета Kerberos. Если параметр **Использование цепочки ключей** заблокирован, этот параметр не применяется.
- **Область по умолчанию** (только для типа "Kerberos"). Выберите вариант **Включить**, и значение, введенное для параметра **Область**, будет использоваться в качестве значения области по умолчанию. Если оставить вариант **Не настроено** (по умолчанию), область по умолчанию не будет задана.

  > [!TIP]
  > - Выберите значение **Включить** для этого параметра, если необходимо настроить несколько расширений Kerberos для приложения в своей организации.
  > - Выберите значение **Включить** для этого параметра, если вы используете несколько областей. Это позволяет задать значение параметра **Область** в качестве области по умолчанию.
  > - Если есть только одна область, оставьте значение **Не настроено** (по умолчанию) для этого параметра.

- **Имя субъекта** (только для типа "Kerberos"). Введите имя для субъекта Kerberos. Вам не нужно включать в него имя области. Например, в примере `user@contoso.com`, `user` — имя субъекта, а `contoso.com` — имя области.

  > [!TIP]
  > - В имени субъекта также можно использовать переменные путем ввода фигурных скобок `{{ }}`. Например, чтобы показать имя пользователя, введите `Username: {{username}}`. 
  > - Однако соблюдайте осторожность при подстановке переменных, так как они не проверяются в пользовательском интерфейсе и их регистр учитывается. Убедитесь, что указаны правильные данные.

- **Код сайта Active Directory** (только для типа "Kerberos"). Введите имя сайта Active Directory, который должно использовать расширение Kerberos. Возможно, вам не потребуется изменять это значение, так как расширение Kerberos может автоматически найти код сайта Active Directory.
- **Имя кэша** (только для типа "Kerberos"). Введите имя Generic Security Services (универсальных служб безопасности, GSS) для кэша Kerberos. Вероятнее всего, вам не потребуется указывать это значение.
- **ИД пакетов приложений** (только для типа "Kerberos"). **Добавьте** идентификаторы пакетов приложений, которые должны использовать единый вход на устройствах. Этим приложениям предоставляется доступ к билету на получение билетов Kerberos, билету проверки подлинности и проверке подлинности пользователей в службах, к которым у них есть доступ.
- **Сопоставление области домена** (только для типа "Kerberos"). **Добавьте** DNS-суффиксы доменов, которые необходимо сопоставить с вашей областью. Используйте этот параметр, если DNS-имена узлов не соответствуют имени области. Вероятнее всего, вам не нужно будет создавать это пользовательское сопоставление между доменами и областью.
- **Сертификат PKINIT** (только для типа "Kerberos"). **Выберите** сертификат шифрования с открытым ключом для первоначальной проверки подлинности (PKINIT), который можно использовать для проверки подлинности Kerberos. Вы можете выбрать сертификат [PKCS](../protect/certficates-pfx-configure.md) или [SCEP](../protect/certificates-scep-configure.md), добавленные в Intune. Дополнительные сведения о сертификатах см. в статье [Use certificates for authentication in Microsoft Intune](../protect/certificates-configure.md) (Использование сертификатов для проверки подлинности в Microsoft Intune).

## <a name="wallpaper"></a>Фоновый рисунок

Если назначить профиль без изображения устройствам с настроенным изображением, результат может быть непредвиденным. Например, вы создаете профиль без изображения. Этот профиль назначается устройствам, на которых уже задано изображение. В этом случае исходное изображение либо останется, либо будет заменено изображением по умолчанию. Данное поведение контролируется и ограничивается платформой MDM компании Apple.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Область применения параметров: Автоматическая регистрация устройств (защищенная).

- **Расположение фонового рисунка на экране**. Выберите расположение, где будет показано изображение на экране. Доступны следующие параметры:
  - **Не настроено**. Пользовательское изображение не добавлено на устройство. На устройстве используются параметры операционной системы по умолчанию.
  - **Экран блокировки**. Добавляет изображение на экран блокировки.
  - **Начальный экран**. Добавляет изображение на начальный экран.
  - **Экран блокировки и начальный экран**. Одинаковое изображение используется на экране блокировки и начальном экране.
- **Изображение фонового рисунка**. Отправьте файл с расширением .png, .jpg или .jpeg, который вы хотите использовать. Размер файла должен быть не более 750 КБ. Также можно **удалить** изображение, которое вы добавили.

> [!TIP]
> Чтобы показывать на экране блокировки и начальном экране разные изображения, создайте профиль с изображением экрана блокировки. Создайте другой профиль с изображением начального экрана. Назначьте оба профиля своему пользователю iOS или iPadOS или группам устройств.

## <a name="next-steps"></a>Дальнейшие шаги

[Назначьте профиль](device-profile-assign.md) и [отслеживайте его состояние](device-profile-monitor.md).

Вы также можете создать профили конфигурации устройств [macOS](macos-device-features-settings.md).