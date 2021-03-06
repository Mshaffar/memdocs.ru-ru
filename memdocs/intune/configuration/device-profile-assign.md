---
title: Назначение профилей устройств в Microsoft Intune | Документы Майкрософт
description: Используйте Центр администрирования Microsoft Endpoint Manager для назначения профилей и политик устройств пользователям и устройствам. Сведения об исключении групп из назначения профилей в Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f6f5414d-0e41-42fc-b6cf-e7ad76e1e06d
ms.reviewer: altsou
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a05e36a2da42bf88e2d9d7e94a67e2d81b8f1271
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078283"
---
# <a name="assign-user-and-device-profiles-in-microsoft-intune"></a>Назначение профилей пользователей и устройств в Microsoft Intune

При создании профиля он содержит все настройки, которые вы ввели. Следующим шагом является развертывание или "назначение" профиля для групп пользователей или устройств Azure Active Directory (Azure AD). Когда он назначен, пользователи и устройства получают ваш профиль, и применяются введенные вами параметры.

В этой статье показано, как назначить профиль, и приведена некоторая информация об использовании тегов области в ваших профилях.

> [!NOTE]  
> При удалении профиля или если его больше не назначают устройству, в зависимости от параметров профиля могут возникнуть различные действия. Эти параметры основаны на CSP, и каждый CSP может обрабатывать удаление профиля по-разному. Например, параметр может сохранить существующее значение и не вернуться к значению по умолчанию. Поведение управляется каждым CSP в операционной системе. Список CSP для Windows см. в статье [Configuration service provider reference](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference) (Справочник по CSP).
>
> Чтобы изменить значение параметра на другое, создайте новый профиль, задайте для параметра значение **Не настроено**и назначьте профиль. После применения к устройству пользователи должны иметь контроль над изменением параметра на предпочтительное значение.
>
> При настройке этих параметров мы рекомендуем выполнить развертывание в пилотной группе. Дополнительные советы по планах развертывания Intune см. в статье [Разработка плана внедрения](../fundamentals/planning-guide-rollout-plan.md).

## <a name="before-you-begin"></a>Подготовка к работе

Убедитесь, что у вас есть соответствующая роль для назначения профилей. Дополнительные сведения см. в разделе [Управление доступом на основе ролей (RBAC) с помощью Microsoft Intune](../fundamentals/role-based-access-control.md).

## <a name="assign-a-device-profile"></a>Назначение профиля устройства

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Устройства** > **Профили конфигурации**. Перечисляются все профили.
3. Выберите профиль, который вы хотите назначить, щелкнув **Назначения**.
4. Щелкните **Включить** или **Исключить**, чтобы включить или исключить группы соответственно, а затем выберите группы. При выборе групп вы выбираете группу Azure AD. Чтобы выбрать сразу несколько групп, удерживайте нажатой клавишу **CTRL** и выберите группы.

    ![Снимок экрана с параметрами включения или исключения групп в назначении профиля](./media/device-profile-assign/group-include-exclude.png)

5. **Сохраните** внесенные изменения.

### <a name="evaluate-how-many-users-are-targeted"></a>Оценка количества затронутых пользователей

При назначении профиля вы также можете **оценить** количество затронутых пользователей. Эта функция вычисляет пользователей, но не вычисляет устройства.

1. В центре администрирования выберите **Устройства** > **Профили конфигурации**.
2. Выберите политику, щелкнув **Назначения** > **Оценить**. Отобразится сообщение о том, на какое количество пользователей распространяется этот профиль.

Если кнопка **Оценить** неактивна, убедитесь, что этот профиль назначен одной или нескольким группам.

## <a name="use-scope-tags-or-applicability-rules"></a>Использование тегов области или правил применимости

При создании или обновлении профиля в него также можно добавить теги области и правила применимости.

**Теги областей** — это отличный способ фильтрации профилей для конкретных групп, таких как `US-NC IT Team` или `JohnGlenn_ITDepartment`. Дополнительные сведения см. в статье [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md) (Использование управления доступом на основе ролей (RBAC) и тегов области для распределенной ИТ разработки).

