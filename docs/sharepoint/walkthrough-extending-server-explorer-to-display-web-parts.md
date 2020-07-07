---
title: 演练：扩展要显示 Web 部件的服务器资源管理器 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint commands
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5e5221d1cce065a352051ca700cf0fc5ef4ae843
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015631"
---
# <a name="walkthrough-extend-server-explorer-to-display-web-parts"></a>演练：扩展服务器资源管理器以显示 web 部件
  在 Visual Studio 中，可以使用**服务器资源管理器**的 " **sharepoint 连接**" 节点来查看 SharePoint 站点上的组件。 但是，默认情况下**服务器资源管理器**不显示某些组件。 在本演练中，您将扩展**服务器资源管理器**以便它在每个连接的 SharePoint 站点上显示 Web 部件库。

 本演练演示了下列任务：

- 创建可通过以下方式扩展**服务器资源管理器**的 Visual Studio 扩展：

  - 该扩展在**服务器资源管理器**中的每个 SharePoint 站点节点下添加一个**Web 部件库**节点。 此新节点包含表示站点上 Web 部件库中的每个 Web 部件的子节点。

  - 扩展定义了表示 Web 部件实例的新节点类型。 此新节点类型是 "新建**Web 部件库**" 节点下的子节点的基础。 新 Web 部件节点类型在 "**属性**" 窗口中显示有关它所表示的 Web 部件的信息。 节点类型还包括一个自定义快捷菜单项，您可以将其用作执行与 Web 部件相关的其他任务的起点。

