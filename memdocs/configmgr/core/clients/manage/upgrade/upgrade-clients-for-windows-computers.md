---
title: Обновление клиентов в Windows
titleSuffix: Configuration Manager
description: Сведения об обновлении клиентов на компьютерах Windows в Configuration Manager.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7476f27c050a7870cd8f860f2e1b6bfa3d68a7e9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696292"
---
# <a name="how-to-upgrade-clients-for-windows-computers-in-configuration-manager"></a>Обновление клиентов для компьютеров Windows в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Вы можете обновить клиент Configuration Manager на компьютерах Windows с помощью методов установки или функции автоматического обновления клиента. Ниже приведены допустимые способы обновления клиентского программного обеспечения на компьютерах Windows:  

- Установка с использованием групповой политики  

- Установка сценария входа  

- Установка вручную  

- Установка обновления  

Дополнительные сведения см. в статье [Развертывание клиентов на компьютерах Windows в Configuration Manager](../../deploy/deploy-clients-to-windows-computers.md).

Вы можете указать коллекцию исключений для клиентов, обновление которых не требуется. Дополнительные сведения см. в статье [Как исключить клиенты на компьютерах Windows из обновления в System Center Configuration Manager](exclude-clients-windows.md). Исключенные клиенты по-прежнему будут скачивать и запускать CCMSETUP, но обновляться не будут.

> [!TIP]  
> Если вы обновляете инфраструктуру серверов с предыдущей версии Configuration Manager, завершите обновление сервера перед обновлением клиентов Configuration Manager. Этот процесс включает в себя установку всех текущих обновлений ветви. Последнее текущее обновление ветви содержит последнюю версию клиента. Обновите клиенты после установки всех обновлений Configuration Manager.

