---
title: Назначение клиентов сайту
titleSuffix: Configuration Manager
description: Назначение клиентских компьютеров сайту в Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: ba9b623f-6e86-4006-93f2-83d563de0cd0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ab2270435ac13585cb0b7d3271f1faa02cc728d3
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075750"
---
# <a name="how-to-assign-clients-to-a-site-in-configuration-manager"></a>Назначение клиентских компьютеров сайту в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

После установки клиента Configuration Manager его необходимо присоединить к первичному сайту Configuration Manager, прежде чем им можно будет управлять. Сайт, к которому присоединяется клиент, называется *назначенным сайтом*. Клиентов нельзя назначать сайту центра администрирования или вторичному сайту.  

Процесс назначения происходит после успешной установки клиента и определяет сайт, который управляет клиентским компьютером. Клиент можно назначить сайту вручную либо использовать автоматическое назначение сайта, при котором клиент автоматически обнаруживает подходящий сайт на основании текущего сетевого расположения. Кроме того, можно назначить клиент резервному сайту, настроенному для иерархии.

При установке клиента мобильного устройства в ходе регистрации Configuration Manager устройство всегда автоматически назначается сайту. При установке клиента на компьютере можно решить, будет ли он назначен сайту. Если клиент установлен, но не назначен, он является неуправляемым до назначения сайту.  
 

> [!NOTE]  
>  Всегда назначайте клиенты сайтам с той же версией Configuration Manager. Не следует назначать клиент Configuration Manager более новой версии сайту более старой версии.   При необходимости обновите первичный сайт до версии Configuration Manager, используемой для клиентов.  

После назначения клиента сайту назначение сохраняется, даже если клиент меняет свой IP-адрес и перемещается на другой сайт. Только администратор может вручную назначить клиент другому сайту или удалить назначение клиента.  

> [!WARNING]  
>  Исключением, когда клиент остается назначенным сайту, является назначение клиента на устройстве с Windows Embedded при включенных фильтрах записи. Если не отключить фильтры записи перед назначением клиента, при следующем перезапуске устройства будет установлено исходное состояние назначения клиента.  
>   
>  Например, если клиент настроен для автоматического назначения, то при перезапуске произойдет повторное назначение, и клиент может быть назначен другому сайту. Если клиент не настроен для автоматического назначения, но требует назначения вручную, необходимо вручную переназначить клиент после запуска. Только после этого можно будет управлять этим клиентом с помощью Configuration Manager.  
>   
>  Чтобы избежать такой ситуации, отключите фильтры записи перед назначением клиента на встроенных устройствах, а затем, убедившись, что назначение прошло успешно, снова включите фильтры записи.  

Если назначение клиента завершается неудачей, программное обеспечение клиента остается установленным, но будет неуправляемым. Клиент считается неуправляемым, когда он установлен, но не назначен сайту, или назначен сайту, но не может связываться с точкой управления.  

##  <a name="using-manual-site-assignment-for-computers"></a>Назначение сайта компьютерам вручную  
 Можно вручную назначить клиентские компьютеры сайту следующими двумя способами.  

-   Свойство установки клиента, указывающее код сайта.  

-   В панели управления в узле **Configuration Manager**укажите код сайта.  

> [!NOTE]  
>  Если вручную назначить клиентский компьютер коду сайта Configuration Manager, который не существует, назначение сайта завершится сбоем.   

##  <a name="using-automatic-site-assignment-for-computers"></a><a name="BKMK_AutomaticAssignment"></a> Автоматическое назначение сайта компьютерам  
 Автоматическое назначение сайта может осуществляться во время развертывания клиента или при нажатии кнопки **Найти сайт** на вкладке **Дополнительно** окна **Свойства Configuration Manager** на панели управления. Клиент Configuration Manager сравнивает свое сетевое расположение с границами сайта, настроенными в иерархии Configuration Manager. Если сетевое расположение клиента находится в рамках группы границ, для которой включено назначение сайта, или иерархия настроена для резервного сайта, клиент автоматически привязывается к данному сайту без необходимости указывать код сайта.  

 Чтобы настроить границы, используйте один или несколько элементов, перечисленных ниже.  

