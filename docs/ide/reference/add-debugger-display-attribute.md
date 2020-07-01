---
title: 添加 DebuggerDisplay 属性
ms.date: 05/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 611df048d4ce569c10ae933be9053acf1174c06f
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290778"
---
# <a name="add-debuggerdisplay-attribute"></a>添加 DebuggerDisplay 属性

此代码生成适用于：

- C#

**功能：** [DebuggerDisplay 属性](https://docs.microsoft.com/visualstudio/debugger/using-the-debuggerdisplay-attribute)控制对象、属性或字段在调试器变量窗口中的显示方式。

**使用时机：** 你希望在代码中以编程方式在调试器中[固定属性](https://docs.microsoft.com/visualstudio/debugger/view-data-values-in-data-tips-in-the-code-editor#pin-properties-in-datatips)。

操作原因：固定属性使你能够，通过将对象属性向上浮升到调试器中对象属性列表的顶部，来按属性快速检查对象。 

## <a name="how-to"></a>操作说明

1. 将光标置于类型、委托、属性或字段上。 

2. 按“Ctrl”+ **。** 触发“快速操作和重构”菜单，然后选择“添加 DebuggerDisplay 属性”。

    ![生成比较运算符](media/add-debugger-display-attribute.png)

3. DebuggerDisplay 属性将与返回默认 ToString() 的自动方法一起添加。 

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)
