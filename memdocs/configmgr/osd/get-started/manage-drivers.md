---
title: Управление драйверами
titleSuffix: Configuration Manager
description: Каталог драйверов Configuration Manager позволяет импортировать драйверы устройств, группировать драйверы в пакеты и передавать эти пакеты в точки распространения.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8fffa72e45f2f9e063fb0072882c2a5278694cee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708902"
---
# <a name="manage-drivers-in-configuration-manager"></a>Управление драйверами в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Configuration Manager содержит каталог драйверов, с помощью которого можно управлять драйверами устройств Windows в среде Configuration Manager. Каталог драйверов позволяет импортировать драйверы устройств в Configuration Manager для их объединения в пакеты и передавать эти пакеты в точки распространения. Драйверы устройств можно использовать при установке полной версии ОС на конечный компьютер и использовании среды предустановки Windows в загрузочном образе. Драйверы устройств Windows состоят из файла сведений установки (INF) и дополнительных файлов, необходимых для поддержки устройства. При развертывании ОС Configuration Manager получает данные об оборудовании и платформе для устройства из соответствующего INF-файла. 



## <a name="driver-categories"></a><a name="BKMK_DriverCategories"></a> Категории драйверов

При импорте драйверов устройств им можно присвоить определенную категорию. Категории позволяют группировать драйверы устройств со сходным назначением в каталоге драйверов. Например, можно включить все драйверы сетевых адаптеров в определенную категорию. А затем при создании последовательности задач с шагом [Автоматическое применение драйверов](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) можно указать определенную категорию драйверов устройств. Configuration Manager проверит оборудование и выберет применимые драйверы из этой категории для программы установки Windows.  



## <a name="driver-packages"></a><a name="BKMK_ManagingDriverPackages"></a> пакеты драйверов,

Чтобы упростить развертывание ОС, можно объединить сходные драйверы устройств в пакеты. Например, можно создать пакет драйверов для каждого компьютера определенного поставщика в вашей сети. Пакет драйверов можно создать при импорте драйверов в каталог драйверов или непосредственно в узле **Пакеты драйверов**. Создав пакет драйверов, передайте его в точки распространения. Драйверы можно будет устанавливать на клиентских компьютерах Configuration Manager по мере необходимости. 

Примите во внимание следующее:  

- При создании пакета драйверов в качестве расположения источника должна указываться пустая сетевая папка, которая не используется другим пакетом драйверов. Поставщик SMS должен иметь разрешения на **полный доступ** к этому расположению.  

- При добавлении драйверов устройств в пакет Configuration Manager копирует его в исходное расположение пакета. В пакет драйверов можно добавлять только те драйверы устройств, которые были импортированы в каталог драйверов и включены в нем.  

- Можно скопировать набор драйверов устройств из существующего пакета драйверов. Сперва создайте пакет драйверов. Затем добавьте в него набор драйверов устройств, после чего передайте новый пакет в точку распространения.  

- При использовании последовательностей задач для установки драйверов создавайте пакеты, содержащие не более 500 драйверов.


### <a name="create-a-driver-package"></a><a name="BKMK_CreatingDriverPackages"></a> Создание пакета драйверов  

> [!IMPORTANT]  
> Для создания пакета драйверов необходима пустая сетевая папка, не используемая другим пакетом драйверов. В большинстве случаев перед выполнением этой процедуры создается новая папка.  

1. В консоли Configuration Manager перейдите к рабочей области **Библиотека программного обеспечения**. Разверните узел**Операционные системы** и выберите узел **Пакеты драйверов**.  

2. На вкладке ленты **Главная** в группе **Создать** выберите **Создать пакет драйверов**.  

3. Укажите описательное **имя** для пакета драйверов.  

4. К пакету драйверов при необходимости можно добавить **комментарий**. Это могут быть сведения о содержимом или предназначении пакета драйверов.  

