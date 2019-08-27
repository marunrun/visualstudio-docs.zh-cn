---
title: 类型集合编辑器对话框 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- TypeCollectionEditor.UI
ms.assetid: 63cdea6b-bca2-4c06-b8b4-c8faabd40726
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: be2e6bde6c25c1bb515ec3f017f14506c03a3a71
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697057"
---
# <a name="type-collection-editor-dialog-box"></a>“类型集合编辑器”对话框
**类型集合编辑器**使用对话框添加到已知的类型**发送**并**接收**活动。 此对话框还用于添加到泛型类型参数**InvokeMethod**活动。 当用于**发送**并**接收**活动添加已知的类型**类型集合编辑器**对话框要求添加的类型是唯一的。 如果添加了重复的类型，并通过单击提交更改**确定**，返回一条错误消息。 当用于**InvokeMethod**活动添加泛型类型参数**类型集合编辑器**对话框允许添加重复的类型。  
  
> [!NOTE]
> [!INCLUDE[crabout](../includes/crabout-md.md)] 已知类型的更多信息，请参见 [Data Contract Known Types](https://msdn.microsoft.com/library/1a0baea1-27b7-470d-9136-5bbad86c4337)将 CLR 类型映射到 XSD。  
  
 下表介绍的用户界面 (UI) 元素**类型的集合**对话框。  
  
|UI 元素|描述|  
|----------------|-----------------|  
|**类型列表**|已添加或移除的类型的列表。|  
  
## <a name="to-bring-up-the-type-collection-editor"></a>打开“类型集合编辑器”  
  
#### <a name="to-bring-up-the-type-collection-editor-for-the-send-and-receive-activities"></a>为 Send 和 Receive 活动打开“类型集合编辑器”  
  
1. 选择**发送**或**接收**设计视图中的活动。  
  
2. 按**F4**以打开**属性**窗口。  
  
3. 在中**属性**窗口中，单击旁边的省略号按钮**KnownTypes**属性。  
  
#### <a name="to-bring-up-the-type-collection-editor-for-the-invokemethod-activity"></a>为 InvokeMethod 活动打开“类型集合编辑器”  
  
1. 选择**InvokeMethod**设计视图中的活动。  
  
2. 按**F4**以打开**属性**窗口。  
  
3. 在中**属性**窗口中，单击旁边的省略号按钮**GenericTypeArguments**属性。