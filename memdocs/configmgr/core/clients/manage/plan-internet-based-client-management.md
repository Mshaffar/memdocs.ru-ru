---
title: Управление клиентами через Интернет
titleSuffix: Configuration Manager
description: Создание плана управления интернет-клиентами в Configuration Manager.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f7054c75643c6ffa37decba74f9fe85831728985
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587214"
---
# <a name="plan-for-internet-based-client-management-in-configuration-manager"></a>Планирование управления клиентами через Интернет в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Управление клиентами через Интернет (IBCM) используется для управления клиентами Configuration Manager, когда они не подключены к внутренней сети. IBCM дает ряд преимуществ:

- полный контроль над серверами и ролями, предоставляющими службу;
- отсутствие зависимости от облачной службы;
- отсутствие потребности в виртуальной частной сети (VPN);
- возможность свести все расходы к затратам на локальную службу.

Из-за более высоких требований к безопасности управления клиентскими компьютерами в общедоступной сети IBCM требует использования PKI-сертификатов. Такая конфигурация гарантирует, что подключения проходят проверку подлинности в независимом центре. Когда клиенты IBCM и серверы сайта отправляют данные, они шифруются и защищаются.  

## <a name="client-communications"></a>Взаимодействие с клиентом

Подключения от клиентов, находящихся в недоверенных расположениях, поддерживают следующие роли системы сайта на первичных сайтах:

> [!NOTE]
> Хотя использование IBCM в основном ориентировано на сценарий подключения через Интернет, подход аналогичен тому, который применяется к клиентам в недоверенном лесу Active Directory. Вторичные сайты не поддерживают подключения клиентов из недоверенных расположений.

- Точка регистрации сертификатов для модуля политики Configuration Manager (NDES)

- Точка распространения

- Облачная точка распространения

- Прокси-точка регистрации.

- Резервная точка состояния

- Точка управления

- Точка обновления программного обеспечения

> [!NOTE]
> Поддержка ролей каталога приложений прекращена в версии 1910. Дополнительные сведения см. в разделе [Удаление каталога приложений](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat). Для Configuration Manager 1906 и более ранних (по-прежнему поддерживаемых) версий точка веб-сайта каталога приложений может принимать подключения от клиентов через Интернет.

### <a name="about-internet-facing-site-systems"></a>Сведения о системах сайта с выходом в Интернет

Доверие между лесом клиента и лесом сервера системы сайта не требуется. Но в случае, если лес, который содержит систему сайта с выходом в Интернет, доверяет лесу, который содержит учетные записи пользователей, эта конфигурация поддерживает пользовательские политики для устройств в Интернете при включении параметра **Включить запросы политик пользователей от интернет-клиентов** **политики клиента**.

Например, следующие конфигурации демонстрируют ситуации, когда IBCM поддерживает политики пользователей для устройств в Интернете.

- Интернет-точка управления находится в сети периметра. У этой сети также есть доступный только для чтения контроллер домена для проверки подлинности пользователя. Брандмауэр между периметром и внутренними сетями позволяет передавать пакеты Active Directory.

- Учетная запись пользователя находится в лесу в интрасети. Интернет-точка управления находится в лесу внутри периметра. Лес периметра доверяет внутреннему лесу. Брандмауэр между периметром и внутренними сетями позволяет выполнять проверку подлинности пакетов.

- Учетная запись пользователя и интернет-точка управления находятся в лесу в интрасети. Вы публикуете точку управления в Интернете с помощью веб-прокси в Интернете.

### <a name="use-a-web-proxy-server"></a>Использование веб-прокси

С помощью веб-прокси системы сайта в Интернете можно разместить в интрасети при их публикации в Интернете. Эти системы сайта настраиваются только для подключений клиента из Интернета или для подключений клиента из Интернета и интрасети. Используемый веб-прокси можно настроить для моста SSL-SSL или туннелирования SSL.

#### <a name="ssl-bridging-to-ssl"></a>Мост SSL-SSL

Мост SSL-SSL считается рекомендуемой и более безопасной конфигурацией, так как она использует завершение запросов SSL с проверкой подлинности. Он выполняет проверку подлинности клиентских компьютеров. Мобильные устройства, зарегистрированные в Configuration Manager, не поддерживают мост SSL.

