---
title: 使用自动化模型 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], automation model
ms.assetid: 0c7f7889-fbfb-4b19-804f-b742138baecd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2b9d7bd789a41f7a5e801552ca07f9f228921867
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704223"
---
# <a name="using-the-automation-model"></a>使用自动化模型
将 VSPackage 连接到自动化后，可以通过调用<xref:EnvDTE.DTEClass.GetObject%2A><xref:EnvDTE._DTE>对象上的方法来获取属性和方法，传递表示要检索的对象的字符串。

## <a name="obtaining-project-objects"></a>获取项目对象
 下面是两个代码示例，它们显示了自动化使用者如何获取项目自动化对象。 有关如何获取 DTE 对象的信息，请参阅[如何：获取对 DTE 和 DTE2 对象的引用](https://msdn.microsoft.com/Library/c92e3c8e-82e6-4a67-85da-e43c50ffd8e4)。

```vb
Sub DoAutomation()
    Dim MyProjects As Projects
    MyProjects = DTE.GetObject("AcmeProject")
End Sub
```

```cpp
void DoAutomation(void)
{
  CComQIPtr<Projects> pMyPkg; // Use an IDispatch-derived object type.
    pMyPkg = pDTE->GetObject("AcmeProjects");

   // The '=' performs a Query Interface.
   // Assumes pDTE is already available as a global.
   // Use pMyPkg to access your projects object's properties and methods.
}

```

 此时，您可以使用作为特定 VSPackage 一部分的标准项目对象向下移动层次结构模型。

 以下代码示例演示如何获取自定义项目类型的属性的自定义对象：

```vb
Dim MyPrj As Project
Dim MyPrjItem As ProjectItem
Dim objMyObject as MyExtendedObject

MyPrj = MyProjects.Item(1) 'use the Projects collection to get a project
objMyObject = MyPrj.Object 'You call .Object to get to special Project
                           'implementation
objMyObject.MySpecialMethodOrProperty
```

 以下代码列出了[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**"工具**"菜单上的环境 **"常规"** 选项中的所有属性的名称：

```vb
dim objDTE
dim objEnv
set objDTE = CreateObject("VisualStudio.DTE")
set objEnv = objDTE.Properties("Environment", "General")
for each obj in ObjEnv
MsgBox obj.Name
Next

```

## <a name="see-also"></a>请参阅
- <xref:EnvDTE.DTEClass.GetObject%2A>
