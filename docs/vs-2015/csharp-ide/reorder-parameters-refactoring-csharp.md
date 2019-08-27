---
title: 重新排列参数重构 (C#) |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: daf77a60256e59cabd176990f3642a2206a7f0d8
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444547"
---
# <a name="reorder-parameters-refactoring-c"></a>重新排列参数重构 (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`Reorder Parameters` 一个 Visual C# 重构操作，提供了方便地更改为方法、 索引器和委托参数的顺序。 `Reorder Parameters` 更改的声明，并在调用该成员的所有位置，重新排列参数，以反映新的顺序。  
  
 若要执行`Reorder Parameters`操作，将光标置于或旁边方法、 索引器或委托。 位置光标时，调用`Reorder Parameters`操作通过按键盘快捷方式，或通过单击快捷菜单中的命令。  
  
> [!NOTE]
> 不能对扩展方法中的第一个参数重新排序。  
  
### <a name="to-reorder-parameters"></a>若要重新排列参数  
  
1. 创建一个名为类库`ReorderParameters`，然后替换`Class1`用下面的示例代码。  
  
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
  
2. 将光标置于`MethodB`，在方法声明或方法调用。  
  
3. 上**重构**菜单上，单击**重新排列参数**。  
  
     **重新排列参数**对话框随即出现。  
  
4. 在中**重新排列参数**对话框中，选择`int i`中**参数**列表，，然后单击向下按钮。  
  
     或者，可以拖动`int i`后`bool b`中**参数**列表。  
  
5. 在中**重新排列参数**对话框中，单击**确定**。  
  
     如果**预览引用更改**中选择选项**重新排列参数**对话框中，**预览更改-重新排列参数**对话框将出现。 它提供的参数列表中的更改的预览`MethodB`在签名和方法调用。  
  
    1. 如果**预览更改-重新排列参数**出现对话框，请单击**应用**。  
  
         在此示例中，该方法声明和所有方法调用站点的`MethodB`进行更新。  
  
## <a name="remarks"></a>备注  
 可以对从方法声明或方法调用的参数重新排序。 将光标上或旁边方法或委托声明但未在正文中。  
  
## <a name="see-also"></a>请参阅  
 [重构 (C#)](../csharp-ide/refactoring-csharp.md)