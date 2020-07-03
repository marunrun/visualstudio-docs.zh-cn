---
title: 如何：在库中标识符号 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Call Browser tool, identifying symbols in the library
- Call Browser tool
ms.assetid: 8fb0de61-71e7-42d1-8b41-2ad915474384
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fd091f003909110c696c2e42ad80d6c6ea4859d2
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905407"
---
# <a name="how-to-identify-symbols-in-a-library"></a>如何：标识库中的符号
符号浏览工具显示符号的层次结构视图。 符号表示命名空间、对象、类、类成员和其他语言元素。

 层次结构中的每个符号均可由符号库通过 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 以下接口传递给对象管理器的导航信息进行标识：

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfoNode>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes>.

 该符号在层次结构中的位置区分符号。 它允许符号浏览工具导航到特定符号。 符号的唯一的完全限定路径确定位置。 路径中的每个元素都是一个节点。 路径从顶级节点开始，以特定符号结尾。 例如，如果 M1 方法是 C1 类的成员，并且 C1 在 N1 命名空间中，则 M1 方法的完整路径为 N1。低耗.限. 此路径包含三个节点： N1、C1 和 M1。

 导航信息允许 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 对象管理器查找、选择和保留选择层次结构中的符号。 它允许从一个浏览工具导航到另一个。 使用**对象浏览器**浏览项目中的符号时 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] ，可以右键单击方法并启动**调用浏览器**工具，以便在调用关系图中显示该方法。

 两个窗体描述符号位置。 规范形式基于符号的完全限定路径。 它表示该符号在层次结构中的唯一位置。 它独立于符号浏览工具。 为了获得规范形式的信息， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 对象管理器调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumCanonicalNodes%2A> 方法。 演示窗体介绍符号在特定的符号浏览工具内的位置。 符号的位置相对于层次结构中其他符号的位置。 给定的符号可以有多个表示路径，但只能有一个规范路径。 例如，如果 C1 类继承自 C2 类，并且这两个类都位于 N1 命名空间中，则**对象浏览器**显示以下层次结构树：

```
N1
    C1
        Bases and Interfaces
            C2
    C2
        Bases and Interfaces
. . . . . . . . . . .

```

 C2 类的规范路径在此示例中为 N1 + C2。 C2 的演示路径包含 C1 和 "基和接口" 节点： N1 + C1 + "基和接口" + C2。

 若要获取演示窗体信息，对象管理器将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumPresentationNodes%2A> 方法。

## <a name="to-obtain-canonical-and-presentation-forms-information"></a>获取规范和展示形式信息

1. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumCanonicalNodes%2A> 方法。

     对象管理器调用此方法以获取该符号的规范路径中包含的节点的列表。

    ```vb
    Public Function EnumCanonicalNodes(ByRef ppEnum As Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes) As Integer
        Dim EnumNavInfoNodes As CallBrowserEnumNavInfoNodes = _New CallBrowserEnumNavInfoNodes(m_strMethod)
        ppEnum = CType(EnumNavInfoNodes, IVsEnumNavInfoNodes)
        Return 0
    End Function
    ```

    ```csharp
    public int EnumCanonicalNodes(out Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes ppEnum)
    {
        CallBrowserEnumNavInfoNodes EnumNavInfoNodes =
            new CallBrowserEnumNavInfoNodes(m_strMethod);
        ppEnum = (IVsEnumNavInfoNodes)(EnumNavInfoNodes);
        return 0;
    }

    ```

2. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumPresentationNodes%2A> 方法。

     对象管理器调用此方法以获取符号的表示路径中包含的节点的列表。

## <a name="see-also"></a>另请参阅
- [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [如何：向对象管理器注册库](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [如何：将库提供的符号列表公开给对象管理器](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