При завершении запросов SSL на прокси-сервере он проверяет пакеты из Интернета перед их перенаправлением во внутреннюю сеть. Прокси-сервер проверяет подлинность подключения от клиента, закрывает его, а затем открывает новое проверенное подключение к системам сайта в Интернете. Когда клиенты Configuration Manager используют прокси-сервер, их идентификатор (GUID) безопасно хранится в полезных данных пакета. Поэтому точка управления не принимает прокси-сервер за клиент. В Configuration Manager не поддерживаются мосты HTTP-HTTPS или HTTPS-HTTP.

> [!NOTE]
> Configuration Manager не поддерживает сторонние конфигурации моста SSL, например Citrix Netscaler или F5 BIG-IP. Обратитесь к поставщику устройства, чтобы настроить его для использования с Configuration Manager.

#### <a name="tunneling"></a>Туннелирование

Если веб-прокси не может обеспечить выполнение требований к мостовому соединению SSL, можно воспользоваться тем, что Configuration Manager поддерживает также туннелирование SSL. Его можно использовать для поддержки мобильных устройств, зарегистрированных в Configuration Manager. Это менее безопасный вариант, поскольку прокси-сервер перенаправляет пакеты SSL из Интернета в системы сайта без завершения запросов SSL. Прокси-сервер не проверяет пакеты на наличие вредоносного содержимого. При использовании туннелирования SSL сертификаты для прокси-сервера в Интернете не требуются.

## <a name="plan-for-internet-based-clients"></a>Планирование интернет-клиентов

Решите, следует ли настраивать интернет-клиенты для управления как по интрасети, так и через Интернет или же ими следует управлять только через Интернет. Этот параметр управления можно настроить только во время установки клиента. Чтобы изменить его позже, переустановите клиент.

> [!NOTE]
> Если для точки управления настроена поддержка интернет-клиентов, подключающиеся к ней клиенты становятся поддерживающими Интернет при следующем обновлении их списков доступных точек управления.
>
> Конфигурацию управления интернет-клиентами необязательно ограничивать лишь зоной Интернета. Управлять ими можно также из интрасети.

Клиенты, настроенные для управление только через Интернет, обмениваются данными только с системами сайта, настроенными для подключения клиентов из Интернета. Такая конфигурация подходит для следующих сценариев:

- для компьютеров, которые никогда не будут подключаться к интрасети, например компьютеров в удаленных точках продаж;
- для обеспечения взаимодействия клиента только по протоколу HTTPS, например для поддержки брандмауэра и ограниченных политик безопасности;
- при установке интернет-систем сайтов в сети периметра, если этими серверами необходимо управлять как клиентами Configuration Manager.

> [!NOTE]
> В случае необходимости управлять клиентами рабочей группы через Интернет при их установке следует настроить для них управление только через Интернет.
>
> При настройке на мобильном устройстве использования Интернет-точки управления она автоматически настраивается как предназначенная для управления только через Интернет.

Другие клиенты можно настроить для управления как через Интернет, так и по интрасети. При обнаружении изменения сети они автоматически переключаются между IBCM и управлением клиентами по интрасети. Если такие клиенты могут обнаружить точку управления, поддерживающую подключения клиентов из интрасети, и подключиться к ней, управление ими осуществляется как для клиентов в интрасети. Для клиентов интрасети доступна вся функциональность Configuration Manager. Если клиентам не удается найти точку управления, поддерживающую подключения клиентов в интрасети, или подключиться к ней, они пытаются подключиться к Интернет-точке управления. Если это удается сделать, управление такими клиентами осуществляется системами сайта в Интернете на назначенном им сайте.

Преимущество автоматического переключения заключается в том, что клиенты могут использовать все функции при подключении к интрасети и получить необходимое управление при работе через Интернет. Процесс скачивания содержимого, начатый через Интернет, может быть автоматически возобновлен в интрасети и наоборот.

## <a name="prerequisites"></a>Предварительные условия

IBCM в Configuration Manager имеет следующие зависимости.

- Клиентам необходимо подключение к Интернету. Configuration Manager использует имеющееся на устройстве подключение к Интернету. Мобильные устройства должны быть подключены к Интернету напрямую. Все клиентские компьютеры, в свою очередь, могут подключаться как напрямую, так и через веб-прокси.

