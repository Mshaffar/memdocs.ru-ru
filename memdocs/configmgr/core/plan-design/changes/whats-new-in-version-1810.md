---
title: Новые возможности в версии 1810
titleSuffix: Configuration Manager
description: Сведения об изменениях и новых возможностях, появившихся в Configuration Manager версии 1810 (Current Branch).
ms.date: 04/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6a9770dca209669659abf6e4fc9c23d5e6972981
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073557"
---
# <a name="whats-new-in-version-1810-of-configuration-manager-current-branch"></a>Новые возможности в версии Configuration Manager 1810 (Current Branch)

*Область применения: Configuration Manager (Current Branch)*

Обновление 1810 для выпуска Configuration Manager Current Branch доступно в виде обновления в консоли. Примените это обновление к сайтам, работающим под управлением версий 1710, 1802 или 1806. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.--> В этой статье перечислены изменения и новые функции в Configuration Manager, версия 1810.  

Всегда проверяйте последний контрольный список для установки этого обновления. Дополнительные сведения см. в разделе [Контрольный список для установки обновления 1810 для System Center Configuration Manager](../../servers/manage/checklist-for-installing-update-1810.md). После обновления сайта следует также просмотреть [Контрольный список действий, выполняемых после обновления](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist).

Чтобы воспользоваться преимуществами новых функций Configuration Manager, сначала необходимо обновить клиенты до последней версии. Хотя новые функции появляются в консоли Configuration Manager после обновления ее и сайта, полный сценарий будет работать только с последней версией клиента.

