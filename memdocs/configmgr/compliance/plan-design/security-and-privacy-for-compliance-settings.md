---
title: Безопасность и конфиденциальность параметров соответствия требованиям
titleSuffix: Configuration Manager
description: Сведения о рекомендациях по обеспечению безопасности параметров соответствия требованиям в Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1c409244-6778-4970-a99c-d2508c9cf62b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: eae705b97add7515403549eb668e68f1489d6756
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692182"
---
# <a name="security-and-privacy-for-compliance-settings-in-configuration-manager"></a>Безопасность и конфиденциальность параметров соответствия в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*


## <a name="security-best-practices-for-compliance-settings"></a>Рекомендации по безопасности для параметров соответствия требованиям  

|Рекомендация по безопасности|Дополнительные сведения|  
|----------------------------|----------------------|  
|Не отслеживайте конфиденциальные данные.|Чтобы избежать раскрытия сведений, не настраивайте элементы конфигурации для отслеживания конфиденциальных данных.|  
|Не настраивайте правила соответствия, которые используют данные, доступные для изменения конечными пользователями.|При создании правила соответствия требованиям на основе данных, которые пользователи могут изменять, таких как параметры реестра для вариантов конфигурации, результаты проверки соответствия будут ненадежными.|  
|Импортируйте пакеты конфигурации Microsoft System Center и другие данные конфигурации из внешних источников, только если они имеют действительную цифровую подпись доверенного издателя.|Опубликованные данные конфигурации могут иметь цифровую подпись, чтобы проверить источник публикации и убедиться в том, что данные не были незаконно изменены. Если проверка цифровой подписи не пройдена, отображается соответствующее предупреждение и запрос на продолжение импорта. Не импортируйте неподписанные данные, если невозможно проверить их источник и целостность.|  
|Внедряйте средства управления доступом для защиты эталонных компьютеров.|Убедитесь в том, что при настройке пользователем параметра реестра или файловой системы путем обзора компьютера-образца этот компьютер не был скомпрометирован.|  
|Обеспечьте безопасность коммуникационного канала при обзоре компьютера-образца.|Чтобы предотвратить незаконное изменение данных, передаваемых по сети, используйте протокол IPsec или SMB для взаимодействия между компьютером с запущенной консолью Configuration Manager и компьютером-образцом.|  
|Ограничьте и отслеживайте действия пользователей, которым предоставлена роль системы безопасности на основе роли "Менеджер параметров соответствия".|Пользователи с правами администратора, которым предоставлена роль **Менеджер по параметрам соответствия** , могут развертывать элементы конфигурации на всех устройствах и для всех пользователей иерархии. Элементы конфигурации могут предоставлять большие возможности и включать в себя, например, сценарии и изменение настройки реестра.|  

## <a name="privacy-information-for-compliance-settings"></a>Сведения о соблюдении конфиденциальности для параметров соответствия требованиям  
 Параметры соответствия требованиям можно использовать для оценки соответствия клиентских устройств элементам конфигурации, развертываемым в базовых шаблонах конфигурации. Часть параметров можно автоматически исправлять, если они не соответствуют требованиям. Сведения о соответствии отправляются точкой управления на сервер сайта и сохраняются в базе данных сайта. Эта информация шифруется, когда устройства отправляют ее в точку управления, но не хранится в зашифрованном виде в базе данных сайта. Информация хранится в базе данных до тех пор, пока не будет удалена при выполнении задачи обслуживания сайта **Удаление устаревших данных управления конфигурацией** через каждые 90 дней. Можно настроить интервал удаления. Сведения о соответствии не отправляются в Майкрософт.  

 По умолчанию устройства не оценивают параметры соответствия. Кроме того, необходимо настроить элементы и базовые шаблоны конфигурации, а затем развернуть их на устройствах.  