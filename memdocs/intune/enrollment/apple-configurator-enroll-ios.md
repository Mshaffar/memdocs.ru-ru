---
title: Регистрация устройств iOS и iPadOS с использованием Apple Configurator и помощника по настройке
titleSuffix: Microsoft Intune
description: Узнайте, как зарегистрировать корпоративные устройства iOS и iPadOS с использованием Apple Configurator и помощника по настройке.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/04/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 671e4d76-0c61-11e8-ba89-0ed5f89f718b
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a85ff2ae7f0724a2ff41be5bda22877cc099ef2a
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79339505"
---
# <a name="set-up-iosipados-device-enrollment-with-apple-configurator"></a>Настройка регистрации устройств iOS и iPadOS с помощью Apple Configurator

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune поддерживает регистрацию устройств iOS и iPadOS с помощью средства [Apple Configurator](https://itunes.apple.com/app/apple-configurator-2/id1037126344), запущенного на компьютере Mac. Для регистрации через Apple Configurator требуется подключить каждое устройство iOS и iPadOS через USB к компьютеру Mac для настройки корпоративной регистрации. Зарегистрировать устройства в Intune с помощью Apple Configurator можно двумя способами:
- **Регистрация с использованием помощника по настройке**. Очищает устройство и подготавливает его для регистрации с использованием помощника по настройке.
- **Прямая регистрация.** Этот процесс не выполняет очистку устройства. Он регистрирует устройство, используя параметры iOS и iPadOS. Этот способ предназначен только для устройств **без сходства пользователей**.

Методы регистрации Apple Configurator нельзя использовать с [диспетчером регистрации устройств](device-enrollment-manager-enroll.md).

## <a name="prerequisites"></a>Предварительные условия

- Физический доступ к устройствам iOS и iPadOS
- [Настройка центра MDM](../fundamentals/mdm-authority-set.md)
- [Сертификат Apple MDM Push Certificate](apple-mdm-push-certificate-get.md)
- Серийные номера устройств (только для регистрации с использованием помощника по настройке)
- Соединительные USB-кабели
- Компьютер с macOS и запущенным средством [Apple Configurator 2.0](https://itunes.apple.com/app/apple-configurator-2/id1037126344)

## <a name="create-an-apple-configurator-profile-for-devices"></a>Создание профиля Apple Configurator для устройств

Профиль регистрации устройств задает параметры, применяемые во время регистрации. Эти параметры применяются только один раз. Выполните следующие действия, чтобы создать профиль регистрации для регистрации устройств iOS и iPadOS через Apple Configurator.

1. В [Центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) выберите **Устройства** > **iOS** > **Регистрация iOS** > **Конфигуратор Apple** > **Профили** > **Создать**.

    ![Создание профиля для Apple Configurator](./media/apple-configurator-enroll-ios/apple-config-create-profile.png)

2. В разделе **Создание профиля регистрации** введите **имя** и **описание** профиля для использования в административных целях. Пользователям эти сведения не отображаются. Поле "Имя" можно использовать для создания динамической группы в Azure Active Directory. Используйте имя профиля для определения параметра enrollmentProfileName, чтобы назначать устройства с этим профилем регистрации. Узнайте больше о динамических группах Azure Active Directory.

    ![Снимок экрана создания профиля с выбранным параметром регистрации со сходством пользователей.](./media/apple-configurator-enroll-ios/apple-configurator-profile-create.png)

3. В поле **Сходство пользователей** укажите, должны ли устройства с этим профилем регистрироваться с назначенным пользователем или без него.

    - **Регистрация со сходством пользователей** — выберите этот вариант для устройств, которые принадлежат пользователям и которые должны использовать корпоративный портал для выполнения таких действий, как установка приложений. Устройство должно быть связано с пользователем с помощью помощника по настройке, после чего оно может получить доступ к корпоративным данным и электронной почте. Поддерживается только при регистрации с использованием помощника по настройке. Для сходства пользователей требуется [конечная точка WS-Trust 1.3 в режиме "Имя пользователя/смешанный"](https://technet.microsoft.com/library/adfs2-help-endpoints). [Дополнительные сведения](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint).

    - **Регистрация без сходства пользователей** — выберите этот вариант для устройств, не связанных с одним пользователем. Используйте этот вариант для устройств, которые выполняют задачи без осуществления доступа к локальным данным пользователя. Приложения, для которых необходимо связывание с пользователем (включая приложение корпоративного портала, используемое для установки бизнес-приложений), не будут работать. Требуется для прямой регистрации.

     > [!NOTE]
     > Если выбрано значение **Подключение с сопоставлением пользователей**, в течение первых 24 часов после регистрации устройства с помощью помощника по настройке убедитесь, что устройство связано с пользователем. В противном случае может произойти сбой регистрации, а для регистрации устройства потребуется сброс параметров до заводских настроек.

4. Если выбран вариант **Регистрация со сходством пользователей**, вы можете разрешить пользователям выполнять аутентификацию с помощью корпоративного портала, а не помощника по настройке Apple.

    > [!NOTE]
    > Задайте для параметра **Проверять подлинность с помощью корпоративного портала, а не помощника по настройке Apple** значение **Да**, чтобы выполнить любое из следующих действий:
    >    - Использование многофакторной проверки подлинности.
    >    - Предложение пользователям изменить пароль при первом входе.
    >    - Предложение пользователям сбросить пароли с истекшим сроком действия во время регистрации.
    >
    > Не поддерживается при проверке подлинности с помощником по настройке Apple.


6. Выберите **Создать**, чтобы сохранить профиль.

## <a name="setup-assistant-enrollment"></a>Регистрация с использованием помощника по настройке

### <a name="add-apple-configurator-serial-numbers"></a>Добавление серийных номеров Apple Configurator

1. Создайте список значений с разделителями-запятыми (CSV-файл) с двумя столбцами без заголовка. Добавьте серийный номер в левый столбец, а сведения — в правый. Текущая максимальная длина списка составляет 5000 строк. В текстовом редакторе список CSV-файлов выглядит примерно так:

    F7TLWCLBX196, сведения об устройстве</br>
    DLXQPCWVGHMJ, сведения об устройстве

   Узнайте, [как найти серийный номер устройства iOS и iPadOS](https://support.apple.com/HT204073).
2. В [Центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) выберите **Устройства** > **iOS** > **Регистрация iOS** > **Конфигуратор Apple** > **Устройства** > **Добавить**.

5. Выберите **Профиль регистрации**, к которому применяются импортируемые серийные номера. Чтобы существующие данные о серийном номере перезаписать новыми данными, установите флажок **Перезапись сведений для существующих идентификаторов**.
6. В разделе **Импортировать устройства** перейдите к CSV-файлу с серийными номерами и выберите **Добавить**.

### <a name="reassign-a-profile-to-device-serial-numbers"></a>Переназначение профиля серийным номерам устройств

Профиль регистрации можно назначить при импорте серийных номеров iOS и iPadOS для регистрации через Apple Configurator. Профили также можно назначать на портале Azure:
- **Устройства Apple Configurator**
- **Профили AC**

#### <a name="assign-from-apple-configurator-devices"></a>Назначение из устройств Apple Configurator
1. В [Центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) выберите **Устройства** > **iOS** > **Регистрация iOS** > **Конфигуратор Apple** > **Устройства**, выберите серийные номера и затем выберите **Назначить профиль**.
2. В разделе **Назначить профиль** выберите **новый профиль**, который следует назначить, а затем щелкните **Назначить**.

#### <a name="assign-from-profiles"></a>Назначение из профилей
1. В [Центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) выберите **Устройства** > **iOS** > **Регистрация iOS** > **Конфигуратор Apple** > **Профили** и выберите профиль.
2. В профиле выберите **Назначенные устройства**, а затем щелкните **Назначить**.
3. Выполните фильтрацию для поиска серийных номеров устройств, которые необходимо назначить профилю, выберите устройства, а затем щелкните **Назначить**.

### <a name="export-the-profile"></a>Экспорт профиля
После создания профиля и назначения серийных номеров необходимо экспортировать профиль из Intune в виде URL-адреса. Затем он импортируется в Apple Configurator на компьютер Mac для развертывания на устройствах.

1. В [Центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) выберите **Устройства** > **iOS** > **Регистрация iOS** > **Конфигуратор Apple** > **Профили** и выберите профиль для экспорта.
2. В профиле выберите **Экспорт профиля**.
3. Скопируйте **URL-адрес профиля**. Позже его можно добавить в Apple Configurator для определения профиля Intune, используемого устройствами iOS и iPadOS.

   Затем этот профиль импортируется в Apple Configurator, как описано далее, для определения профиля Intune, используемого устройствами iOS и iPadOS.

### <a name="enroll-devices-with-setup-assistant"></a>Регистрация устройств с использованием помощника по настройке

1. На компьютере Mac откройте **Apple Configurator 2**. В строке меню щелкните **Apple Configurator 2** и выберите **Preferences** (Предпочтения).
    > [!WARNING]
    > Во время процесса регистрации настройки устройств сбрасываются до заводских. Рекомендуется выполнить сброс устройства и включить питание. При подключении на устройстве должен отображаться экран **приветствия**.
    > Если устройство уже зарегистрировано с помощью учетной записи Apple ID, его следует удалить из Apple iCloud перед началом процесса регистрации. Появится сообщение об ошибке "Не удалось активировать [имя_устройства]".

2. На панели **предпочтений** выберите **Серверы** и щелкните значок "+", чтобы запустить мастер сервера MDM. Нажмите кнопку **Далее**.
3. Введите **имя узла или URL-адрес** и **URL-адрес регистрации** сервера MDM в разделе "Регистрация помощника по установке" для устройств iOS и iPadOS с Microsoft Intune. В поле "URL-адрес регистрации" введите URL-адрес профиля регистрации, экспортированный из Intune. Нажмите кнопку **Далее**.  
    Предупреждением "server URL is not verified" (URL-адрес сервера не проверен) можно пренебречь. Чтобы продолжить, нажимайте кнопку **Далее** до завершения работы мастера.
4. Подключите мобильные устройства iOS и iPadOS к компьютеру Mac с помощью USB-адаптера.
5. Выберите устройства iOS и iPadOS, которыми необходимо управлять, а затем щелкните **Подготовить**. На панели **Prepare iOS/iPadOS Device** (Подготовка устройства iOS и iPadOS) выберите **Manual** (Вручную) и нажмите кнопку **Next** (Далее).
6. На панели **Enroll in MDM Server** (Регистрация на сервере MDM) выберите имя созданного вами сервера и нажмите кнопку **Далее**.
7. На панели **Supervise Devices** (Контроль за устройствами) выберите уровень контроля и нажмите кнопку **Next** (Далее).
8. На панели **Create an Organization** (Создание организации) выберите **Организация** или создайте организацию, а затем нажмите кнопку **Далее**.
9. На панели **Configure iOS/iPadOS Setup Assistant** (Настройка помощника по настройке iOS и iPadOS) выберите действия, которые будут отображаться для пользователя, и нажмите кнопку **Подготовить**. При появлении запроса пройдите проверку подлинности, чтобы обновить параметры отношения доверия.  
10. После завершения подготовки устройства iOS и iPadOS отключите кабель USB.  

### <a name="distribute-devices"></a>Распределение устройств
Теперь устройства подготовлены к корпоративной регистрации. Выключите устройства и распределите их пользователям. Когда пользователи включат свои устройства, запустится помощник по настройке.

После получения устройств пользователи должны выполнить действия в помощнике по настройке. Устройства, для которых настроено сходство пользователей, могут установить и запустить приложение корпоративного портала для скачивания приложений и управления устройствами.

## <a name="direct-enrollment"></a>Прямая регистрация
Для выполнения прямой регистрации устройств iOS и iPadOS с помощью Apple Configurator не требуется серийный номер устройства. Кроме того, в целях идентификации можно указать имя устройства, которое будет использоваться Intune во время регистрации. Приложение корпоративного портала не поддерживается для устройств с прямой регистрацией. Этот метод не очищает устройство.

Приложения, для которых необходимо взаимодействие с пользователем (включая приложение корпоративного портала, используемое для установки бизнес-приложений), нельзя установить.

### <a name="export-the-profile-as-mobileconfig-to-iosipados-devices"></a>Экспорт профиля в качестве MOBILECONFIG-файла на устройства iOS и iPadOS

1. В [Центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) выберите **Устройства** > **iOS** > **Регистрация iOS** > **Конфигуратор Apple** > **Профили**, выберите профиль для экспорта и затем выберите **Экспорт профиля**.
2. В разделе **Прямая регистрация** выберите **Скачать профиль** и сохраните файл. Файл профиля регистрации действует только две недели, после чего его нужно создать заново.
3. Переместите файл на компьютер Mac с запущенным средством [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12), чтобы отправить его напрямую на устройства iOS и iPadOS как профиль управления.
4. Подготовьте устройство с помощью Apple Configurator, сделав следующее:
    1. На компьютере Mac откройте Apple Configurator 2.0.
    2. Подключите устройство iOS и iPadOS к компьютеру Mac с помощью кабеля USB. При обнаружении устройства закройте средство просмотра фотографий, iTunes и другие приложения, открытые на устройстве.
    3. В Apple Configurator выберите подключенное устройство iOS и iPadOS и нажмите кнопку **Добавить**. В раскрывающемся списке отображаются параметры, которые могут быть добавлены к устройству. Выберите **Профили**.

        ![Снимок экрана: экспорт профиля для регистрации с использованием помощника по настройке с выделенным URL-адресом профиля](./media/apple-configurator-enroll-ios/ios-apple-configurator-add-profile.png)

    4. Используйте средство выбора файлов, чтобы выбрать MOBILECONFIG-файл, экспортированный из Intune, и нажмите кнопку **Добавить**. Профиль будет добавлен в устройство. Если устройство настроено как незащищенное, для установки нужно принять условия на устройстве.
5. Следуйте инструкциям ниже, чтобы установить профиль на устройстве iOS и iPadOS. Помощник по настройке уже должен завершить свою работу, и устройство должно быть готово к использованию. Если регистрация влечет за собой развертывания приложений, то у устройства должен быть задан Apple ID, так как для развертывания приложений необходимо выполнить вход в магазин приложений с Apple ID.
    1. Разблокируйте устройство iOS и iPadOS.
    2. В диалоговом окне **Install profile** (Установка профиля) для параметра **Management profile** (Профиль управления) выберите **Install** (Установить).
    3. Укажите секретный код устройства или Apple ID, если это необходимо.
    4. Примите **Предупреждение** и нажмите кнопку **Установить**.
    5. Примите **Удаленное предупреждение** и нажмите кнопку **Доверяю**.
    6. Когда состояние профиля в окне **Profile Installed** (Профиль установлен) изменится на установленный, нажмите кнопку **Done** (Готово).

6. На устройстве iOS и iPadOS откройте экран **Settings** (Параметры) и выберите **General** > **Device Management** > **Management Profile** (Общие > Управление устройством > Профиль управления). Убедитесь в том, что профиль установлен, проверьте ограничения политики iOS и iPadOS и установленные приложения. Для появления на устройстве ограничений политик и приложений может потребоваться до 10 минут.

7. Распределите устройства. Теперь устройство iOS и iPadOS зарегистрировано в Intune и является управляемым.