- 创建扩展程序集调用的两个自定义 SharePoint 命令。 SharePoint 命令是扩展程序集可以调用的方法，以在 SharePoint 的服务器对象模型中使用 Api。 在本演练中，您将创建用于从开发计算机上的本地 SharePoint 站点检索 Web 部件信息的命令。 有关详细信息，请参阅[调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

- 生成用于部署扩展的 Visual Studio 扩展（VSIX）包。

- 调试和测试扩展。

> [!NOTE]
> 对于本演练的替代版本，该版本使用 SharePoint 的客户端对象模型而不是其服务器对象模型，请参阅[演练：在服务器资源管理器扩展中调入 SharePoint 客户端对象模型](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)。

## <a name="prerequisites"></a>先决条件
 若要完成本演练，开发计算机上需要以下组件：

- 受支持的 Windows、SharePoint 和 Visual Studio 版本。

- Visual Studio SDK。 本演练使用 SDK 中的**Vsix 项目**模板来创建用于部署项目项的 vsix 包。 有关详细信息，请参阅[在 Visual Studio 中扩展 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

  以下概念的知识非常有用，但不是必需的，无法完成本演练：

- 使用 SharePoint 的服务器对象模型。 有关详细信息，请参阅[使用 SharePoint Foundation 服务器端对象模型](/previous-versions/office/developer/sharepoint-2010/ee538251(v=office.14))。

- SharePoint 解决方案中的 Web 部件。 有关详细信息，请参阅[Web 部件概述](/previous-versions/office/ms432401(v=office.14))。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，必须创建三个项目：

- 用于创建 VSIX 包以部署扩展的 VSIX 项目。

- 实现扩展的类库项目。 此项目必须针对 .NET Framework 4.5。

- 用于定义自定义 SharePoint 命令的类库项目。 此项目必须以 the.NET Framework 3.5 为目标。

  通过创建项目开始演练。

#### <a name="to-create-the-vsix-project"></a>创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

3. 在 "**新建项目**" 对话框中，展开 " **Visual c #** " 或 " **Visual Basic** " 节点，然后选择 "**扩展性**" 节点。

    > [!NOTE]
    > 只有在安装 Visual Studio SDK 时，"**扩展性**" 节点才可用。 有关详细信息，请参阅本主题前面的先决条件部分。

4. 在对话框顶部，选择 .NET Framework 的版本列表中 **.NET Framework "4.5** "。

5. 选择 " **VSIX 项目**" 模板，将项目命名为 " **WebPartNode**"，然后选择 **"确定"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将**WebPartNode**项目添加到**解决方案资源管理器**。

#### <a name="to-create-the-extension-project"></a>创建扩展项目

1. 在**解决方案资源管理器**中，打开 "解决方案" 节点的快捷菜单，选择 "**添加**"，然后选择 "**新建项目**"。

2. 在 "**新建项目**" 对话框中，展开 " **Visual c #** " 节点或**Visual Basic** "节点，然后选择" **Windows**节点 "。

3. 在对话框顶部，选择 .NET Framework 的版本列表中 **.NET Framework "4.5** "。

4. 在项目模板列表中，选择 "**类库**"，将项目命名为 " **WebPartNodeExtension**"，然后选择 **"确定"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将**WebPartNodeExtension**项目添加到解决方案，并打开默认的 Class1 代码文件。

5. 从项目中删除 Class1 代码文件。

#### <a name="to-create-the-sharepoint-commands-project"></a>创建 SharePoint 命令项目

1. 在**解决方案资源管理器**中，打开 "解决方案" 节点的快捷菜单，选择 "**添加**"，然后选择 "**新建项目**"。

2. 在 "**新建项目**" 对话框中，展开 " **Visual c #** " 节点或**Visual Basic** "节点，然后选择" **Windows** "节点。

3. 在对话框顶部，选择 .NET Framework 的版本列表中 **.NET Framework "3.5** "。

4. 在项目模板列表中，选择 "**类库**"，将项目命名为 " **WebPartCommands**"，然后选择 **"确定"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将**WebPartCommands**项目添加到解决方案，并打开默认的 Class1 代码文件。

5. 从项目中删除 Class1 代码文件。

## <a name="configure-the-projects"></a>配置项目
 在编写代码以创建扩展之前，你必须添加代码文件和程序集引用，并配置项目设置。

#### <a name="to-configure-the-webpartnodeextension-project"></a>配置 WebPartNodeExtension 项目

1. 在 WebPartNodeExtension 项目中，添加四个具有以下名称的代码文件：

    - SiteNodeExtension

    - WebPartNodeTypeProvider

    - WebPartNodeInfo

    - WebPartCommandIds

2. 打开**WebPartNodeExtension**项目的快捷菜单，然后选择 "**添加引用**"。

3. 在 "**引用管理器-WebPartNodeExtension** " 对话框中，选择 "**框架**" 选项卡，然后选中以下每个程序集对应的复选框：

    - System.ComponentModel.Composition

    - System.Windows.Forms

4. 选择 "**扩展**" 选项卡，选中 "VisualStudio" 程序集对应的复选框，然后选择 **"确定"** 按钮。

5. 在**解决方案资源管理器**中，打开**WebPartNodeExtension**项目节点的快捷菜单，然后选择 "**属性**"。

     将打开“项目设计器”****。

6. 选择“应用程序”**** 选项卡。

7. 在 "**默认命名空间**" 框（c #）或 "**根命名空间**" 框（ [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] ）中，输入**ServerExplorer. SharePointConnections. WebPartNode**。

#### <a name="to-configure-the-webpartcommands-project"></a>配置 webpartcommands 项目

1. 在 WebPartCommands 项目中，添加一个名为 WebPartCommands 的代码文件。

2. 在**解决方案资源管理器**中，打开**WebPartCommands**项目节点的快捷菜单，选择 "**添加**"，然后选择 "**现有项**"。

3. 在 "**添加现有项**" 对话框中，浏览到包含 WebPartNodeExtension 项目的代码文件的文件夹，然后选择 "WebPartNodeInfo" 和 "WebPartCommandIds" 代码文件。

4. 选择 "**添加**" 按钮旁边的箭头，然后在出现的菜单中选择 "**添加为链接**"。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将代码文件作为链接添加到 WebPartCommands 项目中。 因此，代码文件位于 WebPartNodeExtension 项目中，但文件中的代码也编译在 WebPartCommands 项目中。

5. 再次打开**WebPartCommands**项目的快捷菜单，然后选择 "**添加引用**"。

6. 在 "**引用管理器-WebPartCommands** " 对话框中，选择 "**扩展**" 选项卡，选中以下每个程序集对应的复选框，然后选择 "**确定"** 按钮：

    - Microsoft SharePoint

    - VisualStudio 命令

7. 在**解决方案资源管理器**中，再次打开**WebPartCommands**项目的快捷菜单，然后选择 "**属性**"。

     将打开“项目设计器”****。

8. 选择“应用程序”**** 选项卡。

9. 在 "**默认命名空间**" 框（c #）或 "**根命名空间**" 框（ [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] ）中，输入**ServerExplorer. SharePointConnections. WebPartNode**。

## <a name="create-icons-for-the-new-nodes"></a>创建新节点的图标
 为**服务器资源管理器**扩展创建两个图标： "新建**Web 部件库**" 节点的图标，以及 " **web 部件库**" 节点下的每个子 Web 部件节点的另一个图标。 稍后在本演练中，你将编写用于将这些图标与节点关联的代码。

#### <a name="to-create-icons-for-the-nodes"></a>创建节点的图标

1. 在**解决方案资源管理器**中，打开**WebPartNodeExtension**项目的快捷菜单，然后选择 "**属性**"。

2. 将打开“项目设计器”****。

3. 选择 "**资源**" 选项卡，然后选择 "**此项目不包含默认资源文件"。单击此处创建一个**链接。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]创建一个资源文件，并在设计器中将其打开。

4. 在设计器的顶部，选择 "**添加资源**" 菜单命令旁的箭头，然后在出现的菜单中选择 "**添加新图标**"。

5. 在 "**添加新资源**" 对话框中，将新图标命名为**WebPartsNode**，然后选择 "**添加**" 按钮。

     此时会在**图像编辑器**中打开 "新建" 图标。

6. 编辑该图标的16x16 版本，使其具有可轻松识别的设计。

7. 打开32x32 版图标的快捷菜单，然后选择 "**删除图像类型**"。

8. 重复步骤5到步骤8，将第二个图标添加到项目资源，并将其命名为 " **Web 部件**"。

9. 在**解决方案资源管理器**的 " **WebPartNodeExtension** " 项目的 "**资源**" 文件夹下，打开**WebPartsNode**的快捷菜单。

10. 在 "**属性**" 窗口中，选择 "**生成操作**" 旁边的箭头，然后在显示的菜单上选择 "**嵌入的资源**"。

11. 对于**WebPart**，重复最后两个步骤。

## <a name="add-the-web-part-gallery-node-to-server-explorer"></a>将 Web 部件库节点添加到服务器资源管理器
 创建一个类，用于将新的**Web 部件库**节点添加到每个 SharePoint 站点节点。 为了添加新节点，类实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 接口。 每当要扩展**服务器资源管理器**中现有节点的行为（例如，将子节点添加到节点）时，请实现此接口。

#### <a name="to-add-the-web-part-gallery-node-to-server-explorer"></a>将 Web 部件库节点添加到服务器资源管理器

1. 在 WebPartNodeExtension 项目中，打开 SiteNodeExtension 代码文件，然后将以下代码粘贴到其中。

    > [!NOTE]
    > 添加此代码后，该项目将会出现一些编译错误，但当你在后续步骤中添加代码时，这些错误将消失。

     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#1](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/sitenodeextension.cs#1)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#1](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/sitenodeextension.vb#1)]

## <a name="define-a-node-type-that-represents-a-web-part"></a>定义表示 web 部件的节点类型
 创建一个类，用于定义表示 Web 部件的新类型的节点。 Visual Studio 使用此新节点类型显示 " **Web 部件库**" 节点下的子节点。 每个子节点表示 SharePoint 站点上的单个 Web 部件。

 若要定义新的节点类型，类实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 接口。 如果要在**服务器资源管理器**中定义新类型的节点，请实现此接口。

#### <a name="to-define-the-web-part-node-type"></a>定义 web 部件节点类型

1. 在 WebPartNodeExtension 项目中，打开 WebPartNodeTypeProvder 代码文件，然后将以下代码粘贴到其中。

     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#2](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartnodetypeprovider.vb#2)]
     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#2](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartnodetypeprovider.cs#2)]

## <a name="define-the-web-part-data-class"></a>定义 web 部件数据类
 定义一个包含有关 SharePoint 站点上单个 Web 部件的数据的类。 稍后在本演练中，将创建一个自定义 SharePoint 命令，该命令检索有关站点上的每个 Web 部件的数据，然后将数据分配给此类的实例。

#### <a name="to-define-the-web-part-data-class"></a>定义 web 部件数据类

1. 在 WebPartNodeExtension 项目中，打开 WebPartNodeInfo 代码文件，然后将以下代码粘贴到其中。

     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#3](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartnodeinfo.vb#3)]
     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#3](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartnodeinfo.cs#3)]

## <a name="define-the-ids-for-the-sharepoint-commands"></a>定义 SharePoint 命令的 Id
 定义几个标识自定义 SharePoint 命令的字符串。 稍后在本演练中将执行这些命令。

#### <a name="to-define-the-command-ids"></a>定义命令 Id

1. 在 WebPartNodeExtension 项目中，打开 WebPartCommandIds 代码文件，然后将以下代码粘贴到其中。

     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#4](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartcommandids.cs#4)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#4](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartcommandids.vb#4)]

## <a name="create-the-custom-sharepoint-commands"></a>创建自定义 SharePoint 命令
 创建调入 SharePoint 服务器对象模型的自定义命令，以检索有关 SharePoint 站点上的 Web 部件的数据。 每个命令都是一个应用了的方法 <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> 。

#### <a name="to-define-the-sharepoint-commands"></a>定义 SharePoint 命令

1. 在 WebPartCommands 项目中，打开 WebPartCommands 代码文件，然后将以下代码粘贴到其中。

     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#6](../sharepoint/codesnippet/CSharp/WebPartNode/WebPartCommands/WebPartCommands.cs#6)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#6](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartcommands/webpartcommands.vb#6)]

## <a name="checkpoint"></a>检查点
 在本演练的此时， **Web 部件库**节点和 SharePoint 命令的所有代码现在都在项目中。 生成解决方案，确保两个项目都在编译时不会出错。

#### <a name="to-build-the-solution"></a>生成解决方案

1. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

    > [!WARNING]
    > 此时，WebPartNode 项目可能会出现生成错误，因为 VSIX 清单文件没有作者的值。 在后续步骤中添加值时，此错误将消失。

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>创建 VSIX 包以部署扩展
 若要部署扩展，请使用解决方案中的 VSIX 项目创建 VSIX 包。 首先，通过修改 VSIX 项目中的 source.extension.vsixmanifest 文件来配置 VSIX 包。 然后，通过生成解决方案创建 VSIX 包。

#### <a name="to-configure-the-vsix-package"></a>配置 VSIX 包

1. 在**解决方案资源管理器**的 WebPartNode 项目下，在清单编辑器中打开**source.extension.vsixmanifest**文件。

     Source.extension.vsixmanifest 文件是所有 VSIX 包都需要的 source.extension.vsixmanifest 文件的基础。 有关此文件的详细信息，请参阅[VSIX 扩展架构1.0 引用](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)。

2. 在 "**产品名称**" 框中，输入**服务器资源管理器的 "Web 部件库" 节点**。

3. 在 "**作者**" 框中，输入 " **Contoso**"。

4. 在 "**说明**" 框中，输入**将 "自定义 Web 部件库" 节点添加到服务器资源管理器中的 "SharePoint 连接" 节点。此扩展插件使用自定义 SharePoint 命令调入服务器对象模型。**

5. 选择编辑器的 "**资产**" 选项卡，然后选择 "**新建**" 按钮。

     此时将显示 "**添加新资产**" 对话框。

6. 在 "**类型**" 列表中，选择 " **VisualStudio. microsoft.visualstudio.mefcomponent**"。

    > [!NOTE]
    > 此值与 `MefComponent` source.extension.vsixmanifest 文件中的元素相对应。 此元素指定 VSIX 包中扩展程序集的名称。 有关详细信息，请参阅[Microsoft.visualstudio.mefcomponent 元素（VSX 架构）](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))。

