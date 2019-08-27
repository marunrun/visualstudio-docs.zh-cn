---
title: 演练：扩展服务器资源管理器以显示 Web 部件 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 1c84cfcde4a5ffac1e1563a4d2b141bd6240b772
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67821989"
---
# <a name="walkthrough-extend-server-explorer-to-display-web-parts"></a>演练：扩展服务器资源管理器以显示 web 部件
  在 Visual Studio 中，你可以使用**SharePoint 连接**的节点**服务器资源管理器**来查看 SharePoint 站点上的组件。 但是，**服务器资源管理器**默认情况下不会显示某些组件。 在本演练中，你将扩展**服务器资源管理器**，以便它显示在 Web 部件库在每个连接 SharePoint 站点。

 本演练演示了下列任务：

- 创建 Visual Studio 扩展来扩展**服务器资源管理器**以下方面：

  - 通过扩展添加**Web 部件库**节点下的每个 SharePoint 站点节点**服务器资源管理器**。 此新节点包含表示每个 Web 部件在站点上的 Web 部件库中的子节点。

  - 扩展插件定义新类型的表示 Web 部件实例的节点。 此新的节点类型是在新的子节点的基础**Web 部件库**节点。 新的 Web 部件节点类型中显示信息**属性**有关 Web 部件，它表示的窗口。 节点类型还可以用作起始点执行与 Web 部件相关的其他任务的自定义的快捷菜单项。

