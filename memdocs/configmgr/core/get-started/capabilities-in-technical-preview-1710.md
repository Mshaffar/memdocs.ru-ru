---
title: Technical Preview 1710 | Документация Майкрософт
titleSuffix: Configuration Manager
description: Сведения о функциях, доступных в Technical Preview для Configuration Manager, версия 1710.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4706a58-1f11-4eab-b1eb-3d1a0da02d0f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3dd4c3f22a0f2c24153e6d26be2e3098511c5dc4
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905321"
---
# <a name="capabilities-in-technical-preview-1710-for-configuration-manager"></a>Возможности в Technical Preview 1710 для Configuration Manager

*Область применения: Configuration Manager (ветвь Technical Preview)*

В этой статье содержатся сведения о функциях, доступных в версии 1710 Technical Preview для Configuration Manager. Этот выпуск можно установить для обновления и добавления новых возможностей в ознакомительную техническую версию сайта Configuration Manager. Перед установкой этой версии прочтите статью [Technical Preview для Configuration Manager](../../core/get-started/technical-preview.md). В ней приведены общие требования и ограничения на использование ознакомительной технической версии, а также сведения о том, как выполнять обновления и оставлять отзывы о функциях этого выпуска.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Известные проблемы в этой версии Technical Preview:**
- **Поддержка для Windows 10 версии 1709 (обновление Fall Creators Update)** .  Начиная с этой версии Windows, проигрыватель Windows Media включает несколько выпусков. При настройке последовательности задач для использования пакета обновления операционной системы или образа операционной системы не забудьте выбрать [выпуск, который поддерживается в Configuration Manager](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).
- **Если сервер сайта находится в пассивном режиме, происходит сбой обновления до предварительной версии**. Если вы запустили предварительную версию, [сервер первичного сайта которой находится в пассивном режиме](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), удалите сервер сайта в пассивном режиме, чтобы обновить сайт предварительной версии до новой версии. Вы можете повторно установить сервер сайта в пассивном режиме, когда на сайте завершится обновление.

  Удаление сервера сайта в пассивном режиме
  1. Откройте консоль и выберите **Администрирование** > **Обзор** > **Конфигурация сайта** > **Серверы и роли системы сайта**. Затем выберите сервер сайта в пассивном режиме.
  2. На панели **Системные роли сайта** щелкните правой кнопкой мыши роль **Сервер сайта** и нажмите кнопку **Удалить роль**.
  3. Щелкните правой кнопкой мыши сервер сайта в пассивном режиме, а затем выберите **Удалить**.
  4. Удалив сервер сайта на активном сервере первичного сайта, перезапустите службу **CONFIGURATION_MANAGER_UPDATE**.

**Ниже перечислены новые возможности, доступные в этой версии.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-deploying-powershell-scripts-from-configuration-manager"></a>Улучшения для развертывания сценариев PowerShell из Configuration Manager
В этом выпуске развертываемые вами сценарии PowerShell теперь поддерживают следующие усовершенствования: 
- **Области безопасности**.  Теперь для управления созданием и выполнением сценариев используются области безопасности. Для этого присваиваются теги, представляющие группы пользователей. Дополнительные сведения об использовании областей безопасности см. в статье [Настройка ролевого администрирования для Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).
- **Мониторинг в реальном времени**. Теперь мониторинг выполнения сценариев осуществляется в режиме реального времени.
- **Проверка параметров**. Для каждого параметра в сценарии доступно диалоговое окно **Script Parameter Properties** (Свойства параметра сценариев), где можно добавить проверку соответствующего параметра. После добавления проверки вы будете получать ошибки при вводе для параметра значения, не соответствующего условиям проверки.

