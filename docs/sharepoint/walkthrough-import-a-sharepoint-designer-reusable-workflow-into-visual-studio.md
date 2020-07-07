---
title: 演练：将 SharePoint Designer 可重用工作流导入 Visual Studio |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.WSPImport.ImportWF
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing reusable workflows
- reusable workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6a589f14ea60d50c0062d85be81523f27c81b455
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015697"
---
# <a name="walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio"></a>演练：将 SharePoint Designer 可重用工作流导入 Visual Studio
  本演练演示如何将在 SharePoint Designer 2010 中创建的可重用工作流导入到 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] sharepoint 工作流项目中。

 在 SharePoint 设计器或*声明性工作流*中创建的工作流由 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 语句而不是代码组成。 SharePoint Designer 2010 引入了可移植的*工作流，这些工作流*可供 SharePoint 站点中的不同列表使用。

 在中创建的工作流（ [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] 例如顺序和状态机工作流）称为 "*代码工作*流"。 代码工作流由 XML 文件和代码模块组成，用户可以在其中自定义工作流的行为。

 Visual Studio 允许你在 SharePoint Designer 2010 中导入可重用工作流，并将其转换为代码工作流，以便在 SharePoint 网站中使用。

 本演练演示了下列任务：

- 在 SharePoint 设计器中创建一个简单的可重用工作流。

- 将 SharePoint Designer 可重用工作流导出到 *.wsp*文件和 sharepoint。

