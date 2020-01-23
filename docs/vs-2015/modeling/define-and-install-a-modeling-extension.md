---
title: 定义和安装建模扩展 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML - extending
- UML model, extending
ms.assetid: 82a58dc5-c7cf-4521-a6da-7ff09cd0de9d
caps.latest.revision: 39
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c38150dd84ef8898b2aa894a614dfb79e289b593
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75850455"
---
# <a name="define-and-install-a-modeling-extension"></a>定义和安装建模扩展
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 中，可以为建模图定义扩展。 以这种方式，你可以根据自己的需要调整关系图和模型。 例如，可以定义菜单命令、UML 配置文件、有效性约束和工具箱项。 可以在单个的扩展中定义多个组件。 此外，还可以以 [Visual Studio 集成扩展 (VSIX)](https://msdn.microsoft.com/library/dd393694(VS.100).aspx)的形式将这些扩展分发给其他 Visual Studio 用户。 可以使用 Visual Studio 中的 VSIX 项目创建 VSIX。

## <a name="requirements"></a>需求
 请参阅 [要求](../modeling/extend-uml-models-and-diagrams.md#Requirements)。

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="creating-a-modeling-extension-solution"></a>创建一个建模扩展解决方案
 若要定义建模扩展，必须创建一个包含这些项目的解决方案：

- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 集成扩展 (VSIX) 项目。 这将生成一个文件，为你的扩展组件充当安装程序。

- 包括程序代码的组件所需的类库项目。

  如果想要使扩展具有多个组件，可以在单个解决方案中对组件进行开发。 只需要有一个 VSIX 项目。

  不需要代码的组件（例如，自定义工具箱项和自定义的 UML 配置文件）可以直接添加到 VSIX 项目中，而无需使用单独的类库项目。 需要程序代码的组件在单独的类库项目中定义更容易。 需要代码的组件包括笔势处理程序、菜单命令和验证代码。

#### <a name="to-create-a-class-library-project-for-menu-commands-gesture-handlers-or-validation"></a>为菜单命令、笔势处理程序或验证创建一个类库项目

1. 在“文件” 菜单上，选择“新建”、“项目”。

2. 在“已安装的模板”下，选择“Visual C#” 或“Visual Basic”，然后选择“类库”。

#### <a name="to-create-a-vsix-project"></a>创建 VSIX 项目

1. 若要创建具有代码的组件，最简单的方法就是先创建类库项目。 然后，向该项目添加你的代码。

2. 创建 VSIX 项目。

    1. 在“解决方案资源管理器”中，该解决方案的快捷菜单上，选择“添加”、“新建项目”。

    2. 在 **“已安装的模板”** 下，展开 **“Visual C#”** 或 **“Visual Basic”** ，然后选择 **“扩展性”** 。 在中间栏中，选择“VSIX 项目”。

3. 将 VSIX 项目设置为解决方案的启动项目。

    - 在“解决方案资源管理器”中，VSIX 项目的快捷菜单上选择“设为启动项目”。

4. 打开 **source.extension.vsixmanifest**。 将在清单编辑器中打开该文件。

5. 在“元数据” 选项卡上，设置 VSIX 的名称和描述性字段。

6. 在“安装目标” 选项卡上，选择“新建” ，并将 Visual Studio 版本设置为目标。

7. 在“资产” 选项卡上，将组件添加到 Visual Studio 扩展。

    1. 选择 **“新建”** 。

    2. 对于具有代码的组件，在“添加新资产” 对话框中对这些字段进行设置：

        |||
        |-|-|
        |**类型** =|**Microsoft.VisualStudio.MefComponent**|
        |**Source** =|**当前解决方案中的项目**|
        |**Project** =|*你的类库项目*|
        |**嵌入此文件夹** =|*空白处*|

         有关其他组件类型，请参阅下一部分中的链接。

## <a name="developing-the-component"></a>开发组件
 对每个组件（如菜单命令或笔势处理程序），必须定义一个单独的处理程序。 可以将多个处理程序置于相同的类库项目中。 下表总结了不同类型的处理程序。

|扩展类型|主题|每个组件通常声明的方式|
|--------------------|-----------|----------------------------------------------|
|菜单命令|[在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)|`[ClassDesignerExtension]`<br /><br /> `// or other diagram types`<br /><br /> `[Export(typeof(ICommandExtension))]`<br /><br /> `public class MyCommand : ICommandExtension`<br /><br /> `{...`|
|拖放或双击|[在建模图上定义笔势处理程序](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)|`[ClassDesignerExtension]`<br /><br /> `// or other diagram types`<br /><br /> `[Export(typeof(IGestureExtension))]`<br /><br /> `public class MyGesture : IGestureExtension`<br /><br /> `{...`|
|有效性约束|[为 UML 模型定义验证约束](../modeling/define-validation-constraints-for-uml-models.md)|`[Export(typeof(     System.Action<ValidationContext, object>))]`<br /><br /> `[ValidationMethod(ValidationCategories.Save`<br /><br /> `&#124; ValidationCategories.Menu)]`<br /><br /> `public void ValidateSomething`<br /><br /> `(ValidationContext context, IClassifier elementToValidate)`<br /><br /> `{...}`|
|工作项链接事件处理程序|[定义工作项链接处理程序](../modeling/define-a-work-item-link-handler.md)|`[Export(typeof(ILinkedWorkItemExtension))]`<br /><br /> `public class MyWorkItemEventHandler : ILinkedWorkItemExtension`<br /><br /> `{...`|
|UML 配置文件|[定义用于扩展 UML 的配置文件](../modeling/define-a-profile-to-extend-uml.md)|（待定义）|
|工具箱项|[定义自定义建模工具箱项](../modeling/define-a-custom-modeling-toolbox-item.md)|（待定义）|

## <a name="running-an-extension-during-its-development"></a>在其开发期间运行扩展

#### <a name="to-run-an-extension-during-its-development"></a>在其开发期间运行扩展

1. 在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]**调试**"菜单中，选择"**启动调试**"。

     将生成项目，并且 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 的新实例将在实验模式下启动。

    - 或者可以选择“启动但不调试”。 这将减少启动该程序所花费的时间。

2. 创建或打开 Visual Studio 的实验实例中的一个建模项目并创建或打开一个关系图。

     你的扩展将进行加载并运行。

3. 如果使用了“启动但不调试” ，但想要使用调试器，请返回到 Visual Studio 的主实例。 在 **“调试”** 菜单上，单击 **“附加到进程”** 。 在对话框中，选择具有程序名 **devenv**的 Visual Studio 的实验实例。

## <a name="Installing"></a>安装和卸载扩展
 执行以下步骤以在你自己的计算机上或在其他计算机上的 Visual Studio 的主实例中运行你的扩展。

1. 在你的计算机中，找到由你的扩展项目生成的 **.vsix** 文件。

    1. 在“解决方案资源管理器”中，项目的快捷菜单上，选择“在 Windows 资源管理器中打开文件夹”。

    2. **\*\\** _项目_**中**查找文件 bin\\

2. 将 **.vsix** 文件复制到要安装该扩展的目标计算机。 该计算机可以是自己的计算机或其他计算机。

    - 目标计算机必须具有在 **source.extension.vsixmanifest** 的“安装目标”选项卡上指定的 Visual Studio 版本之一。

3. 在目标计算机上，打开 **.vsix** 文件，例如双击打开。

     “” 将会打开并安装扩展。

4. 启动或重新启动 Visual Studio。

#### <a name="to-uninstall-an-extension"></a>若要卸载扩展

1. 在 “工具”菜单上，单击“扩展和更新”。

2. 展开“已安装的扩展”。

3. 选择扩展，然后单击“卸载”。

   在极少数情况下，有错误的扩展无法加载并在错误窗口中创建报告，但不显示在扩展管理器中。 在这种情况下，可以通过从以下位置删除文件来删除扩展，其中 *% LocalAppData%* 通常为*DriveName*： \Users\\*UserName*\AppData\Local：

   *%LocalAppData%* **\Microsoft\VisualStudio\\[version]\Extensions**

## <a name="see-also"></a>请参阅
 [定义用于扩展 UML 的配置文件](../modeling/define-a-profile-to-extend-uml.md)[定义自定义建模工具箱项](../modeling/define-a-custom-modeling-toolbox-item.md)[为 UML 模型定义验证约束](../modeling/define-validation-constraints-for-uml-models.md)[在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)
