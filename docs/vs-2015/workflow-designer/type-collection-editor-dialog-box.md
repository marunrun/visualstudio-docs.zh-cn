---
title: "\"类型集合编辑器\" 对话框 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- TypeCollectionEditor.UI
ms.assetid: 63cdea6b-bca2-4c06-b8b4-c8faabd40726
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: dae99166b8b811df75f2e2777d176e6778b60c7d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670147"
---
# <a name="type-collection-editor-dialog-box"></a>“类型集合编辑器”对话框
"**类型集合编辑器**" 对话框用于向**发送**和**接收**活动添加已知类型。 此对话框还用于将泛型类型参数添加到**InvokeMethod**活动。 当用于**发送**和**接收**活动以添加已知类型时，"**类型集合编辑器**" 对话框要求类型添加项是唯一的。 如果添加了重复类型并且通过单击 **"确定**" 来提交更改，则返回一条错误消息。 当用于**InvokeMethod**活动以添加泛型类型参数时，"**类型集合编辑器**" 对话框允许添加重复的类型。

> [!NOTE]
> [!INCLUDE[crabout](../includes/crabout-md.md)] 已知类型的更多信息，请参见 [Data Contract Known Types](https://msdn.microsoft.com/library/1a0baea1-27b7-470d-9136-5bbad86c4337)将 CLR 类型映射到 XSD。

 下表描述了 "**类型集合**" 对话框的用户界面（UI）元素。

|UI 元素|描述|
|----------------|-----------------|
|**类型列表**|已添加或移除的类型的列表。|

## <a name="to-bring-up-the-type-collection-editor"></a>打开“类型集合编辑器”

#### <a name="to-bring-up-the-type-collection-editor-for-the-send-and-receive-activities"></a>为 Send 和 Receive 活动打开“类型集合编辑器”

1. 在 "设计" 视图中选择 "**发送**" 或 "**接收**" 活动。

2. 按**F4**以显示 "**属性**" 窗口。

3. 在 "**属性**" 窗口中，单击 " **KnownTypes** " 属性旁边的省略号按钮。

#### <a name="to-bring-up-the-type-collection-editor-for-the-invokemethod-activity"></a>为 InvokeMethod 活动打开“类型集合编辑器”

1. 在 "设计" 视图中选择 " **InvokeMethod** " 活动。

2. 按**F4**以显示 "**属性**" 窗口。

3. 在 "**属性**" 窗口中，单击 " **GenericTypeArguments** " 属性旁边的省略号按钮。