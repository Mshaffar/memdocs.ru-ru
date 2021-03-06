---
title: Планирование управления приложениями
titleSuffix: Configuration Manager
description: Внедрите и настройте необходимые зависимости для развертывания приложений в Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03fda62774b930a1cc3603415f3b872050b9cb71
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689052"
---
# <a name="plan-for-and-configure-application-management-in-configuration-manager"></a>Планирование и настройка управления приложениями в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Используйте сведения из этой статьи, чтобы внедрить необходимые зависимости для развертывания приложений в Configuration Manager.  



## <a name="dependencies-external-to-configuration-manager"></a>Внешние зависимости Configuration Manager  


### <a name="internet-information-services-iis"></a>IIS

Службы IIS требуются для серверов, на которых выполняются следующие роли системы сайта:

- Точка управления  
- Точка распространения  

Дополнительные сведения см. в разделе [Необходимые компоненты для сайта и системы сайта](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

> [!Note]  
> Каталогу приложений также требуются службы IIS. Но учтите, что пользовательский интерфейс Silverlight не поддерживается начиная с версии Current Branch 1806. Начиная с версии 1906, обновленные клиенты автоматически используют точку управления для развертываний приложений, доступных пользователю. Но вы не можете устанавливать новые роли каталога приложений. Поддержка ролей каталога приложений прекращена в версии 1910.  
>
> Дополнительные сведения см. в следующих статьях:
>
> - [Настройка центра программного обеспечения](plan-for-software-center.md#bkmk_userex)
> - [Удаленные и устаревшие компоненты](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>Сертификаты для приложений с подписыванием кода на мобильных устройствах

Если вы подписываете код приложений для развертывания на мобильных устройствах, не используйте сертификат, созданные на основе шаблона версии 3 (**Windows Server 2008 Enterprise Edition**). На основе этого шаблона создаются сертификаты, которые не совместимы с приложениями Configuration Manager для мобильных устройств.

Если для подписания кода приложений для мобильных устройств используются службы сертификатов Active Directory, не следует использовать версию 3 шаблона сертификатов.


### <a name="audit-sign-in-events-for-user-device-affinity"></a>Аудит событий входа в систему для сопоставления пользователей и устройств  

Если вы хотите автоматически создавать сопоставления пользователей и устройств, настройте для клиентов аудит событий входа в систему.

Чтобы определить автоматические сопоставления пользователей и устройств, клиент Configuration Manager считывает события входа в систему с типом **Успешно** из журнала событий безопасности Windows. Чтобы включить эти события, используйте следующие две политики аудита:

- **Аудит событий входа в учетную запись**
- **Аудит событий входа в систему**

Для автоматического создания отношений между пользователями и устройствами убедитесь, что эти два параметра включены на клиентских компьютерах. Эти параметры можно настроить с помощью групповой политики Windows.

Дополнительные сведения о сопоставлении пользователей и устройств см. в статье [Связывание пользователей и устройств с помощью сопоставления пользователей и устройств в System Center Configuration Manager](../deploy-use/link-users-and-devices-with-user-device-affinity.md).  



## <a name="configuration-manager-dependencies"></a>Зависимости Configuration Manager


### <a name="management-point"></a>Точка управления

Клиенты связываются с точкой управления, чтобы скачать клиентскую политику и найти контент.

Начиная с версии 1906, обновленные клиенты автоматически используют точку управления для развертываний приложений, доступных пользователю.

В версии 1902 и более ранних клиенты используют точку управления для подключения к каталогу приложений. Если точка управления недоступна для клиентов, они не смогут использовать каталог приложений.

> [!Note]  
> Начиная с версии 1806 роли каталога приложений больше не нужны для отображения доступных пользователям приложений в центре программного обеспечения. Дополнительные сведения см. в разделе [Настройка центра программного обеспечения](plan-for-software-center.md#bkmk_userex).<!--1358309-->  
>
> Начиная с версии 1906, вы не можете устанавливать новые роли каталога приложений. Поддержка ролей каталога приложений прекращена в версии 1910.  
  

### <a name="distribution-point"></a>Точка распространения

Для развертывания приложений на клиентах необходимо, чтобы в иерархии существовала хотя бы одна точка распространения. Во время стандартной установки роль точки распространения по умолчанию включена на сервере сайта. Количество и расположение точек распространения зависит от определенных требований вашей среды.

Дополнительные сведения об установке точек распространения и управлении содержимым см. в разделе [Управление содержимым и инфраструктурой содержимого](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


### <a name="reporting-services-point"></a>Точка служб отчетов

Для использования отчетов в Configuration Manager при управлении приложениями сначала нужно установить и настроить точку служб отчетов.

Дополнительные сведения см. в разделе [Общие сведения об отчетах](../../core/servers/manage/introduction-to-reporting.md).  


### <a name="client-settings"></a>Параметры клиента

Многие клиентские параметры управляют тем, как приложения устанавливаются на клиенте и как пользователь взаимодействует с устройством. К этим параметрам, в частности, относятся следующие группы:

- Агент компьютера  
- Перезагрузка компьютера  
- Центр программного обеспечения  
- Развертывание программного обеспечения  
- Сопоставление пользователей и устройств  

Дополнительные сведения см. в следующих статьях:

- [О параметрах клиентов](../../core/clients/deploy/about-client-settings.md)  
- [Настройка параметров клиента](../../core/clients/deploy/configure-client-settings.md)  


### <a name="security-permissions-for-application-management"></a>Разрешения безопасности для управления приложениями.

- Роль безопасности **Автор приложений** включает разрешения на создание и изменение приложений, а также прекращение их использования.  

- Роль безопасности **Менеджер развертывания приложений** включает необходимые разрешения для развертывания приложений.  

- Роль безопасности **Администратор приложения** имеет все разрешения ролей безопасности **Автор приложения** и **Менеджер по развертыванию приложений**.  

Дополнительные сведения см. в разделе [Настройка ролевого администрирования](../../core/servers/deploy/configure/configure-role-based-administration.md).  


### <a name="app-v-46-sp1-or-later-client-to-run-virtual-applications"></a>Клиент App-V 4.6 с пакетом обновления 1 (SP1) или более поздней версии для запуска виртуальных приложений

Чтобы создать виртуальные приложения в Configuration Manager, установите на устройства App-V 4.6 с пакетом обновления 1 (SP1) или более поздней версии.

Кроме того, перед развертыванием виртуальных приложений обновите клиент App-V с исправлением, описанным в [статье службы поддержки Майкрософт №2645225](https://support.microsoft.com/help/2645225).  


### <a name="application-catalog"></a>Каталог приложений

> [!Important]  
> Поддержка ролей каталога приложений прекращена в версии 1910. Дополнительные сведения см. в разделе [Удаление каталога приложений](#bkmk_remove-appcat).  

#### <a name="application-catalog-web-service-point"></a>Точка веб-службы каталога приложений

Точка веб-службы каталога приложений — это роль системы сайта, которая предоставляет сведения о доступном ПО в соответствующей библиотеке для веб-сайта каталога приложений, к которому обращаются пользователи.

Подробные сведения о настройке этой роли системы сайта см. в разделе [Установка и настройка каталога приложений](#bkmk_appcat).  

#### <a name="application-catalog-website-point"></a>Точка веб-сайта каталога приложений

Точка веб-сайта каталога приложений — это роль системы сайта, которая обеспечивает доступ к списку доступного ПО.

Подробные сведения о настройке этой роли системы сайта см. в разделе [Установка и настройка каталога приложений](#bkmk_appcat).

#### <a name="discovered-user-accounts-for-application-catalog"></a>Обнаруженные учетные записи пользователей для каталога приложений

Чтобы пользователи могли просматривать и запрашивать приложения из каталога приложений, сначала их учетные записи должны быть обнаружены в Configuration Manager. Дополнительные сведения см. в разделе [Запуск обнаружения](../../core/servers/deploy/configure/run-discovery.md).  



## <a name="configure-software-center"></a><a name="bkmk_userex"></a> Настройка центра программного обеспечения  

Подробные сведения о настройке центра программного обеспечения и использовании в нем фирменной символики см. в статье [Plan for Software Center](plan-for-software-center.md) (План для центра программного обеспечения).


## <a name="remove-the-application-catalog"></a><a name="bkmk_remove-appcat"></a> Удаление каталога приложений

<!-- SCCMDocs-pr issue 3051 -->

Поддержка ролей каталога приложений прекращена в версии 1910. Дополнительные сведения см. в разделе [Удаленные и устаревшие компоненты](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). Ниже приведен сводный список изменений.

- Начиная с версии 1806 **пользовательский интерфейс Silverlight** для точки веб-сайта каталога приложений больше не поддерживается.<!--1358309--> Роль точки веб-службы каталога приложений больше *не является обязательной*, но по-прежнему *поддерживается*.

- Начиная с версии 1906, обновленные клиенты автоматически используют точку управления для развертываний приложений, доступных пользователю. Но вы не можете устанавливать новые роли каталога приложений.

- Поддержка ролей каталога приложений прекращена в версии 1910.  

Эти поэтапные улучшения центра программного обеспечения и точки управления упростят инфраструктуру и устранят необходимость в использовании каталога приложений для развертывания приложений, доступных для пользователей. Центр программного обеспечения может доставлять все развертывания приложений без каталога приложений. Кроме того, если включить TLS 1.2 и использовать протокол HTTP вместе с каталогом приложений, пользователи не будут видеть адресуемые и доступные им развертывания. Обновите Configuration Manager до версии 1906 или более поздней, чтобы получить преимущества от последних улучшений.

1. Обновите все клиенты до версии не ниже 1806. Рекомендуется использовать версию 1906.  

1. Устанавливайте фирменную символику в центре программного обеспечения, а не в свойствах роли веб-сайта каталога приложения. Дополнительные сведения см. в разделе о [параметрах клиентов в центре программного обеспечения](../../core/clients/deploy/about-client-settings.md#software-center).  

1. Просмотрите все пользовательские параметры клиента и параметры, заданные по умолчанию. В группе **Агент компьютера** параметру **Точка веб-сайта каталога приложений по умолчанию** нужно задать значение `(none)`.  

    В версии 1902 и более ранних клиент переключается на использование точки управления, если в иерархии отсутствуют роли каталога приложения. В противном случае клиенты будут использовать один из экземпляров каталога приложения в иерархии. Это поведение характерно для отдельных первичных сайтов.  

1. Удалите роли системы сайта для **веб-сайта каталога приложений** и **веб-службы каталога приложений** на всех первичных сайтах.

После удаления ролей каталога приложений центр программного обеспечения будет использовать точки управления для доступных развертываний, адресуемых пользователям. В версии 1902 и более ранних применение этого изменения может занять до 65 минут. Чтобы проверить это поведение на определенном клиенте, просмотрите `SCClient_<username>.log` и найдите запись следующего типа:

`Using endpoint Url: https://mp.contoso.com/CMUserService_WindowsAuth, Windows authentication`


## <a name="install-and-configure-the-application-catalog"></a><a name="bkmk_appcat"></a> Установка и настройка каталога приложений  

> [!Important]  
> Поддержка ролей каталога приложений прекращена в версии 1910. Дополнительные сведения см. в разделе [Удаление каталога приложений](#bkmk_remove-appcat).  

### <a name="step-1-web-server-certificate-for-https"></a>Шаг 1. Сертификат веб-сервера для протокола HTTPS

Если вы используете подключения по HTTPS, разверните сертификат веб-сервера на серверах систем сайта, на которых будет работать точка веб-сайта каталога приложений и точка веб-службы каталога приложений.

Чтобы клиенты использовали каталог приложений из Интернета, разверните сертификат веб-сервера как минимум на одной точке управления. Настройте возможность подключения к клиенту через Интернет.

Дополнительные сведения о требованиях к сертификатам см. в статье [Требования к PKI-сертификатам для System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md).  


### <a name="step-2-client-authentication-certificate-for-https"></a>Шаг 2. Сертификат проверки подлинности клиента для протокола HTTPS

Если для подключения к точкам управления используется PKI-сертификат клиента, разверните сертификат проверки подлинности клиента на клиентских компьютерах. Хотя для подключения клиентов к каталогу приложений PKI-сертификат клиента не используется, для работы с каталогом приложений клиенты должны подключаться к точке управления.

Разверните сертификат проверки подлинности клиента на клиентских компьютерах в следующих случаях:

- Все точки управления в интрасети принимают подключения клиентов только по протоколу HTTPS.
- Клиенты будут подключаться к каталогу приложений из Интернета.

Дополнительные сведения о требованиях к сертификатам см. в статье [Требования к PKI-сертификатам для System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md).  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>Шаг 3. Установка и настройка ролей каталога приложений

Установите роль точки веб-службы каталога приложений и роль веб-сайта каталога приложений на одном сайте. Устанавливать их на одном и том же сервере или в одном лесу Active Directory не обязательно. При этом точка веб-службы каталога приложений должна находиться в одном лесу с базой данных сайта.

Дополнительные сведения о размещении ролей сервера см. в статье [Планирование серверов системы сайта и ролей системы сайта в Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

> [!NOTE]  
> Установите каталог приложений на основном сайте. Установить его на дополнительный сайт или сайт центра администрирования невозможно.  

Установите каталог приложений на новый сервер системы сайта или на существующий сервер сайта. Дополнительные сведения об общей процедуре см. в статье [Установка ролей системы сайта для System Center Configuration Manager](../../core/servers/deploy/configure/install-site-system-roles.md). В мастере добавления ролей системы сайта или создания сервера системы сайта выберите следующие роли:  

- **Точка веб-службы каталога приложений**;  
- **Точка веб-сайта каталога приложений**.  

> [!TIP]  
> Чтобы каталог приложений был доступен для клиентских компьютеров через Интернет, укажите его полное доменное имя в Интернете.  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>Проверьте установку этих ролей системы сайта  

- Сообщения о состоянии. Используйте компоненты **SMS_PORTALWEB_CONTROL_MANAGER** и **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Например, идентификатор состояния **1015** для **SMS_PORTALWEB_CONTROL_MANAGER** означает, что диспетчер компонентов сайта успешно установил точку веб-сайта каталога приложений.  

- Файлы журнала. Файлы журналов – **SMSAWEBSVCSetup.log** и **SMSPORTALWEBSetup.log**.  

    Дополнительные сведения см. в файлах журнала **awebsvcMSI.log** и **portlwebMSI.log**.  


### <a name="step-4-configure-client-settings"></a>Шаг 4. Настройка параметров клиента

Установите параметры клиента, используемые по умолчанию, если хотите, чтобы у всех пользователей были одинаковые настройки. Вместо этого можно настроить пользовательские параметры клиента для конкретных коллекций.

Дополнительные сведения см. в следующих статьях:

- [О параметрах клиентов](../../core/clients/deploy/about-client-settings.md)  
    - Агент компьютера  
    - Перезагрузка компьютера  
    - Центр программного обеспечения  
    - Развертывание программного обеспечения  
    - Сопоставление пользователей и устройств  
- [Настройка параметров клиента](../../core/clients/deploy/configure-client-settings.md)  

Клиент Configuration Manager настроит устройства с помощью этих параметров при следующем скачивании клиентской политики. Сведения об активации получения политики для отдельного клиента см. в статье [Управление клиентами в System Center Configuration Manager](../../core/clients/manage/manage-clients.md).


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Шаг 5. Проверка работоспособности каталога приложений.

С помощью следующих процедур можно проверить работоспособность каталога приложений.

> [!NOTE]  
> Для работы с каталогом приложений требуется Microsoft Silverlight. Если вы используете каталог приложений непосредственно в браузере, сначала убедитесь, что на вашем компьютере установлена платформа Microsoft Silverlight.  

> [!TIP]  
> Отсутствующие необходимые компоненты являются наиболее частой причиной неправильной работы каталога приложений после установки. Проверьте соблюдение предварительных требований для ролей системы сайта каталога приложений. Дополнительные сведения см. в разделе [Необходимые компоненты для сайта и системы сайта](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

Введите адрес веб-сайта каталога приложений в адресной строке браузера. Убедитесь, что отображается веб-страница с тремя вкладками: **Каталог приложений**, **Мои запросы приложений** и **Мои устройства**.  

Используйте подходящий адрес каталога приложений из следующего списка, где `<server>` — это имя компьютера или полное доменное имя в интрасети либо в Интернете:  

- Подключения клиентов по HTTPS и параметры роли системы сайта, используемые по умолчанию: `https://<server>/CMApplicationCatalog`.  

- Подключения клиентов по HTTP и параметры роли системы сайта, используемые по умолчанию: `http://<server>/CMApplicationCatalog`.  

- Подключения клиентов по HTTPS и настраиваемые параметры роли системы сайта: `https://<server>:<port>/<web application name>`.  

- Подключения клиентов по HTTP и настраиваемые параметры роли системы сайта: `http://<server>:<port>/<web application name>`.  

> [!NOTE]  
> Если вы вошли в систему с учетной записью администратора домена, клиент Configuration Manager не будет показывать уведомления, например о наличии нового программного обеспечения.  
