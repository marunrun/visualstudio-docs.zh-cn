---
title: 删除参数重构（C#） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.csharp.refactoring.remove
dev_langs:
- CSharp
helpviewer_keywords:
- parameters [C#], removing
- refactoring [C#], Remove Parameters
- Remove Parameters refactoring [C#]
ms.assetid: f4fc3265-0ef8-4398-a691-c338178697a6
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 40c373c3575f007952143e29c8dfc2cfac3d080f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667492"
---
# <a name="remove-parameters-refactoring-c"></a>移除参数重构 (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`Remove Parameters` 是一种重构操作，它提供了一种简单的方法来从方法、索引器或委托中移除参数。 删除参数会更改声明;在调用该成员的任何位置，都将删除该参数以反映新声明。

 您可以通过先将游标定位在方法、索引器或委托上，来执行删除参数操作。 当光标位于某个位置时，若要调用删除 `Parameters` 操作，请单击 "**重构**" 菜单，按键盘快捷方式，或从快捷菜单中选择该命令。

> [!NOTE]
> 不能删除扩展方法中的第一个参数。

### <a name="to-remove-parameters"></a>删除参数

1. 创建一个名为 `RemoveParameters` 的控制台应用程序，然后将 `Program` 替换为以下代码。

    ```csharp
    class A
    {
        // Invoke on 'A'.
        public A(string s, int i) { }
    }

    class B
    {
        void C()
        {
            // Invoke on 'A'.
            A a = new A("a", 2);
        }
    }
    ```

2. 将光标置于方法声明或方法调用中 `A`。

3. 从 "**重构**" 菜单中，选择 "**删除参数**" 以显示 "**删除参数**" 对话框。

     还可以键入键盘快捷方式 CTRL + R，V 以显示 "**删除参数**" 对话框。

     您还可以右键单击光标，指向 "**重构**"，然后单击 "**删除参数**" 以显示 "**删除参数**" 对话框。

4. 使用 "**参数**" 字段，将光标置于 `int i` 上，然后单击 "**删除**"。

5. 单击“确定”。

6. 在 "**预览更改-删除参数**" 对话框中，单击 "**应用**"。

## <a name="remarks"></a>备注
 可以从方法声明或方法调用中移除参数。 将光标置于方法声明或委托名称中，并调用 Remove 参数。

> [!CAUTION]
> 通过 "删除参数"，您可以删除在成员的主体中引用的参数，但不会删除方法主体中对该参数的引用。 这可能会将生成错误引入你的代码。 但是，您可以使用 "**预览更改**" 对话框在执行重构操作之前查看您的代码。

 如果要移除的参数在调用方法的过程中被修改，则删除该参数也将删除修改。 例如，如果方法调用从

```csharp
MyMethod(param1++, param2);
```

 实例部署到 Windows Azure 虚拟机 (VM) 中的

```csharp
MyMethod(param2);
```

 通过重构操作，不会增加 `param1`。

## <a name="see-also"></a>请参阅
 [重构 (C#)](../csharp-ide/refactoring-csharp.md)