---
title: 演练：SharePoint Designer 可重用工作流导入 Visual Studio |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: c7d1373339fac4768e2af1eda5770d5058ae8078
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63446603"
---
# <a name="walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio"></a>演练：导入 Visual Studio SharePoint Designer 可重用工作流
  本演练演示如何导入到的 SharePoint Designer 2010 中创建的可重用工作流[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]SharePoint 工作流项目。

 在 SharePoint Designer 中创建的工作流或*声明性工作流*，组成[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]语句而不是代码。 SharePoint Designer 2010 引入了*可重用工作流*，这是可由 SharePoint 站点中的不同列表的可移植的声明性工作流。

 在中创建的工作流[!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)]，例如顺序和状态机工作流，称为*代码工作流*。 代码工作流包含 XML 文件和代码模块中的用户可以自定义工作流的行为。

 Visual Studio 允许你在 SharePoint Designer 2010 中导入可重用工作流，并将其转换为代码工作流，以便在 SharePoint 网站中使用。

 本演练演示了下列任务：

- 在 SharePoint Designer 中创建简单的可重用工作流。

- 导出到 SharePoint Designer 可重用工作流 *.wsp*文件并在 SharePoint 中。

- 导入 *.wsp*文件到[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]使用导入可重用工作流项目。

- 通过添加代码来更改工作流。

- 在 SharePoint 站点中使用导入工作流。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- 支持的版本[!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)]和 SharePoint。

- Visual Studio。

