---
title: 如何：通过使用事务来保存数据
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- saving data, using transactions
- System.Transactions namespace
- transactions, saving data
- data [Visual Studio], saving
ms.assetid: 8b835e8f-34a3-413d-9bb5-ebaeb87f1198
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: cfb03944743609d20d14f6104e5fadd529a5cfa6
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72641309"
---
# <a name="how-to-save-data-by-using-a-transaction"></a>如何：通过使用事务来保存数据

使用 <xref:System.Transactions> 命名空间将数据保存在事务中。 使用 <xref:System.Transactions.TransactionScope> 对象参与自动管理的事务。

项目不是使用对*system.web*程序集的引用创建的，因此，您需要手动添加对使用事务的项目的引用。

实现事务的最简单方法是实例化 `using` 语句中的 <xref:System.Transactions.TransactionScope> 对象。 （有关详细信息，请参阅[using 语句](/dotnet/visual-basic/language-reference/statements/using-statement)和[using 语句](/dotnet/csharp/language-reference/keywords/using-statement)。）在 `using` 语句中运行的代码参与到事务中。

若要提交事务，请调用 <xref:System.Transactions.TransactionScope.Complete%2A> 方法，作为使用块中的最后一个语句。

若要回滚事务，请在调用 <xref:System.Transactions.TransactionScope.Complete%2A> 方法之前引发异常。

## <a name="to-add-a-reference-to-the-systemtransactionsdll"></a>添加对 System.object 的引用

1. 在 "**项目**" 菜单上，选择 "**添加引用**"。

2. 在 " **.net** " 选项卡（"SQL Server 项目**SQL Server** " 选项卡）上，选择 "**系统**"，然后选择 **"确定"** 。

     对*system.object*的引用将添加到项目。

## <a name="to-save-data-in-a-transaction"></a>在事务中保存数据

- 添加代码以在包含事务的 using 语句中保存数据。 下面的代码演示如何在 using 语句中创建并实例化 <xref:System.Transactions.TransactionScope> 对象：

     [!code-vb[VbRaddataSaving#11](../data-tools/codesnippet/VisualBasic/save-data-by-using-a-transaction_1.vb)]
     [!code-csharp[VbRaddataSaving#11](../data-tools/codesnippet/CSharp/save-data-by-using-a-transaction_1.cs)]

## <a name="see-also"></a>请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
- [演练：在事务中保存数据](../data-tools/save-data-in-a-transaction.md)