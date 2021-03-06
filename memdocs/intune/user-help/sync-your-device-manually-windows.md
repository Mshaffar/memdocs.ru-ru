---
title: Синхронизация устройства с Windows вручную | Документы Майкрософт
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/24/2018
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: priyar
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 5346a288a8411a66ab79b0816385a530eeabb8c2
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881859"
---
# <a name="sync-your-windows-device-manually"></a>Синхронизация устройства с Windows вручную.

Если скорость установки приложения не соответствует ожиданиям, настройте синхронизацию устройства вручную. Если синхронизация настроена вручную, устройство подключается к Intune для получения последних обновлений и сообщений. Когда синхронизация устройства будет завершена, скорость установки может повыситься.

Intune поддерживает синхронизацию вручную из приложения "Корпоративный портал", с панели задач на рабочем столе или из меню "Пуск", а также из приложения "Параметры устройства". Функции приложения "Корпоративный портал" поддерживаются для устройств под управлением Windows 10 Creators Update (1703) или более поздней версии. 

Все устройства Windows можно синхронизировать с помощью приложения параметров устройств, включая:

* [Windows 10 Desktop](#windows-10-desktop)  
* [Microsoft HoloLens](#microsoft-hololens);   
* [Windows 10 Mobile](#windows-10-mobile)  
* [Windows Phone 8.1](#windows-phone-81)    

## <a name="sync-directly-from-company-portal-app-for-windows"></a>Синхронизация из приложения корпоративного портала для Windows
Чтобы вручную выполнить синхронизацию любого устройства под управлением Windows 10 Creators Update 1709 или более поздней версии, сделайте следующее:

1. Откройте приложение "Корпоративный портал" на устройстве.

2. Последовательно выберите **Параметры** > **Синхронизации**.

    ![Снимок экрана: домашняя страница приложения "Корпоративный портал", выделен пункт "Параметры"](./media/RS1_homePage_settings_04.png)  
    
    ![Снимок экрана: страница параметров для приложения "Корпоративный портал", выделена кнопка синхронизации](./media/RS1_settingspage_sync05.png)  

## <a name="sync-from-device-taskbar-or-start-menu"></a>Синхронизация с панели задач устройства или из меню "Пуск"   

Контроль синхронизации также можно осуществлять за пределами приложения, с рабочего стола вашего устройства. Это удобно, если приложение закреплено непосредственно на панели задач или в меню "Пуск" и вам нужно быстро выполнить синхронизацию.  

1. Найдите значок приложения корпоративного портала на панели задач или в меню "Пуск".  
2. Щелкните значок приложения правой кнопкой мыши, чтобы отобразить его меню (также называется "список переходов").  

    ![Снимок экрана панели задач Windows на рабочем столе устройства. При нажатии значка приложения "Корпоративный портал" отображается меню со следующими параметрами: "Закрепить на панели задач", "Закрыть окно" и "Синхронизировать это устройство".](./media/sync-device-from-start-menu-1807.png)  

3. Выберите **Синхронизировать это устройство**. В приложении "Корпоративный портал" откроется страница **Параметры** и запустится синхронизация.  

## <a name="sync-from-settings-app"></a>Синхронизация с помощью приложения "Параметры" 
Чтобы вручную настроить синхронизацию устройств под управлением Microsoft HoloLens, Windows 10 Desktop, Windows 10 Mobile или Windows Phone 8.1 с помощью приложения "Параметры", сделайте следующее.  

### <a name="windows-10-desktop"></a>Windows 10 Desktop
1. На своем устройстве последовательно выберите **Пуск** > **Параметры**.

2. Выберите **Учетные записи**.

    ![Выбор учетных записей на странице параметров](./media/win10pc-sync-2-settings-accounts.png)  

3. Есть несколько классических версий Windows 10. Сравните изображение на экране своего устройства с представленными ниже снимками экрана, чтобы определить, какой набор инструкций нужно выполнить. 

    * Если на экране отображается параметр **Доступ к рабочей или учебной учетной записи**, перейдите к инструкциям для параметра [Доступ к рабочей или учебной учетной записи](#access-work-or-school-steps).

    ![Параметр "Доступ к рабочей или учебной учетной записи" в приложении параметров](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

    * Если на экране отображается параметр **Рабочий доступ**, перейдите к инструкциям для параметра [рабочего доступа](#work-access-steps).  

    ![Выбор рабочего доступа в качестве типа учетной записи](./media/win10pc-sync-3-work-access.png)

#### <a name="access-work-or-school-steps"></a>Инструкции для параметра доступа к рабочей или учебной учетной записи

1. Выберите **Доступ к рабочей или учебной учетной записи**.

    ![Снимок экрана с параметром "Доступ к рабочей или учебной учетной записи"](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

2. Выберите учетную запись, рядом с которой отображается значок портфеля. Если эта учетная запись не отображается, возможно, в вашей компании заданы другие настройки. В таком случае щелкните учетную запись, рядом с которой отображается логотип корпорации Майкрософт.

     ![Выберите имя учетной записи рядом со значком портфеля или логотипом Майкрософт](./media/win10pc-rs1-sync-info-button.png)

3. Щелкните **Информация**. 

4. Щелкните **Синхронизировать**. 

#### <a name="work-access-steps"></a>Инструкции для параметра рабочего доступа

1. Щелкните **Рабочий доступ**.

    ![Выбор рабочего доступа в качестве типа учетной записи](./media/win10pc-sync-3-work-access.png)

2. В разделе **Регистрация в системе управления устройствами** выберите название своей организации.

    ![Выбор названия компании для управления устройствами](./media/win10pc-sync-4-tap-com-name.png)

3. Щелкните **Синхронизировать**. Кнопка останется неактивной до завершения синхронизации.

    ![Нажатие кнопки синхронизации](./media/win10pc-sync-5-tap-sync.png)  


### <a name="windows-10-mobile"></a>Windows 10 Mobile

   1. На своем устройстве последовательно выберите пункты **Все приложения** > **Параметры** > **Учетные записи**.

       ![Выбор учетных записей на экране настройки](./media/win10m-sync-1-settings-accounts.png)

   2. Выберите **Рабочий доступ**.

       ![Выбор рабочего доступа в качестве типа учетной записи](./media/win10m-sync-2-work-access.png)

   3. В разделе **Регистрация в системе управления устройствами** выберите название своей организации.

       ![Выбор названия компании для управления устройствами](./media/win10m-sync-3-tap-comp-name.png)

   4. Щелкните значок **синхронизации**. Кнопка останется неактивной до завершения синхронизации.

       ![Выбор значка синхронизации](./media/win10m-sync-4-tap-sync.png)  
### <a name="microsoft-hololens"></a>Microsoft HoloLens  
Эти инструкции относятся к устройствам HoloLens под управлением юбилейного обновления Windows 10 (также называется RS1). 
1. Откройте на устройстве приложение "Параметры".  

2. Последовательно выберите **Учетные записи** > **Рабочий доступ**.  
    ![Снимок экрана: приложение параметров HoloLens, выделена ссылка "Учетные записи"](./media/RS1_holoLens_SettingsRS1_Accounts_06.png)  

3. Выберите свою подключенную учетную запись и нажмите кнопку **Синхронизировать**.  ![Снимок экрана: приложение параметров HoloLens, выделена кнопка синхронизации](./media/RS1_holoLens_SyncRS1_Sync_08.png)  

### <a name="windows-phone-81"></a>Windows Phone 8.1

1. Последовательно выберите пункты **Все приложения** > **Параметры** > **Рабочая область**.

    ![Список параметров](./media/wp81-1-sync-settings-workplace.png)

2. Выберите название своей компании.

    ![Выбор названия компании для учетной записи рабочей области](./media/wp81-2-sync-tap-compname.png)

3. Щелкните значок **синхронизации**.

    ![Выбор значка синхронизации](./media/wp81-3-sync-tap-sync-button.png)

По-прежнему нужна помощь? Обратитесь в службу поддержки вашей компании. Его контактные данные доступны на [веб-сайте корпоративного портала](https://go.microsoft.com/fwlink/?linkid=2010980).