- Microsoft [!INCLUDE[TLA2#tla_office](../sharepoint/includes/tla2sharptla-office-md.md)] SharePoint Designer 2010。

## <a name="create-target-sharepoint-subsites"></a>创建目标 SharePoint 子站点
 首先创建两个新的 SharePoint 子站点： 一个用于承载从 SharePoint Designer 中，另一个用于托管的转换后的工作流的可重用工作流。

#### <a name="to-create-sharepoint-subsites"></a>若要创建 SharePoint 子站点

1. 在 SharePoint Designer 2010，在菜单栏上，选择**文件** > **新建空白网站**。

2. 在中**新建空白网站**对话框中，浏览到 SharePoint 站点，你想要创建工作流，或使用值 http://<em>SystemName</em>/，然后选择**确定**按钮。

    将显示该主页。

3. 在中**子站点**部分中，选择**新建**按钮。

4. 在中**新建**对话框框中，选择**SharePoint 模板**从列表中的左窗格中，然后选择**团队网站**从右窗格中列表。

5. 中**指定的 Web 站点位置**框中，替换的单词**子站点**在 URL 中以**SPD1**，然后选择**确定**按钮。

    这将打开 SharePoint Designer 到新的子网站。 关闭 SharePoint Designer 的此实例，并返回到第一个实例 （顶层站点）。

6. 重复步骤 3-5，创建第二个子站点，这一次替换为单词**subsite**中[!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)]与**SPD2**。

## <a name="create-a-sharepoint-designer-reusable-workflow"></a>创建 SharePoint Designer 可重用工作流
 因为 SharePoint 中不包含任何可用于此示例中的可重用工作流，则将创建一个。 此简单的工作流用户具有特定标题的任务列表中输入新任务的任务分配给该用户。

#### <a name="to-create-a-sharepoint-designer-reusable-workflow"></a>若要创建 SharePoint Designer 可重用工作流

1. 在中**子站点**部分中，选择**SPD1**站点对其进行修改。

2. 在功能区中，选择**可重用工作流**按钮。

     创建可重用工作流向导会显示。

3. 在中**名称**框中，输入**SPD 任务工作流**。

4. 在中**内容类型**列表中，选择**任务**，然后选择**确定**按钮。

     在 SharePoint Designer 工作流设计器中打开工作流。

5. 在工作流设计器中，选择步骤 1，然后，在功能区中，依次选择**条件**按钮。

6. 在条件列表中，选择**如果当前项字段等于值**。

     此步骤将添加名为的条件**如果字段等于值**。

7. 在中**如果字段等于值**条件中，选择**字段**链接。

8. 在值列表中，选择**标题**。

9. 在中**如果字段等于值**条件中，选择**值**链接。

10. 在框中，输入**新的任务**。

     条件语句现在显示为**如果 Current Item: Title 等于新任务**。

11. 选择条件语句，下面的行，然后在功能区中选择**操作**按钮。

12. 在操作列表中，选择**中当前项的组字段**。

13. 在中**设置为值的字段**操作，选择**字段**链接，，然后在列表中，选择**分配给**。

14. 在**设置为值的字段**操作，选择**值**链接，，然后在现有的用户和组的列表中，选择**创建项用户**。

15. 选择**外**按钮，，然后选择**确定**按钮。

     操作语句现在显示为**将分配对象设置为当前项： 创建者**。

## <a name="save-and-deploy-the-reusable-workflow"></a>保存和部署可重用工作流
 因为[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]可以只导入 *.wsp*文件，您必须将保存为可重用工作流 *.wsp*文件，并在导入到之前将其部署到 SharePoint [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

> [!IMPORTANT]
> 如果收到运行时错误，执行以下过程，您必须能够访问 SharePoint 站点的系统上执行该过程。

#### <a name="to-save-and-deploy-the-reusable-workflow"></a>若要保存和部署可重用工作流

1. 在 SharePoint Designer 顶部，选择**保存**按钮来保存进度，，然后选择**发布**按钮以部署到工作流**SPD1** SharePoint 站点.

2. 在导航窗格中，选择**工作流**对象。

3. 下**可重用工作流**，选择**SPD 任务工作流**。

4. 在功能区中，选择**另存为模板**按钮以保存工作流作为 *.wsp*文件。

5. 打开**SPD1**在浏览器中查看的 SharePoint 站点 *.wsp*在 SharePoint 中的文件。

6. 在快速启动栏上依次选择**库**链接。

7. 在中**文档库**部分中，选择**站点资产**链接。

     **SPD 任务工作流**文件与其他站点资产一起列出。

8. 在文件列表中，选择该文件的名称

9. 在中**文件下载**对话框框中，选择**保存**按钮以保存 *.wsp*本地系统上的文件。

## <a name="import-the-wsp-file-into-visual-studio"></a>.Wsp 文件导入到 Visual Studio
 导入 *.wsp*文件到[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]使用导入可重用工作流项目。 此项目将在工作流代码工作流转换为可重用的声明性工作流。 转换工作流后，将使用代码来修改其行为。

#### <a name="to-import-a-workflow-from-a-wsp-file-and-modify-it"></a>若要从.wsp 文件导入工作流并对其进行修改

1. 在中[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，在菜单栏上依次选择**文件** > **新建** > **项目**。

2. 在中**新的项目**对话框框中，展开**SharePoint**下**Visual C#** 或**Visual Basic**，然后选择**2010年**节点。

3. 在**模板**窗格中，选择**导入可重用 SharePoint 2010 工作流**模板中，将作为项目的名称**WorkflowImportProject1**，然后选择**确定**按钮。

    SharePoint 自定义向导将显示。

4. 上**指定用于调试的网站和安全级别**页上，输入[!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)]第二个 SharePoint 子站点之前创建的： http://<em>系统名称</em>/SPD2。

5. 在中**此 SharePoint 解决方案的信任级别是什么？** 部分中，选择**部署为场解决方案**选项按钮，然后选择**下一步**按钮。

    有关沙盒的详细信息与场解决方案，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

6. 在中**指定新项目源**页上，浏览到以前保存的位置在系统上 *.wsp*文件，打开该文件，然后选择**下一步**按钮。

   > [!NOTE]
   > 选择**完成**按钮以导入中的所有可用项 *.wsp*文件。

    这将显示可用于导入可重用工作流的列表。

7. 在中**选择要导入的项**框中，选择**SPD 任务工作流**工作流，然后选择**完成**按钮。

    导入操作完成后，一个名为项目**WorkflowImportProject1**将创建包含名为工作流**SPD_Workflow_TestFT**。 在此文件夹是工作流的定义文件*Elements.xml*和工作流设计器文件 (*.xoml*)。 该设计器包含两个文件： 规则文件 (.rules) 和代码隐藏文件 (任一 *.cs*或 *.vb*，取决于你的项目的编程语言)。

8. 在中**解决方案资源管理器**，删除**其他已导入文件**文件夹。

9. 在中*Elements.xml*文件，请删除`InstantiationURL="_layouts/IniErkflIP.sspx"`。

10. 在中**解决方案资源管理器**，选择**WorkflowImportProject1**，然后在菜单栏上选择**项目** > **设为启动项目**若要设置**WorkflowImportProject1**为启动项。

     立即在调试项目时，这会显示的列表。

11. 因为**导入可重用 SharePoint 2010 工作流**模板不能导入已导入工作流的关联属性值，则必须输入它们。 具体方法为：

    1. 在中**解决方案资源管理器**，选择**SPD_Workflow_TestFT**节点。

    2. 选择省略号 (![ASP.NET 移动设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器椭圆")) 按钮旁边的一个列表属性，如**目标列表**属性。

    3. 在 SharePoint 自定义向导中，缺少的值填充，然后选择**完成**按钮。

12. 选择.xoml 文件，然后在菜单栏上选择**视图** > **设计器**若要在工作流设计器中查看已导入工作流。

13. 在中**Windows 工作流 v3.0**的节点**工具箱**，执行以下步骤之一：

    - 打开快捷菜单**代码**活动，然后选择**副本**。 在工作流设计器中，打开下方的行的快捷菜单**SequenceActivity1**活动，然后选择**粘贴**。

    - 拖动**代码**活动从**工具箱**到工作流设计器，并将其连接到下一行**SequenceActivity1**活动。

      这将活动添加到名为工作流设计器**CodeActivity1**。 在此活动中，您将添加在通知列表中创建一个公告，当用户开始工作流的代码操作。

14. 执行下面的某一组步骤：

    - 双击**CodeActivity1**以生成一个事件处理程序，并查看代码。

    - 在中**属性**窗口**CodeActivity1**，将的值设置**ExecuteCode**属性设置为**codeActivity_ExecuteCode**。

15. 现有下添加以下**使用**或**导入**语句：

     [!code-csharp[SP_SPDWFImport#1](../sharepoint/codesnippet/CSharp/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.cs#1)]
     [!code-vb[SP_SPDWFImport#1](../sharepoint/codesnippet/VisualBasic/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.vb#1)]

16. 替换为`codeActivity1_ExecuteCode`以下：

     [!code-csharp[SP_SPDWFImport#2](../sharepoint/codesnippet/CSharp/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.cs#2)]
     [!code-vb[SP_SPDWFImport#2](../sharepoint/codesnippet/VisualBasic/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.vb#2)]

## <a name="deploy-the-project-and-associate-the-workflow"></a>部署项目并将关联工作流
 接下来，运行 WorkflowImportProject1 将其部署到 SharePoint 站点，然后将该工作流关联的任务列表以查看和测试修改后，使用转换工作流。

#### <a name="to-deploy-the-project-and-associate-the-workflow"></a>若要部署该项目并将关联工作流

1. 在中[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，选择**F5**键以运行和部署转换的工作流项目。

2. 在快速启动栏上依次选择**任务**链接以显示任务列表。

3. 上**列表工具**选项卡上，选择**项**按钮，，然后选择**新项**按钮。

     **任务-新项**对话框随即打开。

4. 在中**标题**框中，输入**新任务**，然后选择**保存**按钮。

5. 上**列表工具**选项卡上，选择**列表**按钮，，然后选择**列表设置**按钮。

     **列表设置**页将出现。

6. 在中**权限和管理**部分中，选择**工作流设置**链接。

     **工作流设置**页将出现。

7. 选择**添加工作流**链接。

8. 在中**工作流**列表中，选择**WorkflowImportProject1-SPD 工作流测试**。

9. 在中**名称**框中，输入**SPD 工作流测试**，然后选择**确定**按钮。

10. 在快速启动栏中，选择**任务**列表。

11. 选择箭头旁边**新的任务**，然后在列表中，选择**工作流**。

12. 在中**启动新工作流**部分中，选择的链接**SPD 工作流测试**，然后选择**启动**按钮以启动工作流。

    > [!NOTE]
    > 或者，您可以自动关联工作流与列表运行工作流设置向导，并设置要自动关联的工作流。

     请注意，由工作流执行两项操作： 在任务中显示您的姓名**分配给**列中和公告将出现在**公告**列表。

## <a name="see-also"></a>请参阅
- [从现有的 SharePoint 网站导入项目](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [创建 web 部件或应用程序页的可重用的控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
