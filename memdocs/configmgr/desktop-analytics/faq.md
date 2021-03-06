---
title: Часто задаваемые вопросы по Аналитике компьютеров
titleSuffix: Configuration Manager
description: Часто задаваемые вопросы по Аналитике компьютеров.
ms.date: 02/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: d1f18c135f200b2a9e40b970871c73a0d98893a2
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429810"
---
# <a name="desktop-analytics-faq"></a>Часто задаваемые вопросы по Аналитике компьютеров

## <a name="prerequisites"></a>Предварительные условия

### <a name="can-i-use-cloud-enabled-analytics-with-intune-managed-devices"></a><a name="bkmk_intune"></a> Можно ли использовать облачную аналитику с устройствами, управляемыми Intune?

На сегодняшний день такая возможность отсутствует, однако рекомендуем ознакомиться с сообщением, прозвучавшим на конференции Microsoft Ignite 2019, касательно [управления устройствами на основе аналитических сведений](https://myignite.techcommunity.microsoft.com/sessions/81690?source=sessions). Это запланированное решение является последователем решений "Работоспособность устройств" и "Проверка готовности к обновлению".

Подавляющее большинство клиентов, которые могут воспользоваться преимуществами рабочего процесса Аналитики компьютеров, используют Configuration Manager для развертывания Windows. Мы понимаем, что клиентам Intune нравятся дополнительные аналитические сведения из данных аналитики, и мы работаем над способами совместного использования этих сведений.

### <a name="its-been-over-72-hours-and-the-portal-is-still-processing-data-what-next"></a>Прошло уже 72 часа, а портал все еще обрабатывает данные. Что делать дальше?

При первой настройке Аналитики компьютеров в отчетах Configuration Manager и Аналитики компьютеров сразу могут отображаться не все данные. Обработка данных службой может занять 2–3 дня. Если прошло уже 72 часа, а портал все еще обрабатывает данные, сделайте следующее:

- Чтобы убедиться, что активные устройства настроены правильно, используйте [панель мониторинга работоспособности подключения](monitor-connection-health.md). Эта панель мониторинга не обновляется в режиме реального времени.
- Убедитесь, что устройства отправляют диагностические данные в службу "Аналитика компьютеров". Дополнительные сведения см. в статье [Enable data sharing for Desktop Analytics](enable-data-sharing.md) (Обеспечение обмена данными для Аналитики компьютеров).
- Подготовьте к работе [приложения Azure AD](troubleshooting.md#bkmk_AzureADApps) в Azure AD.
- Проверьте устройства, которые были связаны с вашей организацией за последние семь дней. На [портале Аналитики компьютеров](https://aka.ms/desktopanalytics) перейдите в область **Подключенные службы**. Выберите **Регистрация устройств**, а затем **Просмотреть последние данные**.

  > [!IMPORTANT]
  > Параметр Desktop Analytics для **просмотра последних данных** является нерекомендуемым. Это действие будет удалено в следующем выпуске службы "Аналитика компьютеров". Дополнительные сведения см. в разделе [Устаревшие компоненты](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!--7080949-->  

Если устройства настроены правильно, а вы по-прежнему не видите данные в рабочей области, [обратитесь в службу поддержки Майкрософт](https://support.microsoft.com/hub/4343728/support-for-business).

## <a name="connect-configuration-manager"></a>Подключение Configuration Manager

### <a name="can-i-change-the-target-or-additional-collections"></a>Можно ли изменить целевую или дополнительную коллекцию?

Да, используйте следующую процедуру.

- В консоли Configuration Manager перейдите в рабочую область **Администрирование**, разверните узел **Облачные службы** и выберите узел **Службы Azure**. Откройте свойства записи, связанной со службой "Аналитика компьютеров".

- На вкладке **Подключение Аналитики компьютеров** измените **целевую коллекцию** или управляйте дополнительными коллекциями.

<!-- 7130169 -->
> [!Note]
> Не включайте более 20 коллекций в список дополнительных коллекций. Внимательно отслеживайте общее число устройств в каждой коллекции. Всегда принимайте решение о том, [какие коллекции включить в глобальный пилотный проект, а какие исключить](deploy-pilot.md#bkmk_GlobalPilot).  

> [!IMPORTANT]  
> Configuration Manager использует политику параметров для настройки устройств в целевой коллекции. Эта политика включает параметры диагностических данных, позволяющие устройствам передавать данные в корпорацию Майкрософт. Изменение целевой коллекции не отменяет политику параметров на устройствах, которые больше не находятся в целевой коллекции. Если вы не хотите, чтобы устройства продолжали отправлять диагностические данные, [перенастройте устройства](account-close.md#reconfigure-clients).

## <a name="windows-upgrade"></a>Обновление Windows

### <a name="can-i-upgrade-windows-and-change-architecture"></a>Можно ли обновить Windows и изменить архитектуру?

Аналитика компьютеров обеспечивает лучшую поддержку обновлений на месте. Обновления на месте не поддерживают переход от 32-разрядной на 64-разрядную версию архитектуры. Если необходимо перенести компьютеры в рамках этого сценария, используйте сценарий обновления. Аналитические сведения Аналитики компьютеров по-прежнему ценны в этом сценарии, но вы можете пропустить рекомендации по обновлению.

Дополнительные сведения см. в статье об [обновлении существующего компьютера до новой версии Windows](../osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md).

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>Можно ли заменить BIOS на UEFI при обновлении Windows?

Да. Дополнительные сведения см. в разделе [Переход от BIOS к UEFI при обновлении на месте](../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>Можно ли использовать Аналитику компьютеров с Windows 10 LTSC?

Аналитика компьютеров не поддерживает устройства с Windows 10 Long-Term Servicing Channel (LTSC). Дополнительные сведения см. в разделе с [обзором Windows как службы](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>Можно ли сократить время, затрачиваемое на обновление данных на портале Аналитики компьютеров?

На портале Аналитики компьютеров имеется два типа данных: данные администратора и диагностические данные. Чтобы по запросу обновить данные администратора, откройте всплывающий элемент актуальности данных и выберите **Применить изменения**. При этом сразу же активируется однократное обновление всех ожидающих изменений для администратора в рабочих областях. Изменения распространяются и становятся доступными в течение 15–60 минут. Время зависит от размера рабочего пространства и объема ожидающих изменений. Вы можете запросить обновление данных по требованию до шести раз за 24 часа.

Все данные обновляются автоматически раз в день, даже если вы не запрашиваете обновление данных по требованию. Невозможно активировать обновление диагностических данных по требованию. Дополнительные сведения о различных типах данных в Аналитике компьютеров см. в разделе [Задержка данных](troubleshooting.md#data-latency).

## <a name="privacy"></a>Конфиденциальность

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>Можно ли использовать Аналитику компьютеров без прямого подключения клиента к службе "Управление данными" Microsoft?

Нет, вся служба работает на основе диагностических данных Windows, что требует прямого подключения устройств.

### <a name="can-i-choose-the-data-center-location"></a>Можно ли выбрать расположение центра обработки данных?

Для Azure Log Analytics. Да, при настройке Аналитики компьютеров и создании рабочей области Log Analytics.

Для службы "Управление данными" Microsoft и Службы хранилища Azure аналитики. Нет, эти две службы размещаются в США.

### <a name="where-is-my-organizations-data-stored"></a>Где хранятся данные моей организации?

Диагностические данные Windows с ваших компьютеров шифруются, отправляются и обрабатываются в управляемых корпорацией Майкрософт защищенных центрах обработки данных, расположенных в США. Корпорация Майкрософт предоставляет анализ данных, связанных с Аналитикой компьютеров, с помощью решения "Аналитика компьютеров" на портале Azure. Аналитика компьютеров поддерживается в большинстве регионов, где [доступна Log Analytics](https://azure.microsoft.com/global-infrastructure/services/?products=monitor&regions=all). При выборе международного региона Azure ваши данные диагностики будут так же отправляться и обрабатываться в защищенных центрах обработки данных Майкрософт в США.

## <a name="existing-windows-analytics-customers"></a>Имеющиеся пользователи Windows Analytics

> [!Important]  
> Поддержка службы Windows Analytics прекращена 31 января 2020 г.
>
> Дополнительные сведения см. в статье базы знаний [KB 4521815 о прекращении поддержки Windows Analytics с 31 января 2020 г.](https://support.microsoft.com/help/4521815/windows-analytics-retirement)

### <a name="can-i-use-update-compliance-together-with-desktop-analytics"></a>Можно ли использовать Поддержку обновлений вместе с Аналитикой компьютеров?

Да. Если вы уже используете [Поддержку обновлений](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started) на портале Azure, то можете продолжать и после января 2020 г.

Дополнительные сведения см. в статье базы знаний [KB 4521815 о прекращении поддержки Windows Analytics с 31 января 2020 г.](https://support.microsoft.com/help/4521815/windows-analytics-retirement)

### <a name="are-there-any-windows-analytics-features-that-arent-available-in-desktop-analytics"></a>Есть ли функции Windows Analytics, недоступные в Аналитике компьютеров?

<!-- 3616924 -->
Да, для следующих функций Windows Analytics мы прекратили поддержку, или они недоступны в Аналитике компьютеров.

#### <a name="general"></a>Общие

- Поддержка сценариев, которым не нужен Configuration Manager. Например, [поддержка по Intune](#bkmk_intune).
- Обязательное условие лицензирования любой действительной лицензии Windows (в отличие от планов E3 или E5).
- Поддержка нескольких рабочих областей в одном клиенте Azure AD.
- Возможность выполнять пользовательские запросы и экспортировать необработанные данные решения.
- Документация по модели данных для пользовательских отчетов.

#### <a name="upgrade-readiness"></a>Проверка готовности к обновлению

- Данные обнаружения сайтов Internet Explorer.
- Аналитические сведения о надстройке Office (теперь [доступны в Configuration Manager](#bkmk_office)).
- Аналитические сведения о концентраторе обратной связи.

#### <a name="update-compliance"></a>Соответствие обновлений

- Поддержка Центра обновления Windows для бизнеса.
- Аналитические сведения об оптимизации доставки.
- Поддержка Windows 10 LTSC.
- Отчеты программы предварительной оценки Windows.
- Состояние Защитника Windows.

> [!Note]
> Все имеющиеся функции Поддержки обновлений, включая те, которые недоступны в Аналитике компьютеров, остаются доступными в решении [Поддержка обновлений](/windows/deployment/update/update-compliance-get-started) на портале Azure.

#### <a name="device-health"></a>Работоспособность устройств

- Работоспособность драйвера.
- Работоспособность приложения (за пределами плана развертывания).
- Устройства с частыми сбоями или аварийные завершения, вызванные драйвером.
- Работоспособность входа Windows.
- Windows Information Protection
- Поддержка Windows Server.

## <a name="other"></a>другой

### <a name="can-i-use-desktop-analytics-for-my-office-365-proplus-upgrades"></a><a name="bkmk_office"></a> Можно ли использовать Аналитику компьютеров для обновлений Office 365 профессиональный плюс?

Нет, в Аналитике компьютеров основное внимание уделяется Windows. Корпорация Майкрософт разработала Аналитику компьютеров в тесном сотрудничестве с клиентами. Клиенты сообщают о том, как Аналитика компьютеров позволяет увереннее управлять развертываниями Windows. Они также сообщают, что хотят, чтобы [подготовка к переходу на версию Office 365 профессиональный плюс](../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness) была теснее связана с инструментами управления Office в Configuration Manager и Intune. Корпорация Майкрософт развивается в этих направлениях, уделяя внимание сценариям Windows в Аналитике компьютеров.

### <a name="how-can-i-provide-feedback-about-desktop-analytics"></a>Как можно отправить отзыв об Аналитике компьютеров?

Чтобы поделиться своими отзывами об Аналитике компьютеров, выберите значок **Отправить смайлик** в верхней части портала. Добавьте снимок экрана, чтобы ваш отзыв был понятнее для корпорации Майкрософт. Вы также можете отправить предложения по продуктам и проголосовать за другие идеи на [UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas?category_id=366805).

> [!Note]
> Никогда не делитесь конфиденциальными сведениями, такими как идентификатор клиента и коммерческий идентификатор, с помощью функции "Отправить смайлик" или UserVoice. Корпорация Майкрософт не предоставляет поддержку через каналы отправки смайликов или UserVoice. Чтобы получить справку по рабочей области Аналитики компьютеров, выберите ссылку **Справка и поддержка** в меню навигации для создания запроса в службу поддержки.