5. В поле **Путь** укажите исходную папку пакета драйверов. Каждому пакету драйверов требуется отдельная папка. Путь является обязательным параметром, определяющим расположение пакета в сети.  

   > [!IMPORTANT]  
   > Учетной записи сервера сайта должны быть предоставлены разрешения на **полный доступ** к указанной исходной папке.  

Новый пакет драйверов не содержит драйверов. Следующий шаг заключается в добавлении драйверов в пакет.  

Если узел **Пакеты драйверов** содержит несколько пакетов, можно создать в нем папки, чтобы разделить пакеты на логические группы.  


### <a name="additional-actions-for-driver-packages"></a><a name="BKMK_PackageActions"></a> Дополнительные действия для пакетов драйверов  

Выбрав в узле **Пакеты драйверов** один или несколько пакетов драйверов, можно выполнить дополнительные действия по управлению пакетами драйверов. 


#### <a name="create-prestage-content-file"></a>Создать файл с предварительно подготовленным содержимым
Создаются файлы, которые можно использовать для импорта содержимого и связанных метаданных вручную. Следует использовать предварительно подготовленное содержимое при низкоскоростном соединении между сервером сайта и точками распространения, в которых сохранен пакет драйверов.

#### <a name="delete"></a>Удалить
Удаляет пакет драйверов из узла **Пакеты драйверов** .

#### <a name="distribute-content"></a>Распространение содержимого
Распространяет пакет драйверов в в точки распространения, группы точек распространения, а также группы точек распространения, связанные с коллекциями.

#### <a name="manage-access-accounts"></a>Управление учетными записями доступа
Добавляет, изменяет или удаляет учетные записи пакета драйвера.

Дополнительные сведения об учетных записях доступа к пакетам см. в статье [Учетные записи, используемые в Configuration Manager](../../core/plan-design/hierarchy/accounts.md).

#### <a name="move"></a>Переместить
Перемещает пакет драйверов в другую папку узла **Пакеты драйверов** .

#### <a name="update-distribution-points"></a>Обновить точки распространения
Обновляет пакет драйвера устройства на всех точках распространения, где хранится этот пакет. Это действие копирует только содержимое, которое было изменено со времени последней операции распространения.

#### <a name="properties"></a>Элемент Property
Отображается диалоговое окно **Свойства**. Оно позволяет просматривать и изменять содержимое и свойства драйвера (например, изменять имя и описание драйвера, включать или отключать его и указывать поддерживаемые драйвером платформы). 

<!--3607716, fka 1358270-->
Начиная с версии 1810 в пакеты драйверов добавлены дополнительные поля метаданных — **Производитель** и **Модель**. Используйте эти поля, чтобы пометить пакеты драйверов сведениями, упрощающими общее обслуживание или помогающими определить старые и дублирующиеся драйверы, которые можно удалить. На вкладке **Общие** выберите существующее значение в раскрывающемся списке или введите строку для создания новой записи.

В узле **Пакеты драйверов** эти поля отображаются в списке как столбцы **Производитель драйвера** и **Модель драйвера**. Их также можно использовать как условия поиска.

Начиная с версии 1906, эти атрибуты используются для предварительного кэширования содержимого на клиенте. Дополнительные сведения см. в разделе [Настройка предварительного кэширования содержимого](../deploy-use/configure-precache-content.md).<!--4224642-->  




## <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a> Драйверы устройств

Драйверы можно установить на конечных компьютерах, не включая их в развертываемый образ ОС. Configuration Manager предоставляет каталог драйверов, содержащий ссылки на все драйверы, импортируемые в Configuration Manager. Каталог драйверов размещается в рабочей области **Библиотека программного обеспечения** и состоит из двух узлов: **Драйверы** и **Пакеты драйверов**. Узел **Драйверы** содержит список всех драйверов, импортированных в каталог драйверов.  


### <a name="import-device-drivers-into-the-driver-catalog"></a><a name="BKMK_ImportDrivers"></a> Импорт драйверов устройств в каталог драйверов  

