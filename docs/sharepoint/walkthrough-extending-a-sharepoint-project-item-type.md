---
title: 演练：扩展 SharePoint 项目项类型 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], extending
- SharePoint project items, extending
- SharePoint development in Visual Studio, extending project items
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f949329c7db71386a12c3ab8d7fccf1483b8cca2
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015675"
---
# <a name="walkthrough-extend-a-sharepoint-project-item-type"></a>演练：扩展 SharePoint 项目项类型
  您可以使用 "**业务数据连接模型**" 项目项为 SharePoint 中的业务数据连接（BDC）服务创建模型。 默认情况下，当您使用此项目项创建模型时，不会向用户显示模型中的数据。 还必须在 SharePoint 中创建外部列表，以使用户能够查看数据。

 在本演练中，您将创建**业务数据连接模型**项目项的扩展。 开发人员可以使用该扩展在其项目中创建外部列表，该列表显示 BDC 模型中的数据。 本演练演示了下列任务：

- 创建执行两个主要任务的 Visual Studio 扩展：

  - 它将生成一个外部列表，其中显示 BDC 模型中的数据。 该扩展插件使用 SharePoint 项目系统的对象模型生成定义此列表的*Elements.xml*文件。 它还会将文件添加到项目中，以便与 BDC 模型一起部署。

  - 它将快捷菜单项添加到**解决方案资源管理器**中的**业务数据连接模型**项目项。 开发人员可以单击此菜单项，为 BDC 模型生成外部列表。

- 生成用于部署扩展程序集的 Visual Studio 扩展（VSIX）包。

- 测试扩展。

## <a name="prerequisites"></a>先决条件
 若要完成本演练，开发计算机上需要以下组件：

- 支持的 Microsoft Windows、SharePoint 和 Visual Studio 版本。

