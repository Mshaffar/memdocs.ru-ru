---
title: Расширения схемы
titleSuffix: Configuration Manager
description: Расширение схемы Active Directory для поддержки Configuration Manager.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1ace560130e43fd5675b51b6d507e84043c01407
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904069"
---
# <a name="schema-extensions-for-configuration-manager"></a>Расширения схемы для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Вы можете расширить схему Active Directory для поддержки Configuration Manager. Это изменит схему леса Active Directory: в нее будет добавлен новый контейнер и несколько атрибутов, используемых сайтами Configuration Manager для публикации информации о ключах в Active Directory, где клиенты смогут безопасно применять ее. Эти сведения могут упростить развертывание и настройку клиентов и помогают клиентам находить ресурсы сайта, такие как серверы с развернутым содержимым, или предоставляют клиентам различные службы.  

-   Расширять схему Active Directory рекомендуется, но не требуется.  

Перед [расширением схемы Active Directory](https://docs.microsoft.com/sccm/core/plan-design/network/extend-the-active-directory-schema)необходимо ознакомиться с доменными службами Active Directory и [изменением схемы Active Directory](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc759402(v=ws.10)).  

## <a name="considerations-for-extending-the-active-directory-schema-for-configuration-manager"></a>Вопросы по расширению схемы Active Directory для Configuration Manager  

-   Расширения схемы Active Directory для Configuration Manager не изменились по сравнению с используемыми в Configuration Manager 2007 и Configuration Manager 2012. Если вы расширили схему ранее для любой версии, вам не потребуется расширять ее снова.  

-   Расширение схемы происходит на уровне леса, однократно и необратимо.  

-   Его может выполнять только пользователь, являющийся членом группы "Администраторы схемы", или пользователь, которому были предоставлены разрешения, достаточные для изменения схемы.  

-   Хотя схему можно расширить до или после выполнения установки Configuration Manager, рекомендуется делать это перед началом настройки параметров сайтов и иерархии. Это позволяет упростить многие из описанных далее этапов конфигурации.  

-   После расширения схемы глобальный каталог Active Directory реплицируется во всем лесу. Поэтому расширение схемы следует запланировать на такое время суток, в которое трафик репликации не окажет негативного влияния на другие процессы, использующие ресурсы сети:  

    -   В лесах Windows 2000 расширение схемы обуславливает полную синхронизацию всего глобального каталога.  

    -   Начиная с лесов Windows 2003, реплицируются только вновь добавляемые атрибуты.  

**Устройства и клиенты, которые не используют схему Active Directory:**  

-   Мобильные устройства под управлением коннектора Exchange Server  

-   Клиент для компьютеров Mac  

-   Клиент для серверов Linux и UNIX  

-   Мобильные устройства, зарегистрированные Configuration Manager  

-   Мобильные устройства, зарегистрированные с помощью Microsoft Intune  

-   Устаревшие клиенты мобильных устройств  

-   Клиенты Windows, настроенные для управления только через Интернет  

-   Клиенты Windows, которые определяются Configuration Manager как находящиеся в Интернете  

## <a name="capabilities-that-benefit-from-extending-the-schema"></a>Возможности, которые выигрывают от расширения схемы  
**Установка клиентского компьютера и назначение сайта**. При установке нового клиента на компьютер Windows клиент ищет свойства установки в доменных службах Active Directory.  

-   **Обходные пути**. Если вы не расширили схему, следует использовать одно из следующих решений, чтобы предоставить сведения о конфигурации, требуемые для установки компьютеров:  

    -   **Принудительная установка клиента**. Перед использованием какого-либо метода установки клиента убедитесь в том, что соблюдаются все необходимые условия. Дополнительные сведения см. в подразделе "Зависимости, связанные с конкретными методами установки" раздела [Необходимые условия для развертывания клиентов на компьютерах с Windows](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md).  

    -   **Установка клиентов вручную** и предоставление свойств установки клиента посредством выполнения команды CCMSetup с соответствующими параметрами командной строки. К таким параметрам относятся следующие элементы.  

        -   Укажите точку управления или путь источника, из которого компьютер может скачать файлы установки. Для этого во время установки клиента укажите в командной строке CCMSetup свойство CCMSetup **/mp:=&lt;имя компьютера точки управления\>** или **/source:&lt;путь к исходным файлам клиента\>** .  

        -   Укажите список исходных точек управления, которые должен использовать клиент для назначения сайту, а затем скачайте политику клиента и параметры сайта. Для этого используйте свойство SMSMP программы установки Client.msi CCMSetup.  

    -   **Опубликуйте точку управления в DNS или WINS** и настройте клиенты на использование этого метода нахождения службы.  

**Конфигурация порта для передачи данных между клиентами и серверами**. При установке клиента выполняется настройка используемых им портов на основе сведений, хранящихся в Active Directory. Если вы впоследствии измените порт обмена данными между клиентом и сервером для сайта, клиент сможет получить данные о новом порте из доменных служб Active Directory.  

-   **Обходные пути**. Если схема не была расширена, используйте один из следующих параметров для предоставления новой конфигурации порта для существующих клиентов:  

    -   **Переустановите клиенты** с использованием параметров для настройки нового порта.  

    -   **Разверните на клиентских компьютерах пользовательский сценарий, который обновляет сведения о порте**. Если клиенты не могут обмениваться данными с сайтом из-за того, что был изменен порт, развертывать этот скрипт с помощью Configuration Manager нельзя. Например, можно использовать групповую политику.  

**Сценарии развертывания содержимого**. При создании содержимого на одном сайте и последующем развертывании этого содержимого на другом сайте в иерархии конечный сайт должен иметь возможность проверить подпись данных содержимого, если таковая имеется. Для этого необходим доступ к открытому ключу исходного сайта, где были созданы эти данные. При расширении схемы Active Directory для Configuration Manager открытый ключ сайта доступен всем сайтам в иерархии.  

-   **Обходной путь**. Если схема не была расширена, воспользуйтесь средством обслуживания иерархии **preinst.exe** для безопасного обмена сведениями о ключах между сайтами.  

     Например, если вы планируете создать содержимое на первичном сайте и развернуть его на вторичном сайте, который находится под другим первичным сайтом в иерархии, следует либо расширить схему Active Directory, чтобы вторичный сайт мог получить открытый ключ исходного первичного сайта, либо напрямую предоставить обоим сайтам доступ к ключам с помощью средства preinst.exe.  

## <a name="active-directory-attributes-and-classes"></a>Классы и атрибуты Active Directory  
При расширении схемы для Configuration Manager перечисленные ниже классы и атрибуты добавляются в схему и становятся доступными для всех сайтов Configuration Manager в этом лесу Active Directory.  

-   Атрибуты:  

    -   cn=mS-SMS-Assignment-Site-Code  

    -   cn=mS-SMS-Capabilities  

    -   cn=MS-SMS-Default-MP  

    -   cn=mS-SMS-Device-Management-Point  

    -   cn=mS-SMS-Health-State  

    -   cn=MS-SMS-MP-Address  

    -   cn=MS-SMS-MP-Name  

    -   cn=MS-SMS-Ranged-IP-High  

    -   cn=MS-SMS-Ranged-IP-Low  

    -   cn=MS-SMS-Roaming-Boundaries  
        Вкл.  

    -   cn=MS-SMS-Site-Boundaries  

    -   cn=MS-SMS-Site-Code  

    -   cn=mS-SMS-Source-Forest  

    -   cn=mS-SMS-Version  

-   Классы:  

    -   cn=MS-SMS-Management-Point  

    -   cn=MS-SMS-Roaming-Boundary-Range  

    -   cn=MS-SMS-Server-Locator-Point  

    -   cn=MS-SMS-Site  

> [!NOTE]
> 
>  Расширения схемы могут включать атрибуты и классы, которые переносятся из предыдущих версий продукта, но не используются Configuration Manager. Пример.  
> 
> 
> - Атрибут: cn=MS-SMS-Site-Boundaries  
>   -   Класс: cn=MS-SMS-Server-Locator-Point  

Актуальность приведенных выше списков можно проверить, просмотрев файл **ConfigMgr_ad_schema.LDF** в папке **\SMSSETUP\BIN\x64** на установочном носителе Configuration Manager.  
