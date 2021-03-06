---
title: Настройка инфраструктуры для поддержки профилей сертификатов SCEP с помощью Microsoft Intune в Azure | Документация Майкрософт
description: Для использования SCEP в Microsoft Intune следует настроить локальный домен AD, создать центр сертификации, настроить сервер NDES и установить Intune Certificate Connector.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 45f649a99f6b3d632fea9e46dfdaee89450ebd23
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989274"
---
# <a name="configure-infrastructure-to-support-scep-with-intune"></a>Настройка инфраструктуры для поддержки SCEP с помощью Intune

Intune поддерживает использование протокола SCEP для [проверки подлинности подключений к приложениям и корпоративным ресурсам](certificates-configure.md). SCEP использует сертификат центра сертификации (ЦС) для защиты обмена сообщениями в ходе запроса подписи сертификата (CSR). Если ваша инфраструктура поддерживает SCEP, для развертывания сертификатов на устройствах можно использовать *профили сертификатов SCEP* Intune (тип профиля устройства в Intune). Microsoft Intune Certificate Connector требуется для использования профилей сертификатов SCEP с Intune при использовании центра сертификации служб сертификатов Active Directory. Соединитель не требуется при использовании [сторонних центров сертификации](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration). 

Сведения в этой статье помогут вам настроить инфраструктуру для поддержки SCEP при использовании служб сертификатов Active Directory. После настройки инфраструктуры можно [создавать и развертывать профили сертификатов SCEP](certificates-profile-scep.md) с помощью Intune.