- [!include[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]。 本演练使用 SDK 中的**Vsix 项目**模板来创建用于部署项目项的 vsix 包。 有关详细信息，请参阅[在 Visual Studio 中扩展 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

  以下概念的知识非常有用，但不是必需的，无法完成本演练：

- 中的 BDC 服务 [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] 。 有关详细信息，请参阅[BDC 体系结构](/previous-versions/office/developer/sharepoint-2010/ee558876(v=office.14))。

- BDC 模型的 XML 架构。 有关详细信息，请参阅[BDC 模型基础结构](/previous-versions/office/developer/sharepoint-2010/ee556378(v=office.14))。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，需要创建两个项目：

- 用于创建 VSIX 包以部署项目项扩展的 VSIX 项目。

- 一个实现项目项扩展的类库项目。

  通过创建项目开始演练。

#### <a name="to-create-the-vsix-project"></a>创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

3. 在 "**新建项目**" 对话框中，展开 " **Visual c #** " 或 " **Visual Basic** " 节点，然后选择 "**扩展性**" 节点。

    > [!NOTE]
    > 只有在安装 Visual Studio SDK 时，"**扩展性**" 节点才可用。 有关详细信息，请参阅本主题前面的先决条件部分。

4. 在 "**新建项目**" 对话框顶部的列表中，选择 " **.NET Framework 4.5**"。

     SharePoint 工具扩展需要 .NET Framework 的此版本中的功能。

5. 选择 " **VSIX 项目**" 模板。

6. 在 "**名称**" 框中，输入**GenerateExternalDataLists**，然后选择 "**确定"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将**GenerateExternalDataLists**项目添加到**解决方案资源管理器**。

7. 如果 source.extension.vsixmanifest 文件未自动打开，请在 GenerateExternalDataLists 项目中打开其快捷菜单，然后选择 "**打开**"。

8. 验证 source.extension.vsixmanifest 文件的 "作者" 字段是否有一个非空白条目（输入 Contoso），保存该文件，然后将其关闭。

#### <a name="to-create-the-extension-project"></a>创建扩展项目

1. 在**解决方案资源管理器**中，打开**GenerateExternalDataLists**解决方案节点的快捷菜单，选择 "**添加**"，然后选择 "**新建项目**"。

2. 在 "**添加新项目**" 对话框中，展开 " **Visual c #** " 或 " **Visual Basic** " 节点，然后选择 " **Windows** " 节点。

3. 在对话框顶部的列表中，选择 " **.NET Framework 4.5**"。

4. 在项目模板列表中 **，选择 "类库"**。

5. 在 "**名称**" 框中，输入**BdcProjectItemExtension**，然后选择 "**确定"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将**BdcProjectItemExtension**项目添加到解决方案，并打开默认的 Class1 代码文件。

6. 从项目中删除 Class1 代码文件。

## <a name="configure-the-extension-project"></a>配置扩展项目
 在编写代码以创建项目项扩展之前，请向扩展项目添加代码文件和程序集引用。

#### <a name="to-configure-the-project"></a>配置项目

1. 在 BdcProjectItemExtension 项目中，添加两个具有以下名称的代码文件：

    - ProjectItemExtension

    - GenerateExternalDataLists

2. 选择 BdcProjectItemExtension 项目，然后在菜单栏上选择 "项目" " **Project**  >  **添加引用**"。

3. 在 "**程序集**" 节点下，选择 "**框架**" 节点，并选中以下每个程序集对应的复选框：

    - System.ComponentModel.Composition

    - WindowsBase

4. 在 "**程序集**" 节点下，选择 "**扩展**" 节点，然后选中以下程序集对应的复选框：

    - VisualStudio

5. 选择“确定”  按钮。

## <a name="define-the-project-item-extension"></a>定义项目项扩展
 创建一个类，用于定义**业务数据连接模型**项目项的扩展。 为了定义扩展，类实现了 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 接口。 每当要扩展现有类型的项目项时都实现此接口。

#### <a name="to-define-the-project-item-extension"></a>定义项目项扩展

1. 将以下代码粘贴到 ProjectItemExtension 代码文件中。

    > [!NOTE]
    > 添加此代码后，项目将会出现一些编译错误。 当你在后续步骤中添加代码时，这些错误将消失。

     [!code-csharp[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#1](../sharepoint/codesnippet/CSharp/generateexternaldatalists/bdcprojectitemextension/projectitemextension.cs#1)]
     [!code-vb[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#1](../sharepoint/codesnippet/VisualBasic/generateexternaldatalists/bdcprojectitemextension/projectitemextension.vb#1)]

## <a name="create-the-external-data-lists"></a>创建外部数据列表
 添加 `GenerateExternalDataListsExtension` 类的分部定义，该类为 BDC 模型中的每个实体创建外部数据列表。 若要创建外部数据列表，此代码首先通过分析 BDC 模型文件中的 XML 数据来读取 BDC 模型中的实体数据。 然后，它将创建一个基于 BDC 模型的列表实例，并将此列表实例添加到项目。

#### <a name="to-create-the-external-data-lists"></a>创建外部数据列表

1. 将以下代码粘贴到 GenerateExternalDataLists 代码文件中。

     [!code-vb[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#2](../sharepoint/codesnippet/VisualBasic/generateexternaldatalists/bdcprojectitemextension/generateexternaldatalists.vb#2)]
     [!code-csharp[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#2](../sharepoint/codesnippet/CSharp/generateexternaldatalists/bdcprojectitemextension/generateexternaldatalists.cs#2)]

## <a name="checkpoint"></a>检查点
 在本演练的此时，项目项扩展的所有代码现在都在项目中。 生成解决方案，确保项目编译时不会出错。

#### <a name="to-build-the-solution"></a>生成解决方案

1. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

## <a name="create-a-vsix-package-to-deploy-the-project-item-extension"></a>创建 VSIX 包以部署项目项扩展
 若要部署扩展，请使用解决方案中的 VSIX 项目创建 VSIX 包。 首先，通过修改 VSIX 项目中包含的 source.extension.vsixmanifest 文件来配置 VSIX 包。 然后，通过生成解决方案创建 VSIX 包。

#### <a name="to-configure-and-create-the-vsix-package"></a>配置和创建 VSIX 包

1. 在**解决方案资源管理器**中，在 GenerateExternalDataLists 项目中打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择 "**打开**"。

     Visual Studio 将在清单编辑器中打开该文件。 Source.extension.vsixmanifest 文件是 source.extension.vsixmanifest 文件的基础，所有 VSIX 包都需要此文件。 有关此文件的详细信息，请参阅[VSIX 扩展架构1.0 引用](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)。

2. 在 "**产品名称**" 框中，输入**外部数据列表生成器**。

3. 在 "**作者**" 框中，输入 " **Contoso**"。

4. 在 "**说明**" 框中，输入**可用于生成外部数据列表的业务数据连接模型项目项的扩展**。

5. 在编辑器的 "**资产**" 选项卡上，选择 "**新建**" 按钮。

     此时将显示 "**添加新资产**" 对话框。

6. 在 "**类型**" 列表中，选择 " **VisualStudio. microsoft.visualstudio.mefcomponent**"。

    > [!NOTE]
    > 此值与 `MefComponent` source.extension.vsixmanifest 文件中的元素相对应。 此元素指定 VSIX 包中扩展程序集的名称。 有关详细信息，请参阅[Microsoft.visualstudio.mefcomponent 元素（VSX 架构）](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))。

7. 在 "**源**" 列表中，选择 "**当前解决方案中的项目**"。

8. 在 "**项目**" 列表中，选择 " **BdcProjectItemExtension**"，然后选择 "**确定"** 按钮。

9. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

10. 请确保项目编译和生成时没有错误。

11. 请确保 GenerateExternalDataLists 项目的生成输出文件夹现在包含 GenerateExternalDataLists 文件。

     默认情况下，生成输出文件夹为。包含项目文件的文件夹下的 \bin\Debug 文件夹。

## <a name="test-the-project-item-extension"></a>测试项目项扩展
 你现在已准备好测试项目项扩展。 首先，开始调试 Visual Studio 的实验实例中的扩展项目。 然后，使用 Visual Studio 的实验实例中的扩展来生成 BDC 模型的外部列表。 最后，打开 SharePoint 站点上的外部列表以验证它是否按预期方式工作。

#### <a name="to-start-debugging-the-extension"></a>开始调试扩展

1. 如有必要，请重新启动具有管理凭据的 Visual Studio，然后打开 GenerateExternalDataLists 解决方案。

2. 在 BdcProjectItemExtension 项目中，打开 ProjectItemExtension 代码文件，然后将断点添加到方法中的代码行 `Initialize` 。

3. 打开 GenerateExternalDataLists 代码文件，然后将一个断点添加到方法中的第一行代码 `GenerateExternalDataLists_Execute` 。

4. 选择**F5**键，或在菜单栏上选择 "**调试**" "  >  **开始调试**"，开始调试。

     Visual Studio 会将扩展安装到%UserProfile%\AppData\Local\Microsoft\VisualStudio\10.0Exp\Extensions\Contoso\External Data List Generator\1.0，并启动 Visual Studio 的实验实例。 你将在 Visual Studio 的此实例中测试项目项。

#### <a name="to-test-the-extension"></a>测试扩展

1. 在 Visual Studio 的实验实例中，在菜单栏上选择 "**文件**" "  >  **新建**  >  **项目**"。

2. 在 "**新建项目**" 对话框中，展开 "**模板**" 节点，展开 " **Visual c #** " 节点，展开 " **SharePoint** " 节点，然后选择 " **2010**"。

3. 在对话框顶部的列表中，确保选择 " **.NET Framework 3.5** "。 的项目 [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] 需要此版本的 .NET Framework。

4. 在项目模板列表中，选择 " **SharePoint 2010 项目**"。

5. 在 "**名称**" 框中，输入**SharePointProjectTestBDC**，然后选择 "**确定"** 按钮。

6. 在 "SharePoint 自定义向导" 中，输入要用于调试的站点的 URL，选择 "**部署为场解决方案**"，然后选择 "**完成**" 按钮。

7. 打开 SharePointProjectTestBDC 项目的快捷菜单，选择 "**添加**"，然后选择 "**新建项**"。

8. 在 "**添加 NewItem-SharePointProjectTestBDC** " 对话框中，展开 "已安装的语言" 节点，展开 " **SharePoint** " 节点。

9. 选择 " **2010** " 节点，然后选择 "**业务数据连接模型（仅场解决方案）** " 模板。

10. 在 "**名称**" 框中，输入**TestBDCModel**，然后选择 "**添加**" 按钮。

11. 验证 Visual Studio 的另一个实例中的代码是否在 ProjectItemExtension 代码文件的方法中设置的断点处停止 `Initialize` 。

12. 在 Visual Studio 的停止实例中，选择**F5**键，或在菜单栏上，选择 "**调试**  >  **继续**" 继续调试项目。

13. 在 Visual Studio 的实验实例中，选择**F5**键，或在菜单栏上选择 "**调试**" "  >  **开始调试**" 以生成、部署和运行**TestBDCModel**项目。

     Web 浏览器将打开到为调试指定的 SharePoint 站点的默认页。

14. 验证 "快速启动" 区域中的 "**列表**" 部分尚未包含基于项目中默认 BDC 模型的列表。 您必须首先使用 SharePoint 用户界面或使用项目项扩展创建外部数据列表。

15. 关闭 Web 浏览器。

16. 在已打开 TestBDCModel 项目的 Visual Studio 实例中，打开**解决方案资源管理器**中 " **TestBDCModel** " 节点的快捷菜单，然后选择 "**生成外部数据列表**"。

17. 验证在 Visual Studio 的另一个实例中的代码是否在您在方法中设置的断点处停止 `GenerateExternalDataLists_Execute` 。 选择**F5**键，或在菜单栏上选择 "**调试**  >  **继续**" 以继续调试项目。

18. Visual Studio 的实验实例会将名为**Entity1DataList**的列表实例添加到 TestBDCModel 项目，并且该实例还会生成一个名为**Feature2**的列表实例的功能。

19. 选择**F5**键，或在菜单栏上选择 "**调试**" "  >  **开始调试**" 以生成、部署和运行 TestBDCModel 项目。

     Web 浏览器将打开用于调试的 SharePoint 站点的默认页面。

20. 在 "快速启动" 区域的 "**列表**" 部分中，选择 " **Entity1DataList** " 列表。

21. 验证该列表是否包含名为 Identifier1 和 Message 的列，以及一个具有 Identifier1 值0的项以及 Hello World 的消息值。

     "**业务数据连接模型**" 项目模板生成提供所有这些数据的默认 BDC 模型。

22. 关闭 Web 浏览器。

## <a name="clean-up-the-development-computer"></a>清理开发计算机
 完成项目项扩展测试后，从 SharePoint 站点中删除外部列表和 BDC 模型，并从 Visual Studio 中删除项目项扩展。

#### <a name="to-remove-the-external-data-list-from-the-sharepoint-site"></a>从 SharePoint 站点中删除外部数据列表

1. 在 SharePoint 站点的 "快速启动" 区域中，选择 " **Entity1DataList** " 列表。

2. 在 SharePoint 站点上的功能区中，选择 "**列表**" 选项卡。

3. 在 "**列表**" 选项卡上的 "**设置**" 组中，选择 "**列表设置**"。

4. 在 "**权限和管理**" 下，选择 "**删除此列表**"，然后选择 **"确定"** 以确认要将列表发送到回收站。

5. 关闭 Web 浏览器。

#### <a name="to-remove-the-bdc-model-from-the-sharepoint-site"></a>从 SharePoint 站点中删除 BDC 模型

1. 在 Visual Studio 的实验实例中，在菜单栏上选择 "**生成**  >  **收回**"。

     Visual Studio 将从 SharePoint 站点中删除 BDC 模型。

#### <a name="to-remove-the-project-item-extension-from-visual-studio"></a>从 Visual Studio 中删除项目项扩展

1. 在 Visual Studio 的实验实例中，在菜单栏上选择 "**工具**" "  >  **扩展和更新**"。

     此时，“扩展和更新”**** 对话框打开。

2. 在扩展列表中，选择 "**外部数据列表生成器**"，然后选择 "**卸载**" 按钮。

3. 在出现的对话框中，选择 **"是"** 以确认要卸载该扩展。

4. 选择 "**立即重新启动**" 以完成卸载。

5. 关闭 Visual Studio 的两个实例（实验实例和 GenerateExternalDataLists 解决方案打开的实例）。

## <a name="see-also"></a>另请参阅
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
- [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
