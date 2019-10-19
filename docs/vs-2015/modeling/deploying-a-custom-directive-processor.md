---
title: 部署自定义指令处理器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, custom directive processors
ms.assetid: 80c28722-a630-47b5-923b-024dc3f2c940
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6cce0a918b1b3e029846176832ab2feb74e3e9e4
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669840"
---
# <a name="deploying-a-custom-directive-processor"></a>部署自定义指令处理器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要在任何计算机上的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中使用自定义指令处理器，必须使用本主题中介绍的方法之一注册该处理器。

 可用的方法包括：

- [Visual Studio 扩展（VSIX）](https://msdn.microsoft.com/64ff1452-f7d5-42d9-98b8-76f769f76832)。 通过这种方法，可以在自己或他人的计算机上安装和卸载指令处理器。 通常，可能会在同一 VSIX 中包含其他功能。

- [VSPackage](../extensibility/internals/vspackages.md)。 如果要定义一个包含指令处理器和其他功能的 VSPackage，有一种方便的方法可以注册指令处理器。

- 设置注册表项。 如果采用此方法，则会为指令处理器添加一个注册表项。

  仅当要在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 或 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 中转换文本模板时，才需要从上述方法中选用一种。 如果在自己的应用程序中使用自定义宿主，则由自定义宿主负责查找每条指令的指令处理器。

## <a name="deploying-a-directive-processor-in-a-vsix"></a>在 VSIX 中部署指令处理器
 可以将自定义指令处理器添加到[Visual Studio 扩展（VSIX）](https://msdn.microsoft.com/64ff1452-f7d5-42d9-98b8-76f769f76832)。

 需要确保 .vsix 文件包含以下两项：

- 包含自定义指令处理器类的程序集 (.dll)。

- 注册指令处理器的 .pkgdef 文件。 文件的根名称必须与程序集相同。 例如，文件可以命名为 CDP.dll 和 CDP.pkgdef。

  若要检查或更改 .vsix 文件的内容，请将其文件扩展名更改为 .zip，然后将其打开。 编辑内容之后，将文件扩展名改回为 .vsix。

  有几种方法可以创建 .vsix 文件。 以下过程将介绍其中一种方法。

#### <a name="to-develop-a-custom-directive-processor-in-a-vsix-project"></a>在 VSIX 项目中开发自定义指令处理器

1. 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中创建 VSIX 项目。

    - 在 "**新建项目**" 对话框中，展开**Visual Basic**或 **C#视觉对象**，然后展开 "**扩展性**"。 单击 " **VSIX 项目**"。

2. 在**source.extension.vsixmanifest**中，设置内容类型和支持的版本。

    1. 在 VSIX 清单编辑器中的 "**资产**" 选项卡上，选择 "**新建**" 并设置新项的属性：

         **内容类型** = **VSPackage**

         *当前项目*\<**源项目** =  >

    2. 单击 "**所选版本**"，然后检查要在其中使用指令处理器的安装类型。

3. 添加 .pkgdef 文件，并设置其属性，以便使其包含在 VSIX 中。

    1. 创建一个文本文件，并将其命名 \<*assemblyName*> .pkgdef。

         \<*assemblyName*> 通常与项目的名称相同。

    2. 在解决方案资源管理器中，选中该文件并将其属性设置如下：

         @No__t_1**内容** **生成操作**

         **复制到输出目录** = **始终复制**

         **在 VSIX 中包括** = **True**

    3. 设置 VSIX 的名称并确保该 ID 是唯一的。

4. 向 .pkgdef 文件添加以下文本。

    ```
    [$RootKey$\TextTemplating]
    [$RootKey$\TextTemplating\DirectiveProcessors]
    [$RootKey$\TextTemplating\DirectiveProcessors\ CustomDirectiveProcessorName]
    @="Custom Directive Processor description"
    "Class"="NamespaceName.ClassName"
    "CodeBase"="$PackageFolder$\AssemblyName.dll"
    ```

     用您自己提供的名称替换以下名称：`CustomDirectiveProcessorName`、`NamespaceName`、`ClassName`、`AssemblyName`。

5. 将下列引用添加到该项目中：

    - **VisualStudio. TextTemplating. \***

    - **VisualStudio. TextTemplating. \***

    - **VisualStudio. TextTemplating. Vshost.exe. \***

6. 将自定义指令处理器类添加到项目。

     这是一个公共类，它应实现 <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> 或 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor>。

#### <a name="to-install-the-custom-directive-processor"></a>安装自定义指令处理器

1. 在 Windows 资源管理器（Windows 8 中为文件资源管理器）中，打开生成目录（通常为 bin\Debug 或 bin\Release）。

2. 如果要在另一台计算机上安装指令处理器，请将 .vsix 文件复制到该计算机。

3. 双击 .vsix 文件。 此时将显示 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Extension Installer。

4. 重新启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 现在，可以运行包含引用自定义指令处理器的指令的文本模板。 每个指令的形式如下：

     `<#@ CustomDirective Processor="CustomDirectiveProcessorName" parameter1="value1" … #>`

#### <a name="to-uninstall-or-temporarily-disable-the-custom-directive-processor"></a>卸载或临时禁用自定义指令处理器

1. 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]**工具**"菜单中，单击"**扩展管理器**"。

2. 选择包含指令处理器的 VSIX，然后单击 "**卸载**" 或 "**禁用**"。

### <a name="troubleshooting-a-directive-processor-in-a-vsix"></a>VSIX 中指令处理器的疑难解答
 如果指令处理器不能正常运行，可以尝试以下建议：

- 在自定义指令中指定的处理器名必须与在 .pkgdef 文件中指定的 `CustomDirectiveProcessorName` 一致。

- `IsDirectiveSupported` 方法在传递 `true` 的名称时必须返回 `CustomDirective`。

- 如果在 "扩展管理器" 中看不到该扩展，但是系统将不允许安装该扩展，请从%Localappdata%\Microsoft\VisualStudio 中删除该扩展， **\\ \* .0 \ 扩展 \\** 。

- 打开 .vsix 文件并检查其内容。 若要打开该文件，请将文件扩展名更改为 .zip。 确认该文件包含 .dll、.pkgdef 和 extension.vsixmanifest 文件。 extension.vsixmanifest 文件的 SupportedProducts 节点应包含相应的列表，“内容”节点下还应包含 VsPackage 节点：

     `<Content>`

     `<VsPackage>CustomDirectiveProcessor.dll</VsPackage>`

     `</Content>`

## <a name="deploying-a-directive-processor-in-a-vspackage"></a>在 VSPackage 中部署指令处理器
 如果指令处理器作为 VSPackage 的一部分安装在 GAC 中，则可以由系统生成 .pkgdef 文件。

 为包类添加以下特性：

```
[ProvideDirectiveProcessor(typeof(DirectiveProcessorClass), "DirectiveProcessorName", "Directive processor description.")]
```

> [!NOTE]
> 将此特性置于包类，而不是指令处理器类。

 生成项目时，将生成 .pkgdef 文件。 安装 VSPackage 时，.pkgdef 文件将注册指令处理器。

 确认 .pkgdef 文件显示在生成文件夹中，该文件夹通常是 bin\Debug 或 bin\Release。 如果未显示该文件，请在文本编辑器中打开 .csproj 文件，删除以下节点：`<GeneratePkgDefFile>false</GeneratePkgDefFile>`。

 有关更多信息，请参见 [VSPackages](../extensibility/internals/vspackages.md)。

## <a name="setting-a-registry-key"></a>设置注册表项
 这种自定义指令处理器的安装方法是最不方便的一种方法。 这种方法不能方便地启用和禁用指令处理器，也不能方便地向其他用户分发指令处理器。

> [!CAUTION]
> 注册表编辑不当可能会严重损坏系统。 更改注册表之前，请务必备份计算机中的所有重要数据。

#### <a name="to-register-a-directive-processor-by-setting-a-registry-key"></a>通过设置注册表项注册指令处理器

1. 运行 `regedit`。

2. 在 regedit 中，定位到

    **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio \\ \* 0 \ TextTemplating\DirectiveProcessors**

    如果要在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验版本中安装指令处理器，请在“11.0”之后插入“Exp”。

3. 添加与指令处理器类同名的注册表项。

   - 在注册表树中，右键单击 " **DirectiveProcessors** " 节点，指向 "**新建**"，然后单击 "**项**"。

4. 在新建节点中，根据下表为 Class 和 CodeBase 或 Assembly 添加字符串值。

   1. 右键单击创建的节点，指向 "**新建**"，然后单击 "**字符串值**"。

   2. 编辑值的名称。

   3. 双击该名称，然后编辑数据。

   如果自定义指令处理器不在 GAC 中，则注册表子项应如下表所示：

|“属性”|键入|数据|
|----------|----------|----------|
|(默认)|REG_SZ|(未设置值)|
|实例|REG_SZ|**\<Namespace 名称 >。\<Class 名称 >**|
|CodeBase|REG_SZ|**\<Your 路径 > \\ < 程序集名称 \>**|

 如果程序集在 GAC 中，则注册表子项应如下表所示：

|“属性”|键入|数据|
|----------|----------|----------|
|(默认)|REG_SZ|(未设置值)|
|实例|REG_SZ|\<**完全限定的类名**>|
|Assembly|REG_SZ|\<**GAC 中的程序集名称**>|

## <a name="see-also"></a>请参阅
 [创建自定义 T4 文本模板指令处理器](../modeling/creating-custom-t4-text-template-directive-processors.md)
