---
title: 提取接口重构（C#） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.csharp.refactoring.extractinterface
dev_langs:
- CSharp
helpviewer_keywords:
- refactoring [C#], Extract Interface
- Extract Interface refactoring operation [C#]
ms.assetid: 7d0aa225-3b33-4331-9652-5a67cac6f3d0
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fdcf281e1ace40d1d7cdac0be302810ea173581b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667552"
---
# <a name="extract-interface-refactoring-c"></a>提取接口重构 (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

"提取接口" 是一种重构操作，它提供了一种简单的方法来创建新的接口，该接口具有源自现有类、结构或接口的成员。

 当多个客户端使用类、结构或接口中的成员的相同子集时，或多个类、结构或接口具有共同的成员子集时，体现接口中成员的子集就会很有用。 有关使用接口的详细信息，请参阅[接口](https://msdn.microsoft.com/library/2feda177-ce11-432d-81b4-d50f5f35fd37)。

 提取接口在新文件中生成接口，并将光标置于新文件的开头。 您可以使用 "**提取接口**" 对话框指定要提取到新接口中的成员、新接口的名称以及生成的文件的名称。

### <a name="to-use-extract-interface"></a>使用提取接口

1. 创建一个名为 `ExtractInterface` 的控制台应用程序，然后将 `Program` 替换为以下代码

    ```csharp
    // Invoke Extract Interface on ProtoA.
    // Note:  the extracted interface will be created in a new file.
    class ProtoA
    {
        public void MethodB(string s) { }
    }
    ```

2. 将光标置于 `MethodB` 中，然后单击 "**重构**" 菜单上的 "**提取接口**"。

     "**提取接口**" 对话框随即出现。

     还可以键入键盘快捷方式 CTRL + R，然后显示 "**提取接口**" 对话框。

     您还可以右键单击鼠标，指向 "**重构**"，然后单击 "**提取接口**" 以显示 "**提取接口**" 对话框。

3. 单击 "**全选**"。

4. 单击“确定”。

     你将看到新文件 IProtoA.cs 和以下代码：

    ```csharp
    using System;
    namespace TopThreeRefactorings
    {
        interface IProtoA
        {
            void MethodB(string s);
        }
    }
    ```

## <a name="remarks"></a>备注
 只有当光标位于包含你要提取的成员的类、结构或接口中时，才可以访问此功能。 当光标位于此位置时，调用 "提取接口" 重构操作。

 对类或结构调用 "提取接口" 时，将修改 "基和接口" 列表以包含新的接口名称。 调用接口上的 "提取接口" 时，不会修改 "基本" 和 "接口" 列表。

## <a name="see-also"></a>请参阅
 [重构 (C#)](../csharp-ide/refactoring-csharp.md)