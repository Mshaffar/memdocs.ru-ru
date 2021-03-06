---
title: Настройка ролевого администрирования
titleSuffix: Configuration Manager
ms.date: 11/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 57413dd3-b2f8-4a5f-b27f-8464d357caff
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 14258c3e7e2cfe5423b97064a26fdf5616d6b0a4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078623"
---
# <a name="configure-role-based-administration-for-configuration-manager"></a>Настройка ролевого администрирования для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

В Configuration Manager ролевое администрирование сочетает роли безопасности, области безопасности и назначенные коллекции для определения области администрирования для каждого пользователя с правами администратора. В административную область входят объекты, которые пользователь может просматривать в консоли Configuration Manager, и задачи, связанные с теми объектами, на выполнение которых у пользователя есть разрешения. Конфигурации ролевого администрирования применяются к каждому сайту в иерархии.  

 Если вы не знакомы с концепцией ролевого администрирования, изучите статью [Основы ролевого администрирования для System Center Configuration Manager](../../../understand/fundamentals-of-role-based-administration.md).  

 Используйте сведения в следующих процедурах для создания и настройки ролевого администрирования и связанных параметров безопасности.  

- [Создание настраиваемых ролей безопасности](#BKMK_CreateSecRole)  
- [Настройка ролей безопасности](#BKMK_ConfigSecRole)  
- [Настройка областей безопасности для объекта](#BKMK_ConfigSecScope)  
- [Настройка коллекций для управления безопасностью](#BKMK_ConfigColl)  
- [Создание нового пользователя с правами администратора](#BKMK_Create_AdminUser)  
- [Изменение административной области пользователя с правами администратора](#BKMK_ModAdminUser)  

## <a name="create-custom-security-roles"></a><a name="BKMK_CreateSecRole"></a> Создание настраиваемых ролей безопасности

 Configuration Manager предоставляет несколько встроенных ролей безопасности. Если требуются дополнительные роли безопасности, можно создать настраиваемую роль безопасности путем копирования существующей роли и последующего изменения копии. Создание настраиваемой роли безопасности позволит предоставить пользователям требуемые дополнительные разрешения безопасности, которые не входят в текущую назначенную роль безопасности. С помощью настраиваемой роли безопасности пользователи получат только необходимые им разрешения. Назначение роли безопасности, которая предоставляет больше разрешений, чем нужно, в данном случае исключается.  

 Следующая процедура используется для создания новой роли безопасности с использованием существующей роли безопасности в качестве шаблона.  

### <a name="to-create-custom-security-roles"></a>Создание настраиваемых ролей безопасности

1. В консоли Configuration Manager щелкните **Администрирование**.  

2. В рабочей области **Администрирование** разверните узел **Безопасность** и выберите **Роли безопасности**.  

   Одна из следующих процедур используется для создания новой роли безопасности.  

    - Чтобы создать новую настраиваемую роль безопасности, выполните следующие действия.  

      1. Выберите существующую роль безопасности, которая будет использоваться в качестве основы новой роли безопасности.
      2. На вкладке **Главная** в группе **Роль безопасности** выберите **Копировать**. Это действие создает копию исходной роли безопасности.  
      3. В мастере копирования ролей безопасности укажите значение параметра **Имя** для новой настраиваемой роли безопасности.  
      4. В группе **Назначения операций безопасности**разверните каждый узел **Операции безопасности** , чтобы отобразить доступные действия.  
      5. Чтобы изменить параметр для операции безопасности, в столбце **Значение** нажмите кнопку со стрелкой вниз, а затем выберите **Да** или **Нет**.

            > [!CAUTION]  
            > При настройке роли безопасности не предоставляйте разрешения, которые не требуются пользователям, связанным с новой ролью безопасности. Например, значение **Изменить** для операции безопасности **Роли безопасности** дает пользователям право на изменение любой доступной роли безопасности, даже если эти пользователи не связаны с данной ролью.  

      6. Завершив настройку разрешений, нажмите кнопку **ОК** , чтобы сохранить новую роль безопасности.  

    - Чтобы импортировать роль безопасности, которая была экспортирована из другой иерархии Configuration Manager, выполните указанные ниже действия.  

        1. На вкладке **Главная** в группе **Создать** выберите **Импорт роли безопасности**.  
        2. Укажите XML-файл, содержащий конфигурацию роли безопасности для импорта. Выберите **Открыть**, чтобы завершить процедуру и сохранить роль безопасности.  

            > [!NOTE]  
            > После импорта роли безопасности можно отредактировать ее свойства, чтобы изменить разрешения объекта, связанные с ролью безопасности.  

## <a name="configure-security-roles"></a><a name="BKMK_ConfigSecRole"></a> Настройка ролей безопасности

 Группы разрешений безопасности, которые определены для роли безопасности, называются назначениями операций безопасности. Назначения операций безопасности представляют собой сочетание типов объектов и действий, доступных для каждого типа объекта. Вы можете изменить доступные операции безопасности для любой настраиваемой роли безопасности, однако изменить встроенные роли, предоставляемые Configuration Manager, нельзя.  

 Следующая процедура используется для изменения операций безопасности для роли безопасности.  

### <a name="to-modify-security-roles"></a>Изменение ролей безопасности

1. В консоли Configuration Manager выберите элемент **Администрирование**.  
2. В рабочей области **Администрирование** разверните узел **Безопасность** и выберите **Роли безопасности**.  
3. Выберите настраиваемую роль безопасности, которую требуется изменить.  
4. На вкладке **Главная** в группе **Свойства** нажмите кнопку **Свойства**.  
5. Перейдите на вкладку **Разрешения**.  
6. В группе **Назначения операций безопасности**разверните каждый узел **Операции безопасности** , чтобы отобразить доступные действия.  
7. Чтобы изменить параметр для операции безопасности, в столбце **Значение** нажмите кнопку со стрелкой вниз, а затем выберите **Да** или **Нет**.  

    > [!CAUTION]  
    > При настройке роли безопасности не предоставляйте разрешения, которые не требуются пользователям, связанным с новой ролью безопасности. Например, значение **Изменить** для операции безопасности **Роли безопасности** дает пользователям право на изменение любой доступной роли безопасности, даже если эти пользователи не связаны с данной ролью.  

8. Завершив настройку назначений операций безопасности, нажмите кнопку **ОК**, чтобы сохранить новую роль безопасности.  

##  <a name="configure-security-scopes-for-an-object"></a><a name="BKMK_ConfigSecScope"></a> Настройка областей безопасности для объекта
 Управление связью области безопасности для объекта осуществляется из объекта, а не из области безопасности. Единственными прямыми настройками, поддерживаемыми областями безопасности, являются изменения их имен и описаний. Чтобы изменить имя и описание области безопасности во время просмотра свойств области безопасности, требуется разрешение **Изменить** для защищаемого объекта **Области безопасности** .  

 Когда вы создаете в Configuration Manager новый объект, он сопоставляется с каждой областью безопасности, которая связана с ролями безопасности учетной записи, используемой для создания объекта. Это происходит, если роли безопасности предоставляют разрешение на **создание** или **настройку области безопасности**. Области безопасности для объекта можно изменить после его создания.  

 Например, вам назначена роль безопасности с правом на создание группы границ. При создании группы границ у вас нет объекта, которому можно назначить конкретные области безопасности. Тем не менее, области безопасности, доступные из связанных ролей безопасности, автоматически назначаются новой группе границ. После сохранения новой группы границ можно изменить области безопасности, связанные с новой группой границ.  

 Следующая процедура используется для настройки областей безопасности, назначенных объекту.  

### <a name="to-configure-security-scopes-for-an-object"></a><a name="bkmk_config-sec-scope"></a> Настройка областей безопасности для объекта  

1. В консоли Configuration Manager выберите объект, который поддерживает назначение области безопасности.  
2. На вкладке **Главная** в группе **Классификация** выберите **Установить области безопасности**.
3. В диалоговом окне **Установка ролей безопасности** выберите или отмените выбор областей безопасности, с которыми связан это объект. Каждый объект, который поддерживает области безопасности, должен быть назначен как минимум одной области безопасности.  
4. Нажмите кнопку **ОК** , чтобы сохранить назначенные области безопасности.  

    > [!NOTE]  
    > Новый создаваемый объект можно назначить нескольким областям безопасности. Чтобы изменить число областей безопасности, связанных с объектом, следует изменить данное назначение после создания объекта.

### <a name="to-configure-security-scopes-for-a-folder-starting-in-version-1906"></a><a name="bkmk_config-folder"></a> Настройка областей безопасности для папки (начиная с версии 1906)
<!--3600867-->

1. В консоли Configuration Manager выберите папку.  
1. На вкладке **Папка** на ленте выберите **Установить области безопасности**.
   - Вы также можете щелкнуть папку правой кнопкой мыши и выбрать **Папка** > **Установить области безопасности**.
1. В диалоговом окне **Установка ролей безопасности** выберите или отмените выбор областей безопасности для папки. Необходимо назначить минимум одну область безопасности каждой папке. Всем папкам назначена область безопасности **по умолчанию**, пока вы не измените ее.
1. Нажмите кнопку **ОК** , чтобы сохранить назначенные области безопасности.  

    > [!IMPORTANT]  
    > - Имеющиеся роли безопасности автоматически получают разрешения **класса папок**, добавленные при установке Configuration Manager версии 1906. Вам необходимо добавить разрешения **класса папок** для новых ролей безопасности и убедиться, что существующие роли имеют соответствующие разрешения для вашей среды.
    > 
    > - Элемент доступен для поиска в папке за пределами области безопасности пользователя, если пользователь совместно использует область безопасности с тем, кто создал этот объект. <!--5602690-->

## <a name="configure-collections-to-manage-security"></a><a name="BKMK_ConfigColl"></a> Настройка коллекций для управления безопасностью

 Процедур по настройке коллекций для ролевого администрирования не существует. У коллекций нет конфигураций ролевого администрирования. Коллекции назначаются пользователю во время его настройки. Операции безопасности коллекции, которые включены в назначенных пользователю ролях безопасности, определяют разрешения пользователя для коллекций и ресурсов коллекций (элементов коллекции).  

 Если у пользователя есть разрешения для коллекции, ему также предоставляются разрешения для коллекций, ограниченных данной коллекцией. Предположим, что ваша организация использует коллекцию с именем "Все компьютеры". Также есть коллекция с именем "Все компьютеры России", которая ограничена коллекцией "Все настольные компьютеры". Если пользователь имеет разрешения для коллекции "Все настольные компьютеры", он может пользоваться этими же разрешениями и для коллекции "Все настольные компьютеры России".

 Кроме того, администратор не может использовать разрешение **Удалить** или **Изменить** в коллекции, которая назначена ему непосредственно. Но эти разрешения действуют в коллекциях, ограниченных данной коллекцией. Вернемся к предыдущему примеру. Пользователь может удалить или изменить коллекцию "Все настольные компьютеры Северной Америки", но не может удалить или изменить коллекцию "Все настольные компьютеры".  

## <a name="create-a-new-administrative-user"></a><a name="BKMK_Create_AdminUser"></a> Создание нового пользователя с правами администратора

 Чтобы предоставить отдельным пользователям или членам группы безопасности права на управление Configuration Manager, создайте пользователя в Configuration Manager и укажите учетную запись Windows "Пользователь" или "Группа пользователей". Каждому пользователю с правами администратора в Configuration Manager необходимо назначить по крайней мере одну роль безопасности и одну область безопасности. Чтобы ограничить административную область пользователя, можно также назначить коллекции.  

 Ниже приведены процедуры создания новых администраторов.  

### <a name="to-create-a-new-administrative-user"></a>Создание нового администратора  

1. В консоли Configuration Manager выберите элемент **Администрирование**.  
2. В рабочей области **Администрирование** разверните узел **Безопасность** и выберите **Пользователи**.  
3. На вкладке **Главная** в группе **Создать** щелкните **Добавление пользователя или группы**.  
4. Щелкните **Обзор** и выберите учетную запись пользователя или группу для нового администратора.  

    > [!NOTE]  
    > Если используется администрирование на основе консоли, в качестве администраторов можно указать только пользователей домена или группы безопасности.

5. На вкладке **Associated security roles** (Связанные роли безопасности) выберите **Добавить**, чтобы открыть список доступных ролей безопасности, установите флажок для одной или нескольких ролей безопасности, а затем нажмите кнопку **ОК**.  

6. Выберите один из следующих двух вариантов, чтобы определить режим обработки защищаемых объектов для нового пользователя.  

    - **Все экземпляры объектов, связанные с назначенными ролями безопасности**. Этот параметр сопоставляет администратора с областью безопасности **Все** и коллекциями **Все системы** и **Все пользователи и группы пользователей**. Роли безопасности, назначенные пользователю, определяют доступ к объектам. Новые объекты, создаваемые этим администратором, назначаются области безопасности **По умолчанию** .  

    - **Только экземпляры объектов, назначенные указанным областям безопасности и коллекциям**. По умолчанию этот параметр сопоставляет администратора с областью безопасности **По умолчанию** и коллекциями **Все системы** и **Все пользователи и группы пользователей**. Однако фактические области безопасности и коллекции ограничиваются теми, которые связаны с учетной записью, используемой для создания нового администратора. Этот параметр поддерживает добавление и удаление областей безопасности и коллекций для настройки области администрирования администратора.  

    > [!IMPORTANT]  
    > Предыдущий параметр связывает каждую назначенную область безопасности и коллекцию с каждой ролью безопасности, назначенной администратору. Третий параметр, **Связать назначенные роли безопасности с определенными областями безопасности и коллекциями**, позволяет сопоставить отдельные роли безопасности с определенными областями безопасности и коллекциями. Третий вариант становится доступным после создания нового администратора, когда выполняется его изменение.  

7. В зависимости от варианта, выбранного в действии 6, выполните следующие действия.  

    - Если вы выбрали параметр **Все экземпляры объектов, относящиеся к назначенным ролям безопасности**, нажмите кнопку **ОК**, чтобы завершить процедуру.  

    - Если выбран параметр **Только экземпляры объектов, назначенные указанным областям безопасности и коллекциям**, можно щелкнуть **Добавить** и выбрать коллекции и области безопасности. Или вы можете выбрать в списке один или несколько объектов и щелкнуть **Удалить**, чтобы удалить их. Нажмите кнопку **ОК**, чтобы завершить эту процедуру.  

## <a name="modify-the-administrative-scope-of-an-administrative-user"></a><a name="BKMK_ModAdminUser"></a> Изменение административной области пользователя с правами администратора

 Административную область администратора можно изменить, добавив или удалив роли безопасности, области безопасности и коллекции, связанные с этим пользователем. Каждому администратору необходимо назначить как минимум одну роль безопасности и одну область безопасности. Административной области пользователя может потребоваться назначить одну или несколько коллекций. Большинство ролей безопасности взаимодействует с коллекциями и функционирует неправильно, если коллекция не назначена.  

 При внесении изменений в параметры администратора можно изменить режим связывания защищенных объектов с назначенными ролями безопасности. Ниже приведены три режима, которые можно выбрать.  

- **Все экземпляры объектов, связанные с назначенными ролями безопасности**. Этот параметр сопоставляет администратора с областью **Все** и коллекциями **Все системы** и **Все пользователи и группы пользователей**. Роли безопасности, назначенные пользователю, определяют доступ к объектам.  

- **Только экземпляры объектов, назначенные указанным областям безопасности и коллекциям**. При выборе этого варианта администратор связывается с теми же областями безопасности и коллекциями, которые связаны с учетной записью, используемой для настройки администратора. Этот параметр поддерживает добавление и удаление ролей безопасности и коллекций для настройки области администрирования администратора.  

- **Связать назначенные роли безопасности с определенными областями безопасности и коллекциями**. Этот вариант позволяет создать определенные связи между отдельными ролями безопасности и конкретными областями и коллекциями для пользователя.  

    > [!NOTE]  
    > Этот параметр доступен только при изменении свойств администратора.  

Текущая конфигурация режима обработки защищаемых объектов изменяет процесс, который используется для назначения дополнительных ролей безопасности. Ниже приведены процедуры управления администраторами, основанные на разных режимах обработки защищаемых объектов.  

Для просмотра и управления конфигурацией защищаемых объектов для администратора используется следующая процедура.  

### <a name="to-view-and-manage-the-securable-object-behavior-for-an-administrative-user"></a>Просмотр режима обработки защищаемых объектов для администратора и управление им  

1. В консоли Configuration Manager выберите элемент **Администрирование**.  
2. В рабочей области **Администрирование** разверните узел **Безопасность** и выберите **Пользователи**.  
3. Выберите администратора, свойства которого требуется изменить.  
4. На вкладке **Главная** в группе **Свойства** нажмите кнопку **Свойства**.  
5. Перейдите на вкладку **Области безопасности**, чтобы просмотреть текущую конфигурацию защищаемых объектов для этого администратора.  
6. Чтобы изменить режим обработки защищаемых объектов, выберите новый вариант режима обработки защищаемых объектов. Изменив эту конфигурацию, перейдите к соответствующей процедуре, содержащей дальнейшие указания по настройке областей безопасности и коллекций, а также ролей безопасности для этого администратора.  
7. Нажмите кнопку **OK**, чтобы завершить процедуру.  

Выполните процедуру ниже, чтобы изменить параметры администратора, для которого выбран режим обработки защищаемых объектов **Все экземпляры объектов, связанные с назначенными ролями безопасности**.  

### <a name="for-option-all-instances-of-the-objects-that-are-related-to-the-assigned-security-roles"></a>Для параметра "Все экземпляры объектов, связанные с назначенными ролями безопасности"  

1. В консоли Configuration Manager выберите элемент **Администрирование**.  
2. В рабочей области **Администрирование** разверните узел **Безопасность** и выберите **Пользователи**.  
3. Выберите администратора, свойства которого требуется изменить.  
4. На вкладке **Главная** в группе **Свойства** нажмите кнопку **Свойства**.  
5. Перейдите на вкладку **Области безопасности** и убедитесь, что для администратора задан режим **Все экземпляры объектов, связанные с назначенными ролями безопасности**.  
6. Чтобы изменить назначенные роли безопасности, перейдите на вкладку **Роли безопасности**.  

    - Чтобы назначить дополнительные роли безопасности для администратора, щелкните **Добавить**, установите флажки для нужных дополнительных ролей безопасности и нажмите кнопку **ОК**.  
    - Чтобы удалить роли безопасности, выберите одну или несколько ролей в списке и щелкните **Удалить**.

7. Чтобы изменить режим обработки защищаемых объектов, перейдите на вкладку **Области безопасности** и выберите другой вариант. Изменив эту конфигурацию, перейдите к соответствующей процедуре, содержащей дальнейшие указания по настройке областей безопасности и коллекций, а также ролей безопасности для этого администратора.  

    > [!NOTE]  
    > Если для режима обработки защищаемых объектов выбран вариант **Все экземпляры объектов, связанные с назначенными ролями безопасности**, вы не сможете добавить или удалить области безопасности и (или) коллекции.  

8. Нажмите кнопку **ОК**, чтобы завершить эту процедуру.  

Выполните процедуру ниже, чтобы изменить параметры администратора, для которого задан режим обработки защищаемых объектов **Только экземпляры объектов, назначенные указанным областям безопасности и коллекциям**.  

### <a name="for-option-only-the-instances-of-objects-that-are-assigned-to-the-specified-security-scopes-and-collections"></a>Для параметра "Только экземпляры объектов, назначенные указанным областям безопасности и коллекциям"  

1. В консоли Configuration Manager выберите элемент **Администрирование**.  
2. В рабочей области **Администрирование** разверните узел **Безопасность** и выберите **Пользователи**.  
3. Выберите администратора, свойства которого требуется изменить.  
4. На вкладке **Главная** в группе **Свойства** нажмите кнопку **Свойства**.  
5. Перейдите на вкладку **Области безопасности**, чтобы убедиться, что для пользователя задан режим **Только экземпляры объектов, назначенные указанным областям безопасности и коллекциям**.  
6. Чтобы изменить назначенные роли безопасности, перейдите на вкладку **Роли безопасности**.  

    - Чтобы назначить дополнительные роли безопасности для пользователя, выберите **Добавить**, установите флажки для нужных дополнительных ролей безопасности и нажмите кнопку **ОК**.  
    - Чтобы удалить роли безопасности, выберите одну или несколько ролей в списке и щелкните **Удалить**.  
7. Чтобы изменить области безопасности и коллекции, связанные с ролями безопасности, перейдите на вкладку **Области безопасности**.  

    - Чтобы связать новые области безопасности или коллекции со всеми ролями безопасности, назначенными этому администратору, щелкните **Добавить** и выберите один из четырех вариантов. При выборе варианта **Область безопасности** или **Коллекция**, чтобы завершить выбор, установите флажок для одного или нескольких объектов, а затем нажмите кнопку **ОК**.  
    - Чтобы удалить область безопасности или коллекцию, выберите объект и щелкните **Удалить**.

8. Нажмите кнопку **ОК**, чтобы завершить эту процедуру.  

Выполните процедуру ниже, чтобы изменить параметры администратора, для которого задан режим обработки защищаемых объектов **Связать назначенные роли безопасности с определенными областями безопасности и коллекциями**.  

### <a name="for-option-associate-assigned-security-roles-with-specific-security-scopes-and-collections"></a>Для параметра "Связать назначенные роли безопасности с определенными областями безопасности и коллекциями"  

1. В консоли Configuration Manager выберите элемент **Администрирование**.  
2. В рабочей области **Администрирование** разверните узел **Безопасность** и выберите **Пользователи**.  
3. Выберите администратора, свойства которого требуется изменить.  
4. На вкладке **Главная** в группе **Свойства** нажмите кнопку **Свойства**.  
5. Перейдите на вкладку **Области безопасности**, чтобы убедиться, что для администратора задан режим **Связать назначенные роли безопасности с определенными областями безопасности и коллекциями**.  
6. Чтобы изменить назначенные роли безопасности, перейдите на вкладку **Роли безопасности**.  

    - Чтобы назначить администратору дополнительные роли безопасности, выберите **Добавить**. В диалоговом окне **Добавление роли безопасности** выберите одну или несколько ролей безопасности, щелкните **Добавить** и выберите тип объекта, чтобы связать его с выбранными ролями безопасности. При выборе варианта **Область безопасности** или **Коллекция**, чтобы завершить выбор, установите флажок для одного или нескольких объектов, а затем нажмите кнопку **ОК**.  

        > [!NOTE]  
        > Прежде чем выбранные роли безопасности можно будет назначить администратору, необходимо настроить по крайней мере одну область безопасности. При выборе нескольких ролей безопасности каждая настраиваемая область безопасности и коллекция связывается с каждой из выбранных ролей безопасностей.  

    - Чтобы удалить роли безопасности, выберите одну или несколько ролей в списке и щелкните **Удалить**.  

7. Чтобы изменить области безопасности и коллекции, связанные с определенной ролью безопасности, перейдите на вкладку **Области безопасности**, выберите роль безопасности и щелкните **Изменить**.  

    - Чтобы связать новые объекты с этой ролью безопасности, щелкните **Добавить** и выберите тип объекта, связываемого с выбранными ролями безопасности. При выборе варианта **Область безопасности** или **Коллекция**, чтобы завершить выбор, установите флажок для одного или нескольких объектов, а затем нажмите кнопку **ОК**.  

        > [!NOTE]  
        > Необходимо настроить хотя бы одну область безопасности.  

    - Чтобы удалить область безопасности или коллекцию, связанную с этой ролью безопасности, выберите объект и щелкните **Удалить**.  

    - Завершив изменение связанных объектов, нажмите кнопку **ОК**.  

8. Нажмите кнопку **ОК**, чтобы завершить эту процедуру.  

    > [!CAUTION]  
    > Если роль безопасности предполагает предоставление администраторам разрешения на развертывание коллекции, такие администраторы могут распространять объекты из любой области безопасности, для которой у них имеется разрешение **чтение** , даже если эта область безопасности связана с другой ролью безопасности.  

## <a name="next-steps"></a>Дальнейшие шаги

[Учетные записи, используемые в Configuration Manager](../../../plan-design/hierarchy/accounts.md)
