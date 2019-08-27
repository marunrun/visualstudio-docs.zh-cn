---
title: 创建 SharePoint 项目的自定义部署步骤
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint commands
- SharePoint development in Visual Studio, extending deployment
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4b209fad02cdcb3da230143a2c13ff4eaa648d76
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825624"
---
# <a name="walkthrough-create-a-custom-deployment-step-for-sharepoint-projects"></a>演练：创建 SharePoint 项目的自定义部署步骤
  在部署 SharePoint 项目时，Visual Studio 按特定顺序执行一系列的部署步骤。 Visual Studio 提供了许多内置部署步骤，但您也可以创建您自己。

 在本演练中，将创建自定义部署步骤以升级运行 SharePoint 的服务器上的解决方案。 Visual Studio 提供了内置部署步骤的许多任务，此类，收回或添加解决方案，但它不包括有关升级解决方案的部署步骤。 默认情况下，在部署 SharePoint 解决方案时 Visual Studio 首先会收回该解决方案 （如果已部署），然后重新部署整个解决方案。 有关内置部署步骤的详细信息，请参阅[部署、 发布和升级 SharePoint 解决方案包](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)。

 本演练演示了下列任务：

- 创建 Visual Studio 扩展将执行两项主要任务：

  - 扩展插件定义自定义部署步骤，若要升级 SharePoint 解决方案。

  - 该扩展会定义新的部署配置，这是针对给定项目执行部署步骤的一组项目扩展。 新的部署配置包括自定义部署步骤和几个内置部署步骤。

