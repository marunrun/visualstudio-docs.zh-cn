---
title: 如何：创建。Vsct 文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, creating
ms.assetid: b955f51c-f9f9-49c3-a8e4-63b6eb0e0341
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a2483c000bb7c9446ac51bb94ef4006a7b2ac89f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68158355"
---
# <a name="how-to-create-a-vsct-file"></a>如何：创建 .Vsct 文件
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

有几种方法来创建一个基于 XML 的 Visual Studio 命令表配置 (.vsct) 文件。  
  
- 您可以创建新的 VSPackage 中[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]包模板。  
  
- 可以使用基于 XML 的命令表配置编译器 Vsct.exe，若要从现有的.ctc 文件生成的文件。  
  
- Vsct.exe 可用于从现有.cto 文件生成一个.vsct 文件。  
  
- 您可以手动创建新的.vsct 文件。  
  
  本主题说明如何手动创建新的.vsct 文件。  
  
### <a name="to-manually-create-a-new-vsct-file"></a>若要手动创建新的.vsct 文件  
  
1. 启动 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
2. 上**文件**菜单，依次指向**新建**，然后单击**文件**。  
  
3. 在中**模板**窗格中，单击**XML 文件**，然后单击**打开**。  
  
4. 上**视图**菜单上，单击**属性窗口**显示 XML 文件的属性。  
  
5. 在中**属性**窗口中，单击浏览 （...） 按钮上的架构属性。  
  
6. 在 XSD 架构的列表中，选择 vsct.xsd 架构。 如果不是在列表中，单击**添加**，然后找到本地驱动器上的文件。 单击**确定**完成之后。  
  
7. 在 XML 文件中，键入`<CommandTable`然后按 TAB 键。 通过键入结束标记`>`。  
  
     这将创建一个基本的.vsct 文件。  
  
8. 填写想要添加的 XML 文件的元素，根据[VSCT 架构](../../extensibility/vsct-xml-schema-reference.md)。 有关详细信息，请参阅[创作。Vsct 文件](../../extensibility/internals/authoring-dot-vsct-files.md)  
  
## <a name="compiling-the-code"></a>编译代码  
 只需将.vsct 文件添加到项目并不会进行编译。 必须在生成过程中将其合并。  
  
### <a name="to-add-a-vsct-file-to-project-compilation"></a>若要将.vsct 文件添加到项目编译  
  
1. 在编辑器中打开项目文件。 如果加载该项目，必须先卸载它。  
  
2. 添加[ItemGroup 元素](../../msbuild/itemgroup-element-msbuild.md)的包含 VSCTCompile 元素，如下面的示例中所示。  
  
    ```xml  
    <ItemGroup>  
      <VSCTCompile Include="TopLevelMenu.vsct">  
        <ResourceName>Menus.ctmenu</ResourceName>  
      </VSCTCompile>  
    </ItemGroup>  
  
    ```  
  
     ResourceName 元素应始终设置为`Menus.ctmenu`。  
  
3. 如果你的项目包含.resx 文件，添加包含 MergeWithCTO 元素，一个 EmbeddedResource 元素，如下面的示例中所示。  
  
    ```xml  
    <EmbeddedResource Include="VSPackage.resx">  
      <MergeWithCTO>true</MergeWithCTO>  
      <ManifestResourceName>VSPackage</ManifestResourceName>  
    </EmbeddedResource>  
  
    ```  
  
     此标记应该包含嵌入的资源的 ItemGroup 元素内。  
  
4. 打开包文件，通常名为*ProjectName*Package.cs 或*ProjectName*Package.vb，在编辑器中的。  
  
5. 将 ProvideMenuResource 属性添加到包类，如下面的示例中所示。  
  
    ```csharp  
    [ProvideMenuResource("Menus.ctmenu", 1)]  
    ```  
  
     第一个参数值必须匹配在项目文件中定义的资源名称特性的值。  
  
## <a name="see-also"></a>请参阅  
 [创作。Vsct 文件](../../extensibility/internals/authoring-dot-vsct-files.md)   
 [Visual Studio 命令表 (。Vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)   
 [如何：创建。从现有的 Vsct 文件。启动 Ctc 文件](../../misc/how-to-create-a-dot-vsct-file-from-an-existing-dot-ctc-file.md)   
 [如何：创建。从现有的 Vsct 文件。首席技术官文件](../../misc/how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file.md)   
 [VSCT XML 架构参考](../../extensibility/vsct-xml-schema-reference.md)