- Системам сайта, поддерживающим IBCM, требуется подключение к Интернету. При этом они должны находиться в домене Active Directory. Интернет-системы сайта не требуют наличия отношений доверия с лесом Active Directory сервера сайта. Однако если интернет-точка управления может проверить подлинность пользователя с помощью проверки подлинности Windows, она поддерживает политики пользователей. В случае сбоя проверки подлинности Windows она поддерживает только политики устройств.

    > [!NOTE]
    > Для поддержки политик пользователей необходимо также включить следующие параметры клиента в группе **Политика клиента**.
    >
    > - **Включить опрос политики пользователя на клиентах**
    > - **Включить запросы политик пользователей с интернет-клиентов**  

- Требуется инфраструктура открытых ключей (PKI) для развертывания необходимых сертификатов и управления ими для интернет-клиентов и серверов систем сайта. Дополнительные сведения см. в разделе [Требования к PKI-сертификатам](../../plan-design/network/pki-certificate-requirements.md).

- Необходима регистрация общедоступных записей узлов DNS для полных доменных имен (FQDN) систем сайта, поддерживающих IBCM.

### <a name="client-communication-requirements"></a>Требования к подключениям клиентов

На промежуточных брандмауэрах или прокси-серверах для интернет-систем сайтов должны быть разрешены подключения клиентов.

- Поддержка HTTP 1.1  

- Разрешить тип содержимого HTTP для составного вложения в формате MIME (multipart/mixed и application/octet-stream)  

#### <a name="verbs"></a>Команды

Разрешите следующие команды для ролей сервера интернет-систем сайта.

| Роль | Команды |
|------|-------|
| Точка управления | - HEAD<br>- CCM_POST<br>- BITS_POST<br>- GET<br>- PROPFIND |
| Точка распространения | - HEAD<br>- GET<br>- PROPFIND |
| Резервная точка состояния | POST |
| Точка веб-сайта каталога приложений | -POST<br>-GET |

#### <a name="http-headers"></a>Заголовки HTTP

Разрешите следующие заголовки HTTP для ролей сервера интернет-систем сайта.

| Роль | Заголовки HTTP |
|------|--------------|
| Точка управления | - Range:<br>- CCMClientID:<br>- CCMClientIDSignature:<br>- CCMClientTimestamp:<br>- CCMClientTimestampsSignature: |
| Точка распространения | Диапазон: |

Для получения сведений об аналогичных требованиях к соединениям при использовании точки обновления программного обеспечения с подключением клиентов из Интернета обратитесь к документации служб WSUS.

## <a name="unsupported-features"></a>Неподдерживаемые функции

Не всю функциональность управления клиентами можно использовать через Интернет. Configuration Manager не поддерживает некоторые функции для клиентов в Интернете. Эти неподдерживаемые функции обычно зависят от доменных служб Active Directory или не подходят для общедоступной сети.

При управлении клиентами через Интернет с помощью IBCM не поддерживаются следующие возможности:

- Развертывание клиентов через Интернет, например развертывание клиента на основе принудительной установки клиента и обновления ПО. Использование установки клиента вручную.

- Автоматическое назначение сайта

- Пробуждение по локальной сети.

- Развертывание ОС. Однако можно развернуть последовательности задач, не предусматривающие развертывание ОС.

- Удаленное управление

- Развертывание программного обеспечения для пользователей. Для этой функции требуется каталог приложений, а его использовать не рекомендуется.

- Роуминг клиента. Роуминг дает клиентам возможность всегда находить ближайшие точки распространения для загрузки контента. Независимо от пропускной способности или физического расположения клиенты недетерминированно выбирают одну из интернет-систем сайта.

При настройке точки обновления программного обеспечения, которая принимает подключения из Интернета, интернет-клиенты всегда проверяют эту точку для определения требуемых обновлений программного обеспечения. Когда эти клиенты подключаются к Интернету, сначала они пытаются загрузить обновления программного обеспечения из Центра обновления Майкрософт, а не с интернет-точки распространения. Если это сделать не удается, они пытаются загрузить необходимые обновления из интернет-точки распространения.

> [!TIP]
> Клиент Configuration Manager автоматически определяет, находится ли он в интрасети или в Интернете. Если клиент может связаться с контроллером домена или локальной точкой управления, он задает в качестве типа подключения "*Интрасеть* в данный момент". В противном случае он переключается на подключение "*Интернет* в данный момент" и взаимодействует с системами сайта, назначенными его сайту.
