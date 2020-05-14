---
title: 如何：创建一个 。Vsct 文件 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, creating
ms.assetid: b955f51c-f9f9-49c3-a8e4-63b6eb0e0341
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a5a5f53ec87c9447af232e9d0528108ddbaea01a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708111"
---
# <a name="how-to-create-a-vsct-file"></a>如何：创建 .vsct 文件

有几种方法可以创建基于 XML 的 Visual Studio 命令表配置 *（.vsct*） 文件。

- 您可以在包模板中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]创建新的 VS 包。

- 您可以使用基于 XML 的命令表配置编译器*Vsct.exe*从现有的 *.ctc*文件生成文件。

- 您可以使用*Vsct.exe*从现有的 *.cto*文件生成 *.vsct*文件。

- 您可以手动创建新的 *.vsct*文件。

  本文介绍如何手动创建新的 *.vsct*文件。

### <a name="to-manually-create-a-new-vsct-file"></a>手动创建新的 .vsct 文件

1. 启动 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

2. 在 **“文件”** 菜单上，指向 **“新建”**，然后单击 **“文件”**。

3. 在 **"模板"** 窗格中，单击**XML 文件**，然后单击"**打开**"。

4. 在 **"视图"** 菜单上，单击 **"属性**"以显示 XML 文件的属性。

5. 在 **"属性"** 窗口中，单击 **"架构**"属性上的 **"浏览**"按钮。

6. 在 XSD 架构列表中，选择*vsct.xsd*架构。 如果不在列表中，请单击"**添加**"，然后在本地驱动器上查找该文件。 完成后单击 **"确定**"。

7. 在 XML 文件中，键入*命令表<，* 然后按**Tab**。通过键入*>* 关闭标记。

    此操作将创建一个基本*的 .vsct*文件。

8. 根据[VSCT XML 架构引用](../../extensibility/vsct-xml-schema-reference.md)，填写要添加的 XML 文件的元素。 有关详细信息，请参阅作者[.vsct 文件](../../extensibility/internals/authoring-dot-vsct-files.md)。

<a name="how-to-create-a-dot-vsct-file-from-an-existing-dot-ctc-file"></a>

## <a name="how-to-create-a-vsct-file-from-an-existing-ctc-file"></a>如何：从现有的 .ctc 文件创建 .vsct 文件

可以从现有命令表 *.ctc*源文件创建基于 XML 的 *.vsct*文件。 通过执行此操作，可以利用基于 XML 的新 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 命令表 (VSCT) 编译器格式。

### <a name="to-create-a-vsct-file-from-a-ctc-file"></a>从 .ctc 文件创建 .vsct  文件

1. 获取 Perl 语言的副本。

2. 获取 Perl 脚本*ConvertCTCToVSCT.pl*的副本，通常位于*\<Visual Studio SDK 安装路径>_VisualStudio集成\工具\bin*文件夹中。

3. 获取要转换的 *.ctc*源文件的副本。

4. 将这些文件放在同一个目录中。

5. 在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]命令提示窗口中，导航到目录。

6. 类型

   ```
   perl.exe ConvertCTCtoVSCT.pl PkgCmd.ctc PkgCmd.vsct
   ```

    *其中 PkgCmd.ctc*是 *.ctc*文件的名称 *，PkgCmd.vsct*是要创建的 *.vsct*文件的名称。

    此操作将创建新的 *.vsct* XML 命令表源文件。 您可以使用 VSCT 编译器*Vsct 编译器 Vsct exe*编译文件，就像使用任何其他 *.vsct*文件一样。

   > [!NOTE]
   > 您可以通过重新格式化 XML 注释来提高 *.vsct*文件的可读性。

<a name="how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file"></a>

## <a name="how-to-create-a-vsct-file-from-an-existing-cto-file"></a>如何：从现有的 .cto 文件创建 .vsct 文件

可以从现有的二进制 *.cto*文件创建基于 XML 的 *.vsct*文件。 这样既可充分利用新的命令表编译器格式。 即使 *.cto*文件是从 *.ctc*文件编译的，此过程也有效。 您可以将 *.vsct*文件编辑和编译为另一个 .cto 文件。

### <a name="to-create-a-vsct-file-from-a-cto-file"></a>从 .cto 文件创建 .Vsct 文件

1. 获取 *.cto*文件及其相应的 *.ctsym*文件的副本。

2. 将文件放入与*vsct.exe*编译器相同的目录中。

3. 在 Visual Studio 命令提示符下，转到包含 *.cto*和 *.ctsym*文件的目录。

4. 类型

    ```
    vsct.exe <ctofilename>.cto <vsctfilename>.vsct -S<symfilename>.ctsym
    ```

     其中\<ctofilename\>是 *.cto*文件的名称\<，fctfilename\>是要创建的 *.vsct*文件的名称\<，而 symfilename\>是 *.ctsym*文件的名称。

     此过程创建一个新的 *.vsct* XML 命令表编译器文件。 您可以使用*vsct.exe（vsct*编译器）编辑和编译该文件，就像任何其他 *.vsct*文件一样。

## <a name="compile-the-code"></a>编译代码
 简单地将 *.vsct*文件添加到项目中不会导致它编译。 您必须将其合并到生成过程中。

### <a name="to-add-a-vsct-file-to-project-compilation"></a>将 .vsct 文件添加到项目编译

1. 在编辑器中打开项目文件。 如果加载了项目，则必须首先卸载它。

2. 添加包含`VSCTCompile`元素的[ItemGroup 元素](../../msbuild/itemgroup-element-msbuild.md)，如以下示例所示。

    ```xml
    <ItemGroup>
      <VSCTCompile Include="TopLevelMenu.vsct">
        <ResourceName>Menus.ctmenu</ResourceName>
      </VSCTCompile>
    </ItemGroup>

    ```

     元素`ResourceName`应始终设置为`Menus.ctmenu`。

3. 如果项目包含 *.resx*文件，请添加包含`EmbeddedResource``MergeWithCTO`元素的元素，如以下示例所示：

    ```xml
    <EmbeddedResource Include="VSPackage.resx">
      <MergeWithCTO>true</MergeWithCTO>
      <ManifestResourceName>VSPackage</ManifestResourceName>
    </EmbeddedResource>

    ```

     此标记应进入包含嵌入资源`ItemGroup`的元素内。

4. 在编辑器中打开包文件，通常命名为*\<\>ProjectName Package.cs*或*\<ProjectName\>包.vb。*

5. 向`ProvideMenuResource`包类添加属性，如以下示例所示。

    ```csharp
    [ProvideMenuResource("Menus.ctmenu", 1)]
    ```

     第一个参数值必须与在项目文件中`ResourceName`定义的属性的值匹配。

## <a name="see-also"></a>请参阅
- [作者 .vsct 文件](../../extensibility/internals/authoring-dot-vsct-files.md)
- [可视化工作室命令表 （.vsct） 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML 架构引用](../../extensibility/vsct-xml-schema-reference.md)