- *.wsp* [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 使用 "导入可重用工作流" 项目将 .wsp 文件导入到中。

- 通过添加代码来更改工作流。

- 在 SharePoint 站点中使用导入的工作流。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- 支持的 [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] 和 SharePoint 版本。

- Visual Studio。

- Microsoft [!INCLUDE[TLA2#tla_office](../sharepoint/includes/tla2sharptla-office-md.md)] SharePoint Designer 2010。

## <a name="create-target-sharepoint-subsites"></a>创建目标 SharePoint 子网站
 首先，创建两个新的 SharePoint 子网站：一个用于托管 SharePoint 设计器中的可重用工作流，另一个用于托管转换后的工作流。

#### <a name="to-create-sharepoint-subsites"></a>创建 SharePoint 子网站

1. 在 SharePoint Designer 2010 的菜单栏上，选择 "**文件**" "  >  **新建空白**网站"。

2. 在 "**新建空白网站**" 对话框中，浏览到要在其中创建工作流的 SharePoint 站点，或使用 http://<em>SystemName</em>/的值，然后选择 "**确定"** 按钮。

    此时将显示 "主页"。

3. 在 "**子站点**" 部分中，选择 "**新建**" 按钮。

4. 在 "**新建**" 对话框中，从左侧窗格的列表中选择 " **SharePoint 模板**"，然后从右窗格的列表中选择 "**团队网站**"。

5. 在 "**指定网站的位置**" 框中，将 URL 中的**word 子网站**替换为**SPD1**，然后选择 **"确定"** 按钮。

    这会在 SharePoint Designer 中打开新的子网站。 关闭此 SharePoint 设计器实例，并返回到第一个实例（顶层站点）。

6. 重复步骤 3-5 以创建第二个子网站，这次将替换中的 word**子站点**替换为 [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] **SPD2**。

## <a name="create-a-sharepoint-designer-reusable-workflow"></a>创建 SharePoint 设计器可重用工作流
 由于 SharePoint 不包含可用于此示例的任何可重用工作流，因此你将创建一个。 在此简单工作流中，当用户在任务列表中输入具有特定标题的新任务时，会将该任务分配给该用户。

#### <a name="to-create-a-sharepoint-designer-reusable-workflow"></a>创建 SharePoint 设计器可重用工作流

1. 在 "**子**站点" 部分中，选择**SPD1**站点进行修改。

2. 在功能区上，选择 "**可重用工作流**" 按钮。

     此时将显示 "创建可重用工作流向导"。

3. 在 "**名称**" 框中，输入 " **SPD 任务工作流**"。

4. 在 "**内容类型**" 列表中，选择 "**任务**"，然后选择 **"确定"** 按钮。

     工作流在 SharePoint 设计器工作流设计器中打开。

5. 在工作流设计器中，选择 "步骤 1"，然后在功能区上选择 "**条件**" 按钮。

6. 在条件列表中，选择 "**如果当前项字段等于值**"。

     此步骤添加一个名为 "**如果字段等于值**" 的条件。

7. 在 "**如果字段等于值**" 条件中，选择**字段**链接。

8. 在值列表中，选择 "**标题**"。

9. 在 "**如果字段等于值**" 条件中，选择 "**值**" 链接。

10. 在框中，输入 "**新建任务**"。

     **如果当前项：标题等于新任务**，则 condition 语句现在会读取。

11. 选择 condition 语句下的行，然后在功能区上选择 "**操作**" 按钮。

12. 在操作列表中，选择 "**在当前项中设置字段**"。

13. 在 "**将字段设置为值**" 操作中，选择 "**字段**" 链接，然后在列表中选择 "**分配给**"。

14. 在 "**将字段设置为值**" 操作中，选择 "**值**" 链接，然后在现有用户和组的列表中，选择 **"创建项目的用户**"。

15. 选择 "**添加**" 按钮，然后选择 **"确定"** 按钮。

     操作语句现在读取**分配到设置为当前项： system.createdby**。

## <a name="save-and-deploy-the-reusable-workflow"></a>保存并部署可重用工作流
 由于 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 只能导入 *.wsp*文件，因此必须先将可重用工作流保存为 *.wsp*文件，然后将其部署到 SharePoint，然后再将其导入 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

> [!IMPORTANT]
> 如果在执行以下过程时收到运行时错误，则必须在对 SharePoint 站点具有访问权限的系统上执行该过程。

#### <a name="to-save-and-deploy-the-reusable-workflow"></a>保存和部署可重用工作流

1. 在 SharePoint 设计器的顶部，选择 "**保存**" 按钮以保存进度，然后选择 "**发布**" 按钮将工作流部署到**SPD1** SharePoint 站点。

2. 在导航窗格中，选择 "**工作流**" 对象。

3. 在 "**可重用工作流**" 下，选择 " **SPD 任务工作流**"。

4. 在功能区上，选择 "**另存为模板**" 按钮将工作流另存为 *.wsp*文件。

5. 在浏览器中打开**SPD1** sharepoint 站点以查看 sharepoint 中的 *.wsp*文件。

6. 在快速启动栏上，选择 "**库**" 链接。

7. 在 "**文档库**" 部分中，选择 "**站点资产**" 链接。

     **SPD 任务工作流**文件与其他站点资产一起列出。

8. 在文件列表中，选择该文件的名称

9. 在 "**文件下载**" 对话框中，选择 "**保存**" 按钮以在本地系统上保存 *.wsp*文件。

## <a name="import-the-wsp-file-into-visual-studio"></a>将 .wsp 文件导入 Visual Studio
 使用 " *.wsp* [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 导入可重用工作流" 项目将 .wsp 文件导入到中。 此项目将工作流从可重用的声明性工作流转换为代码工作流。 转换工作流后，你将使用代码来修改其行为。

#### <a name="to-import-a-workflow-from-a-wsp-file-and-modify-it"></a>导入 .wsp 文件中的工作流并对其进行修改

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 的菜单栏上，选择 "**文件**" "  >  **新建**  >  **项目**"。

2. 在 "**新建项目**" 对话框中，展开 " **Visual c #** " 或 " **Visual Basic**" 下的 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

3. 在 "**模板**" 窗格中，选择 "**导入可重用的 SharePoint 2010 工作流**" 模板，将项目名称保留为 " **WorkflowImportProject1**"，然后选择 **"确定"** 按钮。

    “SharePoint 自定义向导”随即出现。

4. 在 "**指定用于调试的站点和安全级别**" 页上， [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] 为之前创建的第二个 SharePoint 子站点输入： Http://<em>system name</em>/SPD2。

5. 在 "**此 SharePoint 解决方案的信任级别是什么？** " 部分中，选择 "**部署为场解决方案**" 选项按钮，然后选择 "**下一步**" 按钮。

    有关沙盒解决方案与场解决方案的详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

6. 在 "**指定新的项目源**" 页上，浏览到系统上你之前保存 *.wsp*文件的位置，打开文件，然后选择 "**下一步**" 按钮。

   > [!NOTE]
   > 选择 "**完成**" 按钮以导入 *.wsp*文件中的所有可用项。

    这会显示可用于导入的可重用工作流的列表。

7. 在 "**选择要导入的项**" 框中，选择 " **SPD 任务工作**流"，然后选择 "**完成**" 按钮。

    导入操作完成后，将创建一个名为**WorkflowImportProject1**的项目，其中包含一个名为**SPD_Workflow_TestFT**的工作流。 在此文件夹中，工作流的定义文件*Elements.xml*和工作流设计器文件（*. xoml*）。 设计器包含两个文件：规则文件（. 规则）和代码隐藏文件（ *.cs*或 *.vb*，具体取决于项目的编程语言）。

8. 在**解决方案资源管理器**中，删除 "**其他已导入文件**" 文件夹。

9. 在*Elements.xml*文件中，删除 `InstantiationURL="_layouts/IniErkflIP.sspx"` 。

10. 在**解决方案资源管理器**中，选择 " **WorkflowImportProject1**"，然后在菜单栏上选择 "**项目**  >  **设置为启动项目**"，将 " **WorkflowImportProject1** " 设置为 "启动项目"。

     调试项目时，这会立即显示列表。

11. 因为 "**导入可重用的 SharePoint 2010 工作流**" 模板不会导入导入工作流的关联属性值，所以必须输入这些值。 为此，请按以下步骤操作：

    1. 在**解决方案资源管理器**中，选择 " **SPD_Workflow_TestFT** " 节点。

    2. 选择其中一个列表属性（如 "**目标列表**" 属性）旁边的省略号（![ASP.NET Mobile 设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")）按钮。

    3. 在 SharePoint 自定义向导中填写缺少的值，然后选择 "**完成**" 按钮。

12. 选择 xoml 文件，然后在菜单栏上选择 "**视图**  >  **设计器**" 以在工作流设计器中查看导入的工作流。

13. 在 "**工具箱**" 的 " **Windows Workflow v3.0** " 节点中，执行以下步骤之一：

    - 打开 "**代码**" 活动的快捷菜单，然后选择 "**复制**"。 在工作流设计器中，打开 " **SequenceActivity1** " 活动下的行的快捷菜单，然后选择 "**粘贴**"。

    - 将 "**代码**" 活动从 "**工具箱**" 拖动到工作流设计器，并将其连接到 " **SequenceActivity1** " 活动下的行。

      这会将活动添加到名为**CodeActivity1**的工作流设计器中。 在此活动中，你将添加一个代码操作，该操作在用户启动工作流时在 "公告" 列表中创建公告。

14. 执行下面的某一组步骤：

    - 双击 " **CodeActivity1** " 以生成事件处理程序并查看代码。

    - 在**CodeActivity1**的 "**属性**" 窗口中，将 " **ExecuteCode** " 属性的值设置为 " **codeActivity_ExecuteCode**"。

15. 在现有**using**或**Imports**指令下添加以下内容：

     [!code-csharp[SP_SPDWFImport#1](../sharepoint/codesnippet/CSharp/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.cs#1)]
     [!code-vb[SP_SPDWFImport#1](../sharepoint/codesnippet/VisualBasic/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.vb#1)]

16. `codeActivity1_ExecuteCode`将替换为以下内容：

     [!code-csharp[SP_SPDWFImport#2](../sharepoint/codesnippet/CSharp/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.cs#2)]
     [!code-vb[SP_SPDWFImport#2](../sharepoint/codesnippet/VisualBasic/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.vb#2)]

## <a name="deploy-the-project-and-associate-the-workflow"></a>部署项目并关联工作流
 接下来，运行 WorkflowImportProject1 以将其部署到 SharePoint 站点，然后将该工作流与 "任务" 列表相关联，以查看和测试已修改的已转换工作流。

#### <a name="to-deploy-the-project-and-associate-the-workflow"></a>部署项目并关联工作流

1. 在中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，选择**F5**键以运行并部署转换后的工作流项目。

2. 在快速启动栏上，选择 "**任务**" 链接以显示 "任务" 列表。

3. 在 "**列表工具**" 选项卡上，选择 "**项**" 按钮，然后选择 "**新建项**" 按钮。

     此时将打开 "**任务-新建项目**" 对话框。

4. 在 "**标题**" 框中，输入 "**新任务**"，然后选择 "**保存**" 按钮。

5. 在 "**列表工具**" 选项卡上，选择 "**列表**" 按钮，然后选择 "**列表设置**" 按钮。

     此时将显示 "**列表设置**" 页。

6. 在 "**权限和管理**" 部分中，选择 "**工作流设置**" 链接。

     此时将显示 "**工作流设置**" 页。

7. 选择 "**添加工作流**" 链接。

8. 在**工作流**列表中，选择 " **WorkflowImportProject1-SPD 工作流测试**"。

9. 在 "**名称**" 框中，输入 " **SPD 工作流测试**"，然后选择 **"确定"** 按钮。

10. 在快速启动栏中，选择 "**任务**" 列表。

11. 选择 "**新建任务**" 旁边的箭头，然后在列表中选择 "**工作流**"。

12. 在 "**启动新工作流**" 部分中，选择 " **SPD 工作流测试**" 链接，然后选择 "**启动**" 按钮以启动工作流。

    > [!NOTE]
    > 或者，您可以通过运行工作流设置向导并将工作流设置为 "自动关联"，自动将工作流与列表相关联。

     请注意，工作流执行两个操作：你的名称显示在任务的 "**分配到**" 列中，"**公告**" 列表中会显示一条公告。

## <a name="see-also"></a>另请参阅
- [从现有 SharePoint 站点导入项](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [为 web 部件或应用程序页创建可重用控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