<!--
> [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized. 
-->  

> [!Tip]  
> Чтобы получать уведомления при обновлении этой страницы, скопируйте и вставьте следующий URL-адрес в средство чтения веб-канала RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1810+-+Configuration+Manager%22&locale=en-us`.



## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> Устаревшие компоненты и операционные системы

Ознакомьтесь с изменениями поддержки до того, как компоненты будут объявлены [удаленными и устаревшими](deprecated/removed-and-deprecated.md).

C 14 августа 2018 года компонент гибридного управления мобильными устройствами является нерекомендуемым. Дополнительные сведения см. в статье о [прекращении использования гибридного управления мобильными устройствами (MDM)](../../../mdm/understand/what-happened-to-hybrid.md).<!--Intune feature 2683117-->  

Поддержка System Center Endpoint Protection (SCEP) для Mac и Linux (все версии) заканчивается 31 декабря 2018 г. По окончании срока поддержки новые определения вирусов для SCEP для Mac и Linux могут быть недоступны. Дополнительные сведения см. в [записи блога об окончании срока поддержки](https://go.microsoft.com/fwlink/?linkid=870182).

Классическое развертывание службы в Azure не рекомендуется использовать в Configuration Manager. Перейдите на использование развертываний Azure Resource Manager для шлюза управления облачными клиентами и облачной точки распространения. Дополнительные сведения см. в разделе [Планирование CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).



## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Инфраструктура сайта

### <a name="support-for-windows-server-2019"></a>Поддержка Windows Server 2019

<!--1359195-->
Configuration Manager теперь поддерживает Windows Server 2019 и Windows Server версии 1809 как системы сайта.

Дополнительные сведения см. в статье [Поддерживаемые операционные системы для серверов системы сайта](../configs/supported-operating-systems-for-site-system-servers.md).


### <a name="hierarchy-support-for-site-server-high-availability"></a>Поддержка иерархии для обеспечения высокой доступности сервера сайта

<!--3607755, fka 1358224-->
Сайты центра администрирования и первичные дочерние сайты теперь могут использовать сервер дополнительного сайта в пассивном режиме.

Дополнительные сведения см. в статье [Высокая доступность сервера сайта](../../servers/deploy/configure/site-server-high-availability.md).


### <a name="improvements-to-setup-prerequisites"></a>Усовершенствования необходимых компонентов

При установке или обновлении до версии 1810 программа установки Configuration Manager теперь включает в себя новые или улучшенные проверки готовности к установке:

- **Ожидание перезагрузки системы**. Эта проверка готовности к установке стала более устойчивой. Она проверяет дополнительные разделы реестра для компонентов Windows. Дополнительные сведения см. в разделе [Ожидание перезагрузки системы](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart). <!--SCCMDocs-pr issue 3010-->  

- **Очистка списка отслеживаемых изменений SQL**. Новая версия проверяет, есть ли невыполненная работа по отслеживанию изменений SQL в базе данных сайта. Дополнительные сведения, включая процедуры для проверки и очистки этой невыполненной работы, см. в разделе [Очистка отслеживания изменений SQL](../../servers/deploy/install/list-of-prerequisite-checks.md#bkmk_changetracking). <!--SCCMDocs-pr issue 3023-->  

- **Версия SQL Native Client**. Эта предварительная проверка обновляется для версий SQL Native Client, которая поддерживает TLS 1.2. Минимальная версия — [SQL 2012 SP4](https://www.microsoft.com/download/details.aspx?id=50402). Дополнительные сведения см. в статье [Список проверок на наличие необходимых компонентов для Configuration Manager](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client). <!--SCCMDocs-pr issue 3094-->  

- **Системы сайта на узле кластера Windows**. Процесс установки Configuration Manager более не блокирует установку роли сервера сайта на компьютере с ролью Windows для отказоустойчивой кластеризации. Эта роль требуется для SQL Always On, в связи с чем ранее было невозможно размещать базу данных сайта на сервере сайта. Благодаря этому изменению вы можете создать сайт с высоким уровнем доступности с меньшим количеством серверов за счет использования SQL Always On и сервера сайта в пассивном режиме. Дополнительные сведения см. в разделе [Отказоустойчивый кластер Windows](../../servers/deploy/install/list-of-prerequisite-checks.md#windows-failover-cluster). <!--1359132-->  


### <a name="new-permission-for-client-notification-actions"></a>Новое разрешение для действий уведомления клиента

<!--SCCMDocs-pr issue #2972-->
Для действий уведомления клиента теперь требуется разрешение **Уведомление ресурса** для объекта SMS_Collection. Следующие встроенные роли имеют эти разрешения по умолчанию:

- Полный администратор  
- Администратор инфраструктуры  

Добавьте это разрешение во все пользовательские роли, которым нужно использовать действия уведомления клиента.

Дополнительные сведения см. в разделе [Уведомление клиента](../../clients/manage/client-notification.md).



## <a name="content-management"></a><a name="bkmk_content"></a> Управление содержимым

### <a name="new-boundary-group-options"></a>Новые параметры группы границ

<!--1358749-->
Для групп границ реализованы дополнительные параметры, позволяющие более эффективно управлять распространением содержимого в среде.

- **Предпочитать точки распространения одноранговым узлам в той же подсети**. По умолчанию точка управления помещает источники однорангового кэша в верхнюю часть списка расположений содержимого. Этот параметр обращает приоритет для клиентов, которые находятся в той же подсети, что и источник однорангового кэша.  

- **Предпочитать облачные точки распространения обычным**. При наличии филиала с более быстрым интернет-каналом можно задать приоритет облачного содержимого.  

Дополнительные сведения см. в разделе [Параметры группы границ для одноранговых скачиваний](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).


### <a name="management-insights-rule-for-peer-cache-source-client-version"></a>Правило аналитики управления для клиентской версии источника однорангового кэша

<!-- 1358008 -->
В узле **Аналитика управления** теперь есть новое правило для идентификации клиентов, которые служат источником однорангового кэша, но не были обновлены с клиентской версии, предшествующей версии 1806. Новое правило называется **Обновить источники однорангового кэша до последней версии клиента Configuration Manager** и является частью новой группы правил **Упреждающее обслуживание**. Клиенты с версией до 1806 нельзя использовать как источник однорангового кэша для клиентов, на которых работает версия 1806 (или более поздняя версия). Выберите **Принять меры**, чтобы открыть представление устройств со списком клиентов.

Дополнительные сведения см. в статье [Аналитика управления](../../servers/manage/management-insights.md).



## <a name="client-management"></a><a name="bkmk_client"></a> Управление клиентами

### <a name="new-client-notification-action-to-wake-up-device"></a>Новое действие уведомления клиента для пробуждения устройств

<!--1317364-->
Теперь клиенты можно пробуждать с консоли Configuration Manager, даже если они не находятся в той же подсети, что и сервер сайта. Если вам требуется выполнить обслуживание или запросить устройства, ваши возможности не ограничены активными удаленными клиентами. Сервер сайта использует канал уведомления клиентов для поиска другого активного клиента в той же удаленной подсети, а затем использует этот клиент для отправки запроса пробуждения по локальной сети (Magic Packet).

Дополнительные сведения см. в статьях [Настройка пробуждения по локальной сети в System Center Configuration Manager](../../clients/deploy/configure-wake-on-lan.md) и [Планирование пробуждения клиентов в System Center Configuration Manager](../../clients/deploy/plan/plan-wake-up-clients.md).

### <a name="new-option-to-perform-client-notification-from-devices-node"></a>В узле устройств доступен новый параметр "Уведомление клиента"

<!--1317364-->
До версии 1810 параметр **Уведомление клиента** можно было использовать только в узле коллекции устройств или при просмотре членства коллекции устройств. Непосредственно в узле **Устройства** возможность **уведомления клиента** была недоступна. Теперь этот параметр не ограничен представлением членства коллекции.

Дополнительные сведения см. в разделе [Уведомление клиента](../../clients/manage/client-notification.md).


### <a name="improvements-to-collection-evaluation"></a>Усовершенствования для оценки коллекции

<!--3607726, fka 1358981-->
Следующие изменения для оценки коллекции повышают производительность веб-сайта.  

- Ранее, когда вы настраивали расписание для коллекции на основе запроса, сайт продолжал вычислять запрос независимо от значения параметра **Запланировать полное обновление этой коллекции**. Чтобы полностью отключить расписание, приходилось отключать расписание (значение **Нет**). Теперь сайт автоматически очищает расписание при отключении этого параметра. Чтобы задать расписание для оценки коллекции, включите параметр **Запланировать полное обновление этой коллекции**.  

- Вы не можете отключить оценку для встроенных коллекций, например **Все системы**, но теперь вы можете настроить для них расписание. Это поведение позволяет назначить это действие на определенное время в соответствии с бизнес-требованиями.

Дополнительные сведения см. в статье [Создание коллекций](../../clients/manage/collections/create-collections.md#bkmk_create).


### <a name="improvement-to-client-installation"></a>Улучшение установки клиента

<!--1358840-->
При установке клиента Configuration Manager процесс ccmsetup подключается к точке управления, чтобы найти необходимое содержимое. Ранее в рамках этого процесса точка управления возвращала только точки распространения в текущей группе границ клиента. Если содержимое недоступно, процесс установки откатывается к скачиванию содержимого из точки управления. При этом отсутствует возможность выполнить откат до точек распространения в других группах границ, в которых может присутствовать необходимое содержимое. Теперь точка управления возвращает точки распространения в зависимости от конфигурации группы границ.

Дополнительные сведения см. в разделе о [настройке групп границ](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup).



## <a name="co-management"></a><a name="bkmk_comgmt"></a> Совместное управление

### <a name="required-app-compliance-policy-for-co-managed-devices"></a>Обязательная политика соответствия приложений требованиям для совместно управляемых устройств

<!--1358196-->
Определите правила политики соответствия в Configuration Manager для требуемых приложений. Эта оценка приложений является частью данных об общем состоянии соответствия, отправляемых в Microsoft Intune для совместно управляемых устройств.

Дополнительные сведения см. в статье [Рабочие нагрузки совместного управления](../../../comanage/workloads.md).


### <a name="improvement-to-co-management-dashboard"></a>Улучшения панели мониторинга совместного управления

<!--1358980-->
В панель мониторинга совместного управления добавлены более подробные сведения.  

- Плитка **Состояние регистрации совместного управления** включает дополнительные состояния.

- Новая плитка **Состояние совместного управления** с воронкообразной диаграммой, на которой отображаются следующие состояния процесса регистрации:

- Новая плитка с числом **ошибок регистрации**.

![Снимок экрана панели мониторинга совместного управления с верхними четырьмя плитками](media/1358980-comgmt-dashboard.png)

Дополнительные сведения см. в разделе [Панель мониторинга совместного управления](../../../comanage/how-to-monitor.md#co-management-dashboard).


### <a name="improvements-to-internet-based-client-setup"></a>Усовершенствования в настройке клиентов в Интернете

<!--3607731, fka 1359181-->
Этот выпуск дополнительно упрощает процесс установки клиента Configuration Manager для клиентов в Интернете. Сайт публикует дополнительные сведения из Azure Active Directory (Azure AD) в шлюзе управления облачными клиентами (CMG). Присоединенный к домену AD клиент Azure получает эти сведения из шлюза управления облачными клиентами во время процесса ccmsetup, используя тот же клиент, к которому он присоединен. Такое поведение дополнительно упрощает регистрацию устройств для совместного управления в среде с несколькими клиентами Azure AD. Теперь нужны только два свойства ccmsetup: **CCMHOSTNAME** и **SMSSiteCode**.

Дополнительные сведения см. в разделе о [подготовке интернет-устройств к совместному управлению](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).



## <a name="application-management"></a><a name="bkmk_app"></a> Управление приложениями

### <a name="convert-applications-to-msix"></a>Преобразование приложений в формат MSIX

<!--3607729, fka 1359029-->
Начиная с версии 1806, Configuration Manager поддерживает развертывание пакетов приложений Windows 10 в новом формате (MSIX). Теперь вы можете преобразовать существующие приложения установщика Windows (MSI) в формат MSIX.

Дополнительные сведения см. в статье [Создание приложений Windows](../../../apps/get-started/creating-windows-applications.md#bkmk_msix).  


### <a name="repair-applications"></a>Исправление приложений

<!--1357866-->
Теперь для типов развертывания установщика Windows и установщика сценариев в командной строке можно указывать параметр repair. Затем при включении этого параметра в развертывании становится доступна новая кнопка в центре программного обеспечения для **восстановления** приложения. Если настроить приложение с помощью программы восстановления, пользователи смогут запускать команды из центра программного обеспечения.

Дополнительные сведения см. в разделах [Создание приложений](../../../apps/deploy-use/create-applications.md#bkmk_dt-content) и [Развертывание приложений](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings).


### <a name="approve-application-requests-via-email"></a>Запросы на утверждение приложений по электронной почте

<!--1321550-->
Настройте отправку уведомлений по электронной почте о запросах на утверждение приложений. Когда пользователь запрашивает приложение, вы получаете по электронной почте уведомление. Щелкнув соответствующую ссылку в сообщении, вы можете утвердить или отклонить запрос без необходимости открывать консоль Configuration Manager.

Дополнительные сведения см. в статье [Утверждение приложений](../../../apps/deploy-use/app-approval.md).


### <a name="detection-methods-dont-load-windows-powershell-profiles"></a>Методы обнаружения не загружают профили Windows PowerShell

<!--3607762, fka 1359239-->
Скрипты Windows PowerShell можно использовать для методов обнаружения приложений и параметров в элементах конфигурации. Когда эти скрипты выполняются на клиентах, клиент Configuration Manager теперь вызывает PowerShell с параметром `-NoProfile`. Этот параметр запускает PowerShell без профилей.

Профиль PowerShell — это скрипт, выполняющийся при запуске PowerShell. Можно создать профиль PowerShell для настройки вашей среды и добавления элементов, относящихся к каждому сеансу PowerShell, который вы запускаете.

> [!Note]  
> Это изменение в поведении не применяется к [скриптам](../../../apps/deploy-use/create-deploy-scripts.md) или [CMPivot](../../servers/manage/cmpivot.md). Обе эти функции уже используют этот параметр PowerShell.  

См. дополнительные сведения о [создании приложений](../../../apps/deploy-use/create-applications.md) и [создании элементов конфигурации](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).



## <a name="os-deployment"></a><a name="bkmk_osd"></a> Развертывание ОС

### <a name="task-sequence-support-of-windows-autopilot-for-existing-devices"></a>Поддержка последовательностей задач в Windows Autopilot для существующих устройств

<!--3607717, fka 1358333-->
[Windows Autopilot для имеющихся устройств](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) теперь предоставляется в Windows 10 версии 1809 или более поздней. Эта новая функция позволяет пересоздавать образ и подготавливать устройство Windows 7 к [режиму Windows Autopilot с управлением пользователем](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) с помощью одной встроенной последовательности задач Configuration Manager.

Дополнительные сведения см. в статье [Windows Autopilot for existing devices](../../../osd/deploy-use/windows-autopilot-for-existing-devices.md) (Windows Autopilot для существующих устройств).


### <a name="specify-the-drive-for-offline-os-image-servicing"></a>Выбор диска для автономного обслуживания образов ОС

<!--1358924-->
Теперь вы можете указать диск, который Configuration Manager использует при добавлении обновлений программного обеспечения в образы ОС и пакеты обновления операционной системы. С учетом временных файлов этот процесс может занимать много места на диске, поэтому данный параметр позволяет выбирать диск, который вы хотите использовать.

Дополнительные сведения см. в разделе [Управление образами ОС](../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive) или [Управление пакетами обновления ОС](../../../osd/get-started/manage-operating-system-upgrade-packages.md#bkmk_servicing-drive).


### <a name="task-sequence-support-for-boundary-groups"></a>Поддержка последовательности задач для групп границ

<!--1359025-->
Когда устройство выполняет последовательность задач и ему нужно получить содержимое, теперь для него доступны режимы группы границ, так же как и для клиента Configuration Manager.

Дополнительные сведения см. в разделе [Группы границ](../../servers/deploy/configure/boundary-groups.md#bkmk_bgr-osd).


### <a name="improvements-to-driver-maintenance"></a>Улучшение обслуживания драйверов

<!--3607716, fka 1358270-->
Пакеты драйверов теперь включают дополнительные поля метаданных **производителя** и **модели**. Используйте эти поля, чтобы пометить пакеты драйверов сведениями, упрощающими общее обслуживание или помогающими определить старые и дублирующиеся драйверы, которые можно удалить.

Дополнительные сведения см. в разделе [Управление драйверами](../../../osd/get-started/manage-drivers.md).

### <a name="improvements-to-windows-10-servicing-plan-filters"></a>Усовершенствования для фильтров плана обслуживания Windows 10

<!--3098809, 3113836, 3204570 -->
В планы обслуживания Windows 10 добавлены дополнительные фильтры. Теперь вы можете фильтровать по **архитектуре**, **категории продуктов** и по условию того, **заменено ли** обновление.

Дополнительные сведения см. в статье [План обслуживания Windows 10](../../../osd/deploy-use/manage-windows-as-a-service.md#BKMK_ServicingPlan).

### <a name="new-task-sequence-variable-for-last-action-name"></a>Новая переменная последовательности задач для имени последнего действия

<!--SCCMDocs-pr issue #2964-->
Вместе с переменной _SMSTSLastActionRetCode с помощью последовательности задач также устанавливается новая переменная **_SMSTSLastActionName**. Она также записывает это значение в файл журнала smsts.log. Эта новая переменная полезна при устранении неполадок в последовательности задач. Если при выполнении шага происходит сбой, настраиваемый сценарий может включать имя шага, а также код возврата.

Дополнительные сведения см. в описании [переменных последовательности задач](../../../osd/understand/task-sequence-variables.md#SMSTSLastActionName).



## <a name="software-updates"></a><a name="bkmk_sum"></a> Обновления программного обеспечения

### <a name="phased-deployment-of-software-updates"></a>Поэтапное развертывание обновлений программного обеспечения

<!--1358146-->
Создайте поэтапные развертывания для обновлений программного обеспечения. Поэтапные развертывания позволяют организовать согласованное, последовательное развертывание программного обеспечения на основе настраиваемых условий и групп.

Подробные сведения см. в статье [Создание поэтапных развертываний с помощью Configuration Manager](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).


### <a name="improvement-to-maintenance-windows-for-software-updates"></a>Улучшения периодов обслуживания для обновлений программного обеспечения

<!--vso2839307-->
Следующий клиентский параметр находится в группе **Обновления программного обеспечения**. Он позволяет управлять поведением установки обновлений программного обеспечения в периоды обслуживания: **Включить установку обновлений программного обеспечения в периоде обслуживания "Все развертывания", когда доступен период обслуживания "Обновление программного обеспечения"** .

По умолчанию этому параметру задано значение **Нет**, чтобы обеспечить соответствие существующему поведению. Значение **Да** разрешает клиентам использовать другие доступные периоды обслуживания для установки обновлений программного обеспечения.

Дополнительные сведения см. в разделе [Включение управления агентом клиента Office 365](../../clients/deploy/about-client-settings.md#bkmk_SUMMaint).


### <a name="improvement-to-software-updates-maintenance"></a>Улучшение обслуживания обновлений программного обеспечения

<!--2839349-->
Задачи очистки WSUS теперь выполняются на вторичных сайтах. Очистка WSUS для просроченных обновлений запущена, и замененные обновления отклоняются на сервере WSUS для вторичных сайтов.

Дополнительные сведения см. в разделе [Поведение очистки WSUS, начиная с версии 1810](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810)

### <a name="improvement-to-software-update-supersedence-rules"></a>Улучшения для правил замены обновления программного обеспечения

<!--3098809, 2977644-->
Теперь вы можете указать правила замены для обновления компонентов отдельно от обновлений, не связанных с компонентами. Это означает, что ваши обновления не будут удалены из Configuration Manager до завершения обслуживания клиентов Windows 10.

Дополнительные сведения см. в разделе [Правила замены](../../../sum/get-started/install-a-software-update-point.md#supersedence-rules).

## <a name="reporting"></a><a name="bkmk_report"></a> Отчеты

### <a name="improvement-to-lifecycle-dashboard"></a>Улучшения панели мониторинга жизненного цикла

<!--1358702-->
Теперь на панели мониторинга жизненного цикла продукта содержатся сведения о **System Center 2012 Configuration Manager и более поздних версиях**.

Есть также новый отчет, **Жизненный цикл 05A — панель мониторинга жизненного цикла продукта**. Этот отчет содержит сведения, аналогичные панели мониторинга в консоли.

Дополнительные сведения об этой панели мониторинга см. в статье [Использование панели мониторинга жизненного цикла продукта](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md).


### <a name="improvement-to-data-warehouse"></a>Улучшения хранилища данных

<!--1358870-->
Теперь вы можете синхронизировать больше таблиц из базы данных сайта с хранилищем данных. Благодаря этому изменению вы можете создавать дополнительные отчеты с учетом ваших бизнес-требований.

Дополнительные сведения см. в статье [Хранилище данных](../../servers/manage/data-warehouse.md).



## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Консоль Configuration Manager

### <a name="configuration-manager-administrator-authentication"></a>Аутентификация администратора Configuration Manager

<!--1357013-->
Теперь вы можете указать минимально необходимый уровень аутентификации для доступа администраторов к сайтам Configuration Manager. Эта функция позволяет настроить для администраторов требование входить в Windows с определенным уровнем. Чтобы настроить этот параметр, найдите вкладку **Проверка подлинности** в разделе **Параметры иерархии**.

Дополнительные сведения см. в разделе [Планирование использования поставщика SMS](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth).


### <a name="support-center"></a>Центр поддержки

<!--1357489-->
Используйте Центр поддержки для устранения неполадок клиента, просмотра журнала в режиме реального времени или записи состояния компьютера клиента Configuration Manager для последующего анализа. Центр поддержки — это единый инструмент, консолидирующий многие инструменты администратора для устранения неполадок. Установщик Центра поддержки находится на сервере сайта в папке **cd.latest\SMSSETUP\Tools\SupportCenter**.

Дополнительные сведения см. в разделе [Центр поддержки](../../support/support-center.md).


### <a name="management-insights-dashboard"></a>Панель мониторинга аналитики управления

<!--1357979-->
В узел **Аналитика управления** теперь включена графическая панель мониторинга. Эта панель содержит общие сведения о состояниях правила, что позволяет оптимизировать отображение хода выполнения. Она содержит следующие элементы:

- **Индекс аналитики управления.** Отслеживает общий ход выполнения для правил аналитики управления. Индекс представляет собой взвешенное среднее значение. Наибольшую значимость имеют критически важные правила. При расчете этого индекса необязательные правила имеют наименьший вес.  

- **Группы аналитики управления.** Показывает процент правил в каждой группе.  

- **Приоритет аналитики управления.** Показывает процент правил за приоритетом.  

- **Вся аналитика.** Таблица аналитических сведений с информацией о приоритете и состоянии.  

![Снимок экрана с изображением панели мониторинга аналитики управления](media/1357979-management-insights-dashboard.png)

Дополнительные сведения см. в статье [Аналитика управления](../../servers/manage/management-insights.md).


### <a name="improvements-to-cmpivot"></a>Улучшения CMPivot

<!--1359068-->
В CMPivot внесены следующие усовершенствования.

- Сохранение **избранных** запросов  

- На вкладке "Сводка запроса" выберите число неисправных или автономных устройств, а затем пункт **Создать коллекцию**.

Дополнительные сведения о прочих усовершенствованиях производительности и диагностики CMPivot см. в разделе [Улучшения сценариев](#bkmk_scripts).

Дополнительные сведения см. в статье [CMPivot](../../servers/manage/cmpivot.md).


### <a name="improvements-to-scripts"></a><a name="bkmk_scripts"></a> Улучшения сценариев

<!--1358239-->
Теперь подробные выходные данные сценария можно просматривать в необработанном виде или в структурированном формате JSON. Такое форматирование упрощает чтение и анализ выходных данных.

Перечисленные ниже усовершенствования производительности и диагностики относятся к CMPivot и сценариям.

- Обновленные клиенты возвращают выходные данные объемом менее 80 КБ на сайт по быстрому коммуникационному каналу. Это изменение повышает производительность просмотра выходных данных сценариев или запросов.  

- Дополнительные журналы для устранения неполадок  

Дополнительные сведения см. в следующих статьях:  

- [Создание и запуск сценариев PowerShell из консоли Configuration Manager](../../../apps/deploy-use/create-deploy-scripts.md)  

- [Устранение неполадок CMPivot](../../servers/manage/cmpivot-tsg.md)


### <a name="sms-provider-api"></a>API поставщика SMS

<!--3607711, fka 1321523-->
Поставщик SMS теперь предоставляет доступ API только для чтения для взаимодействия с WMI по HTTPS. Это решение называется **службой администрирования**. Этот REST API можно использовать вместо пользовательской веб-службы для доступа к информации на сайте.

**Поставщик SMS** отображается как роль с возможностью разрешить обмен данными через шлюз управления облачными клиентами. Этот параметр в текущей версии используется для включения утверждения приложений по электронной почте с удаленного устройства.

Дополнительные сведения см. в разделе [Планирование использования поставщика SMS](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service).



## <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a> Локальное управление мобильными устройствами (MDM)

### <a name="an-intune-connection-is-no-longer-required-for-new-on-premises-mdm-deployments"></a>Подключение к Intune больше не требуется для локального развертывания MDM

<!--1359124-->
Локальный компонент управления мобильными устройствами больше не требуется для настройки подписки Microsoft Intune для новых развертываний. Вашей организации по-прежнему требуется лицензия Intune для использования этой функции. Сейчас вы не можете отказаться от подключения к Intune, используемого для существующих локальных развертываний MDM. Дополнительные сведения см. в [блоге группы поддержки Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).



## <a name="other-updates"></a>Другие обновления

Помимо новых функций, этот выпуск также включает в себя дополнительные изменения, такие как исправление ошибок. Дополнительные сведения см. в статье [Сводка изменений в текущей ветви System Center Configuration Manager, версия 1810](https://support.microsoft.com/help/4482169).

Дополнительные сведения об изменениях командлетов Windows PowerShell для Configuration Manager см. в статье [Заметки о выпуске PowerShell 1810](https://docs.microsoft.com/powershell/sccm/1810-release-notes?view=sccm-ps).

С 25 марта 2019 г. в консоли доступен следующий накопительный пакет обновления (4488598): [Накопительный пакет обновления 2 для текущей ветви Configuration Manager версии 1810](https://support.microsoft.com/help/4488598). Заменяет предыдущее обновление (KB 4486457).


### <a name="hotfixes"></a>Исправления

Для устранения определенных неполадок доступны перечисленные ниже дополнительные исправления.

| ID | Название | Дата | В консоли |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Сертификат соединителя Microsoft Intune не продлевается в Configuration Manager | 18 января 2019 г. | Да |
| [4490434](https://support.microsoft.com/help/4490434) | В Configuration Manager создаются повторяющиеся столбцы с обнаруженными данными пользователей | 22 февраля 2019 г. | Да |
| [4490575](https://support.microsoft.com/help/4490575) | При установке обновлений в Configuration Manager 1810 система перестает отвечать на запросы или не выводит сообщение о завершении | 22 февраля 2019 г. | Да |


## <a name="next-steps"></a>Дальнейшие шаги

Когда вы будете готовы установить эту версию, просмотрите статьи [Обновления и обслуживание для Configuration Manager](../../servers/manage/updates.md) и [Контрольный список для установки обновления 1810 для System Center Configuration Manager](../../servers/manage/checklist-for-installing-update-1810.md).

> [!TIP]  
> Чтобы установить новый сайт, используйте базовую версию Configuration Manager.  
>
> Дополнительные сведения
>
> - [Установка новых сайтов](../../servers/deploy/install/installing-sites.md)  
> - [Базовые и обновленные версии](../../servers/manage/updates.md#bkmk_Baselines)  

Перечень известных серьезных проблем, их описание и способы устранения см. в статье [Заметки о выпуске](../../servers/deploy/install/release-notes.md).

После обновления сайта следует также просмотреть [Контрольный список действий, выполняемых после обновления](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist).