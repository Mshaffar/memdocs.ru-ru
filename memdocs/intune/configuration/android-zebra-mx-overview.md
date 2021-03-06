---
title: Использование Zebra Mobility Extensions на устройствах Android в Microsoft Intune — Azure | Документация Майкрософт
description: Используйте устройства Android Zebra с Zebra Mobility Extensions (MX) и управляйте ими с помощью Microsoft Intune. Просмотрите все шаги, включая установку приложения Корпоративного портала, передачу данных приложения на другое локальное устройство, назначение роли администратора устройства, создание профиля StageNow и многое другое.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 077318d4b55c7e1f2a83864aba51e2282630b9fb
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990144"
---
# <a name="use-and-manage-zebra-devices-with-zebra-mobility-extensions-in-microsoft-intune"></a>Использование устройств Zebra с Zebra Mobility Extensions и управление ими в Microsoft Intune

Intune содержит широкий набор компонентов, включая управление приложениями и настройку параметров устройств. Эти встроенные компоненты и параметры используются для управления устройствами Android, произведенными компанией Zebra Technologies, также известными как "устройства Zebra".

На устройствах Android используйте профили Zebra **Mobility Extensions (MX)** для настройки или добавления параметров Zebra.

В этой статье показано, как использовать Zebra Mobility Extensions (MX) на устройствах Zebra в Microsoft Intune.

Данная функция применяется к:

- Администратор устройства с Android

Для устройств Android Enterprise используйте [OEMConfig](android-oem-configuration-overview.md).

Ваша компания может использовать устройства Zebra для розничной торговли, на заводской площадке и тому подобное. Например, вы занимаетесь розничной торговлей, и ваша среда насчитывает тысячи мобильных устройств Zebra, которыми пользуются продавцы-консультанты. Intune помогает управлять этими устройствами в рамках решения для управления мобильными устройствами.

С помощью Intune вы можете регистрировать устройства Zebra для развертывания бизнес-приложений на устройствах. Профили "Конфигурация устройства" позволяют создавать профили MX для управления параметрами Zebra.

