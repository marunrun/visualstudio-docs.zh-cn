---
title: 扩展 Visual Studio for Mac
description: 可使用被称为“扩展包”的模块扩展 Visual Studio for Mac 的特性和功能。 本指南的第一部分创建了一个简单的 Visual Studio for Mac 扩展包，用于在文档中插入日期和时间。 本指南的第二部分介绍了该扩展包系统和一些构成 Visual Studio for Mac 基础的核心 API 的基础知识。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 04/14/2017
ms.technology: vs-ide-sdk
ms.assetid: D5245AB0-8404-426B-B538-F49125E672B2
ms.openlocfilehash: 29c5bb9c45ae8d859316bd9c63eec10a6a425571
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "75851957"
---
# <a name="extending-visual-studio-for-mac"></a>扩展 Visual Studio for Mac

Visual Studio for Mac 包含一组被称为“扩展包”的模块  。 可使用扩展包为 Visual Studio for Mac 引入新功能，例如对另一种语言或新项目模板的支持。

扩展包从其他扩展包的“扩展点”进行生成  。 扩展点是可展开区域（如菜单或 IDE 命令列表）的占位符。 通过注册名为“扩展”的结构化数据的节点，如新菜单项或新命令，扩展包可从扩展点进行生成。 每个扩展点都接受特定类型的扩展，如“Command”、“Pad”或“FileTemplate”    。 包含扩展点的模块可被其他扩展包扩展，因此又被称为“加载项主机”  。

若要自定义 Visual Studio for Mac，可在 Visual Studio for Mac 中创建一个扩展包，该扩展包从包含在现有库内的加载项主机扩展点进行生成，如下图所示：

![加载项体系结构](media/extending-visual-studio-mac-addin1.png)

若要使扩展包从 Visual Studio for Mac 进行生成，则必须拥有在 Visual Studio for Mac IDE 内从现有扩展点进行生成的扩展。 如果扩展包依赖于加载项主机中定义的扩展点，则称该扩展包上拥有 _依赖项_ 。

此模块化设计的好处是 Visual Studio for Mac 可扩展，即可通过自定义扩展包在许多扩展点上进行生成。 当前扩展包的示例包括对 C# 和 F# 的支持、调试工具和项目模板。

