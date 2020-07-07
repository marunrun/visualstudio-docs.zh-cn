---
title: 演练：创建 SharePoint 项目扩展 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5df10e2da9e6b4c31894dce0669e9aa0e580b92f
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015070"
---
# <a name="walkthrough-create-a-sharepoint-project-extension"></a>演练：创建 SharePoint 项目扩展
  本演练演示如何创建 SharePoint 项目的扩展。 您可以使用项目扩展来响应项目级别的事件，例如，在添加、删除或重命名项目时。 还可以添加自定义属性，或在属性值更改时进行响应。 与项目项扩展不同，项目扩展不能与特定的 SharePoint 项目类型相关联。 当你创建项目扩展时，将在中打开任何类型的 SharePoint 项目时加载该扩展 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

 在本演练中，您将创建一个自定义布尔属性，该属性将添加到在中创建的任何 SharePoint 项目 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 当设置为**True**时，新属性会将 Images 资源文件夹添加到你的项目，或将其映射到你的项目。 如果设置为**False**，则删除 Images 文件夹（如果存在）。 有关详细信息，请参阅[如何：添加和删除映射文件夹](../sharepoint/how-to-add-and-remove-mapped-folders.md)。

 本演练演示了下列任务：

- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]为 SharePoint 项目创建扩展，以执行以下操作：

  - 将自定义项目属性添加到属性窗口。 属性适用于任何 SharePoint 项目。

  - 使用 SharePoint 项目对象模型将映射文件夹添加到项目。

  - 使用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 自动化对象模型（DTE）从项目中删除映射文件夹。

- 生成 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展（VSIX）包以部署项目属性的扩展程序集。

- 调试和测试项目属性。

## <a name="prerequisites"></a>先决条件
 若要完成本演练，开发计算机上需要以下组件：

- 支持的 [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] 、SharePoint 和版本 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

