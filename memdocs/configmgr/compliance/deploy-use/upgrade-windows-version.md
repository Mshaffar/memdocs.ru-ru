---
title: Обновление устройств Windows до другой версии
titleSuffix: Configuration Manager
description: Используйте Configuration Manager для автоматического обновления устройств Windows 10 до другого выпуска Windows.
ms.date: 09/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 77ef255a820104ef2042a370b5056677fddb9d12
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692302"
---
# <a name="upgrade-windows-devices-to-a-new-edition-with-configuration-manager"></a>Обновление устройств с ОС Windows до нового выпуска с помощью Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

**Политика обновления выпуска** позволяет автоматически обновлять выпуск на устройствах под управлением Windows 10.

Поддерживаются следующие варианты обновления:

- Windows 10 Pro до Windows 10 Корпоративная
- Windows 10 Домашняя до Windows 10 для образовательных учреждений
- С Windows 10 Mobile до Windows 10 Mobile Корпоративная

На устройствах должно выполняться клиентское программное обеспечение Configuration Manager. Устройства, управляемые [локальным решением MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md), не поддерживаются.

## <a name="before-you-start"></a>Перед началом работы

Прежде чем начать обновление устройств до последней версии, ознакомьтесь со следующими требованиями:  

- Настольные версии Windows 10 — требуется действительный ключ продукта для установки новой версии Windows на всех целевых устройствах политики. Это может быть ключ многократной активации (MAK) или универсальный ключ многократной установки (GVLK). GVLK также называют ключом установки клиента для службы управления ключами (KMS). Дополнительные сведения см. в статье [Планирование активации корпоративных лицензий](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Список ключей установки клиента KMS см. в [Приложении A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) руководства по активации Windows Server. <!--496871-->  

- Windows 10 Mobile — требуется XML-файл лицензии из Центра обслуживания по программам корпоративного лицензирования (VLSC) Майкрософт. Этот файл содержит сведения о лицензии на новую версию Windows для всех целевых устройств политики.

- Для управления политикой этого типа вам должна быть назначена роль безопасности Configuration Manager **Полный администратор**.

## <a name="configure-the-policy"></a>Настройка политики  

1. В консоли Configuration Manager в рабочей области **Активы и соответствие** разверните узел **Параметры соответствия** и выберите узел **Обновление выпуска Windows 10**.  

2. На вкладке ленты **Главная** в группе **Создать** выберите **Создать политику обновления выпуска**.  

3. Нажмите **Создать политику**.  

4. На странице **Общие** **мастера создания политики обновления выпусков**укажите перечисленные ниже сведения.  

    - **Имя** — введите имя политики обновления выпусков  

    - **Описание** (необязательно) — при необходимости введите описание политики, которое поможет узнать ее в консоли Configuration Manager.  

    - **SKU, до которого нужно обновить устройство** — в раскрывающемся списке выберите целевую версию Windows 10 Desktop или Windows 10 Mobile  

    - **Сведения о лицензии** — выберите один из следующих вариантов:  

        - **Ключ продукта** — введите допустимый ключ продукта для целевого выпуска Windows 10 Desktop  

            > [!NOTE]  
            > Когда вы создадите политику, содержащую ключ продукта, изменить этот ключ позже будет невозможно. Configuration Manager скрывает ключ в целях безопасности. Для изменения ключа продукта потребуется ввести весь ключ повторно.  

        - **Файл лицензии** — щелкните **Обзор**, чтобы выбрать допустимый файл лицензии в формате XML. Configuration Manager использует этот файл лицензии для обновления устройств Windows 10 Mobile.  

5. Завершите работу мастера.  

## <a name="deploy-the-policy"></a>Развертывание политики  

1. В консоли Configuration Manager в рабочей области **Активы и соответствие** разверните узел **Параметры соответствия** и выберите узел **Обновление выпуска Windows 10**.  

2. Выберите политику обновления выпуска Windows 10, которую требуется развернуть. На вкладке **Главная** в ленте в группе **Развертывание** выберите **Развернуть**.  

3. Выберите коллекцию устройств, в которой требуется развернуть политику.

4. Выберите расписание анализа политики клиентом.

5. Завершите работу мастера.

## <a name="next-steps"></a>Дальнейшие шаги

Вы можете отслеживать это развертывание в узле **Развертывания** рабочей области **Мониторинг**. Возможно появление ошибок, свидетельствующих о неудачном развертывании, например:

- **Неприменимо для этого устройства**
- **Не удалось выполнить преобразование типа данных**

Эти ошибки не означают, что развертывание не удалось выполнить. Проверьте на целевом устройстве, что обновление выполнено.

После того как клиент проанализирует целевую политику, он установит обновление в течение двух часов. [Некоторые версии Windows](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-edition-upgrades) в это время могут потребовать перезагрузки. Обязательно проинформируйте всех пользователей, для которых развертывается политика, или запланируйте ее выполнение вне рабочего времени пользователей.

Если в журнале **DcmWmiProvider.log** на стороне клиента возникает следующая ошибка, проверьте, используете ли вы правильный ключ для сценария активации. Дополнительные сведения см. в разделе [Перед началом работы](#before-you-start). Если вы используете для активации службу управления ключами (KMS), обязательно используйте [ключ установки клиента KMS](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys).  <!-- 496871 -->

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`

## <a name="see-also"></a>См. также

- [Планирование многопользовательской активации](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)

- [Обновление выпуска Windows 10](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-edition-upgrades)

- [Обновление выпусков Windows 10 или выход из режима S на устройствах с помощью Microsoft Intune](https://docs.microsoft.com/intune/edition-upgrade-configure-windows-10)