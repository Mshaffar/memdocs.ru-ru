---
title: Средство переноса библиотеки содержимого
titleSuffix: Configuration Manager
description: Используйте средство переноса библиотеки содержимого для переноса содержимого с одного диска на другой в точке распространения Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d07bd0a-7012-47f7-8bc5-509a402915b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7401c80c89b1f1674bdae0b20482d7164837b724
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703442"
---
# <a name="content-library-transfer-tool"></a>Средство переноса библиотеки содержимого

*Область применения: Configuration Manager (Current Branch)*

Средство переноса библиотеки содержимого является одним из [средств Configuration Manager](tools.md). Оно позволяет переносить содержимое с одного диска на другой. Средство предназначено для выполнения в системах сайта точки распространения. Оно поддерживает точки распространения, размещаемые рядом с сайтом или удаленными системами сайта.  

Это средство полезно в случае полного заполнения диска, на котором размещается библиотека содержимого. Сначала добавьте или определите другой жесткий диск с достаточным местом для размещения библиотеки содержимого. Затем с помощью **ContentLibraryTransfer.exe** перенесите содержимое со старого заполненного жесткого диска на новый пустой диск.
 
После завершения переноса содержимое будет доступно клиентским компьютерам в новом расположении.



## <a name="usage"></a>Использование 

Запустите **ContentLibraryTransfer.exe** от имени пользователя с правами администратора на точке распространения. 

#### <a name="syntax"></a>Синтаксис 
`ContentLibraryTransfer.exe –SourceDrive <drive letter of source drive> –TargetDrive <drive letter of destination drive>`

#### <a name="example"></a>Пример
`ContentLibraryTransfer –SourceDrive E –TargetDrive G`



## <a name="limitations"></a>Ограничения

- Средство следует запускать локально в точке распространения. Его нельзя запускать с удаленного компьютера.  

- Средство можно использовать только при отсутствии активного доступа клиентов к точке распространения. Если средство запускается во время обращения клиентов к содержимому, в библиотеке содержимого на целевом диске могут находиться неполные данные. Передача данных может завершиться полным сбоем, что приведет к невозможности использования библиотеки содержимого.  

- Не распространяйте содержимое в точку распространения при запуске средства. Если средство запускается во время записи содержимого в точку распространения, в библиотеке содержимого на целевом диске могут находиться неполные данные. Передача данных может завершиться полным сбоем, что приведет к невозможности использования библиотеки содержимого.



## <a name="see-also"></a>См. также

- [Основные принципы управления содержимым](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Библиотека содержимого](../plan-design/hierarchy/the-content-library.md)