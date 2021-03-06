---
title: Создание носителя последовательности задач
titleSuffix: Configuration Manager
description: Создание носителя последовательности задач для развертывания операционной системы на конечном компьютере в окружении Configuration Manager.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87d5df6edee2adba32f1a49b8e867e930386b4df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690602"
---
# <a name="create-task-sequence-media"></a>Создание носителя последовательности задач

*Область применения: Configuration Manager (Current Branch)*

С помощью носителя можно создать образ операционной системы на основе компьютера-образца или развернуть ОС на конечном компьютере в окружении Configuration Manager. В качестве носителя может применяться набор компакт-дисков, DVD-дисков или USB-устройство флэш-памяти.  

Носители используются преимущественно для развертывания операционных систем на конечных компьютерах, не имеющих достаточно быстрого сетевого подключения к сайту Configuration Manager. Но этот же носитель вы можете применить и для развертывания операционной системы за пределами существующей ОС Windows. Этот метод полезен в тех случаях, когда операционная система отсутствует или не работает, а также для повторного разбиения жесткого диска на разделы.  

Носителями развертывания могут быть загрузочные носители, автономные носители и предварительно подготовленные носители. Содержимое будет разным в зависимости от типа используемого носителя. Например, автономный носитель содержит последовательность задач для развертывания ОС. Другие типы носителей получают последовательности задач из точки управления.  

> [!IMPORTANT]  
> Чтобы создать носитель с последовательностью задач, необходимо быть администратором компьютера, на котором выполняется консоль Configuration Manager. Если вы не являетесь администратором, вам будет предложено ввести учетные данные администратора при запуске мастера создания носителя с последовательностью задач.  


## <a name="capture-media"></a><a name="BKMK_PlanCaptureMedia"></a> Носители для снятия образа

Носитель для снятия образа позволяет снять образ операционной системы с компьютера-образца. Носитель для снятия образа содержит загрузочный образ, который запускает компьютер-образец и выполняет последовательность задач, создающую образ операционной системы.

Дополнительные сведения о создании носителя для записи образа см. в [этой статье ](create-capture-media.md).  


## <a name="bootable-media"></a><a name="BKMK_PlanBootableMedia"></a> Загрузочный носитель

Загрузочный носитель содержит следующие компоненты:

- загрузочный образ;
- (необязательно) [команды перед запуском](../understand/prestart-commands-for-task-sequence-media.md) и файлы для них;
- двоичные файлы Configuration Manager.

Когда запускается конечный компьютер, он подключается к сети и запрашивает через сеть последовательность задач, образ операционной системы и все другое требуемое содержимое. В связи с тем, что последовательность задач расположена не на носителе, вы можете изменять ее и другое содержимое без повторного создания носителя.  

> [!IMPORTANT]  
> Пакеты на загрузочном носителе не шифруются. Примите соответствующие меры безопасности, такие как защита носителя паролем, чтобы предотвратить доступ к носителю неавторизованных пользователей.  

Дополнительные сведения о создании загрузочного носителя см. в [этой статье](create-bootable-media.md).  


## <a name="prestaged-media"></a><a name="BKMK_PlanPrestagedMedia"></a> Предварительно подготовленный носитель

Предварительно подготовленный носитель позволяет поместить на жесткий диск загрузочный носитель и образ операционной системы до начала подготовки. Предварительно подготовленный носитель представляет собой WIM-файл с образом Windows. Он может быть установлен на компьютер без операционной системы производителем или корпоративным центром подготовки даже без подключения к окружению Configuration Manager.  

Предварительно подготовленный носитель содержит загрузочный образ, используемый для запуска конечного компьютера, и образ операционной системы, который применяется к конечному компьютеру. Вы также можете указать приложения, пакеты и пакеты драйверов, включаемые в состав предварительно подготовленного носителя. Последовательность задач, которая развертывает операционную систему, не содержится на этом носителе. При развертывании последовательности задач с использованием предварительно подготовленного носителя клиент сначала проверяет локальный кэш последовательности задач на наличие допустимого содержимого. Если содержимое не найдено или было изменено, оно загружается из точки распространения или с кэширующего узла.  

Предварительно подготовленный носитель применяется к жесткому диску компьютера перед тем, как компьютер будет отправлен конечному пользователю. Когда компьютер впервые запускается после применения предварительно подготовленного носителя, открывается среда предустановки Windows. Компьютер подключается к точке управления и ищет нужную последовательность задач для завершения развертывания ОС.  

> [!IMPORTANT]  
> Пакеты на предварительно подготовленном носителе не шифруются. Примите соответствующие меры безопасности, такие как защита носителя паролем, чтобы предотвратить доступ к носителю неавторизованных пользователей.  

Дополнительные сведения о создании предварительно подготовленного носителя см. в [этой статье](create-prestaged-media.md).  


## <a name="stand-alone-media"></a><a name="BKMK_PlanStandaloneMedia"></a> Автономные носители

Автономные носители содержат все данные, которые необходимы для развертывания операционной системы (в том числе последовательность задач и все остальное необходимое содержимое). Так как все необходимое для развертывания операционной системы хранится на самом носителе, для него требуется существенно больше дискового пространства, чем для носителей других типов.  

Дополнительные сведения о создании автономного носителя см. в [этой статье](create-stand-alone-media.md).  


## <a name="considerations-when-using-https"></a>Рекомендации по использованию протокола HTTPS

Если вы настроите протокол HTTPS для точек управления и распространения, вы сможете создать загрузочный носитель и предварительно подготовленный носитель на первичном сайте, а не на сайте центра администрирования. Кроме того, примите во внимание следующий аспект при выборе динамического или основанного на сайте носителя.  

- Чтобы настроить носитель как динамический, на всех первичных сайтах должен быть настроен корневой ЦС сайта, на котором вы создали носитель. Можно импортировать корневой ЦС для всех первичных сайтов в иерархии.  

- Если первичные сайты в иерархии Configuration Manager применяют разные корневые ЦС, необходимо использовать сайтовый носитель на каждом сайте.  
