---
title: Безопасность и конфиденциальность приложений
titleSuffix: Configuration Manager
description: Советы и рекомендации по безопасности и конфиденциальности при управлении приложениями в Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f7085b7ee6f0f723c9bcf9d10cb85b03f990a44
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689072"
---
# <a name="security-and-privacy-for-application-management-in-configuration-manager"></a>Безопасность и конфиденциальность управления приложениями в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

## <a name="security-guidance-for-application-management"></a>Советы по безопасности при управлении приложениями  

### <a name="use-the-software-center-without-the-application-catalog"></a>Использование центра программного обеспечения без каталога приложений

<!--1358309-->

Пользовательский интерфейс Silverlight каталога приложений не поддерживается в текущей ветви версии 1806. Эта конфигурация позволяет уменьшить объем серверной инфраструктуры, необходимой для предоставления приложений пользователям,

Начиная с версии 1906, обновленные клиенты автоматически используют точку управления для развертываний приложений, доступных пользователю. Но вы не можете устанавливать новые роли каталога приложений. Поддержка ролей каталога приложений прекращена в версии 1910. а также сократить возможные направления атак.

Используйте Azure Active Directory и шлюз облачного управления, чтобы обеспечить последовательное и безопасное взаимодействие с приложениями для интернет-клиентов.

