---
title: Мониторинг работоспособности подключения
titleSuffix: Configuration Manager
description: Сведения о том, как отслеживать работоспособность подключения и состояния устройств для Аналитики компьютеров в Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 6eb0a99043eefcdb54c27a183fbc1e1eec8899bf
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268646"
---
# <a name="monitor-connection-health"></a>Мониторинг работоспособности подключения

Используйте панель мониторинга **Работоспособность подключения** в Configuration Manager, чтобы перейти к подробным сведениям о категориях по работоспособности устройств. В консоли Configuration Manager перейдите в рабочую область **Библиотека программного обеспечения**, разверните узел **Обслуживание Аналитики компьютеров** и выберите панель мониторинга **Работоспособность подключения**.  

[![Снимок экрана панели мониторинга "Работоспособность подключения" Configuration Manager](media/connection-health-dashboard.png)](media/connection-health-dashboard.png#lightbox)

При первой настройке Аналитики компьютеров на этих диаграммах могут отображаться не все данные. Отправка диагностических данных в службу "Аналитика компьютеров" на активных устройствах, обработка данных в службе, а затем синхронизация с сайтом Configuration Manager может занять 2–3 дня.<!-- 4098037 -->

## <a name="connection-details"></a>Сведения о подключении

На этой плитке отображаются следующие основные сведения о подключении из Configuration Manager к Аналитике компьютеров:

- **Имя клиента**. Имя подключения к Аналитике компьютеров в узле **служб Azure**.

- **Целевая коллекция**. Та же *целевая коллекция*, указанная при подключении Configuration Manager к Аналитике компьютеров. В эту коллекцию входят все устройства, которые Configuration Manager настраивает с использованием коммерческого идентификатора и параметров диагностических данных. Это полный набор устройств, которые Configuration Manager подключает к службе "Аналитика компьютеров".

- **Целевые устройства**. Все устройства в целевой коллекции, кроме следующих типов устройств:

  - Cписанные.
  - Устаревшие.
  - Неактивно
  - Неуправляемые.
  - Устройства под управлением версии Long-Term Servicing Channel (LTSC) Windows 10.
  - Устройства под управлением Windows Server.

    Дополнительные сведения об этих состояниях устройств см. в разделе [О статусе клиента](../core/clients/manage/monitor-clients.md#bkmk_about).

    > [!Note]  
    > Configuration Manager отправляет в Аналитику компьютеров все устройства в целевой коллекции, кроме списанных и устаревших клиентов.

- **Устройства, подходящие для DA**. Количество целевых устройств, кроме устройств, которые не подходят для Аналитики компьютеров. Например, устройства в целевой коллекции под управлением Windows Server или LTSC Windows 10.

## <a name="last-sync-details"></a>Сведения о последней синхронизации

На этой плитке показано, когда Configuration Manager выполняет синхронизацию с облачной службой "Аналитика компьютеров", а также количество синхронизируемых устройств.

- **Синхронизировано устройств**. Количество подходящих устройств, которые Configuration Manager отправляет в Аналитику компьютеров. Служба добавляет эти устройства в отображаемый на данный момент моментальный снимок.

- **Последняя синхронизация службы**. То же самое, что и время по параметру **Последнее обновление** на портале Аналитики компьютеров.

- **Следующая синхронизация службы**. Время создания следующего ежедневного моментального снимка в Аналитике компьютеров.

> [!Note]  
> При первой регистрации устройств для Аналитики компьютеров отправка и обработка данных может занять несколько дней. В течение этого времени плитка **Last sync details** (Сведения о последней синхронизации) может быть пустой.
> Кроме того, при запросе моментального снимка по требованию ни одно из значений на этой плитке не обновляется автоматически. Дополнительные сведения см. в разделе о [задержке данных](troubleshooting.md#data-latency).

Если некоторые устройства не отображаются в Аналитике компьютеров, убедитесь, что они поддерживаются в этой службе. Дополнительные сведения см. в разделе [Необходимые условия](overview.md#prerequisites).

## <a name="connection-health"></a>Работоспособность подключения

На диаграмме **Работоспособность подключения** отображается количество устройств в следующих состояниях работоспособности:  

- [Зарегистрировано корректно](#properly-enrolled). Устройство отображается в Аналитике компьютеров с полной инвентаризацией.
- [Не удалось зарегистрировать](#unable-to-enroll). Возникла блокирующая проблема, препятствующая регистрации устройства.
- [Предупреждение конфигурации](#configuration-alert). Устройство не отображается в Аналитике компьютеров или отображается с неполной инвентаризацией. В Configuration Manager также выявлена ошибка при регистрации устройства.
- [Ожидается регистрация](#awaiting-enrollment). В Configuration Manager настроено устройство, но оно еще не отображается в Аналитике компьютеров.
- [Ожидаемое состояние](#status-pending). Configuration Manager по-прежнему настраивает это устройство, или на устройстве недостаточно данных для определения его состояния.
- [Нет данных](#missing-data). В Configuration Manager настроено устройство, но Аналитика компьютеров содержит только часть данных.

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

Общее количество устройств на этой диаграмме должно совпадать со значением **Устройства, подходящие для DA** на плитке "Сведения о подключении".

Выберите сегмент на диаграмме, чтобы перейти к списку устройств с этим состоянием. Дополнительные сведения см. в разделе [Список устройств](#device-list).

Выберите имя категории в условных обозначениях, чтобы удалить ее из диаграммы или добавить на диаграмму. Это действие позволяет увеличить масштаб диаграммы, чтобы увидеть относительные размеры меньших сегментов.

### <a name="properly-enrolled"></a>Зарегистрировано корректно

Устройство содержит следующие атрибуты:

- клиент Configuration Manager версии 1902 или более поздней;  
- ошибки конфигурации отсутствуют;  
- Аналитика компьютеров получила от этого устройства полные диагностические данные в течение последних 28 дней;  
- Аналитика компьютеров содержит полную инвентаризацию конфигурации устройства и установленных приложений.  

### <a name="unable-to-enroll"></a>Не удалось зарегистрировать

Configuration Manager обнаруживает одну или несколько блокирующих проблем, препятствующих регистрации устройств. Дополнительные сведения см. в списке устройств в разделе [Свойства устройства](#bkmk_config-issues).  

Например, версия клиента Configuration Manager ниже 1902 (5.0.8790). Обновите клиент до последней версии. Рассмотрите возможность включения автоматического обновления клиента для сайта Configuration Manager. См. дополнительные сведения об [обновлении клиентов](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  

Начиная с версии 2002, можно с легкостью определять проблемы с конфигурацией прокси-сервера клиентов в двух областях.

- **Проверки подключения конечной точки**: если клиентам не удается подключиться к требуемой конечной точке, на панели мониторинга отобразится соответствующее предупреждение об ошибке конфигурации. Детализируйте сведения о клиентах, которые не удается зарегистрировать, чтобы увидеть конечные точки, к которым клиентам не удается подключиться из-за проблем с конфигурацией прокси-сервера. Дополнительные сведения см. в разделе [Проверки подключения к конечной точке](#endpoint-connectivity-checks).<!-- 4963230 -->

- **Состояние подключения**: если для доступа к службе Аналитики компьютеров клиенты используют прокси-сервер, в Configuration Manager отображаются сообщения о проблемах с проверкой подлинности на прокси-сервере. Выполните детализацию, чтобы просмотреть клиентов, которые не удается зарегистрировать из-за проблем с проверкой подлинности прокси-сервера. Дополнительные сведения см. в статье о [Состояние подключения](#connectivity-status).<!-- 4963383 -->

### <a name="configuration-alert"></a>Предупреждение конфигурации

Устройство не отображается в Аналитике компьютеров или отображается с неполной инвентаризацией. В Configuration Manager также выявлена ошибка при регистрации устройства. Дополнительные сведения см. в списке устройств в разделе [Свойства устройства](#bkmk_config-issues).

Например, устройство не подключено к службе. Дополнительные сведения см. в разделе [Подключение к конечной точке диагностики Windows](#windows-diagnostic-endpoint-connectivity).

### <a name="awaiting-enrollment"></a>Ожидается регистрация

В Аналитике компьютеров нет диагностических данных для этого устройства. Эта проблема может быть вызвана тем, что вы недавно добавили устройство в целевую коллекцию и еще не отправляли данные. Это также может означать, что устройство неправильно взаимодействует со службой и последние данные диагностики обновлялись более 28 дней назад.

Убедитесь, что устройство может взаимодействовать со службой. Дополнительные сведения см. в разделе о [конечных точках](enable-data-sharing.md#endpoints).  

### <a name="status-pending"></a>Ожидаемое состояние

Configuration Manager по-прежнему настраивает это устройство, или на устройстве недостаточно данных для определения его состояния.

### <a name="missing-data"></a>Нет данных

В Configuration Manager устройство успешно настроено, но Аналитика компьютеров не может создать оценку совместимости. Она не содержит полный набор данных для конфигурации устройства (Census) или установленных приложений (инвентаризации).

Эта проблема часто исправляется автоматически при повторной попытке устройства. Если ситуация не меняется, убедитесь, что устройство может взаимодействовать со службой. Дополнительные сведения см. в разделе о [конечных точках](enable-data-sharing.md#endpoints).  

## <a name="device-list"></a>Список устройств

Чтобы просмотреть конкретный список устройств по состоянию, начните с панели мониторинга **Работоспособность подключения**. Выберите один из сегментов плитки **Работоспособность подключения** и перейдите к списку устройств в этом состоянии. В этом настраиваемом представлении устройства по умолчанию отображаются следующие столбцы Аналитики компьютеров:

- Конфигурация коммерческих идентификаторов.
- Обновление минимальных требований к совместимости.
- Согласие на сбор диагностических данных Windows.
- Согласие на сбор коммерческих данных Windows.
- Подключение к конечной точке диагностики Windows
- Состояние подключения (начиная с версии 2002)
- Проверки подключения конечных точек (начиная с версии 2002)

Эти столбцы соответствуют основным [предварительным требованиям](overview.md#prerequisites) для взаимодействия устройств с Аналитикой компьютеров.

[![Снимок экрана: "Не удалось зарегистрировать список устройств"](media/device-list-unable-to-enroll.png)](media/device-list-unable-to-enroll.png#lightbox)

Выберите устройство, чтобы просмотреть полный список доступных свойств в области сведений. В список устройств можно также добавить любое из этих свойств в качестве столбцов.

## <a name="device-properties"></a><a name="bkmk_config-issues"></a> Свойства устройства

Следующие свойства устройства Аналитики компьютеров доступны в виде столбцов в списке устройств Configuration Manager:

- [Проверки подключения конечных точек](#endpoint-connectivity-checks) (начиная с версии 2002)
- [Состояние подключения](#connectivity-status) (начиная с версии 2002)
- [конфигурация средства оценки](#appraiser-configuration);  
- [обновление минимальных требований к совместимости](#minimum-compatibility-update);  
- [версия средства оценки](#appraiser-version);  
- [последний успешный полный запуск средства оценки](#last-successful-full-run-of-appraiser);  
- [сбор данных средства оценки](#appraiser-data-collection);  
- [последний успешный полный запуск Census](#last-successful-full-run-of-census);  
- [сбор данных Census](#census-data-collection);  
- [подключение к конечной точке диагностики Windows](#windows-diagnostic-endpoint-connectivity);  
- [проверка диагностических данных пользователя](#check-end-user-diagnostic-data);  
- [проверка прокси-сервера для пользователей](#check-user-proxy);  
- [конфигурация коммерческих идентификаторов](#commercial-id-configuration);  
- [согласие на сбор коммерческих данных Windows](#windows-commercial-data-opt-in);  
- [проверка имени устройства в диагностических данных](#check-device-name-in-diagnostic-data);  
- [конфигурация службы DiagTrack](#diagtrack-service-configuration);  
- [версия DiagTrack](#diagtrack-version);  
- [получение идентификатора SQM](#sqm-id-retrieval);  
- [получение уникального идентификатора устройства](#unique-device-identifier-retrieval);  
- [согласие на сбор диагностических данных Windows](#windows-diagnostic-data-opt-in).  

На плитке **Наиболее частые блокировки регистрации и предупреждения конфигурации** панели мониторинга "Работоспособность подключения" отображаются свойства, о которых устройства чаще всего сообщают как о проблеме.

### <a name="endpoint-connectivity-checks"></a>Проверки подключения конечных точек

Начиная с версии 2002,<!-- 4963230 --> для обнаружения проблем проверки подлинности прокси-сервера клиенты выполняют проверки подключения к необходимым конечным точкам. Если клиенту не удается связаться с требуемой конечной точкой, это свойство отображает нумерованный список конечных точек, к которым не удается подключиться из-за проблем с конфигурацией прокси-сервера. Сравните этот список с опубликованным списком [обязательных конечных точек](enable-data-sharing.md#endpoints).

### <a name="connectivity-status"></a>Состояние подключения

Начиная с версии 2002,<!-- 4963383 --> если для доступа к службе Аналитики компьютеров клиенты используют прокси-сервер, это свойство показывает проблемы с проверкой подлинности на прокси-сервере. Оно включает следующие сведения, связанные с проверкой подлинности на прокси-сервере.

- Код состояния
- Код возврата

В файле журнала отобразятся ошибки, аналогичные приведенным ниже:

`Error 407: Can't connect to Microsoft %s. Check your network/proxy settings`

Где `%s` — это URL-адрес требуемой конечной точки.

Вы также можете увидеть недетерминированные сообщения об ошибках, которые не требуют внимания, пока устройства не будут зарегистрированы. Пример.

`This status is not related to proxy configuration, consider to investigate only if you are experiencing device enrollment or configuration alert issues.`

Дополнительные сведения о настройке прокси-серверов для Аналитики компьютеров см. в разделе [Проверка подлинности прокси-сервера](enable-data-sharing.md#proxy-server-authentication).

### <a name="appraiser-configuration"></a>Конфигурация средства оценки

<!--20,21-->
Средство оценки — это компонент Windows, который соответствует [обновлениям совместимости](enroll-devices.md#update-devices). Оно оценивает приложения и драйверы на устройстве на предмет совместимости с последней версией Windows.

Если эта проверка прошла успешно, компонент средства оценки настроен на устройстве надлежащим образом.

В противном случае может отобразиться одна из следующих ошибок:

- Не удается настроить сбор данных о совместимости приложений устройства (SetRequestAllAppraiserVersions). Проверьте сведения об исключениях в журналах.  

- Не удается настроить сбор данных о совместимости приложений устройства (SetRequestAllAppraiserVersions). Проверьте сведения об исключениях в журналах.  

- Не удается записать RequestAllAppraiserVersions в раздел реестра `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser`. Проверьте разрешения.  

Проверьте разрешения для этого раздела реестра. Убедитесь, что учетная запись Local System может получить доступ к этому разделу для установки клиента Configuration Manager.  

Дополнительные сведения см. в журнале M365AHandler.log в клиенте.  

### <a name="minimum-compatibility-update"></a>Обновление минимальных требований к совместимости

<!--18,19,32-->
Обновление совместимости (appraiser.dll) не установлено на устройстве или устарело. Его версия более ранняя, чем минимальное требование к Аналитике компьютеров, 10.0.17763.

Установите последнее обновление совместимости. Дополнительные сведения см. в разделе об [обновлениях для обеспечения совместимости](enroll-devices.md#update-devices).

### <a name="appraiser-version"></a>Версия средства оценки

Это свойство отображает текущую версию компонента средства оценки на устройстве. В нем отображается версия файла в `%windir%\System32\appraiser.dll` без десятичных разделителей. Например, версия файла 10.0.17763 отображается как 10017763.

### <a name="last-successful-full-run-of-appraiser"></a>Последний успешный полный запуск средства оценки

Это свойство отображает дату и время последнего успешного запуска средства оценки на устройстве.

### <a name="appraiser-data-collection"></a>Сбор данных средства оценки

<!--Appraiser run status-->
<!--22,33-->
Это свойство показывает последний результат из Windows, где запущено средство оценки.

В противном случае может отобразиться одна из следующих ошибок:

- Не удается собрать данные о совместимости приложений (RunAppraiser). Дополнительные сведения см. в журнале.  

- Сбор данных о совместимости приложений (CompatTelRunner.exe) завершился ошибкой с кодом.  

Дополнительные сведения см. в журнале M365AHandler.log в клиенте.

Проверьте следующий файл: `%windir%\System32\CompatTelRunner.exe`. Если он не существует, переустановите необходимые [обновления совместимости](enroll-devices.md#update-devices). Убедитесь, что никакие другие системные компоненты не удаляют этот файл, например групповая политика или служба защиты от вредоносных программ.

Если файл M365AHandler.log в клиенте содержит одну из следующих ошибок:

``` Log
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005
```

Чтобы устранить эти ошибки, в затронутом клиенте выполните следующие команды из консоли Windows PowerShell с повышенными привилегиями:

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

### <a name="last-successful-full-run-of-census"></a>Последний успешный полный запуск Census

Это свойство отображает дату и время последнего успешного запуска Census на устройстве.

### <a name="census-data-collection"></a>Сбор данных Census

<!-- Census run status -->
<!--51,52-->
Census — это компонент Windows, который выполняет инвентаризацию устройства. Эти данные инвентаризации используются для получения общих сведений об устройстве и его конфигурации.

Это свойство показывает последний результат из Windows, где запущен компонент Census.

В противном случае может отобразиться одна из следующих ошибок:

- Не удается собрать данные об устройстве и его конфигурации (RunCensus). Проверьте сведения об исключениях в журналах.  

- Средство сбора данных о конфигурации и устройствах (devicecensus.exe) не найдено.  

Дополнительные сведения см. в журнале M365AHandler.log в клиенте.

Проверьте следующий файл: `%windir%\System32\DeviceCensus.exe`. Если он не существует, переустановите необходимые [обновления совместимости](enroll-devices.md#update-devices). Убедитесь, что никакие другие системные компоненты не удаляют этот файл, например групповая политика или служба защиты от вредоносных программ.

### <a name="windows-diagnostic-endpoint-connectivity"></a>Подключение к конечной точке диагностики Windows

<!--12,15-->
Если эта проверка прошла успешно, устройство может подключиться к конечной точке службы функциональных возможностей для подключенных пользователей и телеметрии (Vortex).

В противном случае может отобразиться одна из следующих ошибок:  

- Не удается подключиться к конечной точке службы функциональных возможностей для подключенных пользователей и телеметрии (Vortex). Проверьте параметры сети и прокси-сервера.  

- Не удается проверить подключение к конечной точке службы функциональных возможностей для подключенных пользователей и телеметрии (CheckVortexConnectivity). Проверьте сведения об исключениях в журналах.  

Устройства проверяют возможность подключения, отправляя запрос GET в следующую конечную точку на основе версии ОС:

| Версия ОС | Конечная точка |
|------------|----------|
| — Windows 10 версии 1809 или более поздней<br/>— Windows 10 версии 1803 с накопительным пакетом обновления 2018-09 или более поздней | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10 версии 1803 *без* накопительного пакета обновления 2018-09 или более поздней версии | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10 версии 1709 или более ранней | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 или Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Убедитесь, что устройство может взаимодействовать со службой. В рамках этой проверки проверяются некоторые необходимые конечные точки. Дополнительные сведения см. в разделе о [конечных точках](enable-data-sharing.md#endpoints).  

Дополнительные сведения см. в журнале M365AHandler.log в клиенте.  

### <a name="check-end-user-diagnostic-data"></a>Проверка диагностических данных пользователя

<!--1004-->
Если эта проверка не пройдена, пользователь выбрал на устройстве более ранние диагностические данные Windows. Это также может быть вызвано конфликтующим объектом групповой политики. Дополнительные сведения см. в разделе о [параметрах Windows](enroll-devices.md#windows-settings).

В зависимости от бизнес-требований можно отключить выбор пользователя с помощью групповой политики. Используйте параметр, чтобы **настроить пользовательский интерфейс для параметра сбора данных телеметрии**. Дополнительные сведения см. в статье [Настройка диагностических сведений Windows в вашей организации](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).

### <a name="check-user-proxy"></a>Проверка прокси-сервера для пользователей

<!--30,35-->
В Windows 7 параметр DisableEnterpriseAuthProxy включен по умолчанию. На компьютерах Windows 8.1 Configuration Manager задает для параметра DisableEnterpriseAuthProxy значение 0 (не отключено).

Это свойство может отображать следующие ошибки:

- Прокси-сервер проверки подлинности включен. Задайте для DisableEnterpriseAuthProxy значение 0 в разделе `HKLM\Software\Policies\Microsoft\Windows\DataCollection`.

- Не удается проверить состояние прокси-сервера проверки подлинности. Проверьте сведения об исключениях в журналах.

Дополнительные сведения см. в журнале M365AHandler.log в клиенте.  

Проверьте разрешения для этого раздела реестра. Убедитесь, что учетная запись Local System может получить доступ к этому разделу для установки клиента Configuration Manager. Это также может быть вызвано конфликтующим объектом групповой политики. Дополнительные сведения см. в разделе о [параметрах Windows](enroll-devices.md#windows-settings).  

### <a name="commercial-id-configuration"></a>Конфигурация коммерческих идентификаторов.

<!--9, 11, 53-->
Корпорация Майкрософт сопоставляет информацию от устройств с рабочей областью Аналитики компьютеров с помощью уникального коммерческого идентификатора. При интеграции Configuration Manager с Аналитикой компьютеров этот идентификатор автоматически запрашивается у службы. Configuration Manager должен автоматически применять этот идентификатор к клиентам, на которые распространяются параметры Аналитики компьютеров.

Если эта проверка прошла успешно, устройство надлежащим образом настроено с помощью коммерческого идентификатора.

В противном случае может отобразиться одна из следующих ошибок:

- Не удается записать CommercialId в раздел реестра `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Проверьте разрешения.  

- Не удается обновить CommercialId в разделе реестра `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Проверьте сведения об исключениях в журналах.  

- Укажите верное значение CommercialId в разделе `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`.  

Дополнительные сведения см. в журнале M365AHandler.log в клиенте.  

Проверьте разрешения для этого раздела реестра. Убедитесь, что учетная запись Local System может получить доступ к этому разделу для установки клиента Configuration Manager. Это также может быть вызвано конфликтующим объектом групповой политики. Дополнительные сведения см. в разделе о [параметрах Windows](enroll-devices.md#windows-settings).  

Для устройства есть другой идентификатор. Этот раздел реестра используется групповой политикой. Он имеет приоритет над идентификатором, предоставленным Configuration Manager.  

<a name="bkmk_ViewCommercialID"></a> Чтобы просмотреть коммерческий идентификатор на портале "Аналитика компьютеров", выполните описанную ниже процедуру.

1. Перейдите на портал "Аналитика компьютеров" и выберите **Подключенные службы** в группе "Глобальные параметры".  

2. В области **Подключенные службы** по умолчанию выбрана область **Регистрация устройств**. В области "Регистрация устройств" в разделе "Сведения" отображается ключ коммерческого идентификатора.  

[![Снимок экрана коммерческого идентификатора на портале "Аналитика компьютеров"](media/commercial-id.png)](media/commercial-id.png#lightbox)

> [!Important]  
> Воспользуйтесь параметром **Получить новый ключ идентификатора**, только если невозможно использовать текущий. Если вы повторно создали коммерческий идентификатор, [повторно зарегистрируйте устройства с помощью нового идентификатора](enroll-devices.md#device-enrollment). Этот процесс может привести к утрате диагностических данных во время перехода.  

### <a name="windows-commercial-data-opt-in"></a>Согласие на сбор коммерческих данных Windows

<!--64-->
Это свойство характерно для устройств под управлением Windows 7 или Windows 8.1. Оно выполняет проверки, подобные проверкам по свойству [Согласие на сбор диагностических данных Windows](#windows-diagnostic-data-opt-in), за исключением значения CommercialDataOptIn.

### <a name="check-device-name-in-diagnostic-data"></a>Проверка имени устройства в диагностических данных

<!--56,58-->
Если эта проверка прошла успешно, устройство надлежащим образом настроено для совместного использования имени устройства.

В противном случае может отобразиться одна из следующих ошибок:

- Не удается проверить имя устройства, отправляемое в Майкрософт в составе диагностических данных Windows. Проверьте сведения об исключениях в журналах.  

- Не удается записать AllowDeviceNameInTelemetry в раздел реестра `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`. Проверьте разрешения.  

Дополнительные сведения см. в журнале M365AHandler.log в клиенте.  

Проверьте разрешения для этого раздела реестра. Убедитесь, что учетная запись Local System может получить доступ к этому разделу для установки клиента Configuration Manager. Это также может быть вызвано конфликтующим объектом групповой политики. Дополнительные сведения см. в разделе о [параметрах Windows](enroll-devices.md#windows-settings).  

Убедитесь, что другой механизм политики, например групповая политика, не отключает этот параметр.

### <a name="diagtrack-service-configuration"></a>Конфигурация службы DiagTrack

<!--44,45,50-->
Если эта проверка прошла успешно, компонент DiagTrack настроен на устройстве надлежащим образом. Минимальная версия, необходимая для Аналитики компьютеров, — 10010586 (10.0.10586).

В противном случае может отобразиться одна из следующих ошибок:

- Компонент функциональных возможностей для подключенных пользователей и телеметрии (diagtrack.dll) устарел. Проверьте требования.  

- Не удается найти компонент функциональных возможностей для подключенных пользователей и телеметрии (diagtrack.dll). Проверьте требования.  

- Включите и запустите службу функциональных возможностей для подключенных пользователей и телеметрии, чтобы отправлять данные в Майкрософт.  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

Установите последние обновления. Дополнительные сведения см. в разделе об [обновлениях устройств](enroll-devices.md#update-devices).

Убедитесь, что на устройстве запущена служба **Функциональные возможности для подключенных пользователей и телеметрия**.

### <a name="diagtrack-version"></a>Версия DiagTrack

Это свойство отображает текущую версию компонента "Функциональные возможности для подключенных пользователей и телеметрия" на устройстве. В нем отображается версия файла в `%windir%\System32\diagtrack.dll` без десятичных разделителей. Например, версия файла 10.0.10586 отображается как 10010586.

### <a name="sqm-id-retrieval"></a>Получение идентификатора SQM

<!--38-->
Это свойство в основном предназначено для устройств Windows 7. Оно может использоваться в более поздних версиях ОС в качестве резервного идентификатора для устройства.

В противном случае может отобразиться следующая ошибка:

- Не удается получить идентификатор телеметрии устройств старого образца (идентификатор SQM).

Дополнительные сведения см. в журнале M365AHandler.log в клиенте.  

Убедитесь, что в вашей среде нет повторяющихся идентификаторов. Например, если устройства были развернуты с помощью необобщенного образа ОС.

### <a name="unique-device-identifier-retrieval"></a>Получение уникального идентификатора устройства

<!--54-->
Для более надежного удостоверения устройства Аналитика компьютеров использует службу учетных записей Майкрософт.

Убедитесь, что служба **Помощник по входу в учетную запись Майкрософт** не отключена. Тип запуска должен быть **Manual (Trigger Start)** (Вручную (активировать запуск)).

Чтобы отключить доступ к учетной записи Майкрософт для пользователей, вместо блокировки этой конечной точки используйте параметры политики. Дополнительные сведения см. в разделе о [корпоративных учетных записях Майкрософт](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).

### <a name="windows-diagnostic-data-opt-in"></a>Согласие на сбор диагностических данных Windows

<!--8,40,55,62-->
Это свойство проверяет правильность настройки Windows, чтобы разрешить сбор диагностических данных. Оно проверяет значение AllowTelemetry в следующих разделах реестра:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Проверьте разрешения для этих разделов реестра. Убедитесь, что учетная запись Local System может получить доступ к этим разделам для установки клиента Configuration Manager. Это также может быть вызвано конфликтующим объектом групповой политики. Дополнительные сведения см. в разделе о [параметрах Windows](enroll-devices.md#windows-settings).  

Дополнительные сведения см. в журнале M365AHandler.log в клиенте.  

## <a name="see-also"></a>См. также

[Устранение проблем с Аналитикой компьютера](troubleshooting.md)
