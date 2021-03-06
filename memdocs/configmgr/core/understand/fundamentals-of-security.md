---
title: Основы безопасности
titleSuffix: Configuration Manager
description: Сведения об уровнях безопасности в Configuration Manager.
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95b8bf41d74e7011eed40116f4fe34e2c356d67e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707062"
---
# <a name="fundamentals-of-security-for-configuration-manager"></a>Основы безопасности для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

В этой статье перечислены следующие основные компоненты безопасности любой среды Configuration Manager:
- [Уровни безопасности](#bkmk_layers)
- [Администрирование на основе ролей](#bkmk_rba)
- [Обеспечение безопасности клиентских конечных точек](#bkmk_endpoints)
- [Учетные записи и группы Configuration Manager](#bkmk_accounts)
- [Конфиденциальность](#bkmk_privacy)

## <a name="security-layers"></a><a name="bkmk_layers"></a> Уровни безопасности

Обеспечение безопасности для Configuration Manager включает несколько следующие уровни: 
- [Безопасность сети и ОС Windows](#bkmk_layer-windows)
- [Сетевая инфраструктура: брандмауэры, системы обнаружения вторжений, инфраструктуры открытых ключей (PKI)](#bkmk_layer-network)
- [Средства безопасности Configuration Manager](#bkmk_layer-cm)
- [Поставщик SMS](#bkmk_layer-provider)
- [Разрешения базы данных сайта](#bkmk_layer-db)

#### <a name="windows-os-and-network-security"></a><a name="bkmk_layer-windows"></a> Безопасность сети и ОС Windows
Первый уровень обеспечивается функциями безопасности Windows для ОС и сети. Этот уровень включает в себя следующие компоненты:  

-   Общий доступ к файлам для передачи файлов между компонентами Configuration Manager  

-   Списки управления доступом (ACL) для защиты файлов и разделов реестра  

-   Протокол IPsec для защиты обмена данными  

-   Групповая политика для настройки политики безопасности  

-   Разрешения DCOM для распределенных приложений, таких как консоль Configuration Manager  

-   Доменные службы Active Directory для хранения субъектов безопасности  

-   Безопасность учетной записи Windows, включая некоторые группы, создаваемые Configuration Manager в процессе установки  

#### <a name="network-infrastructure"></a><a name="bkmk_layer-network"></a> Сетевая инфраструктура

Дополнительные компоненты безопасности, например брандмауэры и системы обнаружения вторжений, помогают обеспечить защиту всей среды. Сертификаты, изданные в стандартных реализациях инфраструктуры открытых ключей (PKI), обеспечивают проверку подлинности, подписание и шифрование.  

#### <a name="configuration-manager-security-controls"></a><a name="bkmk_layer-cm"></a> Средства безопасности Configuration Manager

В дополнение к функциям безопасности, предоставляемым Windows Server и сетевой инфраструктурой, Configuration Manager управляет доступом к своей консоли и ее ресурсам несколькими способами. По умолчанию только локальные администраторы имеют права в отношении файлов и разделов реестра, необходимых для запуска консоли Configuration Manager на компьютерах, где она установлена.  

#### <a name="sms-provider"></a><a name="bkmk_layer-provider"></a> Поставщик SMS

Следующий уровень безопасности основан на доступе через инструментарий управления Windows (WMI), в частности, это относится к поставщику SMS. Поставщик SMS — это компонент Configuration Manager, который предоставляет пользователю доступ для запроса информации из базы данных сайта. К поставщику по умолчанию имеют доступ только члены локальной группы "Администраторы SMS". Эта группа изначально содержит только пользователя, установившего Configuration Manager. Чтобы предоставить другим учетным записям разрешение на доступ к репозиторию CIM и поставщику SMS, следует добавить в группу "Администраторы SMS" другие учетные записи.  

С версии 1810 вы можете указать минимально необходимый уровень аутентификации для доступа администраторов к сайтам Configuration Manager. Эта функция позволяет настроить для администраторов требование входить в Windows с определенным уровнем. <!--1357013-->  

Дополнительные сведения см. в разделе [Планирование использования поставщика SMS](../plan-design/hierarchy/plan-for-the-sms-provider.md).

#### <a name="site-database-permissions"></a><a name="bkmk_layer-db"></a> Разрешения базы данных сайта

Последний уровень безопасности – это разрешения для объектов в базе данных сайта. По умолчанию локальная системная учетная запись и учетная запись, используемая для установки Configuration Manager, имеют доступ к администрированию всех объектов в базе данных сайта. Можно предоставлять и отменять разрешения для дополнительных административных пользователей в консоли Configuration Manager, используя ролевое администрирование.  



## <a name="role-based-administration"></a><a name="bkmk_rba"></a> Администрирование на основе ролей  

 В Configuration Manager используется ролевое администрирование, позволяющее обеспечить безопасность таких объектов, как коллекции, развертывания и сайты. Эта модель администрирования централизованно определяет и управляет параметрами безопасности в масштабе иерархии для всех сайтов и параметров сайтов. 

 Администраторы назначают *роли безопасности* административным пользователям и групповые разрешения. Разрешения связаны с различными типами объектов Configuration Manager, например разрешения на создание и изменение параметров клиентов. 

 *Области безопасности* объединяют определенные экземпляры объектов, которыми должен управлять пользователь с правами администратора, например приложение, устанавливающее Microsoft Office. 

 Сочетание ролей безопасности, областей безопасности и коллекций определяет объекты, которые пользователь с правами администратора может просматривать и которыми он может управлять. Configuration Manager устанавливает некоторые роли безопасности по умолчанию для типичных задач управления. Кроме того, вы можете создавать свои собственные роли безопасности, соответствующие определенным бизнес-требованиям.  

 Дополнительные сведения см. в разделе [Настройка ролевого администрирования](../servers/deploy/configure/configure-role-based-administration.md).  



## <a name="securing-client-endpoints"></a><a name="bkmk_endpoints"></a> Обеспечение безопасности клиентских конечных точек  

 Configuration Manager защищает подключение клиентов к ролям системы сайта с помощью самозаверяющего или PKI-сертификата или токенов Azure Active Directory (Azure AD). Некоторые сценарии требуют использования PKI-сертификатов. Например, [управление клиентами в Интернет](../clients/manage/plan-internet-based-client-management.md), а также [клиенты мобильных устройств](../../mdm/plan-design/plan-on-premises-mdm.md).  

 Вы можете настроить для ролей систем сайта, к которым подключаются клиенты, протоколы HTTPS или HTTP. Клиентские компьютеры всегда соединяются с использованием наиболее безопасного доступного метода. Менее защищенный метод применяется только в том случае, если имеются роли системы сайта, разрешающие соединения по протоколу HTTP.  

 Дополнительные сведения см. в разделе [Планирование безопасности](../plan-design/security/plan-for-security.md).



## <a name="configuration-manager-accounts-and-groups"></a><a name="bkmk_accounts"></a> Учетные записи и группы Configuration Manager  

 Configuration Manager использует учетную запись Local System для большинства операций с сайтом. Некоторые задачи управления могут потребовать создания и обслуживания дополнительных учетных записей. Configuration Manager создает несколько групп по умолчанию, а также роли SQL Server при установке. Возможно, вам понадобится вручную добавить учетные записи компьютеров или пользователей в эти группы и роли SQL Server по умолчанию.  

 Дополнительные сведения см. в статье [Учетные записи, используемые в Configuration Manager](../plan-design/hierarchy/accounts.md).  



## <a name="privacy"></a><a name="bkmk_privacy"></a> Конфиденциальность  

 Перед развертыванием Configuration Manager следует рассмотреть требования к конфиденциальности. Продукты для управления предприятием дают много преимуществ, позволяя эффективно управлять большим числом клиентов, но это программное обеспечение может повлиять на конфиденциальность пользователей в организации. Configuration Manager включает в себя много средств для сбора данных и наблюдения за устройствами. По некоторым из них могут возникнуть вопросы, касающиеся соблюдения конфиденциальности в вашей организации.  

 Например, при установке клиента Configuration Manager многие параметры управления включены по умолчанию. В результате такой конфигурации клиентское программное обеспечение отправляет данные на сайт Configuration Manager. Сайт сохраняет сведения клиента в базе данных сайта. Сведения клиента не отправляется непосредственно в корпорацию Майкрософт. Дополнительные сведения см. в статье [Данные о диагностике и использовании](../plan-design/diagnostics/diagnostics-and-usage-data.md).



## <a name="see-also"></a>См. также

- [Планирование безопасности](../plan-design/security/plan-for-security.md)  

- [Безопасность и конфиденциальность клиентов Configuration Manager](../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Настройка безопасности](../plan-design/security/configure-security.md)   

- [Связь между конечными точками](../plan-design/hierarchy/communications-between-endpoints.md)  

- [Технический справочник по элементам управления шифрования](../plan-design/security/cryptographic-controls-technical-reference.md)  