> [!NOTE]
> Если вы планируете переназначить сайт для клиентов во время обновления, укажите новый сайт с использованием свойства client.msi `SMSSITECODE`. Если вы используете значение `AUTO` для `SMSSITECODE`, укажите также `SITEREASSIGN=TRUE`. Это свойство позволяет автоматически переназначать сайт во время обновления. Дополнительные сведения см. в статье [Сведения о параметрах и свойствах установки клиента в System Center Configuration Manager —SMSSITECODE](../../deploy/about-client-installation-properties.md#smssitecode).

## <a name="about-automatic-client-upgrade"></a><a name="bkmk_autoupdate"></a> Сведения об автоматическом обновлении клиента

Настройте сайт для автоматического обновления клиентов до последней версии Configuration Manager. Если Configuration Manager определяет, что версия назначенного клиента более ранняя, чем версия иерархии, он автоматически обновляет клиент. Этот сценарий включает обновление клиента до последней версии клиента при попытке назначения узлу Configuration Manager.  

Клиент может быть автоматически обновлен в следующих случаях.  

- Версия клиента ниже, чем версия, которая используется в иерархии.  

- Клиент на сайте центра администрирования имеет языковой пакет, а существующий клиент — нет.  

- Обязательный для клиента компонент в иерархии имеет версию, отличную от версии, установленной на клиенте.  

- Один или несколько клиентских установочных файлов имеют другую версию.  

> [!NOTE]  
> Чтобы узнать о различных версиях клиентов Configuration Manager в иерархии, можно запустить отчет **Число клиентов Configuration Manager по версии клиента** в папке отчетов **Сайт — сведения о клиентах**.  

Configuration Manager создает пакет обновления по умолчанию. Он автоматически отправляет пакет во все точки распространения в иерархии. Если вы вносите изменения в пакет клиента на сайте центра администрирования, Configuration Manager автоматически обновляет пакет и повторно распространяет его. Пример изменения — когда вы добавляете клиентский языковой пакет. Если автоматическое обновление клиента включено, каждый клиент автоматически установит новый языковой пакет.

> [!NOTE]  
> Configuration Manager не выполняет автоматическую отправку пакета обновления клиента в облачные точки распространения Configuration Manager.  

Включите автоматическое обновление клиентов в рамках иерархии. Эта конфигурация позволяет поддерживать актуальное состояние клиентов с меньшими усилиями.  

Если вы также управляете системами сайта Configuration Manager в качестве клиентов, определите, нужно ли включать их в процесс автоматического обновления. Из обновления клиента можно исключить все серверы или определенную коллекцию. Некоторые роли сайта Configuration Manager совместно используют структуру клиента, например точку управления и точку распространения по запросу. Эти роли обновляются при обновлении сайта, поэтому обновление версии клиента на этих серверах происходит одновременно.

## <a name="configure-automatic-client-upgrade"></a><a name="bkmk_configure"></a> Настройка автоматического обновления клиента

Используйте следующую процедуру, чтобы настроить автоматическое обновление клиента на сайте центра администрирования. Эта конфигурация применяется ко всем клиентам в иерархии.  

1. В консоли Configuration Manager перейдите в рабочую область **Администрирование**, разверните узел **Конфигурация сайта** и выберите узел **Сайты**.  

1. На вкладке **Главная** в группе **Сайты** нажмите кнопку **Параметры иерархии**.  

1. Перейдите на вкладку **Обновление клиента**. Просмотрите версию и дату рабочего клиента. Убедитесь, что это версия, которую нужно использовать для обновления клиентов. Если версия отличается от ожидаемой, может потребоваться повышение уровня предварительного клиента до рабочего. Дополнительные сведения см. в статье [Проверка обновления клиента в предварительной коллекции](test-client-upgrades.md).  

1. Выберите параметр **Обновить все клиенты в иерархии с помощью рабочего клиента**. Для подтверждения нажмите кнопку **ОК**.  

1. Если вы не хотите применять обновление клиента к серверам, выберите **Не обновлять серверы**.  

1. Укажите количество дней, в течение которых устройства должны обновлять клиент. После того как устройство получает политику, оно обновляет клиент через произвольный интервал в течение этого количества дней. Такое поведение предотвращает одновременное обновление большого количества клиентов.

    > [!NOTE]
    > Для обновления клиента компьютер должен быть запущен. Если компьютер не запущен, когда по расписанию он должен получить обновление, обновление не производится. Когда компьютер включается и получает политику, он планирует обновление на случайное время в пределах разрешенного числа дней. Если число дней, отведенное для обновления, истекло, обновление планируется на случайное время в течение 24 часов после включения компьютера.
    >
    > Вследствие этого обновление компьютеров, работа которых регулярно завершается, может происходить дольше ожидаемого, если случайным образом назначаемое время обновления не приходится на рабочие часы.

1. Чтобы исключить клиенты из обновления, щелкните **Исключить указанные клиенты из обновления** и укажите исключаемую коллекцию. Дополнительные сведения см. в статье [Как исключить клиенты на компьютерах Windows из обновления в System Center Configuration Manager](exclude-clients-windows.md).

1. Если необходимо, чтобы сайт скопировал пакет установки клиента на точки распространения, где разрешено [предварительно подготовленное содержимое](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent), щелкните параметр **Автоматически распространять пакет установки клиента на точки распространения, на которых разрешено предварительно подготовленное содержимое**.  

1. Нажмите кнопку **ОК**, чтобы сохранить параметры и закрыть окно "Свойства параметров иерархии".

Клиенты получат эти параметры при следующей загрузке политики.

> [!NOTE]
> При обновлении клиента учитываются все настроенные периоды обслуживания Configuration Manager.

## <a name="next-steps"></a>Дальнейшие шаги

Альтернативные способы обновления клиентов см. в статье [Развертывание клиентов на компьютерах Windows в Configuration Manager](../../deploy/deploy-clients-to-windows-computers.md).

Исключите определенные клиенты из автоматического обновления. Дополнительные сведения см. в статье об [отмене обновления для клиентов](exclude-clients-windows.md).