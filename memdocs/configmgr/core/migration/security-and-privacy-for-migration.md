---
title: Безопасность и конфиденциальность при миграции
titleSuffix: Configuration Manager
description: Рекомендации по обеспечению безопасности и сведения о конфиденциальности для миграции в среде Configuration Manager (Current Branch).
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ad92e4906c45b5c720ab35efc055449a27cc0850
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906220"
---
# <a name="security-and-privacy-for-migration-to-configuration-manager-current-branch"></a>Безопасность и конфиденциальность при миграции на Configuration Manager (Current Branch)

*Область применения: Configuration Manager (Current Branch)*

В этом разделе представлены рекомендации по обеспечению безопасности и сведения о конфиденциальности для миграции в среде Configuration Manager (Current Branch).  

## <a name="security-best-practices-for-migration"></a>Рекомендации по обеспечению безопасности во время миграции  
 Примите во внимание следующие рекомендации по обеспечению безопасности при миграции.  

|Рекомендация по безопасности|Дополнительные сведения|  
|----------------------------|----------------------|  
|В качестве учетной записи поставщика SMS исходного сайта и учетной записи SQL Server исходного сайта используйте учетную запись компьютера, а не пользователя.|Если для миграции необходимо использовать учетную запись пользователя, удалите учетные данные после завершения миграции.|  
|При миграции контента из точки распространения в исходном сайте в точку распространения в конечном сайте используйте протокол IPsec.|Хотя переносимое содержимое хэшируется, чтобы выявить искажение, однако при изменении данных во время передачи, происходит сбой миграции.|  
|Ограничьте доступ и отслеживайте действия пользователей, которые могут создавать задания миграции.|Целостность базы данных в конечной иерархии зависит от целостности данных, которые администратор выбирает для импорта из исходной иерархии. Кроме того, администратор может считывать все данные из исходной иерархии.|  

### <a name="security-issues-for-migration"></a>Проблемы безопасности при миграции  
Проблемы безопасности при выполнении миграции.  

-   Клиенты, доступ которых к исходному сайту заблокирован, могут быть успешно назначены в конечную иерархию, прежде чем будет выполнена миграция их записи клиента.  

     Хотя Configuration Manager сохраняет статус блокировки для переносимого клиента, клиент может быть успешно назначен в конечную иерархию, если назначение происходит до завершения миграции записи клиента.  

-   Сообщения аудита не переносятся.  

При переносе данных из исходного сайта в конечный будут потеряны все данные аудита из исходной иерархии.  

## <a name="privacy-information-for-migration"></a>Сведения о конфиденциальности при миграции  
 Функция миграции обнаруживает данные из баз данных сайта, указанных в исходной инфраструктуре, и сохраняет их в базе данных конечной иерархии. Информация, которую Configuration Manager может обнаружить в исходном сайте или иерархии, зависит от функций, которые были включены в исходной среде, а также операций управления, которые были выполнены в этой среде.  

 Дополнительные сведения о безопасности и конфиденциальности см. один из следующих разделов.  

-   Дополнительные сведения о конфиденциальности для Configuration Manager 2007 см. в статье [Обеспечение безопасности и конфиденциальности в Configuration Manager 2007](https://docs.microsoft.com/previous-versions/system-center/configuration-manager-2007/bb680768(v=technet.10)) библиотеки документации Configuration Manager 2007.  

-   Дополнительные сведения о конфиденциальности для System Center 2012 Configuration Manager см. в статье [Обеспечение безопасности и конфиденциальности в System Center 2012 Configuration Manager](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/gg682033(v=technet.10)) библиотеки документации System Center 2012 Configuration Manager.  

-   Дополнительные сведения о конфиденциальности для Configuration Manager см. в статье [Обеспечение безопасности и конфиденциальности в Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

Можно переносить некоторые или все поддерживаемые данные из исходного сайта в конечную иерархию.  

Миграция не включена по умолчанию и требует выполнения нескольких этапов настройки. Сведения о миграции не передаются в корпорацию Майкрософт.  

Перед переносом данных из исходной иерархии оцените свои требования к конфиденциальности.  