- 创建两个扩展插件程序集调用的自定义 SharePoint 命令。 SharePoint 命令都可由扩展插件程序集的 SharePoint 服务器对象模型中使用 Api 调用的方法。 在本演练中，创建从开发计算机上的本地 SharePoint 站点检索 Web 部件的信息的命令。 有关详细信息，请参阅[调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

- 生成 Visual Studio 扩展 (VSIX) 包将扩展部署。

- 调试和测试扩展。

> [!NOTE]
> 此演练，而不是其服务器对象模型中使用 SharePoint 的客户端对象模型的替代版本，请参阅[演练：调入 SharePoint 客户端对象模型中的服务器资源管理器扩展](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)。

## <a name="prerequisites"></a>系统必备
 需要要完成本演练的开发计算机上安装以下组件：

- 支持的 Windows、 SharePoint 和 Visual Studio 版本。

- Visual Studio SDK。 本演练使用**VSIX 项目**中此 SDK 来创建 VSIX 包来部署项目项模板。 有关详细信息，请参阅[扩展 Visual Studio 中的 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

  了解以下概念很有帮助，但不是必需，若要完成本演练：

- 使用 for SharePoint 服务器对象模型。 有关详细信息，请参阅[使用 SharePoint Foundation 服务器端对象模型](http://go.microsoft.com/fwlink/?LinkId=177796)。

- 在 SharePoint 解决方案中的 web 部件。 有关详细信息，请参阅[Web 部件概述](http://go.microsoft.com/fwlink/?LinkId=177803)。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，必须创建三个项目：

- 创建 VSIX 包将扩展部署的 VSIX 项目。

- 实现扩展的类库项目。 此项目必须面向.NET Framework 4.5。

- 一个用于定义自定义的 SharePoint 命令的类库项目。 此项目必须面向.net Framework 3.5。

  首先演练创建项目。

#### <a name="to-create-the-vsix-project"></a>若要创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件”   > “新建”   > “项目”  。

3. 在中**新的项目**对话框框中，展开**Visual C#** 或**Visual Basic**节点，然后选择**扩展性**节点。

    > [!NOTE]
    > **扩展性**节点是安装 Visual Studio SDK 的情况下才可用。 有关详细信息，请参阅本主题前面的先决条件部分。

4. 在对话框的顶部，选择 **.NET Framework 4.5** .NET Framework 版本的列表中。

5. 选择**VSIX 项目**模板，将项目命名**WebPartNode**，然后选择**确定**按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将添加**WebPartNode**投影到**解决方案资源管理器**。

#### <a name="to-create-the-extension-project"></a>若要创建扩展项目

1. 在中**解决方案资源管理器**，打开解决方案节点的快捷菜单，选择**添加**，然后选择**新项目**。

2. 在中**新的项目**对话框框中，展开**Visual C#** 节点或**Visual Basic**节点，然后选择**Windows**节点。

3. 在对话框的顶部，选择 **.NET Framework 4.5** .NET Framework 版本的列表中。

4. 在项目模板列表中，选择**类库**，将项目命名**WebPartNodeExtension**，然后选择**确定**按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将添加**WebPartNodeExtension**到解决方案并打开默认 Class1 代码文件。

5. 从项目中删除的 Class1 代码文件。

#### <a name="to-create-the-sharepoint-commands-project"></a>若要创建 SharePoint 命令项目

1. 在中**解决方案资源管理器**，打开解决方案节点的快捷菜单，选择**添加**，然后选择**新项目**。

2. 在中**新的项目**对话框框中，展开**Visual C#** 节点或**Visual Basic**节点，然后选择**Windows**节点。

3. 在对话框的顶部，选择 **.NET Framework 3.5** .NET Framework 版本的列表中。

4. 在项目模板列表中，选择**类库**，将项目命名**WebPartCommands**，然后选择**确定**按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将添加**WebPartCommands**到解决方案并打开默认 Class1 代码文件。

5. 从项目中删除的 Class1 代码文件。

## <a name="configure-the-projects"></a>配置项目
 编写代码来创建扩展插件之前，必须添加代码文件和程序集引用和配置项目设置。

#### <a name="to-configure-the-webpartnodeextension-project"></a>若要配置 WebPartNodeExtension 项目

1. 在 WebPartNodeExtension 项目中，添加具有以下名称的四个文件：

    - SiteNodeExtension

    - WebPartNodeTypeProvider

    - WebPartNodeInfo

    - WebPartCommandIds

2. 打开快捷菜单**WebPartNodeExtension**项目，，然后选择**添加引用**。

3. 在中**引用管理器-WebPartNodeExtension**对话框框中，选择**Framework**选项卡，然后选择为每个以下程序集复选框：

    - System.ComponentModel.Composition

    - System.Windows.Forms

4. 选择**扩展**选项卡上，对于 Microsoft.VisualStudio.SharePoint 程序集，选中的复选框，然后选择**确定**按钮。

5. 在中**解决方案资源管理器**，打开快捷菜单**WebPartNodeExtension**项目节点，然后选择**属性**。

     将打开“项目设计器”  。

6. 选择“应用程序”  选项卡。

7. 在中**默认命名空间**框 (C#) 或**根命名空间**框 ([!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)])，输入**ServerExplorer.SharePointConnections.WebPartNode**。

#### <a name="to-configure-the-webpartcommands-project"></a>若要配置 webpartcommands 项目

1. 在 WebPartCommands 项目中，添加名为 WebPartCommands 的代码文件。

2. 在中**解决方案资源管理器**，打开快捷菜单**WebPartCommands**项目节点，选择**添加**，然后选择**现有项**.

3. 在中**添加现有项**对话框中，浏览到包含 WebPartNodeExtension 项目的代码文件的文件夹，然后选择 WebPartNodeInfo 和 WebPartCommandIds 代码文件。

4. 选择箭头旁边**外**按钮，，然后选择**添加为链接**中显示的菜单。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将代码文件作为链接添加到 WebPartCommands 项目中。 因此，代码文件位于 WebPartNodeExtension 项目，但文件中的代码还编译 WebPartCommands 项目中。

5. 打开快捷菜单**WebPartCommands**同样，项目，然后选择**添加引用**。

6. 在中**引用管理器-WebPartCommands**对话框框中，选择**扩展**选项卡上，选择以下程序集的每个复选框，然后选择**确定**按钮：

    - Microsoft.SharePoint

    - Microsoft.VisualStudio.SharePoint.Commands

7. 在中**解决方案资源管理器**，打开快捷菜单**WebPartCommands**同样，项目，然后选择**属性**。

     将打开“项目设计器”  。

8. 选择“应用程序”  选项卡。

9. 在中**默认命名空间**框 (C#) 或**根命名空间**框 ([!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)])，输入**ServerExplorer.SharePointConnections.WebPartNode**。

## <a name="create-icons-for-the-new-nodes"></a>创建新节点的图标
 创建的两个图标**服务器资源管理器**扩展： 新的图标**Web 部件库**节点，然后为每个子 Web 部件节点下的另一个图标**Web 部件库**节点。 稍后在本演练中，将编写将这些图标与节点相关联的代码。

#### <a name="to-create-icons-for-the-nodes"></a>若要创建的节点的图标

1. 在中**解决方案资源管理器**，打开快捷菜单**WebPartNodeExtension**项目，，然后选择**属性**。

2. 将打开“项目设计器”  。

3. 选择**资源**选项卡，然后选择**此项目不包含默认资源文件。单击此处可创建一个**链接。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建一个资源文件，并在设计器中打开它。

4. 在设计器的顶部，选择箭头旁边**添加资源**菜单命令时，，然后选择**添加新图标**中显示的菜单。

5. 在中**添加新资源**对话框中，名称新建图标**WebPartsNode**，然后选择**添加**按钮。

     在中打开新建图标**的图像编辑器**。

6. 编辑图标的 16x16 版本，使它具有你可以轻松识别的设计。

7. 打开 32 x 32 版本的图标的快捷菜单，然后选择**删除图像类型**。

8. 重复步骤 5 至 8 第二个图标添加到项目资源，并命名为此图标**WebPart**。

9. 在中**解决方案资源管理器**下**资源**文件夹**WebPartNodeExtension**项目中，打开快捷菜单**WebPartsNode.ico**.

10. 在**属性**窗口中，选择箭头旁边**生成操作**，然后选择**嵌入的资源**上显示的菜单。

11. 重复最后两个步骤**WebPart.ico**。

## <a name="add-the-web-part-gallery-node-to-server-explorer"></a>将 Web 部件库节点添加到服务器资源管理器
 创建将添加新的类**Web 部件库**到每个 SharePoint 站点节点的节点。 若要添加新节点，此类应实现<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension>接口。 实现此接口，只要您想要扩展中的现有节点的行为**服务器资源管理器**，如将子节点添加到节点。

#### <a name="to-add-the-web-part-gallery-node-to-server-explorer"></a>若要将 Web 部件库节点添加到服务器资源管理器

1. 在 WebPartNodeExtension 项目中，打开 SiteNodeExtension 代码文件，以及然后将以下代码粘贴到其中。

    > [!NOTE]
    > 添加此代码，此项目将具有某些编译错误，但它们将消失后添加的代码在后续步骤中。

     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#1](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/sitenodeextension.cs#1)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#1](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/sitenodeextension.vb#1)]

## <a name="define-a-node-type-that-represents-a-web-part"></a>定义表示 web 部件的节点类型
 创建用于定义新类型的节点，表示 Web 部件类。 Visual Studio 将使用此新的节点类型以显示下的子节点**Web 部件库**节点。 每个子节点表示 SharePoint 站点上的单个 Web 部件。

 若要定义新的节点类型，此类应实现<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider>接口。 每当你想要定义新类型的节点中实现此接口**服务器资源管理器**。

#### <a name="to-define-the-web-part-node-type"></a>若要定义 web 部件节点类型

1. 在 WebPartNodeExtension 项目中，打开 WebPartNodeTypeProvder 代码文件，以及然后将以下代码粘贴到其中。

     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#2](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartnodetypeprovider.vb#2)]
     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#2](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartnodetypeprovider.cs#2)]

## <a name="define-the-web-part-data-class"></a>定义 web 部件数据类
 定义包含有关在 SharePoint 站点上的单个 Web 部件的数据的类。 更高版本在本演练中，将创建自定义的 SharePoint 命令，检索有关站点上每个 Web 部件的数据，然后将数据分配到此类的实例。

#### <a name="to-define-the-web-part-data-class"></a>若要定义 web 部件数据类

1. 在 WebPartNodeExtension 项目中，打开 WebPartNodeInfo 代码文件，以及然后将以下代码粘贴到其中。

     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#3](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartnodeinfo.vb#3)]
     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#3](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartnodeinfo.cs#3)]

## <a name="define-the-ids-for-the-sharepoint-commands"></a>定义的 SharePoint 命令的 Id
 定义多个标识的自定义的 SharePoint 命令的字符串。 将在本演练后面实现这些命令。

#### <a name="to-define-the-command-ids"></a>若要定义的命令 Id

1. 在 WebPartNodeExtension 项目中，打开 WebPartCommandIds 代码文件，以及然后将以下代码粘贴到其中。

     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#4](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartcommandids.cs#4)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#4](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartcommandids.vb#4)]

## <a name="create-the-custom-sharepoint-commands"></a>创建自定义的 SharePoint 命令
 创建自定义命令调用到 SharePoint，以检索有关 Web 部件在 SharePoint 站点上的数据的服务器对象模型。 每个命令是一种方法具有<xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute>应用于它。

#### <a name="to-define-the-sharepoint-commands"></a>若要定义的 SharePoint 命令

1. 在 WebPartCommands 项目中，打开 WebPartCommands 代码文件，以及然后将以下代码粘贴到其中。

     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#6](../sharepoint/codesnippet/CSharp/WebPartNode/WebPartCommands/WebPartCommands.cs#6)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#6](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartcommands/webpartcommands.vb#6)]

## <a name="checkpoint"></a>检查点
 在本演练中，所有的代码中这一时刻**Web 部件库**节点和 SharePoint 命令现已在项目中。 生成解决方案以确保这两个项目编译错误。

#### <a name="to-build-the-solution"></a>生成解决方案

1. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

    > [!WARNING]
    > 此时，WebPartNode 项目可能会生成错误，因为 VSIX 清单文件不具有的作者的值。 当在后续步骤中添加值时，此错误将消失。

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>创建 VSIX 包，以将扩展部署
 若要将扩展部署，使用 VSIX 项目在解决方案中创建 VSIX 包。 首先，通过修改 VSIX 项目中的 source.extension.vsixmanifest 文件中配置 VSIX 包。 然后，通过生成解决方案中创建 VSIX 包。

#### <a name="to-configure-the-vsix-package"></a>若要配置 VSIX 包

1. 在中**解决方案资源管理器**，在 WebPartNode 项目下，打开**source.extension.vsixmanifest**清单编辑器中的文件。

     在 source.extension.vsixmanifest 文件是所有 VSIX 包都需要 extension.vsixmanifest 文件的基础。 有关此文件的详细信息，请参阅[VSIX 扩展架构 1.0 参考](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)。

2. 在中**产品名称**框中，输入**服务器资源管理器 Web 部件库节点**。

3. 在中**作者**框中，输入**Contoso**。

4. 在中**描述**框中，输入**将自定义 Web 部件库节点添加到服务器资源管理器中的 SharePoint 连接节点。此扩展使用自定义的 SharePoint 命令来调入服务器对象模型。**

5. 选择**资产**选项卡的编辑器，然后选择**新建**按钮。

     **添加新资产**对话框随即出现。

6. 在中**类型**列表中，选择**Microsoft.VisualStudio.MefComponent**。

    > [!NOTE]
    > 此值对应于`MefComponent`extension.vsixmanifest 文件中的元素。 此元素指定 VSIX 包中的扩展插件程序集名称。 有关详细信息，请参阅[MEFComponent 元素 （VSX 架构）](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))。

7. 在中**源**列表中，选择**当前解决方案中的项目**。

8. 在中**项目**列表中，选择**WebPartNodeExtension** ，然后选择**确定**按钮。

9. 在清单编辑器中，选择**新建**按钮再次。

     **添加新资产**对话框随即出现。

10. 在中**类型**框中，输入**SharePoint.Commands.v4**。

    > [!NOTE]
    > 此元素指定要包含在 Visual Studio 扩展中的自定义扩展插件。 有关详细信息，请参阅[资产元素 （VSX 架构）](https://msdn.microsoft.com/9fcfc098-edc7-484b-9d4c-acd17829d737)。

11. 在中**源**列表中，选择**当前解决方案中的项目**列表项。

12. 在中**项目**列表中，选择**WebPartCommands**，然后选择**确定**按钮。

13. 在菜单栏上依次选择**构建** > **生成解决方案**，然后确保该解决方案在编译时没有错误。

14. 请确保 WebPartNode 项目的生成输出文件夹现在包含 WebPartNode.vsix 文件。

     默认情况下，生成输出文件夹是...包含项目文件的文件夹下的 \bin\Debug 文件夹。

## <a name="test-the-extension"></a>测试此扩展
 现在，你准备好进行测试的新**Web 部件库**中的节点**服务器资源管理器**。 首先，开始调试 Visual Studio 的实验实例中的扩展。 然后，使用新**Web 部件**在实验实例中的节点[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

#### <a name="to-start-debugging-the-extension"></a>若要开始调试扩展

1. 重新启动[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]具有管理凭据，然后打开 WebPartNode 解决方案。

2. 在 WebPartNodeExtension 项目中，打开 SiteNodeExtension 代码文件，并将断点添加到代码中的第一行`NodeChildrenRequested`和`CreateWebPartNodes`方法。

3. 选择**F5**键启动调试。

     Visual Studio 的服务器 Explorer\1.0 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Web 部件库节点扩展到安装该扩展，并启动 Visual Studio 的实验实例。 在 Visual Studio 的此实例中，将测试项目项。

#### <a name="to-test-the-extension"></a>若要测试此扩展

1. 在实验实例中的[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，在菜单栏上依次选择**视图** > **服务器资源管理器**。

2. 如果你想要用于测试的 SharePoint 站点未显示在下，执行以下步骤**SharePoint 连接**中的节点**服务器资源管理器**:

    1. 在中**服务器资源管理器**，打开快捷菜单**SharePoint 连接**，然后选择**添加连接**。

    2. 在中**添加 SharePoint 连接**对话框框中，输入你想要连接，，然后选择 SharePoint 站点的 URL**确定**按钮。

         若要在开发计算机上指定 SharePoint 站点，请输入 **http://localhost** 。

3. 站点连接节点 （这将显示你的站点的 URL），依次展开和一个子节点 (例如，**团队网站**)。

4. 验证在另一个实例的代码[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中设置的断点处停止`NodeChildrenRequested`方法，然后选择**F5**继续调试项目。

5. 在 Visual Studio 的实验实例中，验证新节点名为**Web 部件库**显示在顶层站点节点，然后展开**Web 部件库**节点。

6. 验证中设置的断点处停止 Visual Studio 的其他实例中的代码`CreateWebPartNodes`方法，然后选择**F5**键继续调试项目。

7. 在 Visual Studio 的实验实例中，验证是否已连接的站点上的所有 Web 部件都显示下**Web 部件库**中的节点**服务器资源管理器**。

8. 在中**服务器资源管理器**，打开一个 Web 部件的快捷菜单，然后选择**属性**。

9. 实例中[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]正在调试，验证有关 Web 部件的详细信息显示在**属性**窗口。

## <a name="uninstall-the-extension-from-visual-studio"></a>从 Visual Studio 中卸载扩展
 完成测试扩展后，请从 Visual Studio 卸载扩展。

#### <a name="to-uninstall-the-extension"></a>卸载扩展

1. 在实验实例中的[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，在菜单栏上依次选择**工具** > **扩展和更新**。

     此时，“扩展和更新”  对话框打开。

2. 在扩展的列表，选择**Web 部件库节点扩展服务器资源管理器**，然后选择**卸载**按钮。

3. 在出现的对话框中，选择**是**按钮以确认你要卸载扩展，然后选择**立即重新启动**按钮以完成卸载。

4. 关闭 Visual Studio （实验实例和在其中 WebPartNode 解决方案已打开的 Visual Studio 的实例） 的两个实例。

## <a name="see-also"></a>请参阅
- [扩展服务器资源管理器中的 SharePoint 连接节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [演练：调入 SharePoint 客户端对象模型中的服务器资源管理器扩展](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)
- [图标的图像编辑器](/cpp/windows/image-editor-for-icons)
- [创建图标或其他图像&#40;图标的图像编辑器&#41;](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)