7. 在 "**源**" 列表中，选择 "**当前解决方案中的项目**"。

8. 在 "**项目**" 列表中，选择 " **WebPartNodeExtension** "，然后选择 "**确定"** 按钮。

9. 在清单编辑器中，再次选择 "**新建**" 按钮。

     此时将显示 "**添加新资产**" 对话框。

10. 在 "**类型**" 框中 **，输入 "node.js"。**

    > [!NOTE]
    > 此元素指定要包含在 Visual Studio 扩展中的自定义扩展。 有关详细信息，请参阅[资产元素（VSX Schema）](https://msdn.microsoft.com/9fcfc098-edc7-484b-9d4c-acd17829d737)。

11. 在 "**源**" 列表中，选择 "**当前解决方案中的项目**" 列表项。

12. 在 "**项目**" 列表中，选择 " **WebPartCommands**"，然后选择 "**确定"** 按钮。

13. 在菜单栏上，选择 "**生成**" "生成  >  **解决方案**"，然后确保解决方案在编译时不会出错。

14. 请确保 WebPartNode 项目的生成输出文件夹现在包含 WebPartNode 文件。

     默认情况下，生成输出文件夹为。包含项目文件的文件夹下的 \bin\Debug 文件夹。

## <a name="test-the-extension"></a>测试扩展
 你现在已准备好在**服务器资源管理器**中测试新的**Web 部件库**节点。 首先，开始在 Visual Studio 的实验实例中调试扩展。 然后，使用的实验实例中的新**Web 部件**节点 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

#### <a name="to-start-debugging-the-extension"></a>开始调试扩展

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]用管理凭据重新启动，然后打开 WebPartNode 解决方案。

