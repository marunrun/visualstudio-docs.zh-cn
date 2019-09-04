---
title: EditorConfig
description: 使用 editorconfig 文件在 Visual Studio for Mac 中启用一致的项目编码样式。
author: cobey
ms.author: cobey
ms.date: 05/06/2018
ms.technology: vs-ide-install
ms.assetid: 26A0DE31-2FBF-4E1B-99FB-083111AA1680
ms.openlocfilehash: 8115715950881168e282cd205ea2dd3e64d89f97
ms.sourcegitcommit: cf8c0fef2b9690595e99ce3802586cdd55fd37c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70108296"
---
# <a name="creating-and-editing-a-custom-editorconfig-file"></a>创建并编辑自定义 EditorConfig 文件

在 Visual Studio for Mac 中，可以向项目或解决方案添加 [EditorConfig](http://editorconfig.org/) 文件，强制对使用该基本代码的所有人实施一致的编码样式。 EditorConfig 文件中声明的设置优先于全局 Visual Studio for Mac 文本编辑器设置。 在项目或基本代码中使用 EditorConfig 文件可为项目设置编码样式、首选项和警告。 由于该文件是基本代码的一部分，因此无论使用何种 IDE 或代码编辑器，它都使用户更容易遵守项目的编码操作。

[EditorConfig](http://editorconfig.org/) 文件受到许多 IDE 和代码编辑器（包括 Visual Studio）支持。

## <a name="supported-settings"></a>支持的设置

Visual Studio for Mac 中的编辑器支持 [EditorConfig 属性](http://editorconfig.org/#supported-properties)的核心集：

- `indent_style`
- `indent_size`
- `tab_width`
- `end_of_line`
- `charset`
- `trim_trailing_whitespace`
- `insert_final_newline`
- `root`

EditorConfig 还支持 C# 中的[编码约定](/visualstudio/ide/editorconfig-code-style-settings-reference)。

## <a name="add-an-editorconfig-file-to-a-project"></a>将 EditorConfig 文件添加到项目

### <a name="adding-a-new-editorconfig-file"></a>添加新的 EditorConfig 文件

1. 在 Visual Studio for Mac 中打开项目。 选择要向其添加 EditorConfig 文件的解决方案或项目节点。 将文件添加到解决方案目录会将 .editorconfig 设置应用于解决方案中的所有项目。

2. 右键单击节点，然后选择“添加”>“新建文件”以打开“新文件”对话框   ：

    ![内容菜单项](media/editorconfig-image0.png)

3. 选择“其他”>“空文本文件”并将其命名为 `.editorconfig`   。 按“新建”创建文件并在编辑器中将其打开  ：

    ![“新文件”对话框](media/editorconfig-image1.png)

    在解决方案级别添加该项会自动创建并将其嵌套在解决方案项文件夹中  ：

    ![Solution Pad 中显示的解决方案项](media/editorconfig-image1a.png)

4. 编辑文件。 例如:

    ```EditorConfig
    # This file is the top-most EditorConfig file
    root = true

    # All Files
    [*]
    indent_style = space
    indent_size = 8
    insert_final_newline = false
    trim_trailing_whitespace = false

    [*.cs]
    csharp_new_line_before_open_brace = none
    ```

4. `.editorconfig` 文件中的设置将应用于编写的任何新代码，但可能需要重格式化现有代码以与新设置保持一致。 若要将 `.editorconfig` 文件中的设置应用于现有源文件，请打开该文件，然后从菜单栏中选择“编辑”>“格式”>“设置文档格式”  ：

    ![设置文档格式菜单项](media/editorconfig-image2.png)

### <a name="adding-an-existing-editorconfig-file"></a>添加现有的 EditorConfig 文件

如果正在使用已包含 `.editorconfig` 文件的项目或解决方案，则无需执行任何操作即可应用设置。 任何新的代码行都将根据 EditorConfig 设置设置格式。

可能想重复使用项目中现有的 `.editorconfig` 文件。 若要添加现有文件，请执行以下操作：

1. 右键单击要添加到的文件夹，然后选择“添加”>“添加文件”  。

2. 浏览到所需文件的目录。

3. 以 `.` 开头的文件（例如 `.editorconfig`）是 macOS 中的隐藏文件，因此请按Command + Shift + .  以使 `.editorconfig` 文件可见。

4. 选择 `.editorconfig` 文件并单击“打开”  ：

    ![添加新的文件窗口](media/editorconfig-image3b.png)

5. 看到以下对话框时，选择“将文件复制到目录”选项并选择“确定”   ：

    ![将文件添加到文件夹对话框选项](media/editorconfig-image3.png)

### <a name="reflecting-editorconfig-settings"></a>反映 .editorconfig 设置

将 EditorConfig 文件添加到基本代码后，添加的任何新代码将根据指定的设置自动格式化。 除非设置基本代码格式，否则现有代码不会自动反映设置。

若要从 `.editorconfig` 文件反映设置，请从菜单栏选择解决方案节点并选择“编辑”>“格式”>“设置文档格式”  ：

![菜单栏中的“设置文档格式”](media/editorconfig-image3a.png)

## <a name="editing-an-editorconfig-file"></a>编辑 EditorConfig 文件

EditorConfig 文件使用简单的文件布局来指定设置，下面使用前一个示例来解释：

```EditorConfig
# This file is the top-most EditorConfig file
root = true

# All Files
[*]
indent_style = space
indent_size = 4
insert_final_newline = false
trim_trailing_whitespace = false

[*.cs]
csharp_new_line_before_open_brace = none
```

将 `root` 设置为 `true` 可把该文件标记为代码库中的最顶级文件，并忽略项目中任何更高级的 `.editorconfig` 文件，如[代替 EditorConfig 设置](#override-editorconfig-settings)部分所述。

每个部分用方括号 ([ ]  ) 表示，并指定下列属性应涉及的文件类型的信息。

在以上示例中，一些设置应用于项目的所有文件，其他设置仅添加到 C# 文件。 以下屏幕截图显示应用 `.editorconfig` 设置之前以及之后的情况：

**之前**：

![应用 editorconfig 设置之前](media/editorconfig-image4.png)

**之后**：

![应用 editorconfig 设置之后](media/editorconfig-image5.png)

有关可用的 EditorConfig 设置的详细信息，请参阅 [EditorConfig 的 .NET 编码约定设置](/visualstudio/ide/editorconfig-code-style-settings-reference)一文以及官方文档的[支持的属性](http://editorconfig.org/#supported-properties)部分。

## <a name="override-editorconfig-settings"></a>替代 EditorConfig 设置

每个解决方案可以具有一个以上的 `.editorconfig` 文件。 Visual Studio for Mac 在解决方案中从上到下读取 `.editorconfig` 文件，并在此过程中添加和替代设置。这意味将优先选择 `.editorconfig` 中_最接近_正在编辑的文件的设置。 先采用同一文件夹中 `.editorconfig` 文件（如果存在）中的设置，其次采用父级文件夹中 `.editorconfig`（如果存在）中的设置，以此类推。 直到找到 `root=true`。

如果要确保任何更高级别的 `.editorconfig` 文件中没有设置应用于此部分代码库，请将 `root=true` 属性添加到较低级别的 `.editorconfig` 文件顶部  ：

```EditorConfig
# top-most EditorConfig file
root = true
```

## <a name="see-also"></a>请参阅

- [使用 EditorConfig 创建自定义编辑器设置（Windows 上的 Visual Studio）](/visualstudio/ide/create-portable-custom-editor-options)