Развертывания сценариев PowerShell появилось в версии [Technical Preview 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console). Дополнительные усовершенствования были внесены в версии [Technical Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) и затем [Technical Preview 1708](capabilities-in-technical-preview-1708.md#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager).


### <a name="try-it-out"></a>Попробуйте!

Чтобы оценить функцию запуска сценариев, см. статью [Создание и выполнение сценариев](../../apps/deploy-use/create-deploy-scripts.md).



## <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Ограничение расширенного объема данных Windows 10 только отправкой данных, относящихся к работоспособности устройств Windows Analytics
<!-- 1356148 -->

В этом выпуске вы можете задать для сбора данных диагностики Windows 10 уровень **Расширенный (с ограничениями)** . Этот параметр позволяет получать практические сведения об устройствах в вашей среде. При этом устройства не отправляют все данные, если задан уровень **Расширенные** в Windows 10 версии 1709 и выше.

Уровень "Расширенные (ограничено)" включает метрики из базового уровня, а также подмножество данных, собранных на уровне **Расширенные** и применимых к Windows Analytics.


## <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Центр программного обеспечения больше не искажает значки, размер которых превышает 250 x 250  
<!-- 1356194 -->

В этом выпуске центр программного обеспечения больше не будет искажать значки, размер которых превышает 250 x 250. Раньше в центре программного обеспечения эти значки выглядели нечеткими. Теперь вы можете задать значок с размером до 512 x 512 пикселей, и он будет отображаться без искажений.

### <a name="try-it-out"></a>Попробуйте!
Добавьте значок для приложения в центре программного обеспечения. Чтобы узнать, как это сделать, см. инструкции по [созданию приложений](../../apps/deploy-use/create-applications.md).


## <a name="check-compliance-from-software-center-for-co-managed-devices"></a>Проверка соответствия совместно управляемых устройств с помощью центра программного обеспечения
<!-- 1356374 -->
В этом выпуске пользователи могут использовать центр программного обеспечения для проверки соответствия их совместно управляемых устройств Windows 10, даже если управление условным доступом осуществляется в Intune. Дополнительные сведения см. в руководстве по [совместному управлению устройствами Windows 10](./capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices).


## <a name="support-for-exploit-guard"></a>Поддержка Exploit Guard
В этот выпуск добавлена поддержка Exploit Guard в Защитнике Windows. Вы можете настроить и развернуть политики, которые управляют всеми четырьмя компонентами Exploit Guard. Эти компоненты включают:
-   уменьшение уязвимой зоны;
-   контролированный доступ к папкам;
-   защиту от эксплойтов;
-   защиту сети.

Данные о соответствии развертывания политики Exploit Guard доступны в консоли Configuration Manager.

Дополнительные сведения о наборе Exploit Guard, его отдельных компонентах и правилах см. в статье [Exploit Guard в Защитнике Windows](https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard) в библиотеке документации Windows.

### <a name="prerequisites"></a>Предварительные условия
Управляемые устройства должны работать под управлением Windows 10 1709 Fall Creators Update или более поздней версии. Они должны отвечать следующим требованиям в зависимости от компонентов и настроенных правил:

|Компонент Exploit Guard |Дополнительные необходимые компоненты|
|------------------------|------------------------|
| Уменьшение уязвимой зоны  | На устройствах должен быть включен [Защитник Windows AV в реальном времени]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard).  |
| Контролированный доступ к папкам  | На устройствах должен быть включен [Защитник Windows AV в реальном времени]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard).   |
| Защита от эксплойтов  | Нет  |
| Защита сети  |  На устройствах должен быть включен [Защитник Windows AV в реальном времени]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard).  |

### <a name="create-an-exploit-guard-policy----1355468---"></a>Создание политики Exploit Guard  <!--1355468 -->
1. В консоли Configuration Manager откройте последовательно **Активы и соответствие** > **Endpoint Protection**, а затем выберите **Exploit Guard в Защитнике Windows**.
2. На вкладке **Главная** в группе **Создать** щелкните **Создать политику Exploit**.
3. На странице **Общие** **мастера создания элемента конфигурации**укажите имя и необязательное описание элемента.
4. Затем выберите компоненты Exploit Guard которыми вы хотите управлять с помощью этой политики. Для каждого выбранного компонента можно настроить дополнительные сведения.
   - **Уменьшение уязвимой зоны**. Настройте для угроз в Office, сценариях или электронной почте блокировку или аудит. Вы также можете исключить из этого правила определенные файлы или папки.
   - **Контролированный доступ к папкам**. Настройте аудит или блокировку, а затем добавьте приложения, которые могут обходить эту политику.  Можно также указать дополнительные папки, которые не защищены по умолчанию.
   - **Защита от эксплойтов**.  Укажите XML-файл, содержащий параметры для устранения эксплойтов системных процессов и приложений. Эти параметры можно экспортировать из приложения "Центр безопасности Защитника Windows" на устройстве Windows 10.
   - **Защита сети**. Настройте защиту сети с помощью блокирования или аудита доступа с подозрительных доменов.