Прежде чем использовать драйвер при развертывании ОС, импортируйте его в каталог драйверов. Чтобы оптимизировать управление драйверами, импортируйте только те драйверы, которые вы планируете установить в ходе развертывания ОС. В каталоге драйверов можно хранить несколько версий драйверов устройств. Это упрощает обновление установленных драйверов устройств при изменении требований к оборудованию в сети.  

В ходе импорта драйвера устройства Configuration Manager считывает следующие его свойства:
- Поставщик
- Class
- Версия
- Подпись
- Поддерживаемое оборудование
- Сведения о поддерживаемых платформах

По умолчанию драйверу назначается имя в соответствии с поддерживающим его устройством. Драйвер устройства можно впоследствии переименовать. Список поддерживаемых платформ основан на сведениях в INF-файле драйвера. Так как точность этих сведений может отличаться, следует вручную проверять, поддерживается ли импортированный в каталог драйвер.  

Импортированные в каталог драйверы устройств можно добавлять в пакеты драйверов или пакеты образов загрузки.  

> [!IMPORTANT]  
> Нельзя импортировать драйверы устройств напрямую в подпапку узла **Драйверы**. Чтобы импортировать драйвер в подпапку, сначала следует импортировать драйвер устройства в узел **Драйверы** , после чего переместить драйвер в подпапку.  


#### <a name="process-to-import-windows-device-drivers-into-the-driver-catalog"></a>Импорт драйверов устройств Windows в каталог драйверов  

1. В консоли Configuration Manager перейдите к рабочей области **Библиотека программного обеспечения**. Разверните узел**Операционные системы** и выберите узел **Драйверы**.  

2. На вкладке ленты **Главная** в группе **Создать** выберите **Импортировать драйвер**, чтобы запустить **Мастер импорта нового драйвера**.  

3. На странице **Поиск драйвера** укажите следующие параметры:  

    - **Импортировать все драйверы из следующего сетевого пути (UNC)** . Чтобы импортировать все драйверы устройств из определенной папки, укажите ее сетевой путь. Например, так: `\\servername\share\folder`.  

        > [!NOTE]  
        > Если в папке много вложенных папок и INF-файлов драйверов, этот процесс может занять некоторое время.  

    - **Импортировать конкретный драйвер**. Чтобы импортировать определенный драйвер из папки, укажите сетевой путь к INF-файлу драйвера устройства Windows.  

    - **Укажите способ обработки повторяющихся драйверов**. Укажите, каким образом Configuration Manager будет осуществлять управление категориями драйверов при импорте дублированного драйвера устройства.  
        - **Импортировать драйвер и добавить новую категорию к существующим**.  
        - **Импортировать драйвер и сохранить существующие категории**.  
        - **Импортировать драйвер и перезаписать существующие категории**.  
        - **Не импортировать драйвер**.  

    > [!IMPORTANT]  
    > При импорте драйверов сервер сайта должен иметь разрешение на **чтение** для папки, в противном случае импорт завершится неудачей.  

4. На странице **Сведения о драйвере** укажите следующие параметры:  

    - **Скрыть драйверы, не входящие в класс хранения или сети (для образов загрузки)** : Используйте этот параметр, чтобы отобразить только сетевые драйверы и драйверы запоминающих устройств. Этот параметр позволяет скрыть прочие драйверы, которые обычно не требуются для образа загрузки, например драйверы видеокарты или модема.  

    - **Скрыть драйверы без цифровой подписи**: Корпорация Майкрософт рекомендует использовать только драйверы с цифровой подписью.  

    - В списке драйверов выберите драйверы, которые необходимо импортировать в каталог драйверов.  

    - **Разрешить эти драйверы и позволить компьютерам их установку**. Выберите этот параметр, чтобы разрешить компьютерам установку драйверов устройств. Этот параметр по умолчанию включен.  

        > [!IMPORTANT]  
        > Если драйвер устройства вызвал проблему или требуется приостановить установку драйвера устройства, отключите его во время импорта. Драйверы также можно отключить после импорта.  

    - Выберите **Категории**, чтобы назначить драйверам устройств административную категорию для фильтрации, например "Настольные компьютеры" или "Ноутбуки". Затем выберите существующую категорию или создайте новую. Категории позволяют контролировать применение тех или иных драйверов с помощью такого шага последовательности задач, как [Автоматическое применение драйверов](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).  