> [!NOTE]
> По умолчанию API-интерфейсы Zebra MX не заблокированы на устройствах. Прежде чем устройство будет зарегистрировано в Intune, оно может быть скомпрометировано вредоносным способом. Когда устройство находится в чистом состоянии, рекомендуется заблокировать API-интерфейсы MX с помощью диспетчера доступа (AccessMgr). Например, можно выбрать, что вызов API-интерфейсов MX могут выполнять только приложение корпоративного портала и приложения, которым вы доверяете.
>
> Дополнительные сведения см. в статье [Блокировка устройства](https://developer.zebra.com/community/home/blog/2017/04/11/locking-down-your-device) на веб-сайте Zebra.

## <a name="before-you-begin"></a>Подготовка к работе

- Убедитесь, что у вас последняя версия классического приложения StageNow от компании Zebra Technologies.
- Не забудьте проверить [полную таблицу возможностей Zebra MX](http://techdocs.zebra.com/mx/compatibility) (открывается веб-сайт Zebra) для подтверждения того, что создаваемые профили совместимы с версией MX, версией ОС и моделью устройства.
- Определенные устройства, например TC20/25, не поддерживают все доступные компоненты MX в StageNow. Не забудьте проверить [таблицу возможностей Zebra](http://techdocs.zebra.com/mx/tc2x/) (открывается веб-сайт Zebra) при обновлении информации поддержки.

## <a name="step-1-install-the-latest-company-portal-app"></a>Шаг 1. Установка последней версии приложения корпоративного портала

На устройстве перейдите в магазин Google Play. Скачайте и установите приложение корпоративного портала Intune от Майкрософт. При установке из Google Play Маркет приложение Корпоративного портала автоматически получает обновления и исправления.

Если нет доступа к Google Play Маркет, скачайте [Корпоративный портал Microsoft Intune для Android](https://www.microsoft.com/download/details.aspx?id=49140) (открывается другой веб-сайт Майкрософт) и [передайте данные на другое локальное устройство](#sideload-the-company-portal-app) (в этой статье). При установке таким образом приложение автоматически не получает обновления или исправления. Следует регулярно устанавливать исправления и обновлять приложение вручную.

### <a name="sideload-the-company-portal-app"></a>Передача данных Корпоративного портала на другое локальное устройство

Передача данных на другое локальное устройство применяется, когда вы не используете Google Play Маркет для установки приложения. Для передачи данных Корпоративного портала на другое локальное устройство используйте StageNow. 

Ниже приведены общие сведения. Конкретные сведения см. в документации по Zebra. Полезную информацию можно найти в статье [Enroll in an MDM](http://techdocs.zebra.com/stagenow/3-1/Profiles/enrollmdm/) (Регистрация в MDM) (открывается веб-сайт Zebra).

1. В StageNow создайте профиль для **регистрации в MDM**.
2. В **развертывании** выберите скачивание файла агента MDM.
3. Задайте на этапах **Приложение поддержки** и **Скачивание конфигурации** значение **Нет**.
4. Для параметра **Download MDM** (Скачивание MDM) выберите значение **Transfer/Copy File** (Перемещение или копирование файла). Добавьте источник и назначение пакета корпоративного портала Android (APK).
5. В поле **Launch MDM** (Запуск MDM) оставьте значения по умолчанию. Добавьте следующие сведения:

    - **Имя пакета**: `com.microsoft.windowsintune.companyportal`
    - **Имя класса**: `com.microsoft.windowsintune.companyportal.views.SplashActivity`

Продолжайте публиковать профиль и использовать его на устройстве в приложении StageNow. На устройстве установлено и открыто приложение корпоративного портала.

> [!TIP]
> Дополнительные сведения о StageNow и его назначении см. в статье [STAGENOW ANDROID DEVICE STAGING](https://www.zebra.com/us/en/products/software/mobile-computers/mobile-app-utilities/stagenow.html) (Промежуточное размещение устройства Android StageNow) (открывается веб-сайт Zebra).

## <a name="step-2-confirm-the-company-portal-app-has-device-administrator-role"></a>Шаг 2. Подтверждение того, что у приложения корпоративного портала есть роль администратора устройства

Для приложения Корпоративного портала требуется роль администратора устройства для управления устройствами Android. Для активации роли администратора устройства на некоторых устройствах Zebra предусмотрен пользовательский интерфейс. Если у устройства есть пользовательский интерфейс, приложение Корпоративного портала предложит пользователю предоставить разрешение администратора устройства во время [регистрации](#step-3-enroll-the-device-in-to-intune) (в этой статье).

Если пользовательский интерфейс не поддерживается, используйте **DevAdmin Manager** в StageNow, чтобы создать профиль, который вручную предоставляет разрешение администратора устройства для приложения корпоративного портала.

Ниже приведены общие сведения. Конкретные сведения см. в документации по Zebra. 
Полезную информацию можно найти в статье [Set Battery Swap Mode as Device Administrator using StageNow Tool](https://zebratechnologies.force.com/s/article/Set-Battery-Swap-Mode-as-Device-Administrator-using-StageNow-Tool) (Установка режима замены батареи от имени администратора устройства с помощью StageNow Tool) (открывается веб-сайт Zebra).

1. В StageNow создайте профиль и выберите **Режим Xpert**.
2. Добавьте в профиль **DevAdmin Manager**.
3. Задайте для параметра **Device Administration Action** (Действие администрирования устройства) значение **Turn On as Device Administrator** (Включить от имени администратора устройства).
4. Задайте параметру **Device Admin Package Name** (Имя пакета администратора устройства) значение `com.microsoft.windowsintune.companyportal`.
5. Задайте параметру **Device Admin Class Name** (Имя класса администратора устройства) значение `com.microsoft.omadm.client.PolicyManagerReceiver`.

Продолжайте публиковать профиль и использовать его на устройстве в приложении StageNow. Приложению Корпоративного портала предоставляется роль администратора устройства.

## <a name="step-3-enroll-the-device-in-to-intune"></a>Шаг 3. Регистрация устройства в Intune

После выполнения первых двух шагов на устройстве установлено приложение Корпоративного портала. Устройство готово к регистрации в Intune.

Этапы регистрации устройств Android см. [здесь](../enrollment/android-enroll.md). Если у вас много устройств Zebra, вы можете использовать [учетную запись диспетчера регистрации устройств (DEM)](../enrollment/device-enrollment-manager-enroll.md). С помощью учетной записи DEM также удаляется параметр для отмены регистрации в приложении Корпоративного портала, чтобы пользователи не могли с легкостью отменить регистрацию устройства.

## <a name="step-4-create-a-device-management-profile-in-stagenow"></a>Шаг 4. Создание профиля управления устройством в StageNow

Используйте StageNow для создания профиля, настраивающего параметры, которыми вы хотите управлять на устройстве. Конкретные сведения см. в документации по Zebra. Полезную информацию можно найти в статье [Profiles](http://techdocs.zebra.com/stagenow/3-2/stagingprofiles/) (Профили) (открывается веб-сайт Zebra).

При создании профиля в StageNow на последнем шаге выберите **Export to MDM** (Экспортировать в MDM). На этом шаге создается XML-файл. Сохраните файл. Он понадобится позже.

- Мы советуем протестировать профиль перед его развертыванием на устройствах в организации. Чтобы протестировать на последнем шаге при создании профилей с помощью StageNow на компьютере, используйте параметры **Тестирование**. Затем используйте созданный StageNow файл с помощью приложения StageNow на устройстве.

  В приложении StageNow на устройстве отображаются журналы, созданные при тестировании профиля. Сведения об использовании журналов StageNow для определения ошибок см. в статье [Troubleshoot and see potential issues on Android Zebra devices in Microsoft Intune](android-zebra-mx-logs-troubleshoot.md) (Устранение неполадок и поиск потенциальных проблем устройств Android Zebra в Microsoft Intune).

- Если вы ссылаетесь на приложения, обновляете пакеты или другие файлы в профиле StageNow, вам нужно, чтобы устройство получало эти обновления. Чтобы получить обновления, при применении профиля устройству необходимо подключиться к серверу развертывания StageNow. 

  Или вы можете использовать встроенные компоненты в Intune для получения этих изменений, включая следующие:

  - Функции управления приложениями, такие как [добавление](../apps/apps-add.md), [развертывание](../apps/apps-deploy.md), обновление и [мониторинг](../apps/apps-monitor.md) приложений.
  - Управление [обновлениями системы и приложений](device-restrictions-android-for-work.md#device-owner-only) на устройствах Android для бизнеса.

После тестирования файла следующий шаг — развертывание профиля на устройствах с помощью Intune.

- На устройстве можно развернуть один или несколько профилей MX.
- Можно также экспортировать несколько профилей StageNow и объединить параметры в один XML-файл. Затем отправьте XML-файл в Intune для развертывания на устройствах.

  > [!WARNING]
  > Если для одной и той же группы предназначены несколько профилей MX и настроено одно и то же свойство, на устройстве будут возникать конфликты.
  >
  > Если одно и то же свойство настраивается несколько раз в одном профиле MX, преимущественную силу имеет последняя конфигурация.

## <a name="step-5-create-a-profile-in-intune"></a>Шаг 5. Создание профиля в Intune

В Intune создайте профиль конфигурации устройства:

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Устройства** > **Профили конфигурации** > **Создать профиль**.
3. Укажите следующие свойства.

    - **Имя** — Введите описательное имя для нового профиля.
    - **Описание**. Введите описание профиля. Этот параметр является необязательным, но мы рекомендуем его использовать.
    - **Платформа**. Выберите элемент **Администратор устройств Android**.
    - **Тип профиля**. Выберите **Профиль MX (только Zebra)** .

4. В области **Профиль MX в формате XML** добавьте XML-файл профиля, [экспортированный из StageNow](#step-4-create-a-device-management-profile-in-stagenow) (в этой статье).
5. Щелкните **OK** > **Создать**, чтобы сохранить изменения. Созданная вами политика отображается в списке.

    > [!TIP]
    > По соображениям безопасности вы не увидите XML-текст профиля после его сохранения. Текст зашифрован и вы увидите только звездочки (`****`). Для справки мы советуем сохранять копии профилей MX прежде чем добавлять их в Intune.

Профиль создан, но он пока ничего не делает. Далее [назначьте профиль](device-profile-assign.md) и [отслеживайте его состояние](device-profile-monitor.md).

В следующий раз при проверке устройством наличия обновлений конфигурации профиль MX развертывается на устройстве. Устройства синхронизируются с Intune при регистрации, а затем приблизительно каждые 8 часов. Вы также можете [принудительно синхронизироваться в Intune](../remote-actions/device-sync.md). Кроме того, вы можете на устройстве открыть **приложение Корпоративного портала** > **Параметры** >  **Синхронизация**. 

## <a name="update-a-zebra-mx-configuration-after-its-assigned"></a>Обновление конфигурации Zebra MX после ее назначения

Чтобы обновить конфигурацию устройства Zebra, относящуюся к MX, можно выполнить следующее: 

- Создайте обновленный XML-файл StageNow, измените существующий профиль Intune MX и отправьте новый XML-файл StageNow. Этот новый файл перезаписывает предыдущую политику в профиле и заменяет предыдущую конфигурацию.
- Создайте новый XML-файл StageNow, который настраивает различные параметры, создайте новый профиль Intune MX, отправьте новый XML-файл StageNow и назначьте его той же группе. Развертываются несколько профилей. Если новый профиль настраивает параметры, которые уже имеются в существующих профилях, возникнут конфликты.

## <a name="next-steps"></a>Дальнейшие шаги

- [Назначьте профиль](device-profile-assign.md) и [отслеживайте его состояние](device-profile-monitor.md).
- [Troubleshoot and see potential issues on Android Zebra devices in Microsoft Intune](android-zebra-mx-logs-troubleshoot.md) (Устранение неполадок и поиск потенциальных проблем устройств Android Zebra в Microsoft Intune).
