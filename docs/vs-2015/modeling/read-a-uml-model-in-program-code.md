---
title: 读取程序代码中的 UML 模型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API, reading models
ms.assetid: 0f63105e-6079-498a-94f1-318c0f5f9621
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 37539ee6c031d88b9db279cc61214ac5e3077e76
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387670"
---
# <a name="read-a-uml-model-in-program-code"></a>在程序代码中读取 UML 模型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以使用 UML API 加载 UML 模型及其关系图。  
  
## <a name="Reading"></a> 读取程序代码中的模型  
 若要访问模型的内容而不将其显示在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 窗口中，请使用 `ModelingProject.LoadReadOnly()`。  
  
 例如：  
  
```  
using Microsoft.VisualStudio.Uml.Classes;   
               // for IElement  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility;   
               // for ModelingProject  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;  
               // for IModelStore  
...   
string projectPath = @"C:\MyProjectFolder\MyProject.modelproj";  
using (IModelingProjectReader projectReader =  
           ModelingProject.LoadReadOnly(projectPath))  
{  
   IModelStore store = projectReader.Store;  
   foreach (IClass umlClass in store.AllInstances<IClass>())  
   {   
       ...  
   }  
}  
```  
  
 如果你想要读取关系图中的形状，则必须读取该项目，然后再读取该关系图。  
  
 例如：  
  
```  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;   
                             // for IDiagram  
...  
foreach (string diagramFile in projectReader. DiagramFileNames)  
{   
  IDiagram diagram = projectReader.LoadDiagram(diagramFile);  
  foreach (IShape<IElement> shape   
         in diagram.GetChildShapes<IElement>())  
  { ... }  
}  
```  
  
## <a name="alternative-methods"></a>替代方法  
 对于许多应用程序， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Modelbus 允许你引用模型和这些元素具有更大的可靠性和灵活性比本主题中所述的方法。 它提供了一种在任意元素之间建立链接的标准方法，不论模型是否相同。 有关详细信息，请参阅[与其他模型和工具集成 UML 模型](../modeling/integrate-uml-models-with-other-models-and-tools.md)。  
  
 你还可以使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] API，在用户界面打开模型和关系图。 有关详细信息，请参阅[使用 Visual Studio API 打开 UML 模型](../modeling/open-a-uml-model-by-using-the-visual-studio-api.md)。  
  
## <a name="Standalone"></a> 独立应用程序  
 上一节中的示例将用于 Visual Studio 扩展。 可以在独立的应用程序中读取模型，但你必须向 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目添加一些引用。  
  
> [!NOTE]
> 有关在独立的应用程序中读取模型的方法的详细信息可能会在该产品的将来版本中进行更改。 当前版本中可以访问的一些功能可能在未来版本不会提供。  
  
#### <a name="to-add-references-to-read-a-model-in-a-stand-alone-application"></a>添加引用以读取独立的应用程序中的模型。  
  
1. 在解决方案资源管理器，右键单击的项目要构建应用程序，然后依次**属性**。 在属性编辑器中，在**应用程序**选项卡上，设置**目标框架**到.NET Framework 所需版本。  
  
2. 添加你访问 UML 模型所需的 [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)] 引用，通常为：  
  
   - Microsoft.VisualStudio.Uml.Interfaces.dll  
  
   - Microsoft.VisualStudio.ArchitectureTools.Extensibility.dll  
  
3. 除了前面的部分中列出的参考资料，添加以下项目引用从 **\Program Files\Microsoft Visual Studio [version] \Common7\IDE\PrivateAssemblies**:  
  
   - Microsoft.VisualStudio.Uml.dll  
  
   - Microsoft.VisualStudio.TeamArchitect.ModelStore.Dsl.dll  
  
     如果你想要读取应用程序中的关系图，你可能还需要这些引用：  
  
   - Microsoft.VisualStudio.TeamArchitect.ActivityDesigner.Dsl.dll  
  
   - Microsoft.VisualStudio.TeamArchitect.ComponentDesigner.Dsl.dll  
  
   - Microsoft.VisualStudio.TeamArchitect.LogicalClassDesigner.Dsl.dll  
  
   - Microsoft.VisualStudio.TeamArchitect.SequenceDesigner.Dsl.dll  
  
   - Microsoft.VisualStudio.TeamArchitect.UseCase.Dsl.dll  
  
## <a name="see-also"></a>请参阅  
 [使用 UML API 编程](../modeling/programming-with-the-uml-api.md)   
 [扩展 UML 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)