Дополнительные сведения см. в разделе [Настройка центра программного обеспечения](plan-for-software-center.md#bkmk_userex).

### <a name="use-https-with-the-application-catalog"></a>Использование протокола HTTPS с каталогом приложений

> [!Important]  
> Поддержка ролей каталога приложений прекращена в версии 1910. Дополнительные сведения см. в разделе [Удаление каталога приложений](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Настройте точку веб-сайта каталога приложений и точку веб-службы каталога приложений для приема подключений HTTPS. В этой конфигурации сервер проходит проверку подлинности для пользователей. Переданные данные защищаются от несанкционированного доступа и просмотра.

Чтобы избежать атак, основанных на использовании социотехники, научите пользователей подключаться только к надежным веб-сайтам. Расскажите пользователям об опасностях, связанных с вредоносными веб-сайтами.

Если вы не используете протокол HTTPS, не используйте параметры настройки фирменного стиля, так как эти параметры используют название организации как доказательство подлинности в каталоге приложений.  


### <a name="use-role-separation"></a>Используйте разделение ролей

> [!Important]  
> Поддержка ролей каталога приложений прекращена в версии 1910. Дополнительные сведения см. в разделе [Удаление каталога приложений](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Установите точку веб-сайта каталога приложений и точку веб-службы каталога приложений на разных серверах. Если точка веб-сайта скомпрометирована, она отделяется от точки веб-службы. Так вы защитите клиенты и инфраструктуру Configuration Manager. Это особенно важно, если точка веб-сайта принимает подключения клиентов из Интернета, что делает сервер более уязвимым для атак.  

### <a name="close-browser-windows"></a>Закрывайте окна браузера

> [!Important]  
> Поддержка ролей каталога приложений прекращена в версии 1910. Дополнительные сведения см. в разделе [Удаление каталога приложений](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Расскажите пользователям о необходимости закрывать окно браузера по завершении работы с каталогом приложений. Если пользователи откроют внешний веб-сайт в том же окне браузера, которое использовалось для работы с каталогом приложений, браузер продолжит использовать параметры безопасности, предназначенные для надежных сайтов в интрасети.  

### <a name="centrally-specify-user-device-affinity"></a>Централизованно укажите сопоставление пользователей и устройств

Укажите сопоставление пользователей и устройств вручную, а не позволяйте пользователям идентифицировать свое основное устройство. Не включайте конфигурацию на основе использования.

Не считайте информацию, полученную от пользователей или от устройства, заслуживающей доверия. Если программное обеспечение развертывается путем сопоставления пользователей и устройств, которое указано не доверенным пользователем с правами администратора, то программное обеспечение может быть установлено на те компьютеры и для тех пользователей, которые не имеют прав для получения этого программного обеспечения.  

### <a name="dont-run-deployments-from-distribution-points"></a>Не выполняйте развертывание из точек распространения

Для развертывания всегда выбирайте загрузку содержимого из точек распространения, а не запуск из точек распространения. При настройке развертываний для скачивания содержимого из точки распространения с дальнейшим запуском в локальной системе клиент Configuration Manager проверяет хэш пакета после скачивания содержимого. Клиент отклоняет пакет, если его хэш не совпадает с хэшем в политике.

Если же настроить развертывание напрямую из точки распространения, клиент Configuration Manager не будет проверять хэш пакета. Это означает, что клиент Configuration Manager может устанавливать незаконно измененное программное обеспечение.

Если необходимо запускать развертывание напрямую из точек распространения, используйте минимальные разрешения NTFS для пакетов в точках распространения. Вдобавок можно использовать безопасность интернет-протокола IP (IPsec) для защиты канала между клиентом и точками распространения, а также между точками распространения и сервером сайта.

### <a name="dont-let-users-interact-with-elevated-processes"></a><a name="bkmk_interact"></a> Не разрешайте пользователям взаимодействовать с процессами, для которых нужны повышенные права
  
Если вы включили параметр **Запустить с правами администратора** или **Установить для системы**, не разрешайте пользователям взаимодействовать с такими приложениями. При настройке приложения можно установить параметр **Разрешить пользователям видеть ход установки программы и взаимодействовать с ним**. Этот параметр позволяет пользователям отвечать на все необходимые запросы в пользовательском интерфейсе. Если для программы также настроен параметр **Запустить с правами администратора** или, начиная с версии 1802, параметр **Установить для системы**, злоумышленник на компьютере, на котором запущена эта программа, может использовать пользовательский интерфейс для повышения прав на клиентском компьютере.

Используйте программы установки на базе установщика Windows с повышением прав отдельно для каждого пользователя для развертывания программного обеспечения, требующего учетных данных администратора. Запуск установки должен осуществляться в контексте пользователя, не имеющего прав администратора. Повышение прав установщика Windows отдельно для каждого пользователя представляет собой наиболее безопасный способ развертывания приложений, для которых действует такое требование.

### <a name="restrict-whether-users-can-install-software-interactively"></a>Ограничьте интерактивную установку программного обеспечения

В группе **Агент компьютера** настройте параметр клиента **Разрешения на установку**. Этот параметр позволяет ограничивать типы пользователей, которые могут устанавливать программное обеспечение в центре программного обеспечения.

Например, можно установить для параметра клиента **Разрешения на установку** значение **Только администраторы**. Примените этот параметр к коллекции серверов. Такая конфигурация не позволит пользователям без прав администратора устанавливать программное обеспечение на серверах.  

### <a name="for-mobile-devices-deploy-only-applications-that-are-signed"></a>Для мобильных устройств развертывайте только подписанные приложения

Развертывайте приложения для мобильных устройств, только если код этих приложений подписан доверенным центром сертификации мобильного устройства.

Пример.

- приложение поставщика, подписанное широко известным центром сертификации, таким как VeriSign;  

- Внутреннее приложение, которое вы подписываете независимо от Configuration Manager с помощью внутреннего ЦС.  

- Внутреннее приложение, которое вы подписываете с помощью Configuration Manager при создании типа приложения с использованием сертификата подписи.

### <a name="secure-the-location-of-the-mobile-device-application-signing-certificate"></a>Защитите расположение сертификата для подписи приложений для мобильных устройств

Если вы подписываете приложения для мобильных устройств с помощью **мастера создания приложений** в Configuration Manager, следует защитить расположение файла сертификата подписи и канал передачи данных. Для защиты от атак, связанных с повышением прав, и атак типа "злоумышленник в середине" следует хранить файл сертификата в безопасной папке.

Используйте протокол IPsec между следующими компьютерами:

- компьютер, где запущена консоль Configuration Manager;
- компьютер, на котором хранится файл подписи сертификата;
- компьютер, на котором хранятся исходные файлы приложения.

Кроме того, можно подписать приложение независимо от Configuration Manager перед запуском **мастера создания приложений**.

### <a name="implement-access-controls"></a>Реализуйте элементы управления доступом

Для защиты компьютеров-образцов реализуйте средства управления доступом. Убедитесь, что при настройке способа обнаружения в типе развертывания путем указания компьютера-образца этот компьютер не был скомпрометирован.

### <a name="restrict-and-monitor-administrative-users"></a>Ограничьте и отслеживайте действия пользователей с правами администратора

Ограничьте и отслеживайте действия пользователей с правами администратора, которым предоставлены следующие роли системы безопасности, связанные с управлением приложениями:

- **Администратор приложений**
- **Автор приложений**
- **Менеджер развертывания приложений**

Даже если настроено ролевое администрирование, пользователи с правами администратора, создающие и развертывающие приложения, могут иметь больше разрешений, чем вы себе представляете. Например, пользователи с правами администратора, которые создают или изменяют приложение, могут выбрать зависимые приложения, не входящие в их область безопасности.

### <a name="configure-app-v-apps-in-virtual-environments-with-the-same-trust-level"></a>Настройте одинаковый уровень доверия для приложений App-V в виртуальных средах

При настройке виртуальных сред Microsoft Application Virtualization (App-V) выбирайте приложения с одинаковым уровнем доверия. Приложения в виртуальной среде App-V могут совместно использовать ресурсы, такие как буфер обмена, поэтому следует настроить виртуальную среду так, чтобы у выбранных приложений был одинаковый уровень доверия.

Дополнительные сведения см. в разделе [Создание виртуальных сред App-V](../deploy-use/create-app-v-virtual-environments.md).

### <a name="make-sure-macos-apps-are-from-a-trustworthy-source"></a>Убедитесь в надежности источника приложений для macOS

При развертывании приложений на устройствах macOS удостоверьтесь, что исходные файлы берутся из надежного источника. Средство CMAppUtil не проверяет подпись исходного пакета. Убедитесь, что пакет взят из надежного источника. Средство CMAppUtil не может определить, были ли файлы изменены злоумышленниками.

### <a name="secure-the-cmmac-file-for-macos-apps"></a>Защитите файл cmmac в приложениях macOS

При развертывании приложений на компьютерах macOS защитите расположение файла **.cmmac**. Этот файл создается с помощью CMAppUtil, а затем импортируется в Configuration Manager. Файл не подписывается и не проверяется.

При импорте этого файла в Configuration Manager защитите коммуникационный канал. Храните этот файл в защищенной папке, чтобы предотвратить незаконное изменение. Используйте протокол IPsec между следующими компьютерами:

- компьютер, где запущена консоль Configuration Manager;  
- компьютер, на котором хранится файл **CMMAC**.  

### <a name="use-https-for-web-applications"></a>Используйте протокол HTTPS для веб-приложений

При настройке типа развертывания веб-приложения используйте протокол HTTPS для обеспечения безопасного подключения. Если веб-приложение развертывается с использованием ссылки HTTP, а не HTTPS, устройство может быть перенаправлено на вредоносный сервер. Данные, передаваемые между устройством и сервером, могут быть изменены злоумышленником.


## <a name="security-issues-for-application-management"></a>Проблемы безопасности при управлении приложениями  

- Пользователи с ограниченными правами могут копировать файлы из кэша клиента на клиентских компьютерах.  

     Пользователи могут читать кэш клиента, но не могут записывать данные в него. При наличии разрешений на чтение пользователь может скопировать установочные файлы приложения с одного компьютера на другой.  

- Пользователи с ограниченными правами могут изменять файлы, в которые записывается журнал развертывания ПО на клиентском компьютере.  

     Так как данные журнала приложения не защищены, пользователь может изменить файлы, которые сообщают о том, установлено ли приложение.  

- Пакеты App-V не подписываются.  

     Пакеты App-V в Configuration Manager не поддерживают подписывание. Цифровая подпись позволяет подтвердить, что содержимое было получено из надежного источника и не было изменено во время передачи. Устранить эту проблему безопасности невозможно. Следуйте рекомендациям по безопасности и скачивайте содержимое из доверенных источников и безопасных мест.  

- Опубликованные приложения App-V могут быть установлены на компьютер всеми пользователями.  

     Если приложение App-V опубликовано на компьютере, все пользователи, входящие на этот компьютер, могут установить опубликованное приложение. Вы не можете ограничить круг пользователей, которые смогут устанавливать приложение после его публикации.  


## <a name="certificates-for-microsoft-silverlight-5-and-elevated-trust-mode-required-for-the-application-catalog"></a><a name="BKMK_CertificatesSilverlight5"></a> Сертификаты для Microsoft Silverlight 5 и режим повышенного доверия для каталога приложений  

> [!Important]  
> Поддержка ролей каталога приложений прекращена в версии 1910. Дополнительные сведения см. в разделе [Удаление каталога приложений](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Для клиентов Configuration Manager версии 1710 и более ранних требуется компонент Microsoft Silverlight 5, который должен быть запущен в режиме повышенного доверия, чтобы пользователи могли устанавливать программы из каталога приложений. По умолчанию приложения Silverlight выполняются в режиме частичного доверия. В этом режиме приложения не имеют доступа к данным пользователя. Если Microsoft Silverlight 5 не установлен, Configuration Manager автоматически устанавливает его на клиентах. По умолчанию для клиентского параметра агента **Разрешить приложениям Silverlight запускаться в режиме повышенного доверия** устанавливается значение **Да**. Это дает возможность подписанным и доверенным приложениям Silverlight запрашивать режим повышенного доверия.  

При установке роли системы сайта точки веб-сайта каталога приложений клиент также устанавливает сертификат подписи Майкрософт в хранилище сертификатов "Доверенные издатели" на каждом клиентском компьютере Configuration Manager. Приложения Silverlight, подписанные этим сертификатом, запускаются в режиме повышенного доверия, который необходим для установки программ из каталога приложений на компьютерах. Configuration Manager автоматически управляет этим сертификатом подписи. Чтобы обеспечить непрерывность обслуживания, не следует вручную удалять и перемещать этот сертификат подписи Майкрософт.  

> [!WARNING]  
> Если параметр **Разрешить приложениям Silverlight запускаться в режиме повышенного доверия** установлен, это позволяет всем приложениям Silverlight, подписанным сертификатами из хранилища сертификатов "Доверенные издатели" в хранилище компьютера или хранилище пользователя, запускаться в режиме повышенного доверия. Этот параметр клиента не позволяет включить режим повышенного доверия только для каталога приложений Configuration Manager или для хранилища сертификатов "Доверенные издатели" на компьютере. Если вредоносная программа добавит посторонний сертификат в хранилище "Доверенные издатели", то эта вредоносная программа с собственным приложением Silverlight также сможет работать в режиме повышенного доверия.  

Если установить для параметра **Разрешить приложениям Silverlight запускаться в режиме повышенного доверия** значение **Нет**, то клиенты не удалят сертификат подписи Майкрософт.  

Дополнительные сведения о доверенных приложениях в Silverlight см. в разделе [Доверенные приложения](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/ee721083\(v=vs.95\)).  


## <a name="privacy-information-for-application-management"></a>Сведения о конфиденциальности для управления приложениями  

Управление приложениями позволяет запустить любое приложение, программу или скрипт на любом клиенте в иерархии. Configuration Manager не контролирует типы запускаемых приложений, программ и скриптов и передаваемые ими данные. В процессе развертывания приложений Configuration Manager может передавать между клиентами и серверами данные, идентифицирующие устройство и учетные записи для входа.  

Configuration Manager сохраняет сведения о состоянии процесса развертывания программ. Если обмен данными с клиентом осуществляется не по протоколу HTTPS, то сведения о состоянии развертывания программ не шифруются при передаче. Сведения о состоянии не хранятся в зашифрованном виде в базе данных.  

Использование установки программного обеспечения Configuration Manager для удаленной, интерактивной или автоматической установки программного обеспечения на клиентских компьютерах может подпадать под условия лицензионных соглашений этого программного обеспечения, отдельных от условий лицензионного соглашения Configuration Manager. Всегда читайте и принимайте условия лицензионных соглашений программного обеспечения перед развертыванием программного обеспечения с помощью Configuration Manager.  

Configuration Manager собирает собственные данные о диагностике и использовании приложений, которые корпорация Майкрософт использует для совершенствования будущих выпусков. Дополнительные сведения см. в статье [Данные о диагностике и использовании](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).

Развертывание программ не происходит по умолчанию, для него требуется выполнить некоторые действия по настройке.  

Следующие функции помогают обеспечить эффективное развертывание программного обеспечения.

- **Сопоставление пользователей и устройств** подразумевает сопоставление пользователя с устройствами. Администратор Configuration Manager развертывает программное обеспечение для пользователя. Клиент автоматически устанавливает программное обеспечение на один или несколько компьютеров, наиболее часто используемых данным пользователем.  

- **Центр программного обеспечения** устанавливается автоматически при установке клиента Configuration Manager. Пользователи изменяют параметры, ищут и устанавливают программное обеспечение из центра программного обеспечения.  

- **Каталог приложений** — это веб-сайт, который позволяет пользователям запрашивать программное обеспечение для установки.  

    > [!Important]  
    > Поддержка ролей каталога приложений прекращена в версии 1910. Дополнительные сведения см. в разделе [Удаление каталога приложений](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

### <a name="user-device-affinity-privacy-information"></a><a name="bkmk_privacy-uda"></a> Сведения о конфиденциальности сопоставления пользователей и устройств

- Configuration Manager может передавать информацию между клиентами и системами сайта точек управления. Эта информация может идентифицировать компьютер и учетную запись входа, а также сводные данные использования учетных записей входа.  

- Информация, передаваемая между клиентом и сервером, не шифруется, если для точки управления не включено обязательное использование протокола HTTPS для подключения клиентов.  

- Сведения об использовании компьютера и учетной записи входа, применяемые для сопоставления пользователей и устройств, хранятся на клиентских компьютерах, отправляются в точки управления, а затем сохраняются в базе данных Configuration Manager. По умолчанию устаревшая информация удаляется из базы данных через 90 дней. Параметры удаления можно настроить с помощью задачи обслуживания сайта **Удаление устаревших данных сопоставления пользователей и устройств** .  

- Configuration Manager сохраняет сведения о сопоставлении пользователей и устройств. Сведения о состоянии не шифруются при передаче, если на клиентах не настроено подключение к точкам управления с помощью протокола HTTPS. Сведения о состоянии не хранятся в зашифрованном виде в базе данных.  

- Сведения об использовании компьютера и учетной записи входа, используемые для сопоставления пользователей и устройств, всегда включены. Обычные пользователи и пользователи с правами администратора могут предоставлять данные о сопоставлении пользователей и устройств.  

### <a name="software-center-privacy-information"></a><a name="bkmk_privacy-userex"></a> Сведения о конфиденциальности центра программного обеспечения

- Центр программного обеспечения позволяет администратору Configuration Manager опубликовать любое приложение, программу или скрипт для запуска пользователями. Configuration Manager не контролирует типы программ и скриптов, опубликованных в каталоге, и типы передаваемых ими данных.  

- Configuration Manager может передавать информацию между клиентами и точками управления. Эта информация может идентифицировать компьютер и учетные записи входа. Информация, передаваемая между клиентом и сервером, не шифруется, если для точки управления не включено обязательное использование протокола HTTPS для подключения клиентов.  

- Информация о запросах одобрения приложений сохраняется в базе данных Configuration Manager. Отмененные и отклоненные запросы по умолчанию удаляются через 30 дней вместе с соответствующими записями журнала. Параметры удаления можно настроить с помощью задачи обслуживания сайта **Удаление устаревших данных запросов приложений** . Утвержденные и ожидающие утверждения запросы никогда не удаляются.  

- Центр программного обеспечения устанавливается автоматически при установке клиента Configuration Manager на устройство.  

### <a name="application-catalog-privacy-information"></a>Сведения о конфиденциальности каталога приложений

> [!Important]  
> Поддержка ролей каталога приложений прекращена в версии 1910. Дополнительные сведения см. в разделе [Удаление каталога приложений](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

- Каталог приложений не устанавливается по умолчанию. Установка требует выполнения нескольких действий настройки.  

- Каталог приложений позволяет администратору Configuration Manager опубликовать любое приложение, программу или скрипт для запуска пользователями. Configuration Manager не контролирует типы программ и скриптов, опубликованных в каталоге, и типы передаваемых ими данных.  

- Configuration Manager может передавать информацию между клиентами и системами сайта с ролью каталога приложений. Эта информация может идентифицировать компьютер и учетные записи входа. Информация, передаваемая между клиентом и сервером, не шифруется, если для ролей систем сайта не включено обязательное использование протокола HTTPS для подключения клиентов.  