5. На странице **Добавление драйвера в пакеты** укажите, следует ли добавить драйверы в пакет.  

    - Выберите пакеты драйверов, используемые для распространения драйверов устройств.  

        При необходимости выберите **Создать пакет**, чтобы создать пакет драйверов. При создании пакета драйверов укажите общую сетевую папку, не используемую другими пакетами драйверов.  

    - Если пакет уже передан в точки распространения, выберите **Да** в диалоговом окне для обновления образов загрузки в точках распространения. Нельзя использовать драйверы устройств пока они не будут переданы в точки распространения. Если вы выбрали **Нет**, выполните действие **Обновить точку распространения**, прежде чем использовать образ загрузки. Если пакет драйверов не передавался в точки распространения, нужно выполнить действие **Распространить содержимое** в узле **Пакеты драйверов**.  

6. На странице **Добавление драйвера в загрузочные образы** укажите, следует ли добавлять драйверы устройств в существующие образы загрузки.  

    > [!NOTE]  
    > В образы загрузки добавляйте только сетевые драйверы и драйверы запоминающих устройств.  

    - В диалоговом окне выберите **Да** для обновления загрузочных образов в точках распространения. Нельзя использовать драйверы устройств пока они не будут переданы в точки распространения. Если вы выбрали **Нет**, выполните действие **Обновить точку распространения**, прежде чем использовать образ загрузки. Если пакет драйверов не передавался в точки распространения, нужно выполнить действие **Распространить содержимое** в узле **Пакеты драйверов**.  

    - Configuration Manager выдает предупреждение, если архитектура одного или нескольких драйверов не соответствует архитектуре выбранных загрузочных образов. При их несоответствии выберите **ОК**. Вернитесь на страницу **Сведения о драйвере** и удалите драйверы, которые не соответствуют архитектуре выбранного загрузочного образа. Например, если выбран загрузочный образ x64 и x86, все драйверы должны поддерживать обе архитектуры. Если выбран загрузочный образ x64, все драйверы должны поддерживать архитектуру x64.  

        > [!NOTE]  
        > - Архитектура основана на архитектуре, указанной в INF-файле производителя.  
        > - Если драйвер сообщает, что он поддерживает обе архитектуры, его можно импортировать в любой загрузочный образ.  

    - Configuration Manager выдает предупреждение, если в загрузочный образ добавляются драйверы устройств, которые не являются сетевыми драйверами или драйверами запоминающих устройств. В большинстве случаев такие драйверы не нужны в загрузочном образе. Выберите **Да**, чтобы добавить драйверы в загрузочный образ, или **Нет**, чтобы вернуться назад и выбрать другие драйверы.  

    - Configuration Manager выдает предупреждение, если один или несколько выбранных драйверов не имеют правильной цифровой подписи. Выберите **Да**, чтобы продолжить, или **Нет**, чтобы вернуться назад и выбрать другие драйверы.  

7. Завершите работу мастера.  


### <a name="manage-device-drivers-in-a-driver-package"></a><a name="BKMK_ModifyDriverPackage"></a> Управление драйверами устройств в пакете драйверов  

Используйте следующие процедуры для изменения пакетов драйверов и образов загрузки. Чтобы добавить или удалить драйвер, сначала найдите его в узле **Драйверы**. Затем измените пакеты или образы загрузки, с которыми связан выбранный драйвер.  

1. В консоли Configuration Manager перейдите к рабочей области **Библиотека программного обеспечения**. Разверните узел**Операционные системы** и выберите узел **Драйверы**.  

2. Выберите драйверы устройств, которые требуется добавить в пакет драйверов.  

3. На вкладке ленты **Главная** в группе **Драйвер** щелкните **Изменить** и выберите **Пакеты драйверов**.  

