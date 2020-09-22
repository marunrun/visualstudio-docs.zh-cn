---
title: 扩展独立 Shell |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, isolated mode
ms.assetid: 9a641d8f-211e-4486-a1b1-4a89fafe7ee8
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ea55039de769598b26868727a93cfa11726e4838
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840485"
---
# <a name="extending-the-isolated-shell"></a>扩展独立 Shell
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过将 VSPackage、Managed Extensibility Framework (MEF) 组件部分或泛型 VSIX 项目添加到独立 shell 应用程序来扩展 Visual Studio 独立 shell。  
  
> [!NOTE]
> 以下步骤 presuppose 已使用 Visual Studio Shell 独立项目模板创建了一个基本的独立 shell 应用程序。 有关此项目模板的详细信息，请参阅 [演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。  
  
## <a name="locations-for-the-visual-studio-package-project-template"></a>Visual Studio 包项目模板的位置  
 可在“新建项目” **** 对话框中的三个不同位置找到 Visual Studio 包项目模板：  
  
1. 在 **Visual Basic**，可 **扩展性**。 项目的默认语言为 Visual Basic。  
  
2. 在 **Visual c #** 下，可 **扩展性**。 项目的默认语言为 C#。  
  
3. 在 **其他项目类型**下，可 **扩展性**。 项目的默认语言为 C++。  
  
## <a name="adding-a-vspackage"></a>添加 VSPackage  
 你可以将 VSPackage 添加到你的独立 shell 应用程序。 下面的步骤演示如何创建一个添加菜单命令的。  
  
#### <a name="to-add-a-new-vspackage"></a>添加新的 VSPackage  
  
1. 添加一个名为的 Visual Studio 包项目 `MenuCommandsPackage` 。  
  
2. 在向导的 " **基本 VSPackage 信息** " 页上，将 " **公司名称** " 设置为 `Fabrikam` ，并将 " **VSPackage 名称** " 设置为 `FabrikamMenuCommands` 。 选择“下一步”按钮  。  
  
3. 在下一页上，选择 " **菜单命令** "，然后选择 " **下一步**"。  
  
4. 在下一页上，将 " **命令名称** " 设置为，将 `Fabrikam Command` " **命令 ID** " 设置为 `cmdidFabrikamCommand` ，然后选择 " **下一步**"。  
  
5. 在 " **选择测试项目选项** " 页上，清除 "测试" 选项，然后选择 " **完成** " 按钮。  
  
6. 在 ShellExtensionsVSIX 项目中，打开 source.extension.vsixmanifest 文件。  
  
     " **资产** " 部分应包含 VSShellStub. AboutBoxPackage 项目的条目。  
  
7. 选择 " **新建** " 按钮。  
  
8. 在 " **添加新资产** " 窗口的 " **类型** " 列表中，选择 " **VisualStudio. VsPackage**"。  
  
9. 在 " **源** " 列表中，确保选择了 **当前解决方案中的项目** 。 在 " **项目** " 列表框中，选择 " **MenuCommandsPackage**"。  
  
10. 保存并关闭该文件。  
  
11. 重新生成解决方案并开始调试独立 shell。  
  
12. 在菜单栏上，依次选择 " **工具** " 菜单和 " **Fabrikam 命令**"。  
  
     应该会出现一个消息框。  
  
13. 停止调试应用程序。  
  
## <a name="adding-a-mef-component-part"></a>添加 MEF 组件部件  
 以下步骤演示如何将 MEF 组件部件添加到独立 shell 应用程序。  
  
#### <a name="to-add-a-mef-component"></a>添加 MEF 组件  
  
1. 在 " **添加新项目** " 对话框中的 " **Visual c #** **" 下，使用**" **编辑器边距** " 模板来添加项目。 将它命名为 `ShellEditorMargin`。  
  
2. 在 ShellExtensionsVSIX 项目中，打开设计视图而不是代码视图中的 source.extension.vsixmanifest 文件。  
  
3. 在 `Asset` 部分中，选择 " **添加内容**"。  
  
4. 在 " **添加新资产** " 窗口的 " **类型** " 列表中，选择 " **VisualStudio. microsoft.visualstudio.mefcomponent**"。  
  
5. 在 " **源** " 列表中，确保选择了 **当前解决方案中的项目** 。 在 " **项目** " 列表框中，选择 " **ShellEditorMargin**"。  
  
6. 保存并关闭该文件。  
  
7. 重新生成解决方案并开始调试独立 shell。  
  
8. 打开文本文件。  
  
     绿色边距，其中包含单词 "Hello world！" 应显示在 "文本文件" 窗口的底部。  
  
9. 停止调试应用程序。  
  
## <a name="adding-a-generic-vsix-project"></a>添加通用 VSIX 项目  
  
#### <a name="to-add-a-generic-vsix-project"></a>添加泛型 VSIX 项目  
  
1. 在 " **添加新项目** " 对话框中的 " **Visual c #** **" 下，使用**" **VSIXProject** " 模板来添加项目。 将它命名为 `EmptyVSIX`。  
  
2. 在 ShellExtensionsVSIX 项目中，打开设计视图而不是代码视图中的 source.extension.vsixmanifest 文件。  
  
3. 在 `Assets` 部分中，选择 " **新建**"。  
  
4. 在 " **添加新资产** " 窗口的 " **类型** " 列表中，选择要添加的内容类型。  
  
5. 在 " **源**" 中，确保已选择 " **当前解决方案中的项目** " 选项。 在列表框中，选择 VSIX 项目的名称。  
  
6. 保存并关闭该文件。  
  
7. 如果此项目包含编译的代码，您必须编辑该项目，以使该程序集包括在输出中。  
  
    1. 卸载 VSIX 项目并打开项目文件。  
  
    2. 在第一个 `<PropertyGroup>` 块中，将的值更改 `<CopyBuildOutputToOutputDirectory>` 为 `true` 。  
  
    3. 保存并重新加载项目。  
  
8. 生成并运行解决方案。  
  
## <a name="see-also"></a>另请参阅  
 [演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)
