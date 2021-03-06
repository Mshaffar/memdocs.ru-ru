---
title: Создание поэтапных развертываний
titleSuffix: Configuration Manager
description: Поэтапное развертывание позволяет автоматизировать развертывание программного обеспечения в нескольких коллекциях.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5af0b7c90225a1f42d55767a0296d7e2263f956f
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110463"
---
# <a name="create-phased-deployments-with-configuration-manager"></a>Создание поэтапных развертываний с помощью Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Поэтапные развертывания автоматизируют согласованное и последовательное развертывание программного обеспечения в нескольких коллекциях. Например, можно развернуть программное обеспечение в пилотной коллекции, а затем автоматически продолжить выпуск в соответствии с условиями успеха. Создайте поэтапные развертывания, по умолчанию состоящие из двух этапов, или настройте несколько этапов вручную. 

Создайте поэтапное развертывание для следующих объектов:
- **Последовательность задач**  
    - Поэтапное развертывание последовательностей задач не поддерживает установку с носителя или с помощью PXE-загрузки.   
- **Приложение** (начиная с версии 1806) <!--1358147-->  
- **Обновление программного обеспечения** (начиная с версии 1810) <!--1358146-->  
    - Невозможно использовать правила автоматического развертывания при поэтапном развертывании.

> [!Tip]  
> Поэтапное развертывание появилось в версии 1802 [на стадии предварительного выпуска](../../core/servers/manage/pre-release-features.md). Начиная с версии 1806 эта функция больше не считается функцией предварительной версии.<!--1356837-->  



## <a name="prerequisites"></a>Предварительные условия

#### <a name="security-scope"></a>Область безопасности
Развертывания, созданные с помощью функции поэтапного развертывания, невидимы для пользователей-администраторов, у которых не задана область безопасности **Все**. Дополнительные сведения см. в разделе [Области безопасности](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).

#### <a name="distribute-content"></a>Распространение содержимого
Передайте связанное содержимое в точку распространения, прежде чем создавать поэтапное развертывание приложения.<!--518293-->  

- **Приложение**. Выберите целевое приложение в консоли и используйте действие **Распространить содержимое** на ленте. Дополнительные сведения см. в разделе [Развертывание содержимого и управление им](../../core/servers/deploy/configure/deploy-and-manage-content.md).   

- **Последовательность задач**. Необходимо создать объекты, на которые имеются ссылки, такие как пакет обновления операционной системы, перед созданием последовательности задач. Распространите эти объекты перед созданием развертывания. Используйте действие **Распространить содержимое** для каждого объекта или последовательности задач. Для просмотра состояния всего указанного содержимого выберите последовательность задач и переключитесь на вкладку **Ссылки** в области сведений. Дополнительные сведения см. в разделе о типе конкретного объекта в статье [Подготовка к развертыванию ОС](../get-started/prepare-for-operating-system-deployment.md).   

- **Обновление программного обеспечения**: создайте пакет развертывания и распространите его. Используйте мастер загрузки обновлений программного обеспечения. Дополнительные сведения см. в статье [Скачивание обновлений программного обеспечения](../../sum/deploy-use/download-software-updates.md).  



## <a name="phase-settings"></a><a name="bkmk_settings"></a> Параметры этапа

Эти параметры уникальны для поэтапного развертывания. Настройте эти параметры при создании или редактировании этапов для управления планированием и поведением процесса поэтапного развертывания. 


#### <a name="criteria-for-success-of-the-first-phase"></a>Критерии успешного выполнения первого этапа  

- **Процент успешных развертываний**: укажите процент устройств с успешным развертыванием в качестве критерия успешного завершения первого этапа. По умолчанию это значение равно 95 %. Другими словами, сайт считает, что первый этап завершен успешно, если 95 % устройств имеют состояние соответствия требованиям **Успех** для этого развертывания. Сайт переходит ко второму этапу и создает развертывание программного обеспечения для следующей коллекции.  
- **Число успешно развернутых устройств**. Добавлено в Configuration Manager версии 1902. Укажите число устройств с успешным развертыванием в качестве критерия успешного завершения первого этапа. Этот параметр полезен, если размер коллекции изменяется и вам нужно определенное количество успешных развертываний устройств перед переходом к следующему этапу. <!--3555946-->


#### <a name="conditions-for-beginning-second-phase-of-deployment-after-success-of-the-first-phase"></a>Условия начала второго этапа развертывания после успешного завершения первого этапа  

- **Автоматически начать этот этап после периода отсрочки (в днях)** : выберите число дней до начала второго этапа после успешного завершения первого этапа. По умолчанию это один день.  