На устройствах Windows 10 можно добавить **правила применимости**, чтобы профиль применялся только к определенной версии ОС или к конкретному выпуску Windows. [Правила применимости](device-profile-create.md#applicability-rules) содержат дополнительные сведения.

## <a name="user-groups-vs-device-groups"></a>Группы пользователей и группы устройств

Многие пользователи спрашивают, когда использовать группы пользователей, а когда — группы устройств. Ответ зависит от цели. Вот несколько советов для начала работы.

### <a name="device-groups"></a>Группы устройств

Если вы хотите применять параметры на устройстве, независимо от того, кто вошел в систему, назначьте свои профили группе устройств. Параметры, применяемые к группам устройств, всегда относятся к устройству, а не к пользователю.

Пример.

- Группы устройств используются для управления устройствами, у которых нет выделенного пользователя. Например, у вас есть устройства, которые печатают билеты, сканируют товары, совместно используются сотрудниками разных смен, назначаются определенному хранилищу и т. д. Поместите эти устройства в группу устройств и назначьте свои профили этой группе.

- Вы создали [профиль Intune интерфейса настройки встроенного ПО устройства (DFCI)](device-firmware-configuration-interface-windows.md), который обновляет параметры в BIOS. Например, настройте этот профиль для отключения камеры устройства или блокирования параметров загрузки, чтобы пользователи не могли загружать другую ОС. Этот профиль подходит для назначения группе устройств.

- На некоторых определенных устройствах Windows вы хотите всегда управлять некоторыми параметрами Microsoft Edge независимо от того, кто использует устройство. Например, вам нужно заблокировать все загрузки, ограничить все файлы cookie до текущего сеанса просмотра и удалить историю просмотров. Для этого поместите эти устройства Windows в группу устройств. Затем создайте [административный шаблон в Intune](administrative-templates-windows.md), добавьте эти параметры устройства и назначьте этот профиль группе устройств.

Подытоживая вышесказанное: используйте группы устройств, если не важно, кто вошел в систему устройства или вошел ли кто-то. Параметры всегда должны быть на устройстве.

### <a name="user-groups"></a>Группы пользователей

Параметры профиля, применяемые к группам пользователей, всегда связаны с пользователем, даже если они выполняют вход на многочисленных устройствах. У пользователей может быть много устройств, таких как Surface Pro для выполнения рабочих задач и личное устройство iOS или iPadOS. И это нормально, когда пользователь получает доступ к электронной почте и другим ресурсам организации с этих устройств.

Пример.

- Вы хотите разместить значок службы технической поддержки для всех пользователей на всех их устройствах. В этом случае поместите этих пользователей в группу пользователей и назначьте ей свой профиль значка службы технической поддержки.
- Пользователь получает новое устройство, принадлежащее организации. Пользователь входит в устройство с использованием своей учетной записи домена. Устройство автоматически регистрируется в Azure AD и автоматически управляется службой Intune. Этот профиль подходит для назначения группе пользователей.
- Вы хотите управлять функциями в приложениях, таких как OneDrive или Office, когда пользователь входит в систему устройства. В этом случае присвойте параметры профиля OneDrive или Office группе пользователей.

  Например, вы хотите заблокировать недоверенные элементы ActiveX в своих приложениях Office. Вы можете создать [административный шаблон в Intune](administrative-templates-windows.md), настроить этот параметр, а затем назначить этот профиль группе пользователей.

Подытоживая вышесказанное: используйте группы пользователей, чтобы параметры и правила всегда применялись к пользователю, независимо от используемого им устройства.

## <a name="exclude-groups-from-a-profile-assignment"></a>Исключение групп в назначении профиля

Профили конфигурации устройств Intune позволяют включать группы в назначения профилей и исключать их оттуда.

Мы рекомендуем создавать и назначать профили специально для групп пользователей. При этом лучше создавать и назначать разные профили для групп устройств. См. сведения о [добавлении групп для упорядочивания пользователей и устройств](../fundamentals/groups-add.md).

Назначая профили, используйте следующую таблицу при включении и исключении групп. Флажок означает, что назначение поддерживается:

![Поддерживаемые варианты включения и исключения групп в назначении профиля](./media/device-profile-assign/include-exclude-user-device-groups.png)

### <a name="what-you-should-know"></a>Учитываемые аспекты

- Исключение имеет приоритет над включением в следующих сценариях с одним типом группы:

  - Включение и исключение групп пользователей
  - Включение и исключение групп устройств

  Например, можно назначить профиль устройства для группы пользователей **Все корпоративные пользователи**, исключив при этом всех членов группы пользователей **Руководители старшего звена**. Так как обе группы являются группами пользователей, профиль применяется ко **всем корпоративным пользователям**, за исключением **руководителей старшего звена**.

- Intune не учитывает связи групп "пользователь — устройство". Если вы назначаете профили смешанным группам, результаты могут быть неожиданными.

  Например, можно назначить профиль устройства группе пользователей **Все пользователи**, исключив при этом группу устройств **Все персональные устройства**. В этом смешанном назначении группового профиля он будет применен ко **всем пользователям**. Исключение при этом не выполняется.

  Таким образом, назначать профили смешанным группам не рекомендуется.

## <a name="next-steps"></a>Дальнейшие шаги

Дополнительные инструкции по мониторингу профилей и устройств, на которых выполняются ваши профили, см. в статье [Мониторинг профилей устройств в Microsoft Intune](device-profile-monitor.md).