> [!TIP]
> Intune также поддерживает использование [сертификатов PKCS #12](certficates-pfx-configure.md).

## <a name="prerequisites-for-using-scep-for-certificates"></a>Предварительные требования для использования SCEP для сертификатов

Прежде чем продолжать, убедитесь, что [профиль *доверенного сертификата* создан и развернут](certificates-configure.md#export-the-trusted-root-ca-certificate) на устройствах, которые будут использовать профили сертификатов SCEP. Профили сертификатов SCEP напрямую ссылаются на профиль доверенного сертификата, который используется для инициализации устройств с доверенным корневым сертификатом ЦС.

### <a name="servers-and-server-roles"></a>Серверы и роли сервера

Следующая локальная инфраструктура должна работать на серверах, которые присоединены к домену Active Directory, за исключением прокси-сервера веб-приложения.

- **Центр сертификации**: требуется центр сертификации (ЦС) предприятия служб сертификатов Microsoft Active Directory под управлением выпуска Enterprise Windows Server 2008 R2 с пакетом обновления 1 (SP1) или более поздней версии. Используемая версия Windows Server должна оставаться поддерживаемой корпорацией Майкрософт. Автономный ЦС не поддерживается. Дополнительные сведения см. в разделе [Установка центра сертификации](https://technet.microsoft.com/library/jj125375.aspx). Если ЦС выполняется под управлением Windows Server 2008 R2 с пакетом обновления 1 (SP1), необходимо [установить исправление из KB2483564](https://support.microsoft.com/kb/2483564/).

- **Роль сервера NDES**: на сервере Windows Server 2012 R2 или более поздней версии настройте роль сервера "Служба регистрации сертификатов для сетевых устройств" (NDES). В следующем разделе этой статьи мы поможем вам [установить NDES](#set-up-ndes).

  - Сервер, на котором размещается NDES, должен быть присоединен к домену и находиться в том же лесу, что и ЦС предприятия.
  - Невозможно использовать NDES после установки на сервере, на котором размещен ЦС предприятия.
  - Вы можете установить соединитель Microsoft Intune Certificate Connector на том же сервере, что и NDES.

  Дополнительные сведения об NDES см. в статье [Руководство по службе регистрации сетевых устройств](https://technet.microsoft.com/library/hh831498.aspx) или [Использование модуля политики со службой регистрации сертификатов для сетевых устройств](https://technet.microsoft.com/library/dn473016.aspx).

- **Microsoft Intune Certificate Connector**: требуется для использования профилей сертификатов SCEP с Intune. Эта статья поможет вам [установить соединитель](#install-the-intune-certificate-connector).

  Соединитель поддерживает режим федерального стандарта обработки информации (FIPS). Включать FIPS необязательно, но в таком случае вы можете выдавать и отменять сертификаты.
  - Соединитель предъявляет такие же требования к сети, что и [управляемые устройства](../fundamentals/intune-endpoints.md#access-for-managed-devices).
  - Соединитель должен работать на том же сервере, где находится роль сервера NDES; это может быть сервер под управлением Windows Server 2012 R2 или более поздней версии.
  - Платформа .NET 4.5 Framework, обязательная для соединителя, автоматически входит в состав Windows Server 2012 R2.
  - Конфигурацию усиленной безопасности Internet Explorer [необходимо отключить на сервере NDES](https://technet.microsoft.com/library/cc775800(v=WS.10).aspx), где также размещается соединитель Microsoft Intune Certificate Connector.

Следующая локальная инфраструктура необязательна:

Чтобы разрешить устройствам в Интернете получать сертификаты, необходимо опубликовать URL-адрес NDES, внешний по отношению к корпоративной сети. Вы можете использовать Azure AD Application Proxy, прокси-сервер или другой обратный прокси.

- **Azure AD Application Proxy** (необязательно): вместо отдельного сервера прокси-службы веб-приложения (WAP) можно использовать Azure AD Application Proxy, чтобы открыть доступ к URL-адресу NDES через Интернет. Это позволяет устройствам в интрасети и Интернете получать сертификаты. Дополнительные сведения см. в статье [Как обеспечить безопасный удаленный доступ к локальным приложениям](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy).

- **Сервер прокси-службы веб-приложения** (необязательно): используйте сервер под управлением Windows Server 2012 R2 или более поздней версии в качестве сервера прокси-службы веб-приложения (WAP) для публикации URL-адреса NDES в Интернете.  Это позволяет устройствам в интрасети и Интернете получать сертификаты.

  На сервере, где размещается WAP, [необходимо установить обновление](https://blogs.technet.com/b/ems/archive/2014/12/11/hotfix-large-uri-request-in-web-application-proxy-on-windows-server-2012-r2.aspx) , обеспечивающее поддержку длинных URL-адресов, которые используются службой регистрации сертификатов для сетевых устройств. Это обновление включено в [накопительный пакет обновления за декабрь 2014 г.](https://support.microsoft.com/kb/3013769), или его можно получить отдельно из [KB3011135](https://support.microsoft.com/kb/3011135).

  Сервер WAP должен иметь SSL-сертификат, совпадающий с именем, опубликованным для внешних клиентов, и доверять SSL-сертификату, который используется на компьютере, где размещена служба NDES. Эти сертификаты позволяют WAP-серверу разорвать SSL-соединение клиентов и создать новое SSL-соединение со службой NDES.

  См. дополнительные сведения о [планировании сертификатов для WAP](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383650(v=ws.11)#plan-certificates) и [серверах WAP](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn584113(v=ws.11)).

### <a name="accounts"></a>Учетные записи

- **Учетная запись службы NDES**: перед настройкой NDES укажите учетную запись пользователя домена для использования в качестве учетной записи службы NDES. Эта учетная запись указывается при настройке шаблонов в выдающем ЦС перед настройкой NDES.

  Эта учетная запись должна иметь следующие права на сервере, где размещается NDES:

  - **Локальный вход**
  - **Вход в качестве службы**
  - **Вход в качестве пакетного задания**

  Дополнительные сведения см. в раздел [Создание учетной записи пользователя домена в качестве учетной записи службы NDES](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11)#to-create-a-domain-user-account-to-act-as-the-ndes-service-account).

- **Доступ к компьютеру, на котором размещена служба NDES**: вам потребуется учетная запись пользователя домена с разрешениями на установку и настройку ролей Windows Server на сервере, где устанавливается NDES.

- **Доступ к центру сертификации**: вам потребуется учетная запись пользователя домена с правами на управление центром сертификации.

### <a name="network-requirements"></a>Требования к сети

Рекомендуется публиковать сервер NDES через обратный прокси-сервер, например [Azure AD Application Proxy, прокси веб-доступа](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-publish/) или прокси-сервер стороннего поставщика. Если вы не используете обратный прокси-сервер, разрешите трафик TCP по порту 443 со всех узлов и IP-адресов в Интернете к службе NDES.

Разрешите все необходимые порты и протоколы для связи между сервером NDES и любой вспомогательной инфраструктурой в вашей среде. Например, компьютеру, где размещена служба NDES, необходимо взаимодействовать с ЦС, серверами DNS, контроллерами домена и, возможно, другими службами или серверами в вашей среде, например Configuration Manager.

### <a name="certificates-and-templates"></a>Сертификаты и шаблоны

При использовании SCEP применяются следующие сертификаты и шаблоны.

|Объект    |Сведения    |
|----------|-----------|
|**Шаблон сертификата SCEP**         |Шаблон, который вы настраиваете в выдающем ЦС, используемом для выполнения запросов SCEP от устройств. |
|**Сертификат проверки подлинности клиента**. |Запрашивается у выдающего или общедоступного ЦС.<br /> Этот сертификат устанавливается на компьютере, на котором размещена служба NDES, и используется соединителем Intune Certificate Connector.<br /> Если сертификат имеет набор вариантов использования *client* и *server authentication* (см. раздел **Расширенное использование ключа**), можно использовать тот же сертификат. Затем можно использовать один и тот же сертификат для проверки подлинности сервера и клиента. |
|**Сертификат проверки подлинности сервера** |Сертификат веб-сервера запрашивается у выдающего или общедоступного ЦС.<br /> Этот SSL-сертификат устанавливается и привязывается в службах IIS на компьютере, на котором размещается NDES.<br />Если сертификат имеет набор вариантов использования *client* и *server authentication* (см. раздел **Расширенное использование ключа**), можно использовать тот же сертификат. Затем можно использовать один и тот же сертификат для проверки подлинности сервера и клиента. |
|**Доверенный корневой сертификат ЦС**       |Чтобы использовать профиль сертификата SCEP, устройства должны доверять доверенному корневому центру сертификации (CA). Используйте *профиль доверенного сертификата* в Intune для предоставления доверенного корневого сертификата ЦС пользователям и устройствам. <br/><br/> **-** Для каждой платформы операционной системы используется один доверенный корневой сертификат ЦС, который связывается с каждым созданным вами профилем доверенного сертификата. <br /><br /> **-** При необходимости можно использовать дополнительные доверенные корневые сертификаты ЦС. Например, это можно сделать, чтобы предоставить доверие ЦС, подписывающему сертификаты проверки подлинности сервера для точек доступа Wi-Fi. При необходимости для выдающих ЦС можно использовать дополнительные доверенные корневые сертификаты ЦС.  В профиле сертификата SCEP, созданном в Intune, обязательно укажите профиль доверенного корневого ЦС для выдающего ЦС.<br/><br/> Сведения о профиле доверенного сертификата см. в статье [Экспорт доверенного корневого сертификата ЦС](certificates-configure.md#export-the-trusted-root-ca-certificate) и [Создание профилей доверенных сертификатов](certificates-configure.md#create-trusted-certificate-profiles) в разделе *Использование сертификатов для проверки подлинности в Intune*. |

## <a name="configure-the-certification-authority"></a>Настройка центра сертификации

С помощью следующих разделов вы:

- Настроите и опубликуете требуемый шаблон для NDES.
- Зададите необходимые разрешения для отзыва сертификата.

Эти разделы предполагают, что вы знакомы с Windows Server 2012 R2 и более поздних версий и службами сертификатов Active Directory (ADCS).

### <a name="access-your-issuing-ca"></a>Доступ к выдающему ЦС

1. Войдите в выдающий ЦС с помощью учетной записи домена с правами, достаточными для управления ЦС.

2. Откройте консоль управления (MMC) "Центр сертификации". **Запустите** команду "certsrv.msc" или в **диспетчере сервера** выберите пункты **Сервис** и **Центр сертификации**.

3. Выберите узел **Шаблоны сертификатов** и щелкните **Действие** > **Управление**.

### <a name="create-the-scep-certificate-template"></a>Создание шаблона сертификата SCEP

1. В качестве шаблона сертификата NDES создайте шаблон сертификата версии 2 (с совместимостью с Windows 2003). Можно сделать следующее:

   - В выдающем ЦС создайте пользовательский шаблон с помощью оснастки *Шаблоны сертификатов*.
   - Скопируйте существующий шаблон (например, пользовательский шаблон) и затем обновите копию для использования в качестве шаблона NDES.

2. Настройте следующие параметры на указанных вкладках шаблона:

   - **Общие**

     - Снимите флажок **Опубликовать сертификат в Active Directory**.
     - Укажите понятное **Отображаемое имя шаблона**, чтобы впоследствии можно было определить этот шаблон.

   - **Имя субъекта**.

     - Выберите пункт **Предоставляется в запросе**. Безопасность обеспечивается модулем политики Intune для NDES.

       ![Шаблон, вкладка "Имя субъекта"](./media/certificates-scep-configure/scep-ndes-subject-name.jpg)

   - **Расширения**.

     - Убедитесь, что в разделе **Описание политик приложений** включен пункт **Проверка подлинности клиента**.

       > [!IMPORTANT]
       > Добавляйте только необходимые политики приложений. Согласуйте выбранные параметры с администраторами безопасности.

     - Для шаблонов сертификатов iOS/iPadOS и macOS также измените параметр **Использование ключей** и снимите флажок **Подпись подтверждает подлинность**.

     ![Шаблон, вкладка "Расширения"](./media/certificates-scep-configure/scep-ndes-extensions.jpg)  

   - **Безопасность**.

     - Добавьте **учетную запись службы NDES**. Этой учетной записи требуются разрешения на **чтение** и **регистрацию** для этого шаблона.

     - Добавьте дополнительные учетные записи для администраторов Intune, которые будут создавать профили SCEP. Эти учетные записи должны иметь разрешения на **чтение** шаблона, чтобы администраторы могли переходить к этому шаблону при создании профилей SCEP.

     ![Шаблон, вкладка "Безопасность"](./media/certificates-scep-configure/scep-ndes-security.jpg)

   - **Обработка запросов**

     Ниже приведен пример экрана. Ваша конфигурация может отличаться.  

     ![Шаблон, вкладка "Обработка запроса"](./media/certificates-scep-configure/scep-ndes-request-handling.png)

   - **Требования выдачи**

     Ниже приведен пример экрана. Ваша конфигурация может отличаться.

     ![Шаблон, вкладка "Требования выдачи"](./media/certificates-scep-configure/scep-ndes-issuance-reqs.jpg)

3. Сохраните шаблон сертификата.

### <a name="create-the-client-certificate-template"></a>Создание шаблона сертификата клиента

Для соединителя Intune Certificate Connector требуется сертификат с расширенным использованием ключа *проверки подлинности клиента* и именем субъекта, равным полному доменному имени компьютера, на котором установлен соединитель. Требуется шаблон со следующими свойствами:

- **Расширения** > **Политики приложений** должны содержать **Проверка подлинности клиента**
- **Имя субъекта** > **Предоставляется в запросе**.

Если у вас уже есть шаблон, включающий эти свойства, можно использовать его повторно; в противном случае создайте новый шаблон путем дублирования существующего или создания пользовательского шаблона.

### <a name="create-the-server-certificate-template"></a>Создание шаблона сертификата сервера

При обмене данными между управляемыми устройствами и службами IIS на сервере NDES используется протокол HTTPS, который требует использования сертификата. Для выдаче этого сертификата можно использовать шаблон сертификата **веб-сервера**. Или, если вы предпочитаете использовать отдельный шаблон, необходимы следующие свойства:

- **Расширения** > **Политики приложений** должны содержать **Проверка подлинности сервера**
- **Имя субъекта** > **Предоставляется в запросе**.

> [!NOTE]
> При наличии сертификата, удовлетворяющего требованиям шаблонов сертификатов клиента и сервера, можно использовать один сертификат как для IIS, так и для соединителя Intune Certificate Connector.

### <a name="grant-permissions-for-certificate-revocation"></a>Предоставление разрешений для отзыва сертификата

Чтобы служба Intune могла отозвать сертификаты, которые больше не требуются, необходимо предоставить разрешения в центре сертификации.

Для соединителя Intune Certificate Connector можно использовать **системную учетную запись** сервера NDES или конкретную учетную запись, например **учетную запись службы NDES**.

1. В консоли центра сертификации щелкните правой кнопкой мыши имя центра сертификации и выберите пункт **Свойства**.

2. На вкладке **Безопасность** нажмите кнопку **Добавить**.

3. Предоставьте право **Выдача сертификатов и управление ими**:

   - Если вы хотите использовать **системную учетную запись**сервера NDES, предоставьте разрешения для сервера NDES.
   - Если вы хотите использовать **учетную запись службы NDES**, укажите вместо нее разрешения для этой учетной записи.

### <a name="modify-the-validity-period-of-the-certificate-template"></a>Изменение срока действия шаблона сертификата

Вы можете изменить срок действия шаблона сертификата.  

После [создания шаблона сертификата SCEP](#create-the-scep-certificate-template) можно изменить шаблон, чтобы проверить **срок действия** на вкладке **Общие**.

По умолчанию в Intune используется значение, настроенное в шаблоне. Но в настройках ЦС вы можете разрешить инициатору запроса вводить другое значение, которое можно затем задать в консоли Intune.

> [!IMPORTANT]
> Для iOS/iPadOS и macOS всегда используйте значение, заданное в шаблоне.

#### <a name="to-configure-a-value-that-can-be-set-from-within-the-intune-console"></a>Настройка значения, которое может быть задано в консоли Intune

1. Выполните следующие команды в ЦС:

   -**certutil -setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**
   -**net stop certsvc**
   -**net start certsvc**

2. В выдающем ЦС используйте оснастку центра сертификации, чтобы опубликовать шаблон сертификата. Выберите узел **Шаблоны сертификатов**, щелкните **Действие** > **Создать** > **Выдаваемый шаблон сертификата**, а затем укажите шаблон, созданный в предыдущем разделе.

3. Убедитесь, что шаблон опубликован, просмотрев его в папке **Шаблоны сертификата**.

## <a name="set-up-ndes"></a>Настройка NDES

Следующие процедуры помогут настроить службу NDES для использования с Intune. Дополнительные сведения о службе см. в разделе [Руководство по службе регистрации сертификатов для сетевых устройств](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v%3dws.11)).

### <a name="install-the-ndes-service"></a>Установка службы NDES

1. На сервер, где будет размещена NDES, необходимо войти как **Администратор предприятия**, а затем использовать [мастер добавления ролей и компонентов](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831809(v=ws.11)) для установки NDES:

   1. В мастере выберите **Службы сертификатов Active Directory** , чтобы получить доступ к службам ролей служб сертификатов Active Directory. Выберите пункт **Служба регистрации сертификатов для сетевых устройств**, снимите флажок **Центр сертификации**, а затем завершите работу мастера.

      > [!TIP]
      > В разделе **Ход выполнения установки** не нажимайте кнопку **Закрыть**. Вместо этого щелкните ссылку **Настроить службы сертификатов Active Directory на конечном сервере**. Откроется мастер **настройки служб сертификатов Active Directory**, который используется для следующей процедуры в этой статье, чтобы *настроить службу NDES*. После того, как откроется окно настройки служб сертификатов Active Directory, можно закрыть мастер добавления ролей и компонентов.

   2. При добавлении NDES на сервер мастер также установит IIS. Убедитесь, что в IIS настройки заданы следующим образом:

      - **Веб-сервер** > **Безопасность** > **Фильтрация запросов**
      - **Веб-сервер** > **Разработка приложений** > **ASP.NET 3.5**.

        При установке ASP.NET 3.5 устанавливается платформа .NET Framework 3.5. При установке .NET Framework 3.5 установите основной компонент **.NET Framework 3.5** и компонент **Активация по HTTP**.

      - **Веб-сервер** > **Разработка приложений** > **ASP.NET 4.5**.

        При установке ASP.NET 4.5 устанавливается платформа .NET Framework 4.5. При установке .NET Framework 4.5 установите основной компонент **.NET Framework 4.5**, компонент **ASP.NET 4.5** и компонент **Службы WCF** > **Активация по HTTP**.

      - **Средства управления** > **Совместимость управления IIS 6** > **Совместимость метабазы IIS 6**
      - **Средства управления** > **Совместимость управления IIS 6** > **Совместимость WMI в IIS 6**
      - На сервере добавьте учетную запись службы NDES в качестве участника локальной группы **IIS_IUSR**.

2. Выполните следующую команду с повышенными привилегиями на компьютере, где размещена служба NDES: Выполните следующую команду, чтобы настроить SPN учетной записи службы NDES:

   `setspn -s http/<DNS name of the computer that hosts the NDES service> <Domain name>\<NDES Service account name>`

   Например, если имя компьютера, где размещена служба NDES, — **Server01**, домен — **Contoso.com**, а учетная запись службы — **NDESService**, используйте:

   `setspn –s http/Server01.contoso.com contoso\NDESService`  

### <a name="configure-the-ndes-service"></a>Настройка службы NDES

1. На компьютере, где размещена служба NDES, откройте мастер настройки **служб сертификатов Active Directory** и внесите следующие изменения.

   > [!TIP]
   > Если вы продолжаете работу с последней процедуры и щелкнули ссылку **Настройка служб сертификатов Active Directory на целевом сервере**, этот мастер уже должен быть открыт. В противном случае откройте диспетчер серверов, чтобы получить доступ к настройке служб сертификатов Active Directory после развертывания.

   - На странице **Службы ролей** выберите **Служба регистрации сертификатов для сетевых устройств**.
   - На странице **Учетная запись службы для NDES** укажите учетную запись службы NDES.
   - На странице **ЦС для NDES** щелкните **Выбрать** и укажите выдающий ЦС, в котором настроен шаблон сертификата.
   - На странице **Криптография для NDES** задайте длину ключа, соответствующую требованиям компании.
   - На странице **Подтверждение** щелкните **Настроить**, чтобы завершить работу мастера.

2. После завершения работы мастера измените следующий раздел реестра на компьютере, где размещена служба NDES:

   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP\`

   Чтобы обновить этот раздел, определите **назначение** шаблона сертификата (на его вкладке **Обработка запроса**). Затем обновите соответствующую запись реестра, заменив существующие данные именем шаблона сертификата (не отображаемым именем шаблона), указанным, когда вы [создали шаблон сертификата](#create-the-scep-certificate-template).

   Следующая таблица содержит соответствия назначений шаблона сертификата и значений в реестре:

   |Назначение шаблона сертификата (на вкладке "Обработка запросов")|Изменяемое значение реестра|Значение, отображающееся в консоли администрирования Intune для профиля SCEP|
   |------------------------|-------------------------|---|
   |Подпись               |SignatureTemplate        |Цифровая подпись |
   |Encryption              |EncryptionTemplate       |Шифрование ключа  |
   |Подпись и шифрование|GeneralPurposeTemplate   |Шифрование ключа <br/> Цифровая подпись |

   Например, если назначение шаблона сертификата — **Шифрование**, измените значение **EncryptionTemplate** на имя шаблона сертификата.

3. Настройте фильтрацию запросов IIS, чтобы добавить в службы IIS поддержку длинных URL-адресов (запросов), получаемых службой NDES.

   1. В диспетчере IIS выберите **Веб-сайт по умолчанию** > **Фильтрация запросов** > **Изменить параметры функций**, чтобы открыть страницу **Изменение параметров фильтрации запросов**.

   2. Настройте следующие параметры.

      - **Максимальная длина URL-адреса (байт)** = 65534
      - **Максимальная длина строки запроса (байт)** = 65534

   3. Нажмите кнопку **ОК**, чтобы сохранить конфигурацию и закрыть диспетчер IIS.

   4. Проверьте эту конфигурацию, просмотрев следующий раздел реестра, чтобы убедиться в том, что он содержит указанные значения:

      `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HTTP\Parameters`

      Убедитесь, что в качестве записей DWORD установлены следующие значения:

      - Имя. **MaxFieldLength** с десятичным значением **65534**.
      - Имя. **MaxRequestBytes** с десятичным значением **65534**.

4. Перезапустите сервер, на котором размещена служба NDES. Не используйте **iisreset**; эта команда не выполняет необходимые изменения.

5. Перейдите по адресу *http://* полное доменное имя сервера */certsrv/mscep/mscep.dll*. Вы должны увидеть страницу NDES, аналогичную следующей:

   ![Проверка NDES](./media/certificates-scep-configure/scep-ndes-url.png)

   Если веб-адрес возвращает ответ **503 Служба недоступна**, проверьте окно просмотра событий компьютера. Эта ошибка обычно возникает, когда пул приложений остановлен из-за отсутствия [разрешения для учетной записи службы NDES](#accounts).
  
### <a name="install-and-bind-certificates-on-the-server-that-hosts-ndes"></a>Установка и привязка сертификатов на сервере NDES

> [!TIP]
> В следующей процедуре можно использовать один сертификат как для *проверки подлинности сервера*, так и для *проверки подлинности клиента*, если этот сертификат настроен в соответствии с критериями обоих способов. Критерии для каждого использования описаны в шагах 1 и 3 следующей процедуры.

1. На сервере NDES запросите и установите сертификат **проверки подлинности сервера** из внутреннего или общедоступного ЦС.

   Если сервер использует внешнее и внутреннее имена для одного сетевого адреса, сертификат проверки подлинности сервера должен иметь:

   - **имя субъекта** с внешним общедоступным именем сервера;
   - **альтернативное имя субъекта**, включающее внутреннее имя сервера.

2. Привяжите сертификат проверки подлинности сервера (SSL-сертификат) в IIS:

   1. после установки сертификата проверки подлинности сервера откройте **диспетчер IIS** и выберите **Веб-сайт по умолчанию**. В области **Действия** выберите элемент **Привязки**.

   1. Нажмите кнопку **Добавить**, задайте для пункта **Тип** значение **https**, а затем укажите порт **443**.
   
   1. В качестве **SSL-сертификата**укажите сертификат проверки подлинности сервера.

3. На сервере NDES запросите и установите сертификат **проверки подлинности клиента** из внутреннего или общедоступного ЦС.

   Сертификат проверки подлинности клиента должен иметь следующие свойства:

   - **Расширенное использование ключа**: Это значение должно включать **проверку подлинности клиента**.
   - **Имя субъекта**. Значение должно совпадать с DNS-именем сервера, на котором устанавливается сертификат (сервер NDES).

4. Сервер, на котором размещена служба NDES, теперь готов к поддержке соединителя Intune Certificate Connector.

## <a name="install-the-intune-certificate-connector"></a>Установка Intune Certificate Connector

Можно установить соединитель Microsoft Intune Certificate Connector на том же сервере, что и службу NDES. Не поддерживается использование NDES или соединителя Intune Certificate Connector на том же сервере, где находится выдающий центр сертификации (ЦС).

### <a name="to-install-the-certificate-connector"></a>Установка соединителя Certificate Connector

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Выберите **Администрирование клиента** > **Соединители и токены** > **Соединители сертификатов** > **Добавить**.

3. Скачайте и сохраните файл соединителя для SCEP файла. Сохраните его в расположении, доступном с сервера, на который вы собираетесь установить соединитель.

   ![ConnectorDownload](./media/certificates-scep-configure/download-certificates-connector.png)

4. После скачивания перейдите на сервер, где размещается роль службы регистрации сертификатов для сетевых устройств (NDES). Затем сделайте следующее:

   1. Убедитесь, что установлена платформа .NET 4.5 Framework, так как она необходима для соединителя Intune Certificate Connector. Платформа .NET 4.5 Framework автоматически входит в состав Windows Server 2012 R2 и более новых версий.

   2. Запустите установщик (**NDESConnectorSetup.exe**). Также будет установлен модуль политики для NDES и веб-службы CRP служб IIS. Веб-служба CRP, *CertificateRegistrationSvc*, выполняется в IIS как приложение.

      При установке NDES для автономной службы Intune служба CRP автоматически устанавливается вместе с соединителем сертификатов.

5. При появлении запроса на сертификат клиента для Certificate Connector нажмите кнопку **Выбрать** и выберите сертификат **проверки подлинности клиента**, установленный на сервере NDES на этапе 3 процедуры [установки и привязки сертификатов на сервере, на котором размещается NDES](#install-and-bind-certificates-on-the-server-that-hosts-ndes) ранее в этой статье.

   После выбора сертификата проверки подлинности клиента вы вернетесь на поверхность **Сертификата клиента для соединителя сертификатов Microsoft Intune**. Хотя выбранный сертификат не отображается, нажмите кнопку **Далее**, чтобы просмотреть свойства этого сертификата. После этого нажмите кнопки **Далее** и **Установить**.

> [!NOTE]
> Для клиентов GCC High перед запуском Intune Certificate Connector необходимо внести изменения, описанные ниже.
> 
> Внесите изменения в два перечисленных ниже файла конфигурации, которые будут обновлять конечные точки службы для среды GCC High. Обратите внимание, что эти обновления изменяют коды URI с суффикса **.com** на **.us**. В общем существует три обновления URI, два в файле конфигурации NDESConnectorUI. exe. config и одно в файле NDESConnector.exe.config.
> 
> - Имя файла: <install_Path>\Microsoft Intune\NDESConnectorUI\NDESConnectorUI.exe.config
> 
>   Пример: (%programfiles%\Microsoft Intune\NDESConnectorUI\NDESConnectorUI.exe.config)
>   ```
>    <appSettings>
>        <add key="SignInURL" value="https://portal.manage.microsoft.us/Home/ClientLogon"/>
>        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
>        <add key="AccountPortalURL" value="https://manage.microsoft.us"/>
>    </appSettings>
>   ```
> 
> - Имя файла: <install_Path>\Microsoft Intune\NDESConnectorSvc\NDESConnector.exe.config
>
>   Пример: (%programfiles%\Microsoft Intune\NDESConnectorSvc\NDESConnector.exe.config)
>    ```
>    <appSettings>
>        <add key="BaseServiceAddress" value="https://manage.microsoft.us/" />
>    ```
>
> Если эти изменения не завершены, клиенты GCC High получат сообщение об ошибке: "Доступ запрещен" "У вас отсутствует разрешение на просмотр этой страницы".

6. После завершения работы мастера, но перед тем, как закрыть его, щелкните **Запустить пользовательский интерфейс соединителя сертификатов**.

   Если вы закроете мастер перед запуском пользовательского интерфейса соединителя сертификатов, вы можете повторно открыть его, выполнив следующую команду:

   *<путь_установки>\NDESConnectorUI\NDESConnectorUI.exe*

7. В пользовательском интерфейсе **соединителя сертификатов** :

   1. Щелкните **Войти** и введите учетные данные администратора службы Intune или учетные данные администратора клиента с разрешениями глобального администратора.

   2. Учетной записи, которую вы используете, должна быть назначена действительная лицензия Intune.

   3. После входа в систему Intune Certificate Connector загружает сертификат из Intune. Этот сертификат используется для проверки подлинности между соединителем и Intune. Если у используемой учетной записи нет лицензии Intune, соединителю (NDESConnectorUI.exe) не удастся получить сертификат из Intune.  

      Если ваша организация использует прокси-сервер и он требуется для подключения сервера NDES к Интернету, выберите пункт **Использовать прокси-сервер**. Затем введите имя прокси-сервера, порт и учетные данные учетной записи для подключения.

   4. Откройте вкладку **Дополнительно**, а затем введите учетные данные учетной записи с разрешением **Выдача сертификатов и управление ими** в выдающем центре сертификации. Нажмите кнопку **Применить**, чтобы применить изменения.  

    5. Теперь можно закрыть пользовательский интерфейс соединителя сертификатов.

8. Откройте командную строку, введите **services.msc**, а затем нажмите клавишу **Ввод**. Щелкните правой кнопкой мыши **Служба соединителя Intune** > **Перезапустить**.

Чтобы убедиться, что служба работает, откройте браузер и введите следующий URL-адрес. Он должен вернуть ошибку **403**: `https://<FQDN_of_your_NDES_server>/certsrv/mscep/mscep.dll`

> [!NOTE]
> Intune Certificate Connector поддерживает TLS 1.2. Если сервер, на котором размещен соединитель, поддерживает TLS 1.2, то используется TLS 1.2. Если сервер не поддерживает TLS 1.2, то используется TLS 1.1. Сейчас TLS 1.1 используется для проверки подлинности между устройствами и сервером.

## <a name="next-steps"></a>Дальнейшие шаги

[Создание профиля сертификата SCEP](certificates-profile-scep.md)  
[Устранение неполадок с соединителем Intune Certificate Connector](troubleshoot-certificate-connector-events.md)