4. Чтобы добавить драйвер устройства, установите флажки пакетов драйверов, в которые будут добавлены драйверы устройств. Чтобы удалить драйвер устройства, снимите флажки пакетов драйверов, из которых будет удален драйвер устройства.  

    При добавлении драйверов устройств, которые связаны с пакетами драйверов, при необходимости можно создать новый пакет. Выберите **Создать пакет**, чтобы открыть диалоговое окно **Создание пакета драйверов**.  

5. Если пакет уже передан в точки распространения, выберите **Да** в диалоговом окне для обновления образов загрузки в точках распространения. Нельзя использовать драйверы устройств пока они не будут переданы в точки распространения. Если вы выбрали **Нет**, выполните действие **Обновить точку распространения**, прежде чем использовать образ загрузки. Если пакет драйверов не передавался в точки распространения, нужно выполнить действие **Распространить содержимое** в узле **Пакеты драйверов**. Перед тем как драйверы станут доступными, необходимо обновить пакет драйверов в точках распространения.  

    Выберите **ОК** после завершения.  


### <a name="manage-device-drivers-in-a-boot-image"></a><a name="BKMK_ManageDriversBootImage"></a> Управление драйверами устройств в образе загрузки  

Драйверы устройств Windows, импортированные в каталог драйверов, можно добавлять в загрузочные образы. При добавлении драйверов устройств в загрузочный образ следуйте приведенным ниже рекомендациям.  

- В образы загрузки добавляйте только сетевые драйверы и драйверы запоминающих устройств. Другие типы драйверов обычно не требуются в Windows PE. Лишние драйверы приводят к ненужному увеличению размера загрузочного образа.  

- В загрузочный образ добавляйте только драйверы устройств для Windows 10. Требуемая версия среды предустановки Windows основана на Windows 10.  

- Используйте драйверы устройств, соответствующие архитектуре загрузочного образа. Не добавляйте 32-разрядные (x86) драйверы устройств в 64-разрядный (x64) загрузочный образ.  

#### <a name="process-to-modify-the-device-drivers-associated-with-a-boot-image"></a>Изменение драйверов устройств, связанных с образом загрузки  

1. В консоли Configuration Manager перейдите к рабочей области **Библиотека программного обеспечения**. Разверните узел**Операционные системы** и выберите узел **Драйверы**.  

2. Выберите драйверы устройств, которые требуется добавить в пакет драйверов.  

3. На вкладке ленты **Главная** в группе **Драйвер** щелкните **Изменить** и выберите **Образы загрузки**.  

4. Чтобы добавить драйвер устройства, установите флажок загрузочного образа, в который будут добавлены драйверы устройств. Чтобы удалить драйвер устройства, снимите флажок загрузочного образа, из которого будет удален  драйвер устройства.  

5. Если не требуется обновлять точки распространения, в которых сохраняется загрузочный образ, снимите флажок **Обновить точки распространения по завершении**. По умолчанию точки распространения обновляются одновременно с обновлением загрузочного образа.  

    - В диалоговом окне выберите **Да** для обновления загрузочных образов в точках распространения. Нельзя использовать драйверы устройств пока они не будут переданы в точки распространения. Если вы выбрали **Нет**, выполните действие **Обновить точку распространения**, прежде чем использовать образ загрузки. Если пакет драйверов не передавался в точки распространения, нужно выполнить действие **Распространить содержимое** в узле **Пакеты драйверов**.  

    - Configuration Manager выдает предупреждение, если архитектура одного или нескольких драйверов не соответствует архитектуре выбранных загрузочных образов. При их несоответствии выберите **ОК**. Вернитесь на страницу **Сведения о драйвере** и удалите драйверы, которые не соответствуют архитектуре выбранного загрузочного образа. Например, если выбран загрузочный образ x64 и x86, все драйверы должны поддерживать обе архитектуры. Если выбран загрузочный образ x64, все драйверы должны поддерживать архитектуру x64.  

        > [!NOTE]
        > - Архитектура основана на архитектуре, указанной в INF-файле производителя.  
        > - Если драйвер сообщает, что он поддерживает обе архитектуры, его можно импортировать в любой загрузочный образ.  

    - Configuration Manager выдает предупреждение, если в загрузочный образ добавляются драйверы устройств, которые не являются сетевыми драйверами или драйверами запоминающих устройств. В большинстве случаев такие драйверы не нужны в загрузочном образе. Выберите **Да**, чтобы добавить драйверы в загрузочный образ, или **Нет**, чтобы вернуться назад и выбрать другие драйверы.  

    - Configuration Manager выдает предупреждение, если один или несколько выбранных драйверов не имеют правильной цифровой подписи. Выберите **Да**, чтобы продолжить, или **Нет**, чтобы вернуться назад и выбрать другие драйверы.  


