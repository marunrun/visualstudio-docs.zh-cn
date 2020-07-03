---
title: 如何：创建。.Vsct 文件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- VSCT files, creating
ms.assetid: b955f51c-f9f9-49c3-a8e4-63b6eb0e0341
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a571098deeeca0e8262d855c24d0bf1ce66be08e
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905535"
---
# <a name="how-to-create-a-vsct-file"></a>如何：创建 .vsct 文件

有多种方法可以创建基于 XML 的 Visual Studio 命令表配置（*.vsct*）文件。

- 可以在包模板中创建新的 VSPackage [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- 您可以使用基于 XML 的命令表配置编译器*Vsct.exe*从现有的 *.ctc*文件生成文件。

- 可以使用*Vsct.exe*从现有的*cto*文件生成 *.vsct*文件。

- 可以手动创建 *.vsct*文件。

  本文介绍如何手动创建 *.vsct*文件。

### <a name="to-manually-create-a-new-vsct-file"></a>手动创建新的 .vsct 文件

1. 启动 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

2. 在 **“文件”** 菜单上，指向 **“新建”**，然后单击 **“文件”**。

3. 在 "**模板**" 窗格中，单击 " **XML 文件**"，然后单击 "**打开**"。

4. 在 "**视图**" 菜单上，单击 "**属性**" 以显示 XML 文件的属性。

5. 在 "**属性**" 窗口中，单击 "**架构**" 属性上的 "**浏览**" 按钮。

6. 在 XSD 架构列表中，选择 " *.vsct* " 架构。 如果该文件不在列表中，请单击 "**添加**"，然后在本地驱动器上找到该文件。 完成后，单击 **"确定"** 。

7. 在 XML 文件中，键入 *<CommandTable* ，然后按**tab**。键入即可关闭标记 *>* 。

    此操作创建一个 *.vsct*文件。

8. 根据[.VSCT xml 架构参考](../../extensibility/vsct-xml-schema-reference.md)填写要添加的 xml 文件的元素。 有关详细信息，请参阅[.vsct 文件](../../extensibility/internals/authoring-dot-vsct-files.md)。

<a name="how-to-create-a-dot-vsct-file-from-an-existing-dot-ctc-file"></a>

## <a name="how-to-create-a-vsct-file-from-an-existing-ctc-file"></a>如何：从现有的 .ctc 文件创建 .vsct 文件

你可以从现有命令表 *.ctc*源文件创建基于 XML 的 *.vsct*文件。 通过执行此操作，可以利用基于 XML 的新 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 命令表 (VSCT) 编译器格式。

### <a name="to-create-a-vsct-file-from-a-ctc-file"></a>从 .ctc 文件创建 .vsct  文件

1. 获取 Perl 语言的副本。

2. 获取 Perl 脚本*ConvertCTCToVSCT.pl*的副本（通常位于* \<Visual Studio SDK installation path> \VisualStudioIntegration\Tools\bin*文件夹中）。

3. 获取要转换的 *.ctc*源文件的副本。

4. 将这些文件放在同一个目录中。

5. 在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 命令提示符窗口中，导航到目录。

6. 类型

   ```
   perl.exe ConvertCTCtoVSCT.pl PkgCmd.ctc PkgCmd.vsct
   ```

    其中， *pkgcmd.ctc 是*是 *.ctc*文件的名称，而*pkgcmd.ctc 是*是要创建的 *.vsct*文件的名称。

    此操作会创建一个新的 *.Vsct* XML 命令表源文件。 您可以使用*Vsct.exe*.vsct 编译器来编译该文件，就像使用任何其他 *.vsct*文件一样。

   > [!NOTE]
   > 可以通过重新格式化 XML 注释来提高 *.vsct*文件的可读性。

<a name="how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file"></a>

## <a name="how-to-create-a-vsct-file-from-an-existing-cto-file"></a>如何：从现有的 cto 文件创建 .vsct 文件

可以从现有的*cto*文件创建基于 XML 的 *.vsct*文件。 这样既可充分利用新的命令表编译器格式。 即使*cto*文件是从 *.ctc*文件编译的，此过程仍然有效。 你可以编辑 *.vsct*文件并将其编译到另一个 cto 文件中。

### <a name="to-create-a-vsct-file-from-a-cto-file"></a>从 .cto 文件创建 .Vsct 文件

1. 获取*cto*文件及其相应*的 .ctsym*文件的副本。

2. 将这些文件放入与*vsct.exe*编译器相同的目录中。

3. 在 Visual Studio 命令提示符处，前往包含*cto*和 *.ctsym*文件的目录。

4. 类型

    ```
    vsct.exe <ctofilename>.cto <vsctfilename>.vsct -S<symfilename>.ctsym
    ```

     其中 \<ctofilename\> 是*cto*文件的名称， \<vsctfilename\> 是要创建的 *.vsct*文件的名称， \<symfilename\> 是 *.ctsym*文件的名称。

     此过程将创建一个新的 *.Vsct* XML 命令表编译器文件。 可以像处理任何其他 *.vsct*文件一样，用*vsct.exe*.vsct 编译器编辑和编译文件。

## <a name="compile-the-code"></a>编译代码
 只需将 *.vsct*文件添加到项目不会导致编译。 您必须将其合并到生成过程中。

### <a name="to-add-a-vsct-file-to-project-compilation"></a>将 .vsct 文件添加到项目编译

1. 在编辑器中打开项目文件。 如果已加载项目，则必须先卸载它。

2. 添加一个包含元素的[ItemGroup 元素](../../msbuild/itemgroup-element-msbuild.md) `VSCTCompile` ，如下面的示例中所示。

    ```xml
    <ItemGroup>
      <VSCTCompile Include="TopLevelMenu.vsct">
        <ResourceName>Menus.ctmenu</ResourceName>
      </VSCTCompile>
    </ItemGroup>

    ```

     `ResourceName`元素应始终设置为 `Menus.ctmenu` 。

3. 如果你的项目包含 *.resx*文件，则添加一个 `EmbeddedResource` 包含元素的元素 `MergeWithCTO` ，如下面的示例中所示：

    ```xml
    <EmbeddedResource Include="VSPackage.resx">
      <MergeWithCTO>true</MergeWithCTO>
      <ManifestResourceName>VSPackage</ManifestResourceName>
    </EmbeddedResource>

    ```

     此标记应在 `ItemGroup` 包含嵌入资源的元素内。

4. 在编辑器中打开包文件（通常名为* \<ProjectName\> Package.cs*或* \<ProjectName\> package*）。

5. 将 `ProvideMenuResource` 特性添加到包类，如下面的示例中所示。

    ```csharp
    [ProvideMenuResource("Menus.ctmenu", 1)]
    ```

     第一个参数值必须与 `ResourceName` 项目文件中定义的属性的值相匹配。

## <a name="see-also"></a>另请参阅
- [创作 .vsct 文件](../../extensibility/internals/authoring-dot-vsct-files.md)
- [Visual Studio 命令表（.vsct）文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [.VSCT XML 架构引用](../../extensibility/vsct-xml-schema-reference.md)