2. 在 WebPartNodeExtension 项目中，打开 SiteNodeExtension 代码文件，然后将一个断点添加到和方法中的第一行代码 `NodeChildrenRequested` `CreateWebPartNodes` 。

3. 选择**F5**键开始调试。

     Visual Studio 会将扩展安装到服务器 Explorer\1.0 的%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Web 部件库节点扩展，并启动 Visual Studio 的实验实例。 你将在 Visual Studio 的此实例中测试项目项。

#### <a name="to-test-the-extension"></a>测试扩展

1. 在的实验实例中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，在菜单栏上选择 "**查看**  >  **服务器资源管理器**"。

2. 如果要用于测试的 SharePoint 站点未出现在**服务器资源管理器**中的 " **sharepoint 连接**" 节点下，请执行以下步骤：

    1. 在**服务器资源管理器**中，打开 " **SharePoint 连接**" 的快捷菜单，然后选择 "**添加连接**"。

    2. 在 "**添加 Sharepoint 连接**" 对话框中，输入要连接到的 sharepoint 站点的 URL，然后选择 **"确定"** 按钮。

         若要在开发计算机上指定 SharePoint 站点，请输入 **http://localhost** 。

3. 展开 "站点连接" 节点（显示站点的 URL），然后展开 "子站点" 节点（例如，"**团队网站**"）。

