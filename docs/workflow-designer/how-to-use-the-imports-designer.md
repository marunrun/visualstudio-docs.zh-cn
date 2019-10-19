---
title: 工作流设计器-如何：使用导入设计器
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- System.Activities.Presentation.View.ImportDesigner.UI
ms.assetid: 61328ab6-9b66-4e12-8630-22e30ee8c9d1
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: df019157b6a8bd6199b01a093efb422792804b3e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650261"
---
# <a name="how-to-use-the-imports-designer"></a>如何：使用导入设计器

导入设计器允许您为将在表达式中使用的类型输入命名空间。 与 Visual Basic 和C#中的**导入**或**使用**关键字非常类似，在导入设计器中指定命名空间可让你只需在表达式中输入类型名称，而不是完全限定的版本类型名称。

导入设计器既响应 UI 中的更改，也响应保存工作流时进行的更改。 保存工作流后，会向导入设计器中自动添加命名空间。 这些要求包括：

- 变量和自变量声明中使用的所有类型的命名空间。

- 表达式中使用的所有类型的命名空间。

- 序列化工作流所需的其他任何命名空间（例如，放置在工作流中的自定义活动所使用的命名空间）。

  保存工作流时，您可能会注意到您已手动删除的某些命名空间可能会由于上述列表中描述的逻辑自动重新添加到导入设计器中。

## <a name="to-add-a-namespace-to-the-list-of-imported-namespaces"></a>向导入的命名空间列表中添加命名空间

1. 在 Visual Studio 或重新承载工作流应用程序中打开 WCF 工作流服务应用程序、工作流控制台应用程序或活动库项目。

2. 单击主画布底部的 "**导入**"。 此时将显示导入设计器。

3. 输入或从导入设计器顶部的下拉列表控件中选择一个命名空间。

     您键入时，会显示与键入的字符匹配的有效命名空间列表。

4. 按**enter**将命名空间添加到列表。

5. 如果要从列表中删除命名空间，请选择该命名空间，然后按键盘上的**Delete**键。 请注意如果命名空间因为任何原因（例如，项目不再引用包含命名空间的程序集）而无效，只能删除它。