> [!NOTE]
> 如果有 Add-in Maker 1.2 之前创建的 Add-in Maker 项目，则需按照[此处](https://mhut.ch/addinmaker/1.2)的步骤迁移项目。

<!---The [Walkthrough](~/extending-visual-studio-mac-walkthrough.md) topic explains how to build an extension package that uses a *Command* to insert the date and time into an open text document.--->

本部分介绍 Add-in Maker 生成的不同文件，以及命令扩展需要的数据。

## <a name="attribute-files"></a>属性文件

扩展包存储与其名称、版本、依赖项和其他 C# 属性中的信息相关的元数据。 Add-in Maker 创建两个文件（`AddinInfo.cs` 和 `AssemblyInfo.cs`）来存储和组织该信息。 必须为扩展包的“加载项属性”指定唯一的 ID 和命名空间  ：

```csharp
[assembly:Addin (
   "DateInserter",
   Namespace = "DateInserter",
   Version = "1.0"
)]
```

扩展包还必须声明拥有依赖项，该依赖项所在的扩展包拥有它们所插入的扩展点。 生成时将自动引用这些依赖项。

此外，可通过项目 Solution Pad 中的加载项引用节点添加其他引用，如下图所示：

![插入日期屏幕截图](media/extending-visual-studio-mac-addin13.png)

它们也拥有在生成时添加的对应 `assembly:AddinDependency` 属性。 元数据和依赖项声明就位后，便可专注于扩展包的重要构建基块。

## <a name="extensions-and-extension-points"></a>扩展和扩展点

扩展点是定义数据结构（类型）的占位符，扩展则定义符合特定扩展点所指定结构的数据。 扩展点指定它们在声明中可接受的扩展类型。 可通过使用类型名称或扩展路径声明扩展。 若要深入了解如何创建所需的扩展点，请参阅 [Extension Point reference](https://github.com/mono/mono-addins/wiki/Extension-Points)（扩展点引用）。

扩展/扩展点体系结构保证了快速且模块化的 Visual Studio for Mac 开发。

<!--Since there are a large number of extension types, this article focuses on the ones used in the extension package that was built in the [Walkthrough](~/extending-visual-studio-mac-walkthrough.md).-->

### <a name="command-extensions"></a>命令扩展

<!--[Walkthrough](~/extending-visual-studio-mac-walkthrough.md) uses a Command Extension - an extension that points to methods that are called every time it is executed. -->

命令扩展是指向每次执行都会调用的方法的扩展。

可通过将条目添加到 `/MonoDevelop/Ide/Commands` 扩展点来定义命令扩展。 我们使用以下代码在 `Manifest.addin.xml` 中定义了扩展：

 ```xml
<Extension path="/MonoDevelop/Ide/Commands/Edit">
  <command id="DateInserter.DateInserterCommands.InsertDate"
            _label="Insert Date"
            _description="Insert the current date"
            defaulthandler="DateInserter.InsertDateHandler" />
</Extension>
```

扩展节点包含的路径属性指定它插入的扩展点，在本示例中为 `/MonoDevelop/Ide/Commands/Edit`。 此外，它还充当该命令的父节点。 该命令节点具有以下属性：

* **id** - 为该命令指定标识符。 命令标识符必须声明为枚举成员，用于将命令连接到命令项。
* **_label** - 在菜单中显示的文本。
* **_description** - 作为工具栏按钮的工具提示显示的文本。
* **defaultHandler** - 指定加强该命令的 `CommandHandler` 类

<!--To invoke the command from the Edit Menu, the walkthrough creates a CommandItem extension that plugs into the `/MonoDevelop/Ide/MainMenu/Edit` extension point:-->

下面的代码片段展示了插入 `/MonoDevelop/Ide/MainMenu/Edit` 扩展点的 CommandItem 扩展：

```xml
<Extension path="/MonoDevelop/Ide/MainMenu/Edit">
  <commanditem id="DateInserter.DateInserterCommands.InsertDate" />
</Extension>
```

命令项将其 ID 属性中指定的命令放入菜单中。 该命令项扩展 `/MonoDevelop/Ide/MainMenu/Edit` 扩展点，使该命令的标签显示在“编辑菜单”中  。 请注意，命令项中的“ID”对应于命令节点  **的 ID**`InsertDate`。 如果移除命令项，“编辑菜单”中的“插入日期”选项将消失  。

### <a name="command-handlers"></a>命令处理程序

`InsertDateHandler` 是 `CommandHandler` 类的扩展。 它定义了两个方法，`Update` 和 `Run`。 只要菜单中显示或通过键绑定执行命令，就会查询 `Update` 方法。 通过更改信息对象，可禁用命令或使其不可见、填充数组命令或执行其他操作。 如果 `Update` 方法找不到活动的“文档”和用来插入文本的“文本编辑器”，则会禁用该命令：  

```csharp
protected override void Update (CommandInfo info)
{
    info.Enabled = IdeApp.Workbench.ActiveDocument?.Editor != null;
}
```

如果拥有启用或隐藏该命令的特殊逻辑，只需替代 `Update` 方法。 用户执行命令时就会执行 `Run` 方法，这种情况会在用户从“编辑菜单”中选择命令时发生。 此方法在文本编辑器中的插入点插入日期和时间：

```csharp
protected override void Run ()
{
  var editor = IdeApp.Workbench.ActiveDocument.Editor;
  var date = DateTime.Now.ToString ();
  editor.InsertAtCaret (date);
}
```

在 `DateInserterCommands` 中将命令类型声明为枚举成员：

```csharp
public enum DateInserterCommands
{
  InsertDate,
}
```

这会将命令与命令项联系在一起 - 当从“编辑菜单”中选择命令项时，它就会调用该命令  。

## <a name="ide-apis"></a>IDE API

<!--The extension package detailed in the [Walkthrough](~/extending-visual-studio-mac-walkthrough.md) deals with the Text Editor in Visual Studio for Mac, but this is only one of many possible areas for customization. -->

若要了解有关可用于开发的区域范围，请参阅 [Extension Tree Reference](https://www.monodevelop.com/developers/articles/extension-tree-reference/)（扩展树引用）和 [API Overview](https://www.monodevelop.com/developers/articles/api-overview/)（API 概述）。 生成高级扩展包时，另请参阅[开发者文章](https://www.monodevelop.com/developers/articles/)。 以下是自定义区域的部分列表：

* 面板
* 键绑定方案
* 策略
* 代码格式化程序
* 项目文件格式
* 首选项面板
* 选项面板
* 调试器协议
* 调试器可视化工具
* 工作区布局
* Solution Pad 树节点
* 源编辑器边距
* 单元测试引擎
* 代码生成器
* 代码片段
* 目标框架
* 目标运行时
* VCS 后端
* Refactoring
* 执行处理程序
* 语法突出显示

## <a name="additional-information"></a>其他信息

> [!NOTE]
> 我们正在致力于改善针对 Visual Studio for Mac 的扩展性方案。 若要创建扩展，并需要其他帮助或信息，或希望提供反馈，请填写 [Visual Studio for Mac 扩展创建](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR3YufGX_azhFl7MkrQO9i9JUNVMyMklVVlAzQVdURDg2NjQxTFRBVTJURC4u)表单。

## <a name="see-also"></a>另请参阅

- [开发 Visual Studio 扩展 (Windows)](/visualstudio/extensibility/starting-to-develop-visual-studio-extensions)
