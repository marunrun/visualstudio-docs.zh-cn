---
title: 应用程序设置文件中的连接属性缺失或不正确
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 77724510-ff59-4d43-b933-a0434e1ac597
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: becbc5032c05af1edf5361a54fd0a80b4a0ff412
ms.sourcegitcommit: 50f0c3f2763a05de8482b3579026d9c76c0e226c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65458308"
---
# <a name="the-connection-property-in-the-application-settings-file-is-missing-or-incorrect"></a>应用程序设置文件中的连接属性缺失或不正确

应用程序设置文件中缺少连接属性或连接属性不正确。 已使用 .dbml 文件中的连接字符串来替代它。

.dbml 文件包含对应用程序设置文件中某连接字符串的引用，但无法找到该连接字符串。 此消息是通知性消息；单击“确定”后将创建该连接字符串设置。

若要对此消息做出响应，请选择**确定**。 .dbml 文件中包含的连接信息将添加到应用程序设置中。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)