---
title: 重新排列参数重构C#（） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.csharp.refactoring.reorder
dev_langs:
- CSharp
helpviewer_keywords:
- refactoring [C#], Reorder Parameters
- Reorder Parameters refactoring [C#]
ms.assetid: 4dabf21a-a9f0-41e9-b11b-55760cf2bd90
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e39564fb108b63859620e2c4a650608cdf1e7e82
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72673144"
---
# <a name="reorder-parameters-refactoring-c"></a>重新排列参数重构 (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`Reorder Parameters` 是一种C#可视化重构操作，它提供了一种简单的方法来更改方法、索引器和委托的参数顺序。 `Reorder Parameters` 更改声明，并在调用成员的任何位置更改参数，则会重新排列这些参数以反映新的顺序。

 若要执行 `Reorder Parameters` 操作，请将光标置于方法、索引器或委托的上方或旁边。 当光标位于位置时，通过按键盘快捷方式或单击快捷菜单中的命令来调用 `Reorder Parameters` 操作。

> [!NOTE]
> 不能对扩展方法中的第一个参数重新排序。

### <a name="to-reorder-parameters"></a>重新排列参数

1. 创建一个名为 `ReorderParameters` 的类库，然后将 `Class1` 替换为下面的示例代码。

    ```csharp
    class ProtoClassA
    {
        // Invoke on 'MethodB'.
        public void MethodB(int i, bool b) { }
    }

    class ProtoClassC
    {
        void D()
        {
            ProtoClassA MyClassA = new ProtoClassA();

            // Invoke on 'MethodB'.
            MyClassA.MethodB(0, false);
        }
    }
    ```

2. 将光标置于方法声明或方法调用中 `MethodB` 上。

3. 在 "**重构**" 菜单上，单击 "**重新排列参数**"。

     此时将显示 "**重新排列参数**" 对话框。

4. 在 "**重新排列参数**" 对话框中，在 "**参数**" 列表中选择 "`int i`"，然后单击 "下一按钮"。

     或者，您可以将 `int i` 拖动到 "**参数**" 列表中 `bool b` 之后。

5. 在 "**重新排列参数**" 对话框中，单击 **"确定"** 。

     如果在 "**重新排列参数**" 对话框中选择了 "**预览引用更改**" 选项，则会出现 "**预览更改-重新排序参数**" 对话框。 它为签名和方法调用中的 `MethodB` 提供参数列表中更改的预览。

    1. 如果显示 "**预览更改-重新排列参数**" 对话框，则单击 "**应用**"。

         在此示例中，将更新 `MethodB` 的方法声明和所有方法调用站点。

## <a name="remarks"></a>备注
 您可以重新排列方法声明或方法调用中的参数。 将光标置于方法或委托声明的上方或旁边，而不是放置在正文中。

## <a name="see-also"></a>请参阅
 [重构 (C#)](../csharp-ide/refactoring-csharp.md)