- 创建两个扩展插件程序集调用的自定义 SharePoint 命令。 SharePoint 命令都可由扩展插件程序集的 SharePoint 服务器对象模型中使用 Api 调用的方法。 有关详细信息，请参阅[调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

- 生成 Visual Studio 扩展 (VSIX) 包来部署这两个程序集。

- 测试新的部署步骤。

## <a name="prerequisites"></a>系统必备
 需要要完成本演练的开发计算机上安装以下组件：

- 支持的 Windows、 SharePoint 和 Visual Studio 版本。

- Visual Studio SDK。 本演练使用**VSIX 项目**SDK 来创建 VSIX 包，以将扩展部署中的模板。 有关详细信息，请参阅[扩展 Visual Studio 中的 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

  了解以下概念很有帮助，但不是必需，若要完成本演练：

- 使用 for SharePoint 服务器对象模型。 有关详细信息，请参阅[使用 SharePoint Foundation 服务器端对象模型](http://go.microsoft.com/fwlink/?LinkId=177796)。

- SharePoint 解决方案。 有关详细信息，请参阅[解决方案概述](http://go.microsoft.com/fwlink/?LinkId=169422)。

- 升级 SharePoint 解决方案。 有关详细信息，请参阅[升级解决方案](http://go.microsoft.com/fwlink/?LinkId=177802)。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，必须创建三个项目：

- 创建 VSIX 包将扩展部署的 VSIX 项目。

- 实现扩展的类库项目。 此项目必须面向.NET Framework 4.5。

- 一个用于定义自定义的 SharePoint 命令的类库项目。 此项目必须面向.NET Framework 3.5。

  首先演练创建项目。

#### <a name="to-create-the-vsix-project"></a>若要创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件”   > “新建”   > “项目”  。

3. 在中**新的项目**对话框框中，展开**Visual C#** 或**Visual Basic**节点，然后选择**扩展性**节点。

    > [!NOTE]
    > **扩展性**节点是安装 Visual Studio SDK 的情况下才可用。 有关详细信息，请参阅本主题前面的先决条件部分。

4. 在对话框的顶部，选择 **.NET Framework 4.5** .NET Framework 版本的列表中。

5. 选择**VSIX 项目**模板，将项目命名**UpgradeDeploymentStep**，然后选择**确定**按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将添加**UpgradeDeploymentStep**投影到**解决方案资源管理器**。

#### <a name="to-create-the-extension-project"></a>若要创建扩展项目

1. 在中**解决方案资源管理器**，打开 UpgradeDeploymentStep 解决方案节点的快捷菜单，选择**添加**，然后选择**新项目**。

2. 在中**新的项目**对话框框中，展开**Visual C#** 或**Visual Basic**节点，然后选择**Windows**节点。

3. 在对话框的顶部，选择 **.NET Framework 4.5** .NET Framework 版本的列表中。

4. 选择**类库**项目模板，请将项目命名**DeploymentStepExtension**，然后选择**确定**按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将添加**DeploymentStepExtension**到解决方案并打开默认 Class1 代码文件。

5. 从项目中删除的 Class1 代码文件。

#### <a name="to-create-the-sharepoint-command-project"></a>若要创建 SharePoint 命令项目

1. 在中**解决方案资源管理器**，打开 UpgradeDeploymentStep 解决方案节点的快捷菜单，选择**添加**，然后选择**新项目**。

2. 在中**新的项目**对话框框中，展开**Visual C#** 或**Visual Basic**，然后选择**Windows**节点。

3. 在对话框的顶部，选择 **.NET Framework 3.5** .NET Framework 版本的列表中。

4. 选择**类库**项目模板，请将项目命名**SharePointCommands**，然后选择**确定**按钮。

     Visual Studio 将添加**SharePointCommands**到解决方案并打开默认 Class1 代码文件。

5. 从项目中删除的 Class1 代码文件。

## <a name="configure-the-projects"></a>配置项目
 编写代码以创建自定义部署步骤之前，必须添加代码文件和程序集引用，并且您必须配置项目。

#### <a name="to-configure-the-deploymentstepextension-project"></a>若要配置 DeploymentStepExtension 项目

1. 在中**DeploymentStepExtension**项目中，添加具有以下名称的两个文件：

    - UpgradeStep

    - DeploymentConfigurationExtension

2. 打开上 DeploymentStepExtension 项目的快捷菜单，然后选择**添加引用**。

3. 上**Framework**选项卡上，选择复选框的 System.ComponentModel.Composition 程序集。

4. 上**扩展**选项卡上，对于 Microsoft.VisualStudio.SharePoint 程序集，选中的复选框，然后选择**确定**按钮。

#### <a name="to-configure-the-sharepointcommands-project"></a>若要配置 SharePointCommands 项目

1. 在中**SharePointCommands**项目中，添加名为命令的代码文件。

2. 在中**解决方案资源管理器**，打开快捷菜单上**SharePointCommands**项目节点，然后选择**添加引用**。

3. 上**扩展**选项卡上，对于以下程序集，选中的复选框，然后单击选择**确定**按钮

    - Microsoft.SharePoint

    - Microsoft.VisualStudio.SharePoint.Commands

## <a name="define-the-custom-deployment-step"></a>定义自定义部署步骤
 创建一个类，用于定义升级部署步骤。 若要定义部署步骤，此类应实现<xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep>接口。 实现此接口，只要您想要定义自定义部署步骤。

#### <a name="to-define-the-custom-deployment-step"></a>若要定义自定义部署步骤

1. 在中**DeploymentStepExtension**项目，打开 UpgradeStep 代码文件，然后将以下代码粘贴到其中。

    > [!NOTE]
    > 添加此代码，此项目将具有某些编译错误，但它们将消失后添加的代码在后续步骤中。

     [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#1](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/upgradestep.cs#1)]
     [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#1](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/upgradestep.vb#1)]

## <a name="create-a-deployment-configuration-that-includes-the-custom-deployment-step"></a>创建包含自定义部署步骤的部署配置
 创建项目扩展为新的部署配置，其中包括几个内置部署步骤和新的升级部署步骤。 通过创建此扩展，可帮助 SharePoint 开发人员能够在 SharePoint 项目中使用的升级的部署步骤。

 若要创建的部署配置，此类应实现<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension>接口。 实现此接口，只要您想要创建 SharePoint 项目扩展。

#### <a name="to-create-the-deployment-configuration"></a>若要创建的部署配置

1. 在中**DeploymentStepExtension**项目，打开 DeploymentConfigurationExtension 代码文件，然后将以下代码粘贴到其中。

     [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#2](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/deploymentconfigurationextension.cs#2)]
     [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#2](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/deploymentconfigurationextension.vb#2)]

## <a name="create-the-custom-sharepoint-commands"></a>创建自定义的 SharePoint 命令
 创建 sharepoint 调入服务器对象模型的两个自定义命令。 一个命令将确定是否已部署解决方案时;其他命令升级解决方案。

#### <a name="to-define-the-sharepoint-commands"></a>若要定义的 SharePoint 命令

1. 在中**SharePointCommands**项目，打开命令的代码文件，然后将以下代码粘贴到其中。

     [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#4](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/SharePointCommands/Commands.cs#4)]
     [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#4](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/sharepointcommands/commands.vb#4)]

## <a name="checkpoint"></a>检查点
 此时在演练中，自定义部署步骤和 SharePoint 命令的所有代码现在都处于项目。 生成，以确保它们在编译时未出现错误。

#### <a name="to-build-the-projects"></a>若要生成项目

1. 在中**解决方案资源管理器**，打开快捷菜单**DeploymentStepExtension**项目，，然后选择**生成**。

2. 打开快捷菜单**SharePointCommands**项目，，然后选择**生成**。

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>创建 VSIX 包，以将扩展部署
 若要将扩展部署，使用 VSIX 项目在解决方案中创建 VSIX 包。 首先，通过修改 VSIX 项目中的 source.extension.vsixmanifest 文件中配置 VSIX 包。 通过生成解决方案，然后创建 VSIX 包。

#### <a name="to-configure-and-create-the-vsix-package"></a>若要配置和创建 VSIX 包

1. 在中**解决方案资源管理器**下**UpgradeDeploymentStep**项目中，打开快捷菜单**source.extension.vsixmanifest**文件，，然后选择**打开**。

     Visual Studio 清单编辑器中打开该文件。 在 source.extension.vsixmanifest 文件是所有 VSIX 包都需要 extension.vsixmanifest 文件的基础。 有关此文件的详细信息，请参阅[VSIX 扩展架构 1.0 参考](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)。

2. 在中**产品名称**框中，输入**升级 SharePoint 项目的部署步骤**。

3. 在中**作者**框中，输入**Contoso**。

4. 在中**描述**框中，输入**提供了可以在 SharePoint 项目中使用的自定义升级部署步骤**。

5. 在中**资产**选项卡的编辑器中，选择**新建**按钮。

     **添加新资产**对话框随即出现。

6. 在中**类型**列表中，选择**Microsoft.VisualStudio.MefComponent**。

    > [!NOTE]
    > 此值对应于`MefComponent`extension.vsixmanifest 文件中的元素。 此元素指定 VSIX 包中的扩展插件程序集名称。 有关详细信息，请参阅[MEFComponent 元素 （VSX 架构）](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))。

7. 在中**源**列表中，选择**当前解决方案中的项目**。

8. 在中**项目**列表中，选择**DeploymentStepExtension**，然后选择**确定**按钮。

9. 在清单编辑器中，选择**新建**按钮再次。

     **添加新资产**对话框随即出现。

10. 在中**类型**列表中，输入**SharePoint.Commands.v4**。

    > [!NOTE]
    > 此元素指定要包含在 Visual Studio 扩展中的自定义扩展插件。 有关详细信息，请参阅[资产元素 （VSX 架构）](https://msdn.microsoft.com/9fcfc098-edc7-484b-9d4c-acd17829d737)。

11. 在中**源**列表中，选择**当前解决方案中的项目**。

12. 在中**项目**列表中，选择**SharePointCommands**，然后选择**确定**按钮。

13. 在菜单栏上依次选择**构建** > **生成解决方案**，然后确保该解决方案在编译时没有错误。

14. 请确保 UpgradeDeploymentStep 项目的生成输出文件夹现在包含 UpgradeDeploymentStep.vsix 文件。

     默认情况下，生成输出文件夹是...包含项目文件的文件夹下的 \bin\Debug 文件夹。

## <a name="prepare-to-test-the-upgrade-deployment-step"></a>准备测试升级的部署步骤
 若要测试升级的部署步骤，必须首先将示例解决方案部署到 SharePoint 站点。 首先，调试 Visual Studio 的实验实例中的扩展。 然后创建一个列表定义和列表实例用于测试部署步骤，然后将其部署到 SharePoint 站点。 接下来，修改列表定义和列表实例并重新部署它们来演示默认部署过程将 SharePoint 站点上的解决方案的覆盖。

 稍后在本演练中，将修改的列表定义和列表实例，然后你会将其升级 SharePoint 站点上。

#### <a name="to-start-debugging-the-extension"></a>若要开始调试扩展

1. 使用管理凭据，重新启动 Visual Studio，然后打开 UpgradeDeploymentStep 解决方案。

2. 在 DeploymentStepExtension 项目中，打开 UpgradeStep 代码文件，并将断点添加到代码中的第一行`CanExecute`和`Execute`方法。

3. 开始调试通过选择**F5**关键的或在菜单栏中选择**调试** > **开始调试**。

4. Visual Studio 会安装 SharePoint Projects\1.0 到 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Upgrade 部署步骤扩展，并启动 Visual Studio 的实验实例。 将 Visual Studio 的此实例中测试升级的部署步骤。

#### <a name="to-create-a-sharepoint-project-with-a-list-definition-and-a-list-instance"></a>若要使用列表定义和列表实例创建一个 SharePoint 项目

1. 在实验实例中的 Visual Studio 中，在菜单栏上，选择**文件** > **新建** > **项目**。

2. 在中**新的项目**对话框框中，展开**Visual C#** 节点或**Visual Basic**节点，展开**SharePoint**节点，然后选择**2010年**节点。

3. 在对话框顶部，请确保 **.NET Framework 3.5**将出现在.NET Framework 版本的列表。

    为项目[!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)]和[!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)]需要此版本的.NET Framework。

4. 在项目模板列表中，选择**SharePoint 2010 项目**，将项目命名**EmployeesListDefinition**，然后选择**确定**按钮。

5. 在中**SharePoint 自定义向导**，输入想要用于调试的站点的 URL。

6. 下**此 SharePoint 解决方案的信任级别是什么**，选择**部署为场解决方案**选项按钮。

   > [!NOTE]
   > 升级部署步骤不支持沙盒解决方案。

7. 选择**完成**按钮。

    [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建 EmployeesListDefinition 项目。

8. 打开 EmployeesListDefinition 项目的快捷菜单中，选择**外**，然后选择**新项**。

9. 在中**添加新项-EmployeesListDefinition**对话框框中，展开**SharePoint**节点，然后选择**2010年**节点。

10. 选择**列表**项模板，将项**员工列表**，然后选择**添加**按钮。

     出现 SharePoint 自定义向导

11. 上**选择列表设置**页上，验证以下设置，然后选择**完成**按钮：

    1. **员工列表**将出现在**要列表的显示名称？** 框。

    2. **创建基于的可自定义列表：** 选择选项按钮。

    3. **默认 （空）** 中选择**创建基于的可自定义列表：** 列表。

       [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建员工列表项的标题列和单个的空实例并打开列表设计器。

12. 在列表设计器上**列**选项卡上，选择**键入新的或现有的列名称**行，以及如何将在以下各列**列显示名称**列表：

    1. 名字

    2. 公司

    3. 办公电话

    4. 电子邮件

13. 保存所有文件，然后关闭列表设计器。

14. 在中**解决方案资源管理器**，展开**员工列表**节点，然后展开**员工列表实例**子节点。

15. 在中*Elements.xml*文件中，用下列 XML 替换默认的此文件中的 XML。 此 XML 将更改到列表的名称**员工**并添加具有名为荣的员工的信息。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <ListInstance Title="Employees"
                    OnQuickLaunch="TRUE"
                    TemplateType="10000"
                    Url="Lists/Employees"
                    Description="Simple list to test upgrade deployment step">
        <Data>
          <Rows>
            <Row>
              <Field Name="Title">Hance</Field>
              <Field Name="FirstName">Jim</Field>
              <Field Name="Company">Contoso</Field>
              <Field Name="Business Phone">555-555-5555</Field>
              <Field Name="E-Mail">jim@contoso.com</Field>
            </Row>
          </Rows>
        </Data>
      </ListInstance>
    </Elements>
    ```

16. 保存并关闭*Elements.xml*文件。

17. 打开 EmployeesListDefinition 项目的快捷菜单，然后选择**开放**或**属性**。

     属性设计器随即打开。

18. 上**SharePoint**选项卡上，清除**调试后自动收回**复选框，并将属性然后保存。

#### <a name="to-deploy-the-list-definition-and-list-instance"></a>若要部署的列表定义和列表实例

1. 在中**解决方案资源管理器**，选择**EmployeesListDefinition**项目节点。

2. 在中**属性**窗口中，请确保**活动部署配置**属性设置为**默认**。

3. 选择**F5**键，或在菜单栏上选择**调试** > **开始调试**。

4. 验证是否已成功生成项目、 web 浏览器打开到 SharePoint 站点的**列出了**快速启动栏中的项包括新**员工**列表中，并且**员工**列表包括为荣条目。

5. 关闭 Web 浏览器。

#### <a name="to-modify-the-list-definition-and-list-instance-and-redeploy-them"></a>若要修改的列表定义和列表实例并重新部署

1. 在 EmployeesListDefinition 项目中，打开*Elements.xml*的子文件**员工列表实例**项目项。

2. 删除`Data`元素及其子项来为荣从列表中删除该条目。

     完成后，该文件应包含以下 XML。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <ListInstance Title="Employees"
                    OnQuickLaunch="TRUE"
                    TemplateType="10000"
                    Url="Lists/Employees"
                    Description="Simple list to test upgrade deployment step">
      </ListInstance>
    </Elements>
    ```

3. 保存并关闭*Elements.xml*文件。

4. 打开快捷菜单**员工列表**项，项目，然后选择**打开**或**属性**。

5. 在列表设计器中，选择**视图**选项卡。

6. 在中**所选列**列表中，选择**附件**，然后选择 < 键移动到该列**可用列**列表。

7. 重复上一步移动**办公电话**从列**所选列**到列出**可用列**列表。

     此操作将删除这些字段的默认视图**员工**SharePoint 站点上的列表。

8. 开始调试通过选择**F5**关键的或在菜单栏中选择**调试** > **开始调试**。

9. 确认**部署冲突**对话框随即出现。

     会显示此对话框时 Visual Studio 尝试将解决方案 （列表实例） 部署到 SharePoint 站点已向其部署该解决方案。 在本演练中执行升级部署步骤更高版本时，不会出现此对话框。

10. 在中**部署冲突**对话框框中，选择**自动解决**选项按钮。

     Visual Studio 删除 SharePoint 站点上的列表实例，将部署在项目中，列表项，然后打开 SharePoint 站点。

11. 在中**列出了**部分的快速启动栏中，选择**员工**列表，并验证以下详细信息：

    - **附件**并**住宅电话号码**列不会显示在此视图中的列表。

    - 该列表为空。 使用时**默认**要重新部署该解决方案，部署配置**员工**列表已替换为你的项目中的新空列表。

## <a name="test-the-deployment-step"></a>测试部署步骤
 现在您就可以测试升级的部署步骤。 首先，将项添加到 SharePoint 中的列表实例。 然后更改列表定义和列表实例，将其升级在 SharePoint 网站上，并确认升级部署步骤不会覆盖新项。

#### <a name="to-manually-add-an-item-to-the-list"></a>若要手动将某项添加到列表

1. 在功能区在 SharePoint 站点下**列表工具**选项卡上，选择**项**选项卡。

2. 在中**新建**组中，选择**新项**。

     作为替代方法，你可以选择**添加新项**项列表自身的链接。

3. 在**员工-新项**窗口，请在**标题**框中，输入**设施 Manager**。

4. 在中**名字**框中，输入**Andy**。

5. 在中**公司**框中，键入**Contoso**。

6. 选择**保存**按钮，验证是否在列表中，将出现新项，然后关闭 web 浏览器。

     稍后在本演练中，将使用此项以验证升级部署步骤不会覆盖此列表的内容。

#### <a name="to-test-the-upgrade-deployment-step"></a>若要测试升级的部署步骤

1. 在 Visual Studio 的实验实例中**解决方案资源管理器**，打开快捷菜单**EmployeesListDefinition**项目节点，然后选择**属性**.

    打开属性编辑器/设计器。

2. 上**SharePoint**选项卡上，设置**活动部署配置**属性设置为**升级**。

    此自定义部署配置包括新的升级部署步骤。

3. 打开快捷菜单**员工列表**项，项目，然后选择**属性**或**打开**。

    打开属性编辑器/设计器。

4. 上**视图**选项卡上，选择**电子邮件**列，然后选择 **<** 键，将移动该列从**所选列**到列出**可用列**列表。

    此操作将删除这些字段的默认视图**员工**SharePoint 站点上的列表。

5. 开始调试通过选择**F5**关键的或在菜单栏中选择**调试** > **开始调试**。

6. 验证中设置的断点处停止 Visual Studio 的其他实例中的代码`CanExecute`方法。

7. 选择**F5**再次键，或在菜单栏上选择**调试** > **继续**。

8. 验证代码中设置的断点处停止`Execute`方法。

9. 选择**F5**键，或在菜单栏上选择**调试** > **继续**最后一次。

     Web 浏览器打开 SharePoint 站点。

10. 在中**列出了**部分的快速启动区域中，选择**员工**列表，并验证以下详细信息：

    - 手动添加前面 （对于 Andy、 设施管理器) 的项所做的列表。

    - **办公电话**并**电子邮件地址**列不会显示在此视图中的列表。

      **升级**部署配置修改现有**员工**SharePoint 站点上的列表实例。 如果您使用了**默认**而不是部署配置**升级**配置，则会遇到部署冲突。 Visual Studio 会通过替换来解决该冲突**员工**列表中，Andy，设备管理器的项将删除。

## <a name="clean-up-the-development-computer"></a>清理开发计算机
 测试升级的部署步骤完成后，从 SharePoint 站点中删除列表实例和列表定义，并从 Visual Studio 中删除部署步骤扩展。

#### <a name="to-remove-the-list-instance-from-the-sharepoint-site"></a>若要从 SharePoint 站点中删除列表实例

1. 打开**员工**列出 SharePoint 站点上，如果尚未打开列表。

2. 在功能区中的 SharePoint 站点上，选择**列表工具**选项卡，然后选择**列表**选项卡。

3. 在中**设置**组中，选择**列表设置**项。

4. 下**权限和管理**，选择**删除此列表**命令中，选择**确定**以确认你想要将列表发送到回收站，然后关闭 web浏览器。

#### <a name="to-remove-the-list-definition-from-the-sharepoint-site"></a>若要从 SharePoint 站点中删除列表定义

1. 在实验实例中的 Visual Studio 中，在菜单栏上，选择**构建** > **Retract**。

     Visual Studio 将收回从 SharePoint 站点的列表定义。

#### <a name="to-uninstall-the-extension"></a>卸载扩展

1. 在实验实例中的 Visual Studio 中，在菜单栏上，选择**工具** > **扩展和更新**。

     此时，“扩展和更新”  对话框打开。

2. 在扩展的列表，选择**升级 SharePoint 项目的部署步骤**，然后选择**卸载**命令。

3. 在出现的对话框中，选择**是**以确认你要卸载扩展，然后选择**立即重新启动**以完成卸载。

4. 关闭 Visual Studio （实验实例和在其中 UpgradeDeploymentStep 解决方案已打开的 Visual Studio 的实例） 的两个实例。

## <a name="see-also"></a>请参阅
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