- **Начать второй этап развертывания вручную**: сайт не запустит второй этап автоматически после успешного завершения первого этапа. Этот параметр требует запуска второго этапа вручную. Дополнительные сведения см. в разделе [Переход к следующему этапу](manage-monitor-phased-deployments.md#bkmk_move).  

    > [!Note]  
    > Этот параметр недоступен для поэтапного развертывания приложений.  


#### <a name="gradually-make-this-software-available-over-this-period-of-time-in-days"></a>Постепенно сделать это программное обеспечение доступным за указанный период времени (в днях)
<!--1358578-->
Начиная с версии 1806 можно настроить этот параметр для постепенного развертывания на каждом этапе. Это позволяет уменьшить риск возникновения проблем при развертывании и снижает нагрузку на сеть, вызванную распространением содержимого на клиенты. Сайт постепенно предоставляет доступ к программному обеспечению с учетом настроек для каждого этапа. Для каждого клиента на каждом этапе устанавливается крайний срок, который отсчитывается с момента предоставления доступа к программному обеспечению. Промежуток времени между временем доступности и крайним сроком одинаков для всех клиентов в пределах этапа. По умолчанию для него применяется значение ноль, то есть регулирование для развертывания не применяется. Не устанавливайте значение больше 30.<!--SCCMDocs-pr issue 2767--> 

![Параметры критериев успешного поэтапного развертывания](media/phased-deployment-criteria-for-success.png)

#### <a name="configure-the-deadline-behavior-relative-to-when-the-software-is-made-available"></a>Настроить поведение при достижении крайнего срока, связанного с предоставлением доступа к программному обеспечению  

- **Как можно скорее**: задает крайний срок для установки на устройстве, как только устройство будет выбрано в качестве целевого.  

- **Установка требуется по истечении этого периода**: задает крайний срок для установки в виде определенного числа дней после того, как устройство будет выбрано в качестве целевого. По умолчанию установлено 7 дней.   


<!--### Examples
Include a timeline diagram
-->



## <a name="automatically-create-a-default-two-phase-deployment"></a><a name="bkmk_auto"></a> Автоматически проводить развертывание по умолчанию в два этапа

1. Запустите мастер создания поэтапного развертывания в консоли Configuration Manager. Это действие зависит от типа развертываемого программного обеспечения.  

    - **Приложение** (только в версии 1806 или более поздней): перейдите в область **Библиотека программного обеспечения**, разверните узел **Управление приложениями** и выберите **Приложения**. Выберите существующее приложение и щелкните на ленте элемент **Создать поэтапное развертывание**.  

    - **Обновление программного обеспечения** (только в версии 1810 или более поздней): перейдите в область **Библиотека программного обеспечения** разверните узел **Обновления программного обеспечения** и выберите **Все обновления программного обеспечения**. Выберите одно обновление или несколько и щелкните на ленте элемент **Создать поэтапное развертывание**.  

        Это действие доступно для обновлений программного обеспечения из следующих узлов:  
        - Обновления программного обеспечения  
            - **Все обновления программного обеспечения**  
            - **Группы обновлений программного обеспечения**   
        - Обслуживание Windows 10, **все обновления Windows 10**  
        - Управление клиентами Office 365, **Обновления Office 365**  

    - **Последовательность задач**. Перейдите в рабочую область **Библиотека программного обеспечения**, разверните узел **Операционные системы** и выберите элемент **Последовательности задач**. Выберите существующую последовательность задач, а затем на ленте щелкните **Создать поэтапное развертывание**.  

2. На вкладке **Общие** присвойте поэтапному развертыванию **имя**, **описание** (необязательно) и выберите **Автоматически проводить развертывание по умолчанию в два этапа**.  

3. Нажмите **Обзор** и выберите целевую коллекцию для полей **Первая коллекция** и **Вторая коллекция**. Для последовательности задач и обновлений программного обеспечения выберите коллекции устройств. Для приложения выберите из коллекций пользователей или устройств. Выберите **Далее**.  

    > [!Important]  
    > Мастер создания поэтапного развертывания не уведомляет вас, если развертывание потенциально имеет высокий риск. Дополнительные сведения см. в разделе [Параметры для управления развертываниями с высоким риском](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) и примечание в разделе [Развертывание последовательности задач](deploy-a-task-sequence.md).  

4. На странице **Параметры** выберите одно значение для каждого из параметров планирования. Дополнительные сведения см. в разделе о [параметрах этапа](#bkmk_settings). Выполнив все необходимые операции, нажмите кнопку **Далее**.  

5. На странице **Этапы** посмотрите два этапа, которые мастер создает для указанной коллекции. Выберите **Далее**. Эти инструкции предназначены для автоматического создания развертывания в два этапа по умолчанию. Мастер позволяет добавлять, удалять, изменять порядок, редактировать или просматривать этапы для поэтапного развертывания. Сведения о дополнительных действиях см. в разделе о [создании поэтапного развертывания с использованием настраиваемых вручную этапов](#bkmk_manual).  

6. Подтвердите свой выбор на вкладке **Сводка**, а затем нажмите кнопку **Далее**, чтобы завершить мастер.  

> [!NOTE]
> Начиная с 21 апреля 2020 г. Office 365 профессиональный плюс переименовывается в **Приложения Microsoft 365 для предприятия**. Дополнительные сведения см. в статье [Изменение названия Office 365 профессиональный плюс](https://docs.microsoft.com/deployoffice/name-change). Пока консоль обновляется, в Configuration Manager и сопутствующей документации может встречаться старое название.  

## <a name="create-a-phased-deployment-with-manually-configured-phases"></a><a name="bkmk_manual"></a> Создание поэтапного развертывания с использованием настраиваемых вручную этапов
<!--1358148--> 

Начиная с версии 1806 доступно создание поэтапного развертывания с использованием настраиваемых вручную этапов для последовательности задач. Добавьте до 10 этапов на вкладке **Этапы** в мастере создания поэтапного развертывания. 

> [!Note]  
> В настоящее время создавать этапы для приложения вручную невозможно. Мастер автоматически создает два этапа для развертывания приложений.


1. Запустите мастер создания поэтапного развертывания для обновлений программного обеспечения или последовательности задач.  

2. На странице **Общие** в мастере создания поэтапного развертывания присвойте поэтапному развертыванию **имя**, **описание** (необязательно) и выберите **Настроить все этапы вручную**.  

3. На странице **Этапы** мастера создания поэтапного развертывания доступны следующие действия:  

    - **Фильтр** — для фильтрации списка этапов развертывания. Введите строку символов для поиска по столбцам "Порядок", "Имя" или "Коллекция" без учета регистра. 

    - **Добавить** — для добавления нового этапа:  

        1. На странице **Общие** мастера добавления этапа укажите **имя** этапа, а затем перейдите к целевой **коллекции этапов**. Дополнительные параметры на этой странице такие же, как при обычном развертывании последовательности задач или обновлений программного обеспечения.  

        2. На странице **Параметры этапа** мастера добавления этапа настройте параметры планирования, а затем нажмите кнопку **Далее**. Дополнительные сведения см. в разделе [Параметры](#bkmk_settings).   

            > [!Note]  
            > Вы не можете изменить параметры этапа (**Процент успешных развертываний** или **Число успешно развернутых устройств** (версия 1902 или более поздняя)) на первом этапе. Этот параметр применяется только для этапов, у которых есть предыдущие этапы.  

        3. Параметры на страницах **Взаимодействие с пользователем** и **Точки распространения** мастера добавления этапа такие же, как при обычном развертывании последовательности задач или обновлений программного обеспечения.  

        4. Просмотрите параметры на странице **Сводка** и завершите работу мастера добавления этапа.  

    - **Изменить**. Откроется окно свойств выбранного этапа с такими же вкладками, как в мастере добавления этапа.  

    - **Удалить**. Это действие удаляет выбранный этап.  

       > [!Warning]  
       > Вам не нужно будет подтверждать это действие, и вы не сможете его отменить.  

    - **Переместить вверх** или **Переместить вниз**. Мастер размещает этапы в том порядке, в каком вы их добавляете. Этапы, добавленные последними, будут внизу списка. Чтобы изменить порядок, выберите этап, нажмите на одну из кнопок и переместите этап в списке.  

       > [!Important]  
       > Проверьте параметры этапа после изменения порядка. Убедитесь, что следующие параметры по-прежнему соответствуют требованиям для этого поэтапного развертывания:  
       > 
       > - Условия успешного завершения предыдущего этапа  
       > - Условия начала этого этапа развертывания после успешного завершения предыдущего этапа   

5. Выберите **Далее**. Просмотрите параметры на странице **Сводка** и завершите работу мастера создания поэтапного развертывания.  


После создания поэтапного развертывания откройте его свойства для внесения изменений:  

- **Добавить** — добавьте дополнительные этапы в существующее поэтапное развертывание.  

- Если этап неактивен, вы можете **изменить**, **удалить**, или **переместить** ее вверх или вниз. Невозможно переместить его и расположить до активного этапа.  

- Активный этап доступен только для чтения. Его нельзя изменить, удалить или переместить в списке. Вы можете только **смотреть** свойства этапа.  

- Поэтапное развертывание приложения всегда доступно только для чтения.  



## <a name="next-steps"></a>Дальнейшие шаги

Мониторинг поэтапных развертываний и управление ими:
- [Приложение](manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)
- [Обновление программного обеспечения](manage-monitor-phased-deployments.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [Последовательность задач](manage-monitor-phased-deployments.md)  

