---
title: Включение и исключение назначений приложений в Microsoft Intune
titleSuffix: ''
description: Сведения о том, как включать и исключать назначения приложений в Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c59f6df5-3317-4dff-8f19-fdeec33faedf
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5011e24064c4c546107f950925d12489ed9113c9
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79340610"
---
# <a name="include-and-exclude-app-assignments-in-microsoft-intune"></a>Включение и исключение назначений приложений в Microsoft Intune

В Intune вы можете управлять доступом к приложению, назначая группы включаемых и исключаемых пользователей. Прежде чем назначить приложению группы, необходимо выбрать тип назначения. Тип назначения указывает, что приложение доступно или обязательно, или удаляет приложение. 

Доступность приложения определяется сочетанием групповых назначений, с помощью которых вы можете включать и исключать группы пользователей или устройств. Эта возможность может оказаться полезной, когда для ограничения доступа к приложению сначала включается большая группа, а затем из нее исключается группа меньшего размера. Например, группа меньшего размера может представлять тестовую группу или группу руководителей. 

Мы рекомендуем создавать и назначать приложения специально для групп пользователей, а также отдельно для групп устройств. См. сведения о [добавлении групп для упорядочивания пользователей и устройств](../fundamentals/groups-add.md).  

При включении или исключении назначений приложений есть важные сценарии.

- Исключение имеет приоритет над включением в следующих сценариях с одним типом группы:
  - включение и исключение групп пользователей при назначении приложений;
  - включение и исключение групп устройств при назначении приложений.

    Например, можно назначить группу устройств для группы пользователей **Все корпоративные пользователи**, исключив при этом всех членов группы пользователей **Руководители старшего звена**. При этом группа **Все корпоративные пользователи**, кроме членов группы **Руководители старшего звена**, получит назначение, так как обе группы являются группами пользователей.
- Intune не учитывает связи групп "пользователь — устройство". Если вы назначаете приложения смешанным группам, результаты могут быть неожиданными.

    Например, можно назначить группу устройств группе пользователей **Все пользователи**, исключив при этом группу устройств **Все персональные устройства**. В этом смешанном назначении приложение будет назначено группе **Все пользователи**. Исключение при этом не выполняется.

Таким образом, назначать приложения смешанным группам не рекомендуется.

> [!NOTE]
> Указывая назначения групп для приложения, не используйте тип **Неприменимо**. Этот устаревший механизм заменен функцией исключения групп. 
>
> В консоли Intune доступны предварительно созданные группы **Все пользователи** и **Все устройства**. Чтобы вам было удобнее с ними работать, эти группы имеют ряд встроенных оптимизаций. Мы настоятельно рекомендуем использовать для охвата всех пользователей и всех устройств именно эти группы, и не создавать группы "Все пользователи" и "Все устройства" самостоятельно.  
>
> Android для бизнеса поддерживает включение и исключение групп. Вы можете использовать встроенные группы **Все пользователи** и **Все устройства** для назначения приложений Android для бизнеса. 

## <a name="include-and-exclude-groups-when-assigning-apps"></a>Включение и исключение групп при назначении приложений

Чтобы назначить приложение группам с использованием механизма включений и исключений, сделайте следующее:

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Приложения** > **Все приложения**. Вы увидите список добавленных приложений.
3. Выберите приложение, которое хотите назначить. Панель мониторинга отобразит сведения об этом приложении.
4. В разделе меню **Управление** выберите **Назначения**.

    ![Включение приложений в группы при назначении приложений группам](./media/apps-inc-exl-assignments/apps-inc-exl-01.png)

5. Выберите **Добавить группу**, чтобы добавить группу пользователей, которым назначено приложение. 
6. На панели **Добавить группу** выберите **Тип назначения** из списка доступных типов.
7. Выберите тип назначения **Доступно с регистрацией или без регистрации**.

    ![Назначение приложений Intune — добавление группы](./media/apps-inc-exl-assignments/apps-inc-exl-02.png)
8. Выберите **Включенные группы**, чтобы выбрать группы пользователей, которым должно быть доступно это приложение.

    > [!NOTE]
    > Если при добавлении группы уже есть другая включенная группа с выбранным типом назначения, такой тип становится фиксированным, и его нельзя будет изменить на другой. Вы не сможете назначить для включения группу, которая уже используется.

9. Выберите **Да**, чтобы сделать это приложение доступным для всех пользователей.

    ![Назначение приложений Intune — включение групп](./media/apps-inc-exl-assignments/apps-inc-exl-03.png)
10. Выберите **ОК**, чтобы задать включаемые группы.
11. Выберите **Исключенные группы**, чтобы выбрать группы пользователей, которым это приложение будет недоступно.
12. Выберите группы для исключения. Теперь это приложение будет недоступно для выбранных групп.

    ![Назначение приложений Intune — исключение групп](./media/apps-inc-exl-assignments/apps-inc-exl-04.png)
13. Щелкните **Выбрать**, чтобы завершить выбор групп.
14. На панели **Добавить группу** нажмите кнопку **OK**. Появится список **Назначения** для приложения.
15. Щелкните **Сохранить**, чтобы активировать выбранные для приложения назначения групп.

При назначении групп вы не сможете изменить ранее назначенные группы. Если вы хотите выбрать недоступную группу, сначала удалите ее из списка назначений для приложения.

Чтобы изменить назначения, выберите в списке **Назначения** строку с конкретным назначением, которое вы хотите изменить. Кроме того, вы можете удалить назначение, щелкнув многоточие ( **…** ) в конце строки и выбрав действие **Удалить**. Чтобы изменить представление списка **Назначения**, сгруппируйте его по параметру **Тип назначения** или состоянию **Включено/Исключено**.

![Назначение приложений Intune — завершение](/media/apps-inc-exl-assignments/apps-inc-exl-05.png)

## <a name="next-steps"></a>Дальнейшие шаги

- Дополнительные сведения о включении и исключении назначений групп для приложений см. в [блоге о Microsoft Intune](https://aka.ms/new_app_assignment_process).
- См. дополнительные сведения об [отслеживании сведений о приложении и его назначении с помощью Microsoft Intune](apps-monitor.md).