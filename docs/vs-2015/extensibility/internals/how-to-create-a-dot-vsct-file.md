---
title: 如何：创建。.Vsct 文件 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68158355"
---
# <a name="how-to-create-a-vsct-file"></a>如何：创建 .Vsct 文件
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

有多种方法可以创建基于 XML 的 Visual Studio 命令表配置 ( .vsct) 文件。  
  
- 可以在包模板中创建新的 VSPackage [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
- 您可以使用基于 XML 的命令表配置编译器 Vsct.exe 从现有的 .ctc 文件生成文件。  
  
- 可以使用 Vsct.exe 从现有的 cto 文件生成 .vsct 文件。  
  
- 可以手动创建 .vsct 文件。  
  
  本主题说明如何手动创建 .vsct 文件。  
  
### <a name="to-manually-create-a-new-vsct-file"></a>手动创建新的 .vsct 文件  
  
1. 启动 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
2. 在 **“文件”** 菜单上，指向 **“新建”** ，然后单击 **“文件”** 。  
  
3. 在 " **模板** " 窗格中，单击 " **XML 文件** "，然后单击 " **打开**"。  
  
4. 在 " **视图** " 菜单上，单击 " **属性窗口** " 以显示 XML 文件的属性。  
  
5. 在 " **属性** " 窗口中，单击 "架构" 属性上的 "浏览 ( ..." ) 按钮。  
  
6. 在 XSD 架构列表中，选择 ".vsct" 架构。 如果该文件不在列表中，请单击 " **添加** "，然后在本地驱动器上找到该文件。 完成后，单击 **"确定"** 。  
  
7. 在 XML 文件中，键入 `<CommandTable` ，然后按 tab。 键入即可关闭标记 `>` 。  
  
     这将创建一个 .vsct 文件。  
  
8. 根据 [.Vsct 架构](../../extensibility/vsct-xml-schema-reference.md)填写要添加的 XML 文件的元素。 有关详细信息，请参阅 [创作。.Vsct 文件](../../extensibility/internals/authoring-dot-vsct-files.md)  
  
## <a name="compiling-the-code"></a>编译代码  
 只需将 .vsct 文件添加到项目不会导致编译。 您必须将其合并到生成过程中。  
  
### <a name="to-add-a-vsct-file-to-project-compilation"></a>将 .vsct 文件添加到项目编译  
  
1. 在编辑器中打开项目文件。 如果已加载项目，则必须先卸载它。  
  
2. 添加一个包含 VSCTCompile 元素的 [ItemGroup 元素](../../msbuild/itemgroup-element-msbuild.md) ，如下面的示例中所示。  
  
    ```xml  
    <ItemGroup>  
      <VSCTCompile Include="TopLevelMenu.vsct">  
        <ResourceName>Menus.ctmenu</ResourceName>  
      </VSCTCompile>  
    </ItemGroup>  
  
    ```  
  
     Context.resourcename 元素应始终设置为 `Menus.ctmenu` 。  
  
3. 如果你的项目包含 .resx 文件，则添加一个包含 MergeWithCTO 元素的 EmbeddedResource 元素，如下面的示例中所示。  
  
    ```xml  
    <EmbeddedResource Include="VSPackage.resx">  
      <MergeWithCTO>true</MergeWithCTO>  
      <ManifestResourceName>VSPackage</ManifestResourceName>  
    </EmbeddedResource>  
  
    ```  
  
     此标记应在包含嵌入资源的 ItemGroup 元素中。  
  
4. 在编辑器中打开包文件，通常名为 " *项目名称*Package.cs" 或 " *项目名称*package"。  
  
5. 将 ProvideMenuResource 特性添加到包类，如下面的示例中所示。  
  
    ```csharp  
    [ProvideMenuResource("Menus.ctmenu", 1)]  
    ```  
  
     第一个参数值必须与项目文件中定义的 Context.resourcename 特性的值匹配。  
  
## <a name="see-also"></a>另请参阅  
 [创作..Vsct 文件](../../extensibility/internals/authoring-dot-vsct-files.md)   
 [Visual Studio 命令表 (。.Vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)   
 [如何：创建。来自现有的 .vsct 文件。.Ctc 文件](../../misc/how-to-create-a-dot-vsct-file-from-an-existing-dot-ctc-file.md)   
 [如何：创建。来自现有的 .vsct 文件。Cto 文件](../../misc/how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file.md)   
 [VSCT XML 架构参考](../../extensibility/vsct-xml-schema-reference.md)
