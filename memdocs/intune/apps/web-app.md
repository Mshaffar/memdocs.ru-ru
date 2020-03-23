---
title: Добавление веб-приложений в Microsoft Intune
titleSuffix: ''
description: Сведения о добавлении веб-приложений (приложения на основе архитектуры "клиент-сервер") в Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/22/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5f08752f-0e87-4ad9-a34c-4991b3150775
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3fc6b9fc427ab6e0dc0488061378e78060527676
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79361982"
---
# <a name="add-web-apps-to-microsoft-intune"></a>Добавление веб-приложений в Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune поддерживает множество типов приложений, в том числе веб-приложения. Веб-приложение — это приложение на основе архитектуры "клиент-сервер". Сервер предоставляет веб-приложение, включая его пользовательский интерфейс, содержимое и функциональные возможности. Кроме того, современные платформы размещения веб-приложений, как правило, реализуют функции безопасности, балансировки нагрузки и другие преимущества. Веб-приложение размещается в Интернете. Вы указываете ссылку на него в Microsoft Intune. Вы также назначаете группы пользователей, которым оно доступно. 

Чтобы назначать приложение пользователям и управлять им, добавьте его в Intune. 

Intune создает ярлык со ссылкой на веб-приложение на устройстве пользователя. Для устройств iOS и iPadOS ярлык веб-приложения добавляется на начальный экран. Для устройств с правами администратора на базе Android в виджет портала компании Intune добавляется ярлык к веб-приложению, который пользователь должен прикрепить вручную. Для устройств Windows ярлык веб-приложения помещается в меню "Пуск".

> [!Note]
> Чтобы запускать веб-приложения на устройстве пользователя, на нем должен быть установлен браузер. 

> [!Note]
> Сведения для устройств Android Enterprise см. в разделе [Веб-ссылки в управляемом Google Play](apps-add-android-for-work.md#managed-google-play-web-links)

## <a name="add-a-web-app-to-intune"></a>Добавление веб-приложения в Intune
Чтобы добавить приложение в Intune как ярлык для веб-приложения, сделайте следующее:

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Приложения** > **Все приложения** > **Добавить**.
3. В области **Выбрать тип приложения** выберите в списке доступных типов **Другие** пункт **Веб-ссылка**.
4. Щелкните **Выбрать**. Отобразятся шаги для **добавления приложения**.
5. На странице **Сведения о приложении** добавьте следующие сведения:
    - **Имя** —  Введите имя приложения, которое будет отображаться на корпоративном портале. 

        > [!NOTE]
        > Если после развертывания и установки приложения изменить его имя на портале Intune Azure, использовать для него команды станет невозможно.

    - **Описание**. Введите описание приложения. Оно отображается на корпоративном портале.
    - **Издатель** — Введите имя издателя этого приложения.
    - **URL-адрес приложения**. Укажите URL-адрес веб-сайта, где размещено приложение, которое требуется назначить.
    - **Категория** — При необходимости выберите для приложения одну или несколько встроенных или созданных вами категорий. Это поможет пользователям найти приложение на корпоративном портале.
    - **Отображение этого приложения как рекомендуемого на Корпоративном портале**. Выберите этот параметр, чтобы набор приложений отображался на видном месте на главной странице Корпоративного портала, когда пользователи просматривают приложения.
    - **Требовать Managed Browser, чтобы открыть эту ссылку**. Выберите этот параметр, чтобы назначить пользователям ссылку на веб-сайт или веб-приложение, которую они смогут открыть в Intune Managed Browser. Такой браузер должен быть установлен на устройстве.
    - **Логотип**. Загрузите значок, который будет связан с приложением. Этот значок будет отображаться с приложением при просмотре пользователями корпоративного портала.
6. Нажмите кнопку **Далее**, чтобы отобразить страницу **Теги области**.
7. Щелкните **Выберите теги области**, чтобы дополнительно добавить теги области для приложения. Дополнительные сведения см. в статье [Использование управления доступом на основе ролей (RBAC) и тегов области для распределенных ИТ](../fundamentals/scope-tags.md).
8. Нажмите кнопку **Далее**, чтобы перейти на страницу **Назначения**.
9. Выберите назначения групп для приложения. Дополнительные сведения см. в статье [Добавление групп для организации пользователей и устройств](../fundamentals/groups-add.md). 
10. Выберите **Далее**, чтобы перейти на страницу **Просмотр и создание**. Проверьте значения и параметры, введенные для приложения.
11. По завершении нажмите кнопку **Создать**, чтобы добавить приложение в Intune.

    Отобразится колонка **Обзор** созданного приложения.

> [!Note]
> Сейчас развертывание веб-приложений Intune на устройствах iOS и iPadOS связано с профилем управления и не подлежит удалению вручную. На портале Intune вы можете изменить значение типа развертывания на **Удаление**. После этого веб-приложение можно удалить автоматически. Если вы удалите развертывание, перед тем как изменить намерение для назначения приложений на **Удаление**, веб-приложение будет оставаться на устройстве до отмены регистрации в Intune.

Конечные пользователи могут запускать веб-приложения непосредственно из приложения "Корпоративный портал" для Windows, выбрав веб-приложение и параметр **Открыть в браузере**. Опубликованный URL-адрес открывается непосредственно в веб-браузере. 

## <a name="next-steps"></a>Дальнейшие шаги

Созданное приложение отображается в списке приложений, из которого его можно назначить выбранным группам. Сведения см. в статье [Назначение приложений группам](apps-deploy.md). 