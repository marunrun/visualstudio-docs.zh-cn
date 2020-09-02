---
title: 重命名项目层次结构节点 (c + +) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- HierUtil7 sample [Visual Studio SDK], renaming project nodes
- project nodes, renaming in HierUtil7 sample
ms.assetid: cea5968e-e9f8-41a5-b068-622df542247c
caps.latest.revision: 12
manager: jillfra
ms.openlocfilehash: c7ad43fe1fd0e22cd94194d3079761de812b6ced
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65686587"
---
# <a name="renaming-project-hierarchy-nodes-c"></a>重命名项目层次结构节点 (C++)
您可以使用非托管 c + + 的 HierUtil7 项目框架重命名项目文件夹层次结构节点。 有关详细信息，请参阅 [HierUtil7 示例](https://msdn.microsoft.com/29c15184-a70c-4813-86c2-fb1d47442d11)。  
  
## <a name="expanding-the-hierarchy-node"></a>展开层次结构节点  
  
#### <a name="to-expand-the-hierarchy-node-and-rename-the-folder"></a>展开层次结构节点并重命名文件夹  
  
1. 使用以下方法选择 "层次结构" 节点：  
  
    ```  
    IfFailGo(pNode->ExtExpand(EXPF_SelectItem, GUID_MacroExplorer));  
    ```  
  
     `pNode` 是对应于文件夹的层次结构容器，并且 `EXPF_SelectItem` 来自 <xref:Microsoft.VisualStudio.Shell.Interop.EXPANDFLAGS> 枚举。 `GUID_MacroExplorer`是在 Vsshell 中定义的 GUID 常量，是的 `rguidPersistenceSlot` 函数签名中的一个示例 `ExtExpand` ，在 Hu_node 中定义。  
  
    ```  
    HRESULT ExtExpand(EXPANDFLAGS expandflags, REFGUID rguidPersistenceSlot = GUID_SolutionExplorer) const;  
    ```  
  
     可以在 \<installation root> \Program Files\VSIP 8.0 \ EnvSDK\common\hierutil7 文件夹中找到 Hu_node .h 文件：  
  
2. 重命名文件夹，方法是使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.PostExecCommand%2A>  
  
    ```  
    IfFailGo(srpVsUIShell->PostExecCommand(&guidVSStd97, cmdidRename, 0, NULL));  
    ```  
  
     `srpVsUIShell` 是一个 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> 指针： `<IVsUIShell>``srpVsUIShell` 。 `guiVSStd97` 命令所属的命令组的唯一标识符 `cmdidRename` ，在 Vsshlids 中定义。  
  
## <a name="see-also"></a>另请参阅  
 [创建项目类型](../extensibility/internals/creating-project-types.md)   
 [VSSDK 示例](../misc/vssdk-samples.md)