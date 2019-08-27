---
title: 扩展独立的 Shell |Microsoft Docs
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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443918"
---
# <a name="extending-the-isolated-shell"></a>扩展独立的 Shell
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过将 VSPackage、 Managed Extensibility Framework (MEF) 组件一部分或一个普通的 VSIX 项目添加到独立的 shell 应用程序来扩展 Visual Studio 独立 shell。  
  
> [!NOTE]
> 以下步骤 presuppose 通过使用 Visual Studio Shell 独立的项目模板创建了一个基本的独立的 shell 应用程序。 有关此项目模板的详细信息，请参阅[演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。  
  
## <a name="locations-for-the-visual-studio-package-project-template"></a>Visual Studio 包项目模板的位置  
 可在“新建项目”  对话框中的三个不同位置找到 Visual Studio 包项目模板：  
  
1. 下**Visual Basic**，**扩展性**。 项目的默认语言为 Visual Basic。  
  
2. 下**Visual C#**，**扩展性**。 项目的默认语言为 C#。  
  
3. 下**其他项目类型**，**扩展性**。 项目的默认语言为 C++。  
  
## <a name="adding-a-vspackage"></a>添加 VSPackage  
 VSPackage 可以向独立的 shell 应用程序。 以下步骤说明如何创建一个添加菜单命令。  
  
#### <a name="to-add-a-new-vspackage"></a>若要添加新的 VSPackage  
  
1. 添加一个名为 Visual Studio 包项目`MenuCommandsPackage`。  
  
2. 上**基本 VSPackage 信息**页的向导中，设置**公司名称**到`Fabrikam`并**VSPackage 名称**到`FabrikamMenuCommands`。 选择“下一步”按钮。  
  
3. 在下一页上，选择**菜单命令**，然后选择**下一步**。  
  
4. 在下一步的页中，将**命令名称**到`Fabrikam Command`并**命令 ID**到`cmdidFabrikamCommand`，然后选择**下一步**。  
  
5. 上**选择测试项目选项**页上，清除测试选项，然后选择**完成**按钮。  
  
6. 在 ShellExtensionsVSIX 项目中，打开 source.extension.vsixmanifest 文件中。  
  
     **资产**部分应包含 VSShellStub.AboutBoxPackage 项目的条目。  
  
7. 选择**新建**按钮。  
  
8. 在中**添加新资产**窗口，请在**类型**列表中，选择**Microsoft.VisualStudio.VsPackage**。  
  
9. 在中**源**列表中，请确保**当前解决方案中的项目**处于选中状态。 在中**项目**列表框中，选择**MenuCommandsPackage**。  
  
10. 保存并关闭文件。  
  
11. 重新生成解决方案并启动调试的独立的 shell。  
  
12. 在菜单栏上依次选择**工具**菜单，然后**Fabrikam 命令**。  
  
     应出现一个消息框。  
  
13. 停止调试应用程序。  
  
## <a name="adding-a-mef-component-part"></a>添加 MEF 组件部分  
 以下步骤说明如何将 MEF 组件部分添加到独立的 shell 应用程序。  
  
#### <a name="to-add-a-mef-component"></a>若要添加的 MEF 组件  
  
1. 在中**添加新项目**对话框中的**Visual C#**，**扩展性**，使用**编辑器边距**模板将添加一个项目。 将其命名为 `ShellEditorMargin`。  
  
2. 在 ShellExtensionsVSIX 项目中，打开 Source.extension.vsixmanifest 文件中的在设计视图中，而不是代码视图。  
  
3. 在中`Asset`部分中，选择**添加内容**。  
  
4. 在中**添加新资产**窗口，请在**类型**列表中，选择**Microsoft.VisualStudio.MefComponent**。  
  
5. 在中**源**列表中，请确保**当前解决方案中的项目**处于选中状态。 在中**项目**列表框中，选择**ShellEditorMargin**。  
  
6. 保存并关闭文件。  
  
7. 重新生成解决方案并启动调试的独立的 shell。  
  
8. 打开一个文本文件。  
  
     包含单词"Hello world ！"的绿色边距 应显示在文本文件窗口的底部。  
  
9. 停止调试应用程序。  
  
## <a name="adding-a-generic-vsix-project"></a>添加泛型 VSIX 项目  
  
#### <a name="to-add-a-generic-vsix-project"></a>若要添加一个普通的 VSIX 项目  
  
1. 在中**添加新项目**对话框中的**Visual C#**，**扩展性**，使用**VSIXProject**模板将添加一个项目。 将其命名为 `EmptyVSIX`。  
  
2. 在 ShellExtensionsVSIX 项目中，打开设计视图，而不是代码视图中的 Source.extensions.vsixmanifest 文件。  
  
3. 在中`Assets`部分中，选择**新建**。  
  
4. 在中**添加新资产**窗口，请在**类型**列表中，选择你想要添加的内容类型。  
  
5. 在中**源**，请确保**当前解决方案中的项目**选择选项。 在列表框中，选择您的 VSIX 项目的名称。  
  
6. 保存并关闭文件。  
  
7. 如果此项目包含已编译的代码，必须编辑该项目，以便该程序集包含在输出中。  
  
    1. 卸载该 VSIX 项目并打开项目文件。  
  
    2. 在第一个`<PropertyGroup>`块中，更改的值`<CopyBuildOutputToOutputDirectory>`到`true`。  
  
    3. 保存并重新加载项目。  
  
8. 生成和运行解决方案。  
  
## <a name="see-also"></a>请参阅  
 [演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)
