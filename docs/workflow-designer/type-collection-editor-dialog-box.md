---
title: "\"工作流设计器类型集合编辑器\" 对话框"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- TypeCollectionEditor.UI
ms.assetid: 63cdea6b-bca2-4c06-b8b4-c8faabd40726
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 023d049c5256abe6212dd65df78cd67151be94a2
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593052"
---
# <a name="type-collection-editor-dialog-box"></a>“类型集合编辑器”对话框

"**类型集合编辑器**" 对话框用于向**发送**和**接收**活动添加已知类型。 此对话框还用于将泛型类型参数添加到**InvokeMethod**活动。 当用于**发送**和**接收**活动以添加已知类型时，"**类型集合编辑器**" 对话框要求类型添加项是唯一的。 如果添加了重复类型并且通过单击 **"确定**" 来提交更改，则返回一条错误消息。 当用于**InvokeMethod**活动以添加泛型类型参数时，"**类型集合编辑器**" 对话框允许添加重复的类型。

有关详细信息，请参阅[数据协定已知类型](/dotnet/framework/wcf/feature-details/data-contract-known-types)。

下表描述了 "**类型集合**" 对话框的用户界面（UI）元素。

|UI 元素|描述|
|-|-----------------|
|**类型列表**|已添加或移除的类型的列表。|

## <a name="to-bring-up-the-type-collection-editor-for-the-send-and-receive-activities"></a>为 Send 和 Receive 活动打开“类型集合编辑器”

1. 在 "设计" 视图中选择 "**发送**" 或 "**接收**" 活动。

2. 按**F4**以显示 "**属性**" 窗口。

3. 在 "**属性**" 窗口中，单击 " **KnownTypes** " 属性旁边的省略号按钮。

## <a name="to-bring-up-the-type-collection-editor-for-the-invokemethod-activity"></a>为 InvokeMethod 活动打开“类型集合编辑器”

1. 在 "设计" 视图中选择 " **InvokeMethod** " 活动。

2. 按**F4**以显示 "**属性**" 窗口。

3. 在 "**属性**" 窗口中，单击 " **GenericTypeArguments** " 属性旁边的省略号按钮。
