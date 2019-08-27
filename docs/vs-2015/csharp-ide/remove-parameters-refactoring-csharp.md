---
title: 移除参数重构 (C#) |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 40a884fe2ae6aaf73256d8edbcbd083a193b0342
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444617"
---
# <a name="remove-parameters-refactoring-c"></a>移除参数重构 (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`Remove Parameters` 是提供了方便地从方法、 索引器或委托中移除参数重构操作。 删除参数更改声明;在调用该成员的所有位置，该参数被删除，以反映新的声明。  
  
 通过第一个定位游标的方法、 索引器或委托执行删除参数操作。 当光标处于位置，以便调用 Remove`Parameters`操作中，单击**重构**菜单中，按键盘快捷方式，或从快捷菜单中选择该命令。  
  
> [!NOTE]
> 无法为扩展方法中删除第一个参数。  
  
### <a name="to-remove-parameters"></a>若要删除参数  
  
1. 创建名为一个控制台应用程序`RemoveParameters`，然后替换`Program`用下面的代码。  
  
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
  
2. 方法将光标置于`A`，在方法声明或方法调用。  
  
3. 从**重构**菜单中，选择**移除参数**以显示**移除参数**对话框。  
  
     此外可以键入键盘快捷键 CTRL + R，V 显示**移除参数**对话框。  
  
     此外可以右键单击光标，指向**重构**，然后单击**移除参数**以显示**移除参数**对话框。  
  
4. 使用**参数**字段中，将光标置于`int i`，然后单击**删除**。  
  
5. 单击 **“确定”**。  
  
6. 在中**预览更改-删除参数**对话框中，单击**应用**。  
  
## <a name="remarks"></a>备注  
 您可以从方法声明或方法调用中删除参数。 将光标放置在方法声明或委托名称并调用删除参数。  
  
> [!CAUTION]
> 删除参数允许您删除的成员，但它在正文中引用的参数不会在方法体中删除对该参数的引用。 这可以引入你的代码生成错误。 但是，可以使用**预览更改**对话框在执行重构操作之前检查你的代码。  
  
 如果对方法调用期间修改正在移除的参数，则删除该参数还会删除修改。 例如，如果一个方法调用是从更改  
  
```csharp  
MyMethod(param1++, param2);  
```  
  
 更改为  
  
```csharp  
MyMethod(param2);  
```  
  
 通过此重构操作，`param1`将不会增加。  
  
## <a name="see-also"></a>请参阅  
 [重构 (C#)](../csharp-ide/refactoring-csharp.md)