### <a name="additional-actions-for-device-drivers"></a><a name="BKMK_DriverActions"></a> Дополнительные действия для драйверов устройств  

Можно выполнить дополнительные действия по управлению драйверами, выбрав их в узле **Драйверы**.  

#### <a name="categorize"></a>Категория
Позволяет удалить или назначить административную категорию для выбранных драйверов, а также управлять категориями.

#### <a name="delete"></a>Удалить
Удаляет драйвер из узла **Драйверы** и связанных точек распространения.

#### <a name="disable"></a>Отключено
Запрещает установку драйвера. Это действие временно отключает драйвер. Последовательность задач не сможет установить отключенный драйвер при развертывании ОС. 

> [!Note]  
> Это действие препятствует установке драйвера только при использовании шага последовательности задач **Автоматическое применение драйверов**.

#### <a name="enable"></a>Включите параметр
Позволяет клиентским компьютерам и последовательностям задач Configuration Manager устанавливать драйверы устройств при развертывании ОС.

#### <a name="move"></a>Переместить
Перемещает драйвер устройства в другую папку узла **Драйверы** .

#### <a name="properties"></a>Элемент Property
Отображается диалоговое окно **Свойства**. Позволяет просматривать и изменять содержимое и свойства драйвера (например, изменять имя и описание драйвера, включать или отключать его и указывать поддерживаемые драйвером платформы).



## <a name="use-task-sequences-to-install-drivers"></a><a name="BKMK_TSDrivers"></a> Использование последовательностей задач для установки драйверов устройств  

Последовательности задач позволяют автоматизировать развертывание ОС. На каждом шаге последовательности задач выполняется определенное действие, например установка драйвера. Для установки драйверов устройств в ходе развертывания ОС можно использовать такие два шага последовательности задач:  

- [Автоматическое применение драйверов](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers). Этот шаг позволяет автоматически сопоставлять и устанавливать драйверы устройств в ходе развертывания операционной системы. Этот шаг последовательности задач можно настроить так, чтобы устанавливались только наиболее подходящие драйверы для каждого обнаруженного устройства. Также можно задать установку всех совместимых драйверов для всех обнаруженных устройств, после чего программа установки Windows выберет оптимальные драйверы. Также можно указать категорию драйверов, чтобы ограничить набор драйверов, доступных на этом шаге.  

- [Применить пакет драйверов](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage). Этот шаг позволяет сделать все драйверы устройств из определенного пакета драйверов доступными для программы установки Windows. Программа установки Windows будет искать нужные драйверы в указанных пакетах. При создании автономного носителя необходимо использовать этот шаг для установки драйверов устройств.  

При использовании этих шагов последовательности задач можно также указать способ установки драйверов на компьютер, на котором развертывается ОС. Дополнительные сведения см. в разделе [Управление последовательностями задач для их автоматизации](../deploy-use/manage-task-sequences-to-automate-tasks.md).  



## <a name="driver-reports"></a><a name="BKMK_DriverReports"></a> Отчеты о драйверах  

Для получения общих сведений о драйверах устройств в каталоге драйверов можно использовать ряд отчетов в категории **Управление драйверами** . Дополнительные сведения об отчетах см. в разделе [Введение в отчеты](../../core/servers/manage/introduction-to-reporting.md).

