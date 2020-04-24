---
title: Общие сведения об обновлениях программного обеспечения
titleSuffix: Configuration Manager
description: Основные сведения об обновлениях программного обеспечения в Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 10/30/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9778b13-c8a3-40eb-8655-34ac8ce9cdaa
ms.openlocfilehash: c857997bdbeed51286e874dcbecf00b414dfe6a0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699962"
---
# <a name="introduction-to-software-updates-in-configuration-manager"></a>Общие сведения об обновлении программного обеспечения в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Обновления программного обеспечения в Configuration Manager предоставляют набор инструментов и ресурсов, которые могут помочь в решении сложной задачи отслеживания и установки обновлений программного обеспечения на клиентских компьютерах предприятия. Эффективный процесс управления обновлениями ПО необходим для поддержания высокой производительности работы, защиты от проблем безопасности и поддержания стабильности сетевой инфраструктуры. Однако постоянное развитие технологий и непрерывное возникновение новых угроз безопасности требует применения согласованного подхода к решению данных проблем, а также постоянного внимания к этой области.  

Пример возможного сценария, показывающий развертывание обновлений программного обеспечения в вашей среде, см. в разделе [Пример сценария развертывания обновлений программного обеспечения](../deploy-use/example-scenario-deploy-monitor-monthly-security-updates.md).  

##  <a name="software-updates-synchronization"></a><a name="BKMK_Synchronization"></a> Синхронизация обновлений программного обеспечения  
 Функция синхронизации обновлений программного обеспечения в Configuration Manager подключается к Центру обновления Майкрософт, чтобы получать метаданные обновлений. Сайт верхнего уровня (сайт центра администрирования или автономный первичный сайт) синхронизируется с Центром обновления Майкрософт согласно расписанию или при запуске синхронизации вручную с помощью консоли Configuration Manager. Когда Configuration Manager завершает синхронизацию обновлений ПО на сайте верхнего уровня, синхронизация обновлений ПО начинается на подчиненных сайтах, если они существуют. После завершения синхронизации на каждом из первичных или вторичных сайтов создается политика, с помощью которой клиентским компьютерам предоставляются сведения о расположении точек обновления программного обеспечения. Эта политика действует в масштабах всего сайта, на котором она размещена.  

