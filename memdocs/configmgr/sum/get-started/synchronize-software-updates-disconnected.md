---
title: 'Синхронизация обновлений без подключения к Интернету '
titleSuffix: Configuration Manager
description: Вы можете выполнять синхронизацию обновлений программного обеспечения в точке обновления ПО верхнего уровня, отключенной от Интернета.
ms.date: 02/13/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 1a997c30-8e71-4be5-89ee-41efb2c8d199
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: c2fd85ea9d72e0986f56e24c7ccb66826829079b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689672"
---
# <a name="synchronize-software-updates-from-a-disconnected-software-update-point"></a>Синхронизация обновлений программного обеспечения из отсоединенной точки обновления программного обеспечения  

*Область применения: Configuration Manager (Current Branch)*

 Если точка обновления программного обеспечения для сайта верхнего уровня отключена от Интернета, необходимо воспользоваться функциями экспорта и импорта, представленными в средстве WSUSUtil, чтобы выполнить синхронизацию метаданных обновлений программного обеспечения. Можно выбрать существующий сервер WSUS, не входящий в вашу иерархию Configuration Manager, как источник синхронизации. В этой статье содержится информация об использовании функций экспорта и импорта средства WSUSUtil.  

 Для экспорта и импорта метаданных обновлений программного обеспечения необходимо экспортировать метаданные обновлений из базы данных WSUS на указанном сервере экспорта, скопировать локально хранящиеся файлы условий лицензионного соглашения в отсоединенную точку обновления программного обеспечения, а затем импортировать метаданные обновлений в базу данных WSUS в отсоединенной точке обновления.  

 Сведения в следующей таблице помогут определить сервер экспорта, с которого следует экспортировать метаданные обновлений программного обеспечения.  

|Точка обновления программного обеспечения|Вышестоящий источник обновления для подключенных точек обновления программного обеспечения|Сервер экспорта для отсоединенной точки обновления программного обеспечения|  
|---------------------------|-----------------------------------------------------------------|------------------------------------------------------------|  
|Сайт центра администрирования|Центр обновления Майкрософт (Интернет)<br /><br /> Существующий сервер WSUS|Выберите сервер WSUS, синхронизированный с Центром обновления Майкрософт, с использованием классификаций, продуктов и языков обновления программного обеспечения, необходимых в среде Configuration Manager.|  
|Автономный первичный сайт|Центр обновления Майкрософт (Интернет)<br /><br /> Существующий сервер WSUS|Выберите сервер WSUS, синхронизированный с Центром обновления Майкрософт, с использованием классификаций, продуктов и языков обновления программного обеспечения, необходимых в среде Configuration Manager.|  

 Перед началом процесса экспорта проверьте, что на выбранном сервере экспорта завершена синхронизация обновлений программного обеспечения и самые последние метаданные обновлений программного обеспечения уже синхронизированы. Чтобы убедиться в успешном завершении синхронизации, выполните следующую процедуру.  

#### <a name="to-verify-that-software-updates-synchronization-has-completed-successfully-on-the-export-server"></a>Проверка успешного завершения синхронизации обновлений программного обеспечения на сервере экспорта  

1.  Откройте консоль администрирования WSUS и подключитесь к базе данных WSUS на сервере экспорта.  

2.  В консоли администрирования WSUS щелкните элемент **Синхронизации**. В области результатов будет отображен список попыток синхронизации обновлений программного обеспечения.  

3.  Найдите последнюю попытку синхронизации обновлений программного обеспечения и убедитесь в ее успешном завершении.  

