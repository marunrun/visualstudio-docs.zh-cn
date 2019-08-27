---
title: 如何：使用事务保存数据
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: bf5864d25e78b6050da5c13097503b2998dda44a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62566311"
---
# <a name="how-to-save-data-by-using-a-transaction"></a>如何：使用事务保存数据

您将数据保存在事务中的使用<xref:System.Transactions>命名空间。 使用<xref:System.Transactions.TransactionScope>对象能够参与为您自动管理的事务。

项目不会创建引用*System.Transactions*程序集，因此您需要手动添加对项目使用事务的引用。

若要实现事务的最简单方法是实例化<xref:System.Transactions.TransactionScope>对象中`using`语句。 (有关详细信息，请参阅[Using 语句](/dotnet/visual-basic/language-reference/statements/using-statement)，并[Using 语句](/dotnet/csharp/language-reference/keywords/using-statement)。)在中运行的代码`using`语句参与事务。

若要提交事务，调用<xref:System.Transactions.TransactionScope.Complete%2A>方法中使用的最后一个语句块。

若要回滚事务，会引发异常之前调用<xref:System.Transactions.TransactionScope.Complete%2A>方法。

## <a name="to-add-a-reference-to-the-systemtransactionsdll"></a>若要添加对 System.Transactions.dll 的引用

1. 上**项目**菜单中，选择**添加引用**。

2. 上 **.NET**选项卡 (**SQL Server** SQL Server 项目的选项卡)，选择**System.Transactions**，然后选择**确定**。

     对引用*System.Transactions.dll*添加到项目。

## <a name="to-save-data-in-a-transaction"></a>若要将数据保存在事务中

- 添加代码以保存中使用的数据包含的事务的语句。 下面的代码演示如何创建并实例化<xref:System.Transactions.TransactionScope>对象中的 using 语句：

     [!code-vb[VbRaddataSaving#11](../data-tools/codesnippet/VisualBasic/save-data-by-using-a-transaction_1.vb)]
     [!code-csharp[VbRaddataSaving#11](../data-tools/codesnippet/CSharp/save-data-by-using-a-transaction_1.cs)]

## <a name="see-also"></a>请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
- [演练：在事务中保存数据](../data-tools/save-data-in-a-transaction.md)