> [!NOTE]  
>  Обновления программного обеспечения включены в параметрах клиента по умолчанию. Однако, если присвоить параметру клиента **Включить обновления программного обеспечения для клиентов** значение **Нет** , чтобы отключить обновления программного обеспечения для коллекции или в параметрах по умолчанию, то соответствующим клиентам не будет отправлено расположение точек обновления программного обеспечения. Подробные сведения см. в разделе [Параметры клиентов для обновлений программного обеспечения](../../core/clients/deploy/about-client-settings.md#software-updates).  

 Получив политику, клиент запускает процедуру проверки соответствия обновлений программного обеспечения требованиям и записывает собранные сведения в инструментарий управления Windows (WMI). Сведения о соответствии требованиям передаются точке управления, которая отправляет их серверу сайта. Дополнительные сведения об оценке соответствия требованиям см. в разделе [Software updates compliance assessment](#BKMK_SUMCompliance) этой статьи.  

 На первичном сайте можно установить несколько точек обновления программного обеспечения. Первая установленная точка обновления настраивается в качестве источника синхронизации. Она синхронизируется с Центром обновления Майкрософт или с сервером WSUS, расположенным вне иерархии Configuration Manager. Другие точки обновления программного обеспечения на этом сайте используют первую точку обновления программного обеспечения в качестве источника синхронизации.  

> [!NOTE]  
>  После завершения процесса синхронизации обновлений программного обеспечения на сайте верхнего уровня производится репликация метаданных обновлений программного обеспечения на дочерние сайты путем репликации базы данных. При подключении консоли Configuration Manager к подчиненному сайту Configuration Manager отображает метаданные обновлений ПО. Однако до тех пор, пока на сайте не будет установлена и настроена точка обновления программного обеспечения, клиенты не будут проверять соответствие обновлений ПО требованиям, а также передавать сведения о соответствии в Configuration Manager, и вы не сможете успешно развертывать обновления ПО.  

### <a name="synchronization-on-the-top-level-site"></a>Синхронизация на сайте верхнего уровня  
 Процедура синхронизации обновлений программного обеспечения на сайте верхнего уровня предусматривает получение от Microsoft Update метаданных обновлений программного обеспечения, которые соответствуют критериям, указанным в свойствах компонента "Точка обновления программного обеспечения". Критерии настраиваются только на сайте верхнего уровня.  

> [!NOTE]  
>  Вместо Центра обновления Майкрософт в качестве источника синхронизации можно указать существующий сервер WSUS, не входящий в иерархию Configuration Manager.  

 В следующем списке приведены основные этапы процедуры синхронизации на сайте верхнего уровня:  

1.  Запускается синхронизация обновлений программного обеспечения.  

2.  Диспетчер синхронизации WSUS отправляет запрос в службы WSUS, запущенные в точке обновления программного обеспечения, чтобы запустить синхронизацию с Центром обновления Майкрософт.  

3.  Метаданные обновлений ПО синхронизируются с Центром обновления Майкрософт, все изменения добавляются в базу данных WSUS или обновляются в ней.  

4.  После того как WSUS завершает синхронизацию, диспетчер синхронизации WSUS синхронизирует метаданные обновлений ПО, хранимые в базе данных WSUS, с базой данных Configuration Manager, и любые изменения с момента последней синхронизации попадают в эту базу путем вставки или обновления. Метаданные обновлений программного обеспечения хранятся в базе данных сайта в качестве элемента конфигурации.  

5.  Элементы конфигурации для обновлений программного обеспечения пересылаются дочерним сайтам с помощью репликации базы данных.  

6.  После успешного завершения синхронизации диспетчер синхронизации WSUS создает сообщение о состоянии 6702.  

7.  Диспетчер синхронизации WSUS отправляет запрос на синхронизацию на все дочерние сайты.  

8.  Диспетчер синхронизации WSUS по очереди направляет запросы серверам WSUS, работающим на других точках обновления программного обеспечения этого сайта. Серверы WSUS на других точках обновления программного обеспечения настроены в качестве реплик сервера WSUS, запущенного на точке обновления программного обеспечения по умолчанию, предусмотренной для этого сайта.  

### <a name="synchronization-on-child-primary-and-secondary-sites"></a>Синхронизация на дочерних первичных и вторичных сайтах  
 В ходе процедуры синхронизации обновлений программного обеспечения на сайте верхнего уровня происходит репликация элементов конфигурации обновлений программного обеспечения на дочерние сайты с помощью репликации базы данных. После завершения этой процедуры сайт верхнего уровня отправляет дочернему сайту запрос на синхронизацию, а дочерний сайт запускает синхронизацию WSUS. Следующий список содержит базовые шаги процесса синхронизации на дочернем первичном сайте или на вторичном сайте.  

1.  Диспетчер синхронизации WSUS получает запрос на синхронизацию от сайта верхнего уровня.  

2.  Запускается синхронизация обновлений программного обеспечения.  

3.  Диспетчер синхронизации WSUS отправляет запрос в службы WSUS, запущенные в точке обновления программного обеспечения, чтобы запустить синхронизацию.  

4.  Службы WSUS, запущенные в точке обновления ПО на дочернем сайте, выполняют синхронизацию метаданных обновлений со службами WSUS, запущенными в точке обновления на родительском сайте.  

5.  После успешного завершения синхронизации диспетчер синхронизации WSUS создает сообщение о состоянии 6702.  

6.  Работающий на первичном сайте диспетчер синхронизации WSUS отправляет запрос синхронизации всем дочерним вторичным сайтам. Вторичные сайты запускают процесс синхронизации обновлений программного обеспечения с родительским первичным сайтом. Вторичный сайт настраивается в качестве реплики сервера WSUS, запущенного на родительском сайте.  

7.  Диспетчер синхронизации WSUS по очереди направляет запросы серверам WSUS, работающим на других точках обновления программного обеспечения этого сайта. Серверы WSUS на других точках обновления программного обеспечения настроены в качестве реплик сервера WSUS, запущенного на точке обновления программного обеспечения по умолчанию, предусмотренной для этого сайта.  

##  <a name="software-updates-compliance-assessment"></a><a name="BKMK_SUMCompliance"></a> Software updates compliance assessment  
 Перед развертыванием обновлений ПО на клиентских компьютерах в Configuration Manager необходимо запустить проверку соответствия обновлений ПО требованиям на клиентских компьютерах. Для каждого обновления ПО создается сообщение о состоянии, содержащее состояние соответствие этого обновления ПО требованиям. Сообщения о состоянии отправляются пакетами на точку управления, а затем на сервер сайта, где данные состояния соответствия требованиям добавляются в базу данных сайта. Состояние соответствия обновлений программного обеспечения требованиям отображается в консоли Configuration Manager. Можно развернуть и установить обновления ПО на компьютерах, которым требуются эти обновления. В следующих разделах содержатся сведения о состояниях соответствия требованиям и описывается процесс проверки соответствия обновлений ПО.  

### <a name="software-updates-compliance-states"></a>Состояния соответствия обновлений программного обеспечения  
 Ниже перечисляются и описываются все состояния соответствия требованиям, которые отображаются в консоли Configuration Manager для обновлений ПО.  

-   **Обязательное**  

     Указывает, что обновление программного обеспечения применимо и требуется на клиентском компьютере. Если обновление ПО имеет состояние **Требуется**, то может выполняться любое из перечисленных ниже условий.  

    -   Обновление ПО не развернуто на клиентском компьютере.  

    -   Обновление ПО установлено на клиентском компьютере. Однако наиболее актуальное сообщение о состоянии еще не добавлено в базу данных на сервере сайта. Клиентский компьютер повторно проверяет наличие обновления ПО после завершения установки. Возможна задержка на одну или две минуты, возникающая перед отправкой клиентом обновленного состояния на точку управления, которая затем пересылает обновленное состояние серверу сайта.  

    -   Обновление ПО установлено на клиентском компьютере. Однако установка точки обновления требует перезапуска компьютера перед завершением обновления.  

    -   Точка обновления развернута на клиентском компьютере, но еще не установлена.  

-   **Не требуется**  

     Указывает на неприменимость этого обновления программного обеспечения к клиентскому компьютеру. В связи с этим обновление программного обеспечения не требуется.  

-   **Установлено**  

     Указывает, что обновление программного обеспечения применимо и уже установлено на клиентском компьютере.  

-   **Неизвестно**  

     Указывает, что сервер сайта не получил сообщение о состоянии от клиентского компьютера, как правило, по одной из следующих причин.  

    -   На клиентском компьютере не выполнена проверка обновлений ПО на соответствие требованиям.  

    -   Сканирование успешно завершено на клиентском компьютере. Однако сообщение о состоянии еще не обработано сервером сайта, возможная причина – наличие журнала ожидания сообщений о состоянии.  

    -   Проверка обновлений на соответствие требованиям на клиентском компьютере успешно завершена, но не получено сообщение о состоянии с дочернего сайта.  

    -   Проверка обновлений на соответствие требованиям на клиентском компьютере успешно завершена, но сообщение о состоянии было повреждено, и его не удалось обработать.  

### <a name="scan-for-software-updates-compliance-process"></a>Процесс проверки соответствия обновлений программного обеспечения  
 В ходе установки и синхронизации точки обновления программного обеспечения создается политика компьютера, которая действует на уровне всего сайта и сообщает клиентским компьютерам о том, что для сайта включено обновление программного обеспечения с помощью Configuration Manager. Когда клиент получает политику компьютера, запуск проверки соответствия требованиям планируется на произвольный момент времени в течение двух следующих часов. При запуске проверки процесс агента клиента обновлений очищает историю проверки, отправляет запрос на поиск сервера WSUS, который нужно использовать для проверки, и обновляет локальную групповую политику, указывая расположение сервера WSUS.  

> [!NOTE]  
>  Интернет-клиенты должны подключаться к серверу WSUS по протоколу SSL.  

 Запрос на проверку передается агенту обновления Windows (WUA). Затем WUA подключается к указанному в локальной политике расположению сервера WSUS, получает метаданные обновлений программного обеспечения, синхронизированные с сервером WSUS, и сканирует клиентский компьютер на наличие обновлений. Процесс агента клиента обновлений программного обеспечения обнаруживает, что проверка соответствия требованиям завершена, и создает сообщения о состоянии для каждого обновления ПО, состояние соответствия требованиям которого изменилось после последней проверки. Пакеты сообщений о состоянии отправляются на точку управления каждые 15 минут. Затем точка управления передает сообщения состояния на сервер сайта, где они записываются в базу данных сервера сайта.  

 После первоначальной проверки соответствия обновлений ПО требованиям дальнейшие проверки запускаются по заданному расписанию. Однако, если клиент был просканирован на соответствие требованиям обновлений программного обеспечения до истечения периода времени, указанного в параметре истечения срока ожидания (TTL), то клиент использует локально хранимые метаданные обновлений программного обеспечения. Если последнее сканирование происходит после истечения времени TTL, то клиент должен подключиться к серверу WSUS, запущенному на точке обновления программного обеспечения, и обновить хранящиеся на клиенте метаданные обновлений программного обеспечения.  

 Проверка соответствия обновлений ПО требованиям может быть запущена в следующих случаях (в том числе и по расписанию проверки).  

-   **Расписание проверки обновлений программного обеспечения**. Сканирование для проверки соответствия требованиям обновлений программного обеспечения начинается согласно расписанию сканирования, настроенному в параметрах агента клиента обновлений программного обеспечения. Дополнительные сведения о настройке параметров клиента обновлений ПО см. в разделе [Параметры клиента обновления программного обеспечения](../../core/clients/deploy/about-client-settings.md#software-updates).  

-   **Действие на странице свойств Configuration Manager**. Пользователь может запустить действие **Цикл проверки обновлений программ** или **Цикл оценки развертывания обновлений программ** на вкладке **Действие** в диалоговом окне **Свойства Configuration Manager** на клиентском компьютере.  

-   **Расписание повторной оценки развертывания**. Оценка и проверка развертывания на соответствие обновлений требованиям запускается по расписанию повторной проверки развертывания, настроенному в параметрах агента клиента обновлений. Дополнительные сведения о параметрах клиента обновлений ПО см. в разделе [Параметры клиента обновления программного обеспечения](../../core/clients/deploy/about-client-settings.md#software-updates).  

-   **Перед загрузкой файлов обновлений**. Когда клиентский компьютер получает политику назначения для нового обязательного развертывания, агент клиента обновлений ПО загружает файлы обновлений ПО в локальный кэш клиента. Перед загрузкой файлов обновлений ПО агент клиента обновлений ПО запускает проверку, чтобы убедиться, что данное обновление ПО по-прежнему требуется.  

-   **Перед установкой обновления программного обеспечения**. Непосредственно перед установкой обновления агент клиента обновлений ПО запускает проверку, чтобы убедиться, что данное обновление ПО по-прежнему требуется.  

-   **После установки обновления программного обеспечения**. Сразу после завершения установки обновления ПО агент клиента обновлений ПО запускает проверку, чтобы убедиться, что данное обновление больше не требуется, и создает новое сообщение о состоянии, указывающее, что данное обновление ПО установлено. Если установка завершена, но требуется перезапуск, сообщение о состоянии будет указывать, что клиентский компьютер ожидает перезапуска.  

-   **После перезапуска системы**. Если клиентский компьютер ожидает перезапуска для завершения установки обновления ПО, агент клиента обновлений ПО запускает проверку после перезапуска, чтобы убедиться, что данное обновление больше не требуется, и создает новое сообщение о состоянии, указывающее, что данное обновление установлено.  

#### <a name="time-to-live-value"></a>Значение срока жизни  
 Метаданные об обновлениях ПО, необходимые для проверки обновлений ПО на соответствие требованиям, хранятся на локальном клиентском компьютере и по умолчанию действительны в течение 24 часов. Это значение называется сроком жизни.  

#### <a name="scan-for-software-updates-compliance-types"></a>Типы проверки соответствия обновлений программного обеспечения  
 Клиент проверяет соответствие обновлений ПО требованиям с помощью интерактивной или автономной проверки и принудительной или необязательной проверки (в зависимости от того, как была создана проверка соответствия обновлений ПО). Ниже описываются интерактивные и автономные способы запуска проверки, а также указывается, является ли проверка принудительной.  

-   **Расписание проверки обновлений программного обеспечения** (необязательная проверка в подключенном режиме)  

     В соответствии с настроенным расписанием повторной оценки развертывания клиент подключается к службам WSUS, запущенным на активной точке обновления ПО, для получения метаданных об обновлениях ПО, только если последняя проверка была выполнена после истечения срока жизни.  

-   **Цикл проверки обновлений программ** или **Цикл оценки развертывания обновлений программ** (принудительная проверка в подключенном режиме)  

     Компьютер клиента всегда подключается к серверу WSUS, запущенному на точке обновления программного обеспечения, для получения метаданных обновлений программного обеспечения прежде, чем компьютер клиента выполняет проверку соответствия обновлений программного обеспечения установленным требованиям. После завершения сканирования счетчик срока жизни обнуляется. Например, если значение срока жизни равно 24 часам, то после выполнения пользователем проверки обновлений ПО на соответствие требованиям значение срока жизни сбрасывается на 24 часа.  

-   **Расписание повторной оценки развертывания** (необязательная проверка в подключенном режиме)  

     В соответствии с настроенным расписанием повторной оценки развертывания клиент подключается к службам WSUS, запущенным на активной точке обновления ПО, для получения метаданных об обновлениях ПО, только если последняя проверка была выполнена после истечения срока жизни.  

-   **Перед загрузкой файлов обновлений** (необязательная проверка в подключенном режиме)  

     Перед началом загрузки файлов обновлений в требуемых развертываниях клиент подключается к службам WSUS, запущенным на активной точке обновления ПО, для получения метаданных об обновлениях ПО, только если последняя проверка была выполнена после истечения срока жизни.  

-   **Перед установкой обновления программного обеспечения** (необязательная проверка в подключенном режиме)  

     Перед началом установки файлов обновлений программного обеспечения в требуемых развертываниях клиент подключается к службам WSUS, запущенным на активной точке обновления ПО, для получения метаданных об обновлениях ПО, только если последняя проверка была выполнена после истечения срока жизни.  

-   **После установки обновления программного обеспечения** (принудительная автономная проверка)  

     После установки обновления ПО агент клиента обновлений ПО начинает проверку, используя локальные метаданные. Клиент никогда не подключается к службам WSUS, запущенным на активной точке обновления ПО, для получения метаданных обновлений программного обеспечения.  

-   **После перезапуска системы** (принудительная автономная проверка)  

     После установки обновления программного обеспечения и перезапуска компьютера агент клиента обновлений ПО начинает проверку, используя локальные метаданные. Клиент никогда не подключается к службам WSUS, запущенным на активной точке обновления ПО, для получения метаданных обновлений программного обеспечения.  

##  <a name="software-update-deployment-packages"></a><a name="BKMK_DeploymentPackages"></a> Пакеты развертывания обновлений программного обеспечения  
 Пакет развертывания обновлений программного обеспечения — это средство для загрузки обновлений ПО в общую сетевую папку и для копирования исходных файлов обновлений ПО в библиотеку содержимого на серверах сайта и в точках распространения, указанных в развертывании. С помощью мастера загрузки обновлений можно загружать обновления ПО и добавлять их в пакеты развертывания перед развертыванием. Этот мастер позволяет подготавливать обновления ПО в точках распространения и проверять успешность этого этапа процесса развертывания перед развертыванием обновлений ПО на клиентах.  

 После развертывания загруженных обновлений ПО с помощью мастера развертывания обновлений развертывание автоматически использует пакет развертывания, содержащий обновления программного обеспечения. При развертывании обновлений ПО, которые не были загружены, необходимо указать новый или существующий пакет развертывания в мастере развертывания обновлений программного обеспечения. В этом случае обновления ПО будут загружены после завершения работы мастера.  

> [!IMPORTANT]  
>  Необходимо вручную создать общую сетевую папку для исходных файлов пакета развертывания, а затем указать эту папку в мастере. Каждый пакет развертывания должен использовать отдельную общую сетевую папку.  

> [!IMPORTANT]  
>  Для учетных записей компьютера поставщика SMS и пользователя с правами администратора, который фактически загружает обновления ПО, требуются права на **запись** для источника пакета. Следует ограничить доступ к источнику пакета, чтобы снизить риск подмены злоумышленником исходных файлов обновления ПО.  

 При создании нового пакета развертывания до загрузки любых обновлений ПО для содержимого устанавливается номер версии 1. При загрузке файлов обновления программного обеспечения с использованием пакета версия содержимого увеличивается до 2. Поэтому у всех новых пакетов развертывания версия содержимого равняется 2. При каждом изменении содержимого в пакете развертывания версия содержимого увеличивается на 1. Дополнительные сведения о см. в разделе [Основные принципы управления содержимым](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

 Клиенты устанавливают обновления программного обеспечения в развертывании с помощью любой точки распространения, в которой доступны обновления ПО, вне зависимости от пакета развертывания. Даже если пакет развертывания удален из активного развертывания, клиенты могут по-прежнему устанавливать обновления, содержащиеся в этом развертывании, если каждое обновление загружено по крайней мере в еще один пакет развертывание и доступно в точке распространения, доступной для клиента. После удаления последнего пакета развертывания с обновлением клиентские компьютеры не смогут получать это обновление, пока оно не будет снова загружено в пакет развертывания. Если файлы обновлений ПО отсутствуют в пакетах развертывания, то такие обновления отображаются в консоли Configuration Manager с красной стрелкой. Развертывания отображаются с двойной красной стрелкой, если они содержат обновления ПО в таком состоянии.  

##  <a name="software-update-deployment-workflows"></a><a name="BKMK_DeploymentWorkflows"></a> Рабочие процессы развертывания обновлений программного обеспечения  
 Существует два основных сценария развертывания обновлений программного обеспечения в среде: развертывание вручную и автоматическое развертывание. Как правило, обновления развертываются вручную с целью создания базовой инфраструктуры для клиентских компьютеров, а затем с помощью автоматического развертывания осуществляется управление установкой обновлений на клиенты. В следующих разделах приводятся сводные данные о рабочем процессе для ручного и автоматического развертывания обновлений программного обеспечения.  

###  <a name="manual-deployment-of-software-updates"></a><a name="BKMK_ManualDeployment"></a> Ручное развертывание обновлений программного обеспечения  
 При развертывании обновлений ПО вручную необходимо выбирать обновления с помощью консоли Configuration Manager и затем вручную запускать процесс развертывания. Такой способ развертывания обычно используется для установки на клиентские компьютеры текущих обязательных обновлений ПО перед созданием правил автоматического развертывания, которые будут управлять ежемесячным развертыванием обновлений, и для внешнего развертывания обновлений. В следующем списке приводится описание общего процесса ручного развертывания обновлений программного обеспечения.  

1.  Фильтр для обновлений программного обеспечения, использующих определенные требования. Например, можно создать условие, обеспечивающее получение всех обновлений безопасности или других важных обновлений, необходимых для более чем 50 клиентских компьютеров.  

2.  Создайте группу обновления программного обеспечения, которая содержит обновления программного обеспечения.  

3.  Загрузите содержимое обновлений программного обеспечения в группе обновлений программного обеспечения.  

4.  Вручную разверните группу обновления программного обеспечения.  

###  <a name="automatic-deployment-of-software-updates"></a><a name="BKMK_AutomaticDeployment"></a> Автоматическое развертывание обновлений программного обеспечения  
 Автоматическое развертывание обновлений настраивается с помощью правила автоматического развертывания (ADR). Такой метод развертывания, как правило, используется для ежемесячных обновлений программного обеспечения (обычно во второй вторник каждого месяца) и для управления обновлениями определений. При выполнении правила обновления программного обеспечения удаляются из группы обновления программного обеспечения (если используется существующая группа), обновления программного обеспечения, удовлетворяющие указанным критериям (например, все обновления программного обеспечения безопасности, выпущенные за последнюю неделю), добавляются в группу обновлений программного обеспечения, файлы содержимого для обновлений программного обеспечения загружаются и копируются в точки распространения, а затем обновления программного обеспечения развертываются на клиентских компьютерах в целевой коллекции. В следующем списке приводится описание общего процесса автоматического развертывания обновлений программного обеспечения.  

1. Создается правило автоматического развертывания, определяющее следующие параметры развертывания:  

   -   Целевая коллекция  

   -   Принятие решения о том, что необходимо включить – развертывание или отчеты о соответствии обновлений для клиентских компьютеров в целевой коллекции.  

   -   Условия обновления программного обеспечения  

   -   Расписания оценки и развертывания  

   -   Взаимодействие с пользователем  

   -   Загрузка свойств  

2. Обновления программного обеспечения добавляются к группе обновления программного обеспечения.  

3. Группа обновлений программного обеспечения развертывается на клиентских компьютерах в целевой коллекции, если она указана.  

   Необходимо определить, какая стратегия развертывания будет использоваться в среде. Например, можно создать правило автоматического развертывания и указать в качестве цели коллекцию тестовых клиентов. После проверки установки обновлений в тестовой группе можно добавить в правило новое развертывание или указать другую коллекцию в существующем развертывании, чтобы охватить большее число клиентов. Объекты обновления программного обеспечения, создаваемые правилами автоматического развертывания, являются интерактивными.  

- Обновления программного обеспечения, которые были развернуты с помощью правила автоматического развертывания, автоматически развертываются на новых клиентах, включенных в целевую коллекцию.  

- Новые обновления, добавленные в группу обновления программного обеспечения, автоматически развертываются на клиентах в целевой коллекции.  

- Развертывания для правила автоматического развертывания можно включать и отключать в любое время.  

  После создания правила автоматического развертывания к нему можно добавить дополнительные развертывания. Это позволяет управлять сложным процессом развертывания различных обновлений для разных коллекций. Каждое новое развертывание имеет полный набор функций и средств мониторинга развертывания, а также:  

- использует те же группу и пакет обновлений, который создается при первом запуске ADR;  

- может указывать другую коллекцию;  

- поддерживает уникальные свойства развертывания, в том числе:  

  -   время активации;  

  -   Крайний срок  

  -   отображение или скрытие взаимодействия с конечным пользователем;  

  -   отдельные предупреждения для этого развертывания.  

##  <a name="software-update-deployment-process"></a><a name="BKMK_DeploymentProcess"></a> Процесс развертывания обновлений программного обеспечения  
 После развертывания обновлений программного обеспечения или при развертывании обновлений правилом автоматического развертывания к политике компьютера сайта добавляется политика назначения развертываний. Обновления программного обеспечения загружаются из расположения загрузки, Интернета или общей сетевой папки в исходную папку пакета. Обновления копируются из исходной папки пакета в библиотеку содержимого на сервере сайта, после чего они копируются в библиотеку содержимого на точке распространения.  

 Когда клиентский компьютер в целевой коллекции развертывания получает политику компьютера, агент клиента обновления программного обеспечения запускает оценочное сканирование. Агент клиента скачивает содержимое требуемых обновлений программного обеспечения из точки распространения в локальный кэш клиента, руководствуясь параметром развертывания **Время доступности программного обеспечения**, после чего обновления становятся доступными для установки. Обновления программного обеспечения для необязательных развертываний (развертываниях, для которых не задан срок установки) не загружаются до тех пор, пока пользователь не запустит установку вручную.  

 По истечении заданного срока агент клиента обновления программного обеспечения выполняет сканирование для проверки того, что обновления все еще требуются. Затем выполняется проверка локального кэша на клиентском компьютере с целью подтверждения доступности исходных файлов обновления. Наконец, клиент устанавливает обновления программного обеспечения. Если содержимое было удалено из кэша клиента с целью освобождения дискового пространства для другого развертывания, клиент повторно загружает обновления из точки распространения в кэш клиента. Обновления программного обеспечения всегда загружаются в кэш клиента, независимо от заданного максимального размера кэша. После завершения установки агент клиента проверяет отсутствие требуемых обновлений программного обеспечения, а затем отправляет сообщение состояния для точки управления, в котором указывается факт завершения установки обновлений программного обеспечения на клиенте.  

### <a name="required-system-restart"></a>Обязательная перезагрузка системы  
 Перезапуск системы производится по умолчанию, когда он необходим для завершения установки обновлений программного обеспечения на компьютере клиента с помощью обязательного развертывания. Для всех обновлений программного обеспечения, которые были установлены до наступления крайнего срока, автоматический перезапуск системы откладывается до этого момента, если только перезапуск компьютера не производится раньше по какой-либо другой причине. Можно подавить перезагрузку системы для серверов и рабочих станций. Соответствующие параметры настраиваются на странице **Взаимодействие с пользователем** мастера развертывания обновлений программного обеспечения или мастера создания правил автоматического обновления.  

### <a name="deployment-reevaluation-cycle"></a>Цикл переоценки развертывания  
 По умолчанию клиентские компьютеры запускают цикл переоценки развертывания каждые 7 дней. В ходе этого цикла оценки компьютер клиента проверяет наличие ранее развернутых и установленных обновлений программного обеспечения. Если какие-либо обновления не обнаруживаются, они переустанавливаются из локального кэша. Если обновление больше не доступно в локальном кэше, оно загружается из точки распространения, поле чего происходит его установка. Расписание повторной оценки можно настроить на странице **Обновления программного обеспечения** параметров клиента для сайта.  

##  <a name="support-for-windows-embedded-devices-that-use-write-filters"></a><a name="BKMK_EmbeddedDevices"></a> Поддержка устройств Windows Embedded, использующих фильтры записи  
 При развертывании обновлений программного обеспечения на устройства Windows Embedded с включенными фильтрами записи вы можете указать необходимость отключения фильтров записи на устройстве в ходе развертывания, а после развертывания перезапустить устройство. Если фильтр записи не отключен, то программное обеспечение развертывается во временный оверлей, а его установка не будет завершена после перезапуска устройства, если только другое развертывание не обеспечит принудительного применения изменений.  

> [!NOTE]  
>  При развертывании обновления программного обеспечения на устройство Windows Embedded убедитесь, что устройство входит в коллекцию, для которой настроено окно обслуживания. Это позволит управлять включением и отключением фильтра записи, а также перезапуском устройства.  

 Элемент пользовательского интерфейса, отвечающий за режим работы фильтра записи, представляет собой флажок под названием **Зафиксировать изменения после истечения крайнего срока или в окне обслуживания (необходим перезапуск)** .  

 Дополнительные сведения о том, как Configuration Manager управляет устройствами Windows Embedded с фильтрами записи, см. в разделе [Планирование развертывания клиентов на устройствах Windows Embedded](../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

##  <a name="extend-software-updates-in-configuration-manager"></a><a name="BKMK_ExtendSoftwareUpdates"></a> Расширение обновлений программного обеспечения в Configuration Manager  
 Используйте System Center Updates Publisher для управления обновлениями программного обеспечения, недоступными в Центре обновления Майкрософт. После завершения публикации обновлений ПО на сервере обновлений и синхронизации обновлений ПО в Configuration Manager можно развернуть обновления ПО на клиентах Configuration Manager. Дополнительные сведения об Updates Publisher см в статье [Updates Publisher 2011](https://go.microsoft.com/fwlink/p/?LinkId=252947).  

## <a name="next-steps"></a>Дальнейшие шаги
[Планирование обновлений программного обеспечения](../plan-design/plan-for-software-updates.md)