4. 验证的另一个实例中的代码在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 您之前在方法中设置的断点处停止 `NodeChildrenRequested` ，然后选择**F5**继续调试项目。

5. 在 Visual Studio 的实验实例中，验证名为 " **Web 部件库**" 的新节点是否出现在 "顶层站点" 节点下，然后展开 " **web 部件库**" 节点。

6. 验证 Visual Studio 的另一个实例中的代码是否在您之前在方法中设置的断点处停止 `CreateWebPartNodes` ，然后选择**F5**键继续调试该项目。

7. 在 Visual Studio 的实验实例中，验证连接的站点上的所有 Web 部件都显示在 "**服务器资源管理器**中的" **Web 部件库**"节点下。

8. 在**服务器资源管理器**中，打开某个 Web 部件的快捷菜单，然后选择 "**属性**"。

9. 在要调试的实例中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，验证有关 Web 部件的详细信息是否出现在 "**属性**" 窗口中。

## <a name="uninstall-the-extension-from-visual-studio"></a>从 Visual Studio 卸载扩展
 完成扩展测试后，从 Visual Studio 中卸载该扩展。

#### <a name="to-uninstall-the-extension"></a>卸载扩展

1. 在的实验实例中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，在菜单栏上选择 "**工具**" "  >  **扩展和更新**"。

     此时，“扩展和更新”**** 对话框打开。

2. 在扩展列表中，选择 " **Web 部件库" "服务器资源管理器" 的 "Web 部件库" 节点扩展**，然后选择 "**卸载**" 按钮。

3. 在出现的对话框中，选择 "**是"** 按钮，确认要卸载该扩展，然后选择 "**立即重新启动**" 按钮以完成卸载。

4. 关闭 Visual Studio 的两个实例（在其中打开 WebPartNode 解决方案的实验实例和 Visual Studio 的实例）。

## <a name="see-also"></a>另请参阅
- [扩展中的 "SharePoint 连接" 节点服务器资源管理器](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [演练：在服务器资源管理器扩展中调入 SharePoint 客户端对象模型](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)
- [图标的图像编辑器](/cpp/windows/image-editor-for-icons)
- [为图标 &#40;图像编辑器创建图标或其他图像&#41;](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)
