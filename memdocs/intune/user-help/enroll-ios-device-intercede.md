---
title: Регистрация устройства с iOS или iPadOS с помощью корпоративного портала Intune и Intercede
description: Узнайте, как зарегистрировать устройство с iOS или iPadOS и настроить проверку подлинности производных учетных данных с помощью Intercede.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 1bd216049c5dbda7c044949f9fa39c3b7bd56f9d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79337243"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-intercede"></a>Настройка устройства с iOS или iPadOS с помощью корпоративного портала и Intercede

Зарегистрируйте устройство с помощью приложения "Корпоративный портал Intune" для безопасного доступа к электронной почте, файлам и приложениям вашей организации с мобильного устройства.  После регистрации устройства оно становится *управляемым*. Теперь ваша организация может назначать этому устройству политики и приложения с помощью своего поставщика управления мобильными устройствами (MDM), например Intune.  

Во время регистрации вы также установите на устройстве производные учетные данные. Организация может потребовать использовать производные учетные данные в качестве метода проверки подлинности при доступе к ресурсам, а также для подписывания и шифрования сообщений электронной почты. 

Вам может потребоваться настроить производные учетные данные, если вы используете смарт-карту в следующих целях:

* вход в учебные или рабочие приложения, сети Wi-Fi и виртуальные частные сети (VPN);
* подписывание и шифрование учебных и рабочих сообщений электронной почты с помощью сертификатов S/MIME.  

В этой статье мы затронем следующие вопросы.  

* Регистрация устройства с iOS или iPadOS с помощью корпоративного портала Intune.  
* Получение производных учетных данных от поставщика производных учетных данных организации — [Intercede](https://www.intercede.com/).   


## <a name="what-are-derived-credentials"></a>Что такое производные учетные данные?  
Производные учетные данные — это сертификат, созданный на основе учетных данных смарт-карты и установленный на устройстве. Он предоставляет удаленный доступ к рабочим ресурсам, запрещая неавторизованным пользователям обращаться к конфиденциальной информации.  

Производные учетные данные используются в следующих целях: 
* проверка подлинности учащихся и сотрудников, которые входят в учебные или рабочие приложения, сети Wi-Fi и VPN;
* подписывание и шифрование учебных и рабочих сообщений электронной почты с помощью сертификатов S/MIME.  

Производные учетные данные являются реализацией рекомендаций национального института стандартов и технологий (NIST) для производных учетных данных проверки личности (PIV) в составе специальной публикации (SP) 800-157.  

## <a name="prerequisites"></a>Предварительные условия

 Для регистрации вам необходимы:

* смарт-карта, предоставленная учебным заведением или организацией;
* доступ к компьютеру или киоску самообслуживания, на которые можно войти с помощью смарт-карты;
* Мобильное устройство
* приложение корпоративного портала Intune для iOS and iPadOS, установленное на вашем устройстве.


## <a name="enroll-device"></a>Регистрация устройства  
1. Откройте приложение корпоративного портала для iOS/iPadOS на мобильном устройстве и выполните вход с использованием рабочей учетной записи.  
2. Запишите код, отображаемый на экране.  

    ![Пример изображения приложения корпоративного портала с экранным сообщением и кодом.](./media/copy-code-intercede.png)  
1. Перейдите на устройство с поддержкой смарт-карты и перейдите по адресу https://microsoft.com/devicelogin. 

1. Введите записанный ранее код.
 
2. Вставьте смарт-карту, чтобы войти.   

3. Вернитесь в приложение корпоративного портала на мобильном устройстве и следуйте инструкциям по регистрации устройства на экране.  
4. После завершения регистрации корпоративный портал сообщит вам о настройке доступа по смарт-карте. Коснитесь уведомления. Если вы не получили уведомление, проверьте свою электронную почту.   

    ![Пример снимка экрана корпоративного портала с push-уведомлением на начальном экране устройства.](./media/action-required-in-app-intercede.png)  

5. На экране **Настройка доступа по смарт-карте для мобильного устройства** выполните следующие действия.  
    a. Перейдите по ссылке на инструкции по настройке, предоставленные вашей организацией. Если дополнительных инструкций не будет, вы будете перенаправлены на эту статью.  
    b. Выберите **Начать**.  

    ![Снимок экрана приложения корпоративного портала с экраном "Настройка доступа по смарт-карте для мобильного устройства".](./media/smart-card-info-intercede.png)  

6. Переключитесь на устройство с поддержкой смарт-карт или на киоск самообслуживания и откройте приложение MyID. Войдите в систему с использованием рабочей учетной записи.  
7. Выберите параметр для запроса идентификатора. 
8. Будет предложено выбрать тип используемого профиля. Выберите активацию с мобильными учетными данными. Появится QR-код.  
9. Вернитесь на мобильное устройство. На экране **Получить QR-код** корпоративного портала нажмите **Продолжить**.  

    ![Пример снимка экрана "Получить QR-код" корпоративного портала.](./media/get-qr-code-intercede.png) 
 
10. Выберите **Использовать камеру** > **OK**.  

    ![Пример снимка экрана корпоративного портала с запросом разрешения на доступ к камере.](./media/allow-cp-camera-access-intercede.png)  

11. Проверьте изображение QR-кода на устройстве с поддержкой смарт-карт. 
12. Дождитесь завершения настройки устройства на корпоративном портале.  

## <a name="next-steps"></a>Дальнейшие шаги  
После завершения регистрации вы получите доступ к рабочим ресурсам, таким как электронная почта, Wi-Fi и любым приложениям, доступным в организации. Дополнительные сведения о том, как скачивать, искать, устанавливать и удалять приложения на корпоративном портале см. в следующих статьях:

* [Управление приложениями с веб-сайта корпоративного портала](manage-apps-cpweb.md)  
* [Использование управляемых приложений на устройстве](use-managed-apps-on-your-device-ios.md)  

По-прежнему нужна помощь? Обратитесь в службу поддержки вашей компании. Его контактные данные доступны на [веб-сайте корпоративного портала](https://go.microsoft.com/fwlink/?linkid=2010980).