> [!IMPORTANT]  
> - Чтобы экспортировать метаданные обновлений программного обеспечения, средство WSUSUtil необходимо запустить локально на сервере экспорта, а чтобы импортировать метаданные обновлений программного обеспечения, это средство нужно запустить на сервере отсоединенной точки обновления программного обеспечения. Кроме того, пользователь, работающий со средством WSUSUtil, должен входить в локальную группу "Администраторы" на каждом сервере.  
> - Если вы используете Windows Server 2012, убедитесь, что на серверах WSUS установлен [KB2819484](https://support.microsoft.com/help/2819484/cab-file-that-is-exported-by-using-the-wsusutil-exe-command-is-display).

## <a name="export-process-for-software-updates"></a>Процесс экспорта обновлений программного обеспечения  
 Процесс экспорта обновлений программного обеспечения состоит из двух основных этапов: копирование локально хранящихся файлов условий лицензионного соглашения в отсоединенную точку обновления программного обеспечения и экспорт метаданных обновлений программного обеспечения из базы данных WSUS на сервере экспорта.  

 Следующая процедура используется для копирования локальных метаданных условий лицензионного соглашения в отсоединенную точку обновления программного обеспечения.  

#### <a name="to-copy-local-files-from-the-export-server-to-the-disconnected-software-update-point-server"></a>Копирование локальных файлов с сервера экспорта на сервер отсоединенной точки обновления программного обеспечения  

1. На сервере экспорта найдите папку с обновлениями программного обеспечения и условиями лицензионного соглашения для обновления программного обеспечения. По умолчанию службы WSUS хранят файлы в каталоге <*установочный_диск_WSUS*>\WSUS\WSUSContent\\, где *установочный_диск_WSUS* — это диск, на котором установлены службы WSUS.  

2. Скопируйте все файлы и папки из этого расположения в папку WSUSContent на сервере отсоединенной точки обновления программного обеспечения.  

   Следующая процедура используется для экспорта метаданных обновления программного обеспечения из базы данных WSUS на сервере экспорта.  

#### <a name="to-export-software-updates-metadata-from-the-wsus-database-on-the-export-server"></a>Экспорт метаданных обновления программного обеспечения из базы данных WSUS на сервере экспорта  

1.  В командной строке на сервере экспорта перейдите в папку, содержащую файл WSUSutil.exe. По умолчанию средство находится в каталоге %*ProgramFiles*%\Update Services\Tools. Например, если средство находится в расположении по умолчанию, введите **cd %ProgramFiles%\Update Services\Tools**.  

2.  Чтобы экспортировать метаданные обновлений программного обеспечения в файл пакета, введите:  

     **wsusutil.exe export**  *имя_пакета*  *файл_журнала*  
 
     Пример.  

     **wsusutil.exe export export.xml.gz export.log**  

     Формат можно суммировать следующим образом: за WSUSutil.exe следует параметр экспорта, имя файла экспорта .xml.gz, созданного во время операции экспорта, и имя файла журнала. Средство WSUSutil.exe экспортирует метаданные с севера экспорта и создает файл журнала для выполненной операции.  

    > [!NOTE]  
    >  Имена файла пакета (файла .xml.gz) и файла журнала должны быть уникальными в текущей папке.  

3.  Переместите пакет экспорта в папку, содержащую средство WSUSutil.exe, на сервере импорта WSUS.  

    > [!NOTE]  
    >  Если переместить пакет в эту папку, операция импорта будет проще. Пакет можно переместить в любое доступное серверу импорта расположение, которое следует указать при выполнении средства WSUSutil.exe.  

## <a name="import-software-updates-metadata"></a>Импорт метаданных обновлений программного обеспечения  
 Выполните следующую процедуру по импорту метаданных обновлений программного обеспечения с сервера экспорта в отсоединенную точку обновления программного обеспечения.  

> [!IMPORTANT]  
>  Экспортированные данные необходимо импортировать только из доверенного источника. Импорт содержимого из ненадежного источника может подвергнуть риску безопасность сервера WSUS.  

#### <a name="to-import-metadata-to-the-database-of-the-import-server"></a>Импорт метаданных в базу данных сервера импорта  

1.  В командной строке на сервере импорта WSUS перейдите в папку, содержащую файл WSUSutil.exe. По умолчанию средство находится в каталоге %*ProgramFiles*%\Update Services\Tools.  

2.  Введите следующую команду:  

     **wsusutil.exe import**  *имя_пакета*  *файл_журнала*  

     Пример.  

     **wsusutil.exe import export.xml.gz import.log**  

     Формат можно суммировать следующим образом: за WSUSutil.exe следует команда импорта, имя файла пакета (файла .xml.gz), созданного во время операции экспорта (и путь к файлу пакета, если пакет находится в другой папке), и имя файла журнала. Средство WSUSutil.exe импортирует метаданные с севера экспорта и создает файл журнала для выполненной операции.  

## <a name="next-steps"></a>Дальнейшие шаги
После первоначальной синхронизации обновлений ПО либо появления новых классификаций или продуктов необходимо [настроить новые классификации и продукты](configure-classifications-and-products.md), чтобы синхронизировать обновления ПО с новыми условиями.

После синхронизации обновлений ПО с нужными условиями вы можете [управлять параметрами обновлений ПО](manage-settings-for-software-updates.md).   