- [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]。 本演练使用中的**Vsix 项目**模板 [!INCLUDE[TLA2#tla_sdk](../sharepoint/includes/tla2sharptla-sdk-md.md)] 来创建用于部署项目属性扩展的 vsix 包。 有关详细信息，请参阅[在 Visual Studio 中扩展 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，您必须创建两个项目：

- 用于创建 VSIX 包以部署项目扩展的 VSIX 项目。

- 一个实现项目扩展的类库项目。

  通过创建项目开始演练。

#### <a name="to-create-the-vsix-project"></a>创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

3. 在 "**新建项目**" 对话框中，展开 " **Visual c #** " 或 " **Visual Basic** " 节点，然后选择 "**扩展性**" 节点。

    > [!NOTE]
    > 只有在安装 Visual Studio SDK 时，此节点才可用。 有关详细信息，请参阅本主题前面的先决条件部分。

4. 在对话框顶部，选择 .NET Framework 的版本列表中 **.NET Framework "4.5** "，然后选择 " **VSIX 项目**" 模板。

5. 在 "**名称**" 框中，输入**ProjectExtensionPackage**，然后选择 "**确定"** 按钮。

     **ProjectExtensionPackage**项目显示在**解决方案资源管理器**中。

#### <a name="to-create-the-extension-project"></a>创建扩展项目

1. 在**解决方案资源管理器**中，打开 "解决方案" 节点的快捷菜单，选择 "**添加**"，然后选择 "**新建项目**"。

2. 在 "**新建项目**" 对话框中，展开 " **Visual c #** " 或 " **Visual Basic** " 节点，然后选择 "**窗口**"。

3. 在对话框顶部，选择 ".NET Framework" 版本列表中 **.NET Framework "4.5** "，然后选择 **"类库" 项目模板**。

4. 在 "**名称**" 框中，输入**存在或者 projectextension.baseprojectextension**，然后选择 "**确定"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将**存在或者 projectextension.baseprojectextension**项目添加到解决方案，并打开默认的 Class1 代码文件。

5. 从项目中删除 Class1 代码文件。

## <a name="configure-the-project"></a>配置项目
 在编写代码以创建项目扩展之前，请向扩展项目添加代码文件和程序集引用。

#### <a name="to-configure-the-project"></a>配置项目

1. 将名为**CustomProperty**的代码文件添加到存在或者 projectextension.baseprojectextension 项目。

2. 打开**存在或者 projectextension.baseprojectextension**项目的快捷菜单，然后选择 "**添加引用**"。

3. 在 "**引用管理器-CustomProperty** " 对话框中，选择 "**框架**" 节点，然后选中 "System.componentmodel" 和 "system.web" 程序集旁边的复选框。

4. 选择 "**扩展**" 节点，选中 "VisualStudio" 和 "EnvDTE" 程序集旁边的复选框，然后选择 **"确定"** 按钮。

5. 在**解决方案资源管理器**的**存在或者 projectextension.baseprojectextension**项目的 "**引用**" 文件夹下，选择 " **EnvDTE**"。

6. 在 "**属性**" 窗口中，将 "**嵌入互操作类型**" 属性更改为 " **False**"。

## <a name="define-the-new-sharepoint-project-property"></a>定义新的 SharePoint 项目属性
 创建一个类，用于定义项目扩展和新项目属性的行为。 若要定义新的项目扩展，类实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 接口。 每当要定义 SharePoint 项目的扩展时，都要实现此接口。 此外，将添加 <xref:System.ComponentModel.Composition.ExportAttribute> 到类中。 此特性使 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 能够发现和加载您的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 实现。 将 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 类型传递给特性的构造函数。

#### <a name="to-define-the-new-sharepoint-project-property"></a>定义新的 SharePoint 项目属性

1. 将以下代码粘贴到 CustomProperty 代码文件中。

     [!code-vb[SPExt_ProjectExtension#1](../sharepoint/codesnippet/VisualBasic/projectextension/customproperty.vb#1)]
     [!code-csharp[SPExt_ProjectExtension#1](../sharepoint/codesnippet/CSharp/projectextension/customproperty.cs#1)]

## <a name="build-the-solution"></a>生成解决方案
 接下来，生成解决方案，确保它在编译时不会出错。

#### <a name="to-build-the-solution"></a>生成解决方案

1. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

## <a name="create-a-vsix-package-to-deploy-the-project-property-extension"></a>创建 VSIX 包以部署项目属性扩展
 若要部署项目扩展，请使用解决方案中的 VSIX 项目创建 VSIX 包。 首先，通过修改 VSIX 项目中包含的 source.extension.vsixmanifest 文件来配置 VSIX 包。 然后，通过生成解决方案创建 VSIX 包。

#### <a name="to-configure-and-create-the-vsix-package"></a>配置和创建 VSIX 包

1. 在**解决方案资源管理器**中，打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择 "**打开**" 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]在清单设计器中打开文件。 "**元数据**" 选项卡中显示的信息也会出现在 "**扩展和更新**" 中。 所有 VSIX 包都需要 source.extension.vsixmanifest 文件。 有关此文件的详细信息，请参阅[VSIX 扩展架构1.0 引用](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)。

2. 在 "**产品名称**" 框中，输入 "**自定义项目属性**"。

3. 在 "**作者**" 框中，输入 " **Contoso**"。

4. 在 "**说明**" 框中，输入**一个自定义 SharePoint 项目属性，该属性将图像资源文件夹映射切换到项目**。

5. 选择 "**资产**" 选项卡，然后选择 "**新建**" 按钮。

     此时将显示 "**添加新资产**" 对话框。

6. 在 "**类型**" 列表中，选择 " **VisualStudio. microsoft.visualstudio.mefcomponent**"。

    > [!NOTE]
    > 此值与 `MEFComponent` source.extension.vsixmanifest 文件中的元素相对应。 此元素指定 VSIX 包中扩展程序集的名称。 有关详细信息，请参阅[Microsoft.visualstudio.mefcomponent 元素（VSX 架构）](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))。

7. 在 "**源**" 列表中，选择 "**当前解决方案中的项目**" 选项按钮。

8. 在 "**项目**" 列表中，选择 "**存在或者 projectextension.baseprojectextension**"。

     此值标识要在项目中生成的程序集的名称。

9. 选择 **"确定"** 以关闭 "**添加新资产**" 对话框。

10. 在菜单栏上，选择 "**文件**" "  >  **全部保存**" 完成操作，然后关闭清单设计器。

11. 在菜单栏上，选择 "**生成**" "生成  >  **解决方案**"，然后确保项目编译时不会出错。

12. 在**解决方案资源管理器**中，打开**ProjectExtensionPackage**项目的快捷菜单，然后选择 "**在文件资源管理器中打开文件夹**" 按钮。

13. 在**文件资源管理器**中，打开 ProjectExtensionPackage 项目的生成输出文件夹，然后验证该文件夹是否包含名为 ProjectExtensionPackage 的文件。

     默认情况下，生成输出文件夹为。包含项目文件的文件夹下的 \bin\Debug 文件夹。

## <a name="test-the-project-property"></a>测试项目属性
 你现在已准备好测试自定义项目属性。 最简单的方法是在的实验实例中调试和测试新的项目属性扩展 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 此实例 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 是在运行 VSIX 或其他扩展性项目时创建的。 调试项目后，可以在系统上安装该扩展，然后继续在的一个实例中对其进行调试和测试 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

#### <a name="to-debug-and-test-the-extension-in-an-experimental-instance-of-visual-studio"></a>在 Visual Studio 的实验实例中调试和测试扩展

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]用管理凭据重新启动，然后打开 ProjectExtensionPackage 解决方案。

2. 通过选择**F5**键，或在菜单栏上选择 "**调试**" "  >  **启动调试**"，启动项目的调试版本。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将扩展安装到%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Custom 项目 Property\1.0，并启动的实验实例 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

3. 在的实验实例中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，为场解决方案创建一个 SharePoint 项目，并对向导中的其他值使用默认值。

    1. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

    2. 在 "**新建项目**" 对话框的顶部，选择 .NET Framework 的版本列表中的 **.NET Framework 3.5** 。

         SharePoint 工具扩展需要此版本中的功能 [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)] 。

    3. 在 "**模板**" 节点下，展开 " **Visual c #** " 或 " **Visual Basic** " 节点，选择 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

    4. 选择 " **SharePoint 2010 项目**" 模板，然后输入**ModuleTest**作为项目名称。

4. 在**解决方案资源管理器**中，选择 " **ModuleTest** " 项目节点。

     "**属性**" 窗口中将显示一个新的自定义属性 "**地图图像" 文件夹**，默认值为 " **False**"。

5. 将该属性的值更改为**True**。

     将一个图像资源文件夹添加到 SharePoint 项目中。

6. 将该属性的值更改回**False**。

     如果在 "**删除图像" 文件夹**中选择 "**是"** 按钮，则会从 SharePoint 项目中删除 images 资源文件夹。

7. 关闭 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 的实验实例。

## <a name="see-also"></a>另请参阅
- [扩展 SharePoint 项目](../sharepoint/extending-sharepoint-projects.md)
- [如何：向 SharePoint 项目添加属性](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [在 SharePoint 项目系统类型和其他 Visual Studio 项目类型之间转换](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)
- [在 SharePoint 项目系统的扩展中保存数据](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)
- [将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
