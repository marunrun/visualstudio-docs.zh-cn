---
title: 应用程序设置文件中的连接属性是缺失或不正确 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 77724510-ff59-4d43-b933-a0434e1ac597
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 8538b5ec8f78ac9b648e865f4c6f6c0ee07fb0b9
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697690"
---
# <a name="the-connection-property-in-the-application-settings-file-is-missing-or-incorrect"></a>应用程序设置文件中的连接属性缺失或不正确
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

应用程序设置文件中缺少连接属性或连接属性不正确。 已使用 .dbml 文件中的连接字符串来替代它。  
  
 .dbml 文件包含对应用程序设置文件中某连接字符串的引用，但无法找到该连接字符串。 此消息是通知性消息；单击“确定”后将创建该连接字符串设置。  
  
### <a name="to-respond-to-this-message"></a>响应此消息  
  
- 单击 **“确定”**。 .dbml 文件中包含的连接信息将添加到应用程序设置中。  
  
## <a name="see-also"></a>请参阅  
 [LINQ to SQL 工具在 Visual Studio 中](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [演练：创建 LINQ to SQL 类 （O-R 设计器）](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)   
 [NIB：如何：添加或删除应用程序设置](https://msdn.microsoft.com/a233965c-126d-46ab-add4-efb758f576f4)   
 [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)
