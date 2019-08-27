---
title: 提取接口重构 (C#) |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: deb2e446ff051b52e9c34d28abfa99436c064ad6
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65680906"
---
# <a name="extract-interface-refactoring-c"></a>提取接口重构 (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

提取接口是重构操作，提供了与来自现有类、 结构或接口的成员创建一个新接口的简单方法。  
  
 当多个客户端使用的类、 结构或接口中的成员的同一子集或多个类、 结构或接口的共同点成员的子集时，它可用于体现在接口中的成员的子集。 有关使用接口的详细信息，请参阅[接口](https://msdn.microsoft.com/library/2feda177-ce11-432d-81b4-d50f5f35fd37)。  
  
 提取接口的新文件中生成一个接口，并将光标置于新文件的开头。 可以指定要提取到新的界面、 新接口的名称和生成的文件使用的名称的成员**提取接口**对话框。  
  
### <a name="to-use-extract-interface"></a>若要使用提取接口  
  
1. 创建名为一个控制台应用程序`ExtractInterface`，然后替换`Program`用下面的代码  
  
    ```csharp  
    // Invoke Extract Interface on ProtoA.  
    // Note:  the extracted interface will be created in a new file.  
    class ProtoA  
    {  
        public void MethodB(string s) { }  
    }  
    ```  
  
2. 将光标放在`MethodB`，然后单击**提取接口**上**重构**菜单。  
  
     **提取接口**对话框随即出现。  
  
     此外可以键入键盘快捷方式 CTRL + R，我以显示**提取接口**对话框。  
  
     此外可以右键单击鼠标，指向**重构**，然后单击**提取接口**以显示**提取接口**对话框。  
  
3. 单击**全**。  
  
4. 单击 **“确定”**。  
  
     可看到新文件： IProtoA.cs 和以下代码：  
  
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
 当光标定位在类、 结构或接口包含你想要提取的成员时，才可访问此功能。 此位置光标时，调用提取接口重构操作。  
  
 在调用提取接口的类或结构时，将修改基类和接口列表以包括新的接口名称。 当您调用接口上的提取接口时，不是修改基类和接口列表。  
  
## <a name="see-also"></a>请参阅  
 [重构 (C#)](../csharp-ide/refactoring-csharp.md)