-   IP-подсеть  

-   Сайт Active Directory  

-   Префикс IPv6  

-   Диапазон IP-адресов  

> [!NOTE]  
>  Если у клиента Configuration Manager несколько сетевых адаптеров и, следовательно, несколько IP-адресов, IP-адрес, используемый для определения назначения сайта клиенту, присваивается случайным образом.  

 Сведения о настройке групп границ для назначения сайта и настройке резервного сайта для автоматического назначения см. в разделе [Определение границ сайта и групп границ для Configuration Manager](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

 Клиенты Configuration Manager, использующие автоматическое назначение, пытаются найти группы границ сайта, опубликованные в доменных службах Active Directory. Если этот метод не дает результата (например, схема Active Directory не расширена для Configuration Manager или клиенты являются компьютерами рабочей группы), тогда клиенты могут найти сведения о группах границ в точке управления.  

 Можно указать точку управления для использования клиентами при их установке. Также клиенты могут обнаруживать точку управления с помощью публикации DNS или WINS.  

 Если клиент не может найти сайт, связанный с группой границ, содержащей его сетевое расположение, а в иерархии нет резервного сайта, клиент пытается выполнить это действие каждые 10 минут до тех пор, пока не происходит его назначение сайту.  

 Клиентские компьютеры Configuration Manager не могут быть автоматически назначены сайту в любом из перечисленных ниже случаев. Такое назначение должно выполняться вручную.  

-   Клиенты уже назначены сайту.  

-   Они находятся в Интернете или настроены как клиенты только для Интернета.  

-   Их сетевое расположение не попадает ни в одну из настроенных групп границ в иерархии Configuration Manager, а резервный сайт в иерархии отсутствует.  

##  <a name="completing-site-assignment-by-checking-site-compatibility"></a>Завершение назначения сайта с помощью проверки совместимости сайта  
 После обнаружения клиентом назначенного сайта происходит проверка версии и ОС клиента, которая позволяет убедиться в том, что сайт Configuration Manager сможет им управлять. Например, Configuration Manager не может управлять клиентами Configuration Manager 2007, клиентами System Center 2012 Configuration Manager или клиентами с ОС Windows 2000.  

 Назначение сайта завершается неудачей, если назначить клиент с Windows 2000 сайту Configuration Manager. Назначение клиента Configuration Manager 2007 или System Center 2012 Configuration Manager сайту Configuration Manager (Current Branch) выполняется успешно для поддержки автоматического обновления клиента. Тем не менее, пока клиенты более старого поколения не обновлены до Configuration Manager (Current Branch), Configuration Manager не сможет управлять таким клиентом с помощью параметров, приложений и обновлений программного обеспечения.  

> [!NOTE]  
>  Чтобы назначить клиент Configuration Manager 2007 или System Center 2012 Configuration Manager сайту Configuration Manager (Current Branch), необходимо настроить автоматическое обновление клиента для иерархии. Дополнительные сведения см. в разделе [Обновление клиентов для компьютеров Windows](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

Configuration Manager также проверяет, назначен ли клиент Configuration Manager (Current Branch) сайту, поддерживающему эту версию. Приведенные ниже сценарии могут возникнуть во время перехода с предыдущих версий Configuration Manager.  

- Сценарий: Вы использовали автоматическое назначение сайта, и текущие границы пересекаются с границами, определенными в предыдущей версии Configuration Manager.  

   В этом случае клиент автоматически пытается обнаружить сайт Configuration Manager (Current Branch).  

   Клиент сначала проверяет доменные службы Active Directory. При обнаружении опубликованного сайта Configuration Manager (Current Branch) сайт назначается успешно. Если данные не обнаруживаются (например, если сайт Configuration Manager не опубликован или компьютер является клиентом рабочей группы), то клиент осуществляет поиск сведений о сайте в назначенной ему точке управления.  

  > [!NOTE]  
  >  Вы можете назначить точку управления клиенту при установке клиента с помощью свойства Client.msi **SMSMP=&lt;имя_сервера>** .  

   Если оба этих способа не дают результата, автоматическое назначение сайта будет невозможно; в этом случае необходимо назначить клиент вручную.  

- Сценарий: Вы назначили клиент Configuration Manager (Current Branch) с помощью определенного кода сайта, а не автоматического назначения сайта и по ошибке указали код сайта для версии Configuration Manager, предшествующей версии System Center 2012 R2 Configuration Manager.  

   В этом случае произойдет сбой назначения сайта и необходимо будет вручную переназначить клиент сайту Configuration Manager (Current Branch).  

  Проверка совместимости сайта требует выполнения одного из следующих условий.  

- Клиент может получить доступ к сведениям о сайте, опубликованным в доменных службах Active Directory.  

- Клиент может связаться с точкой управления на сайте.  

  Если проверка совместимости сайта завершается неудачей, назначение сайта не осуществляется, и клиент остается неуправляемым до тех пор, пока проверка совместимости сайта не будет завершена успешно при повторном выполнении.  

  Исключением для выполнения проверки совместимости сайта является ситуация, когда клиент настроен для интернет-точки управления. В этом случае проверка совместимости сайта не проводится. При назначении клиента сайту, у которого есть системы сайта, расположенные в Интернете, и указании интернет-точки управления, убедитесь, что клиент назначается правильному сайту. Если клиент по ошибке был назначен сайту Configuration Manager 2007, сайту System Center 2012 Configuration Manager или сайту Configuration Manager, у которого нет ролей системы сайта управления интернет-клиентами, клиент будет неуправляемым.  

##  <a name="locating-management-points"></a>Поиск точек управления  
 После успешного назначения клиента сайту клиент обнаружит точку управления.  

 Клиентские компьютеры загружают список точек управления на сайте, к которому они могут подключиться. Это происходит при каждом перезапуске клиента, через каждые 25 часов, а также при обнаружении клиентом изменений в сети, например при отключении и повторном подключении компьютера к сети или при получении компьютером нового IP-адреса. Список включает точки управления в интрасети и их способность принимать подключения клиентов по протоколам HTTP и HTTPS. Если клиент находится в Интернете и у него еще нет списка точек управления, он подключается к указанной интернет-точке управления для получения списка точек управления. Если у клиента есть список точек управления для сайта, которому он назначен, происходит выбор точки для установки следующих подключений.  

-   Если клиент находится в интрасети, и у него есть подходящий действительный PKI-сертификат, клиент выбирает в первую очередь точки управления HTTPS, а затем – точки управления HTTP. Затем обнаруживается ближайшая по расположению в лесу точка управления.  

-   Если клиент находится в Интернете, он случайным образом выбирает одну из интернет-точек управления.  

Клиенты мобильных устройств, зарегистрированные с помощью Configuration Manager, могут подключаться только к одной точке управления на назначенном сайте и никогда не подключаются к точкам управления на вторичных сайтах. Эти клиенты всегда подключаются по протоколу HTTPS, а точки управления должны быть настроены для приема подключений клиентов через Интернет. Если для клиентов мобильных устройств на первичном сайте используется несколько точек управления, Configuration Manager случайным образом выбирает одну из этих точек управления при назначении, а клиент на мобильном устройстве продолжает использовать эту же точку управления.  

Если клиент загрузил политику клиента с точки управления своего назначенного сайта, то клиент становится управляемым.  

##  <a name="downloading-site-settings"></a>Загрузка параметров сайта  
 После успешного назначения сайта и нахождения клиентом своей точки управления клиентский компьютер, использующий доменные службы Active Directory для проверки совместимости своего сайта, загружает параметры сайта, связанные с клиентом, для использования с назначенным ему сайтом. Среди этих параметров, например, критерий выбора сертификата клиента, сведения о том. следует ли использовать список отзыва сертификатов, а также номера портов запросов клиентов. Клиент продолжает периодические проверки этих параметров.  

 Если клиентские компьютеры не могут получить параметры из доменных служб Active Directory, они загружаются из соответствующей точки управления. Клиентские компьютеры также могут получить параметры сайта, если они были установлены с помощью принудительной установки; эти параметры также можно указать вручную, используя свойства программы установки CCMSetup.exe. Дополнительные сведения о свойствах установки клиентов см. в разделе [Сведения о свойствах установки клиента](../../../core/clients/deploy/about-client-installation-properties.md).  

##  <a name="downloading-client-settings"></a>Загрузка параметров клиента  
 Все клиенты загружают политику параметров клиента по умолчанию и все применимые настраиваемые политики параметров. Центр программного обеспечения использует эти политики конфигурации для компьютеров под управлением Windows и уведомляет пользователей о том, что Центр программного обеспечения не может успешно работать до тех пор, пока не будут загружены данные сведения о конфигурации. В зависимости от того, как настроены параметры клиента, первоначальная загрузка параметров клиента может занять некоторое время, а некоторые задачи управления клиентом могут не работать до завершения этого процесса.  

##  <a name="verifying-site-assignment"></a>Проверка назначения сайта  
 Успешность назначения сайта можно проверить с помощью любого из приведенных ниже методов.  

-   Для клиентов на компьютерах с ОС Windows откройте компонент Configuration Manager на панели управления и убедитесь в том, что код сайта правильно отображается на вкладке **Сайт**.  

-   Для клиентских компьютеров в рабочей области **Активы и соответствие** в узле **Устройства** убедитесь в отображении значения **Да** в столбце **Клиент** и правильного кода первичного сайта в столбце **Код сайта**.  

-   Для мобильных клиентских устройств в рабочей области **Активы и соответствие** используйте коллекцию **Все мобильные устройства** , чтобы убедиться в отображении значения **Да** в столбце **Клиент** и правильного кода первичного сайта в столбце **Код сайта** .  

-   Используйте отчеты назначения клиентов и регистрации мобильных устройств.  

-   Для клиентских компьютеров используйте файл LocationServices.log на клиенте.  

##  <a name="roaming-to-other-sites"></a>Перемещение на другие сайты  
 Если клиентские компьютеры в интрасети назначены первичному сайту, но затем их расположение в сети меняется, так что они оказываются в группе границ, настроенной для другого сайта, такие компьютеры считаются перемещенными на другой сайт. Если этот сайт является вторичным по отношению к их назначенному сайту, клиенты могут использовать точку управления на вторичном сайте, чтобы загрузить клиентскую политику и отправить данные. Это позволяет избежать отправки данных по потенциально медленному сетевому подключению. Если же эти клиенты перемещаются в границы другого первичного сайта либо вторичного сайта, не являющегося дочерним по отношению к их назначенному сайту, такие клиенты всегда используют точку управления на своем назначенном сайте для загрузки клиентской политики и отправки данных.  

 Эти клиентские компьютеры, перемещающиеся на другие сайты (все первичные и вторичные сайты), всегда могут использовать точки управления на других сайтах для запроса расположения содержимого. Точки управления на текущем сайте могут предоставить клиентам список точек распространения с содержимым, которое требуется клиентам.  

 Для клиентских компьютеров, настроенных для управления только через Интернет, а также для компьютеров Mac и мобильных устройств, зарегистрированных с помощью Configuration Manager, клиенты могут обмениваться данными только с точками управления на назначенном им сайте. Эти клиенты не могут подключаться к точкам управления на вторичных сайтах и на других первичных сайтах.  