5. Завершите работу мастера, чтобы создать политику, которую позднее можно развернуть на устройствах.

### <a name="deploy-an-exploit-guard-policy"></a>Развертывание политики Exploit Guard     
Создав политики Exploit Guard, разверните их с помощью мастера развертывания Exploit Guard. Для этого в консоли Configuration Manager откройте последовательно **Активы и соответствие** > **Endpoint Protection**, а затем выберите **Развернуть политику Exploit Guard**.

## <a name="limited-support-for-cng-certificates"></a>Ограниченная поддержка сертификатов CNG
<!-- 1356191 -->
Начиная с этого выпуска можно использовать шаблоны сертификатов [Cryptography API: Next Generation (CNG)](https://docs.microsoft.com/windows/win32/seccng/cng-features) для следующих сценариев:

- Регистрация клиента и обмен данными с точкой управления HTTPS.   
- Распространение программного обеспечения и развертывание приложений с использованием точки распространения HTTPS.   
- Развертывание операционной системы.  
- Пакет SDK для обмена сообщениями между клиентами (с последним обновлением) и прокси-сервер ISV.   
- Настройка шлюза управления облачными клиентами.  

Чтобы использовать сертификаты CNG, ваш центр сертификации должен предоставить шаблоны сертификатов CNG для целевых компьютеров.  Сведения о шаблоне отличаются в зависимости от сценария. Но следующие свойства являются обязательными:

- Вкладка **Совместимость**

    - **Центр сертификации** должен быть системой Windows Server 2008 или более поздней версии. (Рекомендуется Windows Server 2012).

    - **Получатель сертификата** должен быть системой Windows Vista или Windows Server 2008 или более поздней версии. (Рекомендуется Windows 8 и Windows Server 2012).

- Вкладка **Шифрование**

    - **Категория поставщика** должна иметь значение **Поставщик хранилища ключей**.  (Обязательно)

Для получения лучших результатов рекомендуется создать имя субъекта на основе сведений Active Directory.  Используйте DNS-имя для **формата имени субъекта** и включите DNS-имя в альтернативное имя субъекта.  Иначе вы должны будете указать эти сведения при регистрации устройства в профиле сертификата.


## <a name="improved-descriptions-for-pending-computer-restarts-----1356283---"></a>Улучшенные описания причин ожидания перезагрузки компьютером   <!--1356283 -->
В версию [technical preview 1708](capabilities-in-technical-preview-1708.md#restart-computers-from-the-configuration-manager-console) мы добавили возможность определения в консоли Configuration Manager устройств, которые ожидают перезагрузки.

После выпуска этой версии в консоли отображаются дополнительные сведения о процессе или действии, которые запрашивают перезагрузку.

## <a name="device-guard-policy-changes----1355092---"></a>Изменения политик Device Guard <!-- 1355092 -->
В сборке Technical Preview 1710 в политику Device Guard внесены следующие три изменения:

### <a name="device-guard-policies-renamed-to-windows-defender-application-control-policies"></a>Политики Device Guard переименованы в политики Application Control в Защитнике Windows
Политики Device Guard переименованы в политики Application Control в Защитнике Windows. Например, **мастер создания политик Device Guard** теперь называется **мастер создания политик Application Control в Защитнике Windows** .

### <a name="restart-is-not-required-to-apply-policies"></a>Для применения политик не требуется перезагрузка
После обновления Fall Creators Update версии 1709 для Windows устройства, использующие новую версию Windows, не нужно перезагружать для применения политик Application Control в Защитнике Windows.

Перезапуск выполняется по умолчанию.

#### <a name="try-it-out"></a>Попробуйте!  

Если вы хотите выключить перезагрузку, выполните следующие действия:

1.  Откройте мастер **создания политик Application Control в Защитнике Windows**.
2.  На странице **Общие** снимите флажок **Перезагружать устройства, чтобы политика была применена для всех процессов**.
3.  Нажмите кнопку **Далее** для завершения работы мастера.

В предыдущих версиях Windows по-прежнему применяется автоматическая перезагрузка.

### <a name="automatically-run-software-trusted-by-the-intelligent-security-graph"></a>Автоматический запуск программного обеспечения, которому доверяет Intelligent Security Graph

Теперь администраторы могут разрешать заблокированным устройствам запускать надежное программное обеспечение с хорошей репутацией в системе Microsoft Intelligent Security Graph (ISG). ISG включает SmartScreen в Защитнике Windows и другие службы Майкрософт.

Чтобы программное обеспечение могло стать надежным, на устройстве должен работать фильтр SmartScreen в Защитнике Windows.

#### <a name="try-it-out"></a>Попробуйте!  

Чтобы на устройстве с фильтром SmartScreen в Защитнике Windows работало надежное программное обеспечение, выполните следующие действия:

1.  Откройте мастер **создания политик Application Control в Защитнике Windows**.
2.  На странице **Включения** установите флажок **Авторизовать программное обеспечение, которому доверяет Intelligent Security Graph**.
3.  В поле **Надежные файлы или папки** добавьте надежные файлы и папки.
4.  Нажмите кнопку **Далее** для завершения работы мастера.

## <a name="configure-and-deploy-windows-defender-application-guard-policies----1351960---"></a>Настройка и развертывание политик Application Guard в Защитнике Windows <!-- 1351960 -->

[Application Guard в Защитнике Windows](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) — это новая функция Windows, которая помогает защитить пользователей, открывая ненадежные веб-узлы в безопасном изолированном контейнере, который никак не взаимодействует с другими частями операционной системы. В этом выпуске Technical Preview мы добавили возможность настроить эту функцию с помощью параметров соответствия Configuration Manager. Вы можете настроить их и развернуть в коллекции. Эта функция будет выпущена в предварительной версии для 64-разрядной версии Windows 10 Creator. Чтобы проверить ее в работе, необходимо использовать предварительную версию этого обновления.

### <a name="before-you-start"></a>Перед началом работы
Чтобы создавать и развертывать политики Application Guard в Защитнике Windows, для соответствующих устройств Windows 10 должны быть настроены политики сетевой изоляции. Дополнительные сведения см. в записи блога по ссылке ниже. Эта возможность поддерживается только в текущих сборках Windows 10 Insider. Чтобы проверить ее работу, на клиентах должна быть запущена последняя сборка Windows 10 Insider.

### <a name="try-it-out"></a>Попробуйте!

Прочитайте эту [запись блога](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97), чтобы понять принцип работы Application Guard в Защитнике Windows.

Чтобы создать политику и просмотреть доступные параметры, сделайте следующее.
1. В консоли **Configuration Manager** щелкните элемент **Активы и соответствие**.
2. В рабочей области **Активы и соответствие** выберите пункты **Обзор** > **Endpoint Protection** > **Application Guard в Защитнике Windows**.
3. На вкладке **Главная** в группе **Создать** щелкните **Создать политику Application Guard в Защитнике Windows**.
4. Вы можете просмотреть и настроить доступные параметры, а также испытать функцию в работе, используя запись блога в качестве инструкции.
5. В этом выпуске мы добавили в мастер новую страницу "Определение сети". На этой странице нужно указать удостоверение организации и определить границу корпоративной сети.

    > [!NOTE]
    > Компьютеры с ОС Windows 10 хранят только один список сетевой изоляции в клиенте. В этом выпуске вы можете создать два разных типа списков сетевой изоляции (один — из Windows Information Protection, а другой — из Application Guard в Защитнике Windows) и развернуть их в клиенте. При развертывании обеих политик эти списки сетевой изоляции должны совпадать. Если вы развернете несовпадающие списки на одном клиенте, произойдет сбой развертывания.

    Дополнительные сведения о том, как указать определения сети, см. в [документации по Windows Information Protection]: [Защита корпоративных данных с помощью Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. Когда вы закончите настройку, завершите работу мастера и разверните политику на одном или нескольких устройствах Windows 10.

### <a name="further-reading"></a>Дополнительные сведения

Дополнительные сведения об Application Guard в Защитника Windows см. в [этой записи блога](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Кроме того, в [этой записи блога](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903) см. дополнительные сведения об изолированном режиме Application Guard в Защитнике Windows.

## <a name="next-steps"></a>Дальнейшие шаги
Сведения об установке или обновлении ветви Technical Preview см. в статье [Technical Preview для Configuration Manager](technical-preview.md).    
