---
title: 如何：确定库中的符号 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Call Browser tool, identifying symbols in the library
- Call Browser tool
ms.assetid: 8fb0de61-71e7-42d1-8b41-2ad915474384
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f154c63940189f1a6035246fb7f72ec27be677f5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68191868"
---
# <a name="how-to-identify-symbols-in-a-library"></a>如何：识别库中的符号
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

符号浏览工具显示符号的分层的视图。 符号代表命名空间、 对象、 类、 类成员和其他语言元素。  
  
 可以通过导航信息传递到符号库标识层次结构中的每个符号[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]对象管理器通过以下接口：  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfoNode>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes>。  
  
 在层次结构中的符号的位置将符号区分开来。 它允许导航到特定的符号，符号浏览工具。 符号的唯一的完全限定路径将确定位置。 在路径中的每个元素是一个节点。 路径的顶级节点开始和结束特定的符号。 例如，如果 M1 方法是 C1 类的成员和 C1 是 N1 命名空间中，M1 方法的完整路径是 N1。C1。M1。 此路径包含三个节点：N1 C1 和 M1。  
  
 导航信息允许[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]对象管理器查找、 选择并确保所选层次结构中的符号。 它允许一个浏览工具之间进行浏览。 使用时**对象浏览器**若要浏览中的符号[!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]项目中，您可以右键单击一种方法并启动**调用浏览器**工具调用关系图中显示该方法。  
  
 两种形式描述符号位置。 规范格式取决于该符号的完全限定路径。 它表示符号的层次结构中的唯一位置。 它不依赖于符号浏览工具。 若要获取规范格式的信息，[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]对象管理器调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumCanonicalNodes%2A>方法。 演示文稿形式描述了特定的符号浏览工具中的符号的位置。 符号的位置是相对于 hierarchicy 中其他符号的位置。 给定的符号可能有多个演示文稿路径，但只有一个规范的路径。 例如，如果 C1 类继承自 C2 类，这两个类都在 N1 命名空间**对象浏览器**显示以下层次结构树：  
  
```  
N1  
    C1  
        Bases and Interfaces  
            C2  
    C2  
        Bases and Interfaces  
. . . . . . . . . . .  
  
```  
  
 C2 类，在此示例中的规范路径是 N1 + C2。 C2 的演示文稿路径包括 C1 和"基类和接口"节点：N1 + C1 +"基和接口"+ C2。  
  
 若要获取表示窗体信息的对象管理器调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumPresentationNodes%2A>方法。  
  
## <a name="identifying-a-symbol-in-the-hierarchy"></a>标识在层次结构中的符号  
  
#### <a name="to-obtain-canonical-and-presentation-forms-information"></a>若要获取规范和演示文稿窗体的信息  
  
1. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumCanonicalNodes%2A> 方法。  
  
     对象管理器调用此方法来获取符号的规范路径中包含的节点列表。  
  
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
  
     对象管理器调用此方法来获取符号的演示文稿路径中包含的节点列表。  
  
## <a name="see-also"></a>请参阅  
 [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)   
 [如何：使用对象管理器注册库](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)   
 [如何：向对象管理器公开库提供的符号列表](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
