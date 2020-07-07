---
title: 为 SharePoint 项目创建自定义部署步骤
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 56fac2be1e73de5df9da8aa13e6631c4cc9d1022
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015899"
---
# <a name="walkthrough-create-a-custom-deployment-step-for-sharepoint-projects"></a>演练：为 SharePoint 项目创建自定义部署步骤
  部署 SharePoint 项目时，Visual Studio 会按特定顺序执行一系列部署步骤。 Visual Studio 包含许多内置的部署步骤，但你也可以创建自己的部署步骤。

 在本演练中，您将创建一个自定义部署步骤来升级运行 SharePoint 的服务器上的解决方案。 Visual Studio 包含许多任务（例如，收回或添加解决方案）的内置部署步骤，但它不包括升级解决方案的部署步骤。 默认情况下，在部署 SharePoint 解决方案时，Visual Studio 会先收回解决方案（如果已部署），然后重新部署整个解决方案。 有关内置部署步骤的详细信息，请参阅[部署、发布和升级 SharePoint 解决方案包](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)。

 本演练演示了下列任务：

- 创建执行两个主要任务的 Visual Studio 扩展：

  - 此扩展定义用于升级 SharePoint 解决方案的自定义部署步骤。

  - 该扩展创建一个定义新部署配置的项目扩展，这是针对给定项目执行的一组部署步骤。 新的部署配置包括自定义部署步骤和几个内置的部署步骤。

- 创建扩展程序集调用的两个自定义 SharePoint 命令。 SharePoint 命令是扩展程序集可以调用的方法，以在 SharePoint 的服务器对象模型中使用 Api。 有关详细信息，请参阅[调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

- 生成 Visual Studio 扩展（VSIX）包以部署两个程序集。

- 测试新的部署步骤。

## <a name="prerequisites"></a>先决条件
 若要完成本演练，开发计算机上需要以下组件：

- 支持的 Windows、SharePoint 和 Visual Studio 版本。

- Visual Studio SDK。 本演练使用 SDK 中的**Vsix 项目**模板来创建用于部署扩展的 vsix 包。 有关详细信息，请参阅[在 Visual Studio 中扩展 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

  以下概念的知识非常有用，但不是必需的，无法完成本演练：

- 使用 SharePoint 的服务器对象模型。 有关详细信息，请参阅[使用 SharePoint Foundation 服务器端对象模型](/previous-versions/office/developer/sharepoint-2010/ee538251(v=office.14))。

- SharePoint 解决方案。 有关详细信息，请参阅[解决方案概述](/previous-versions/office/developer/sharepoint-2010/aa543214(v=office.14))。

- 升级 SharePoint 解决方案。 有关详细信息，请参阅[升级解决方案](/previous-versions/office/developer/sharepoint-2010/aa543659(v=office.14))。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，必须创建三个项目：

- 用于创建 VSIX 包以部署扩展的 VSIX 项目。

- 实现扩展的类库项目。 此项目必须针对 .NET Framework 4.5。

- 用于定义自定义 SharePoint 命令的类库项目。 此项目必须针对 .NET Framework 3.5。

  通过创建项目开始演练。

#### <a name="to-create-the-vsix-project"></a>创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

3. 在 "**新建项目**" 对话框中，展开 " **Visual c #** " 或 " **Visual Basic** " 节点，然后选择 "**扩展性**" 节点。

    > [!NOTE]
    > 只有在安装 Visual Studio SDK 时，"**扩展性**" 节点才可用。 有关详细信息，请参阅本主题前面的先决条件部分。

4. 在对话框顶部，选择 .NET Framework 的版本列表中 **.NET Framework "4.5** "。

5. 选择 " **VSIX 项目**" 模板，将项目命名为 " **UpgradeDeploymentStep**"，然后选择 **"确定"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将**UpgradeDeploymentStep**项目添加到**解决方案资源管理器**。

#### <a name="to-create-the-extension-project"></a>创建扩展项目

1. 在**解决方案资源管理器**中，打开 UpgradeDeploymentStep 解决方案节点的快捷菜单，选择 "**添加**"，然后选择 "**新建项目**"。

2. 在 "**新建项目**" 对话框中，展开 " **Visual c #** " 或 " **Visual Basic** " 节点，然后选择 " **Windows** " 节点。

3. 在对话框顶部，选择 .NET Framework 的版本列表中 **.NET Framework "4.5** "。

4. 选择 "**类库" 项目模板**，将项目命名为 " **DeploymentStepExtension**"，然后选择 **"确定"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将**DeploymentStepExtension**项目添加到解决方案，并打开默认的 Class1 代码文件。

5. 从项目中删除 Class1 代码文件。

#### <a name="to-create-the-sharepoint-command-project"></a>创建 SharePoint 命令项目

1. 在**解决方案资源管理器**中，打开 UpgradeDeploymentStep 解决方案节点的快捷菜单，选择 "**添加**"，然后选择 "**新建项目**"。

2. 在 "**新建项目**" 对话框中，展开 " **Visual c #** " 或 " **Visual Basic**"，然后选择 " **Windows** " 节点。

3. 在对话框顶部，选择 .NET Framework 的版本列表中 **.NET Framework "3.5** "。

4. 选择 "**类库" 项目模板**，将项目命名为 " **SharePointCommands**"，然后选择 **"确定"** 按钮。

     Visual Studio 会将**SharePointCommands**项目添加到解决方案中，并打开默认的 Class1 代码文件。

5. 从项目中删除 Class1 代码文件。

## <a name="configure-the-projects"></a>配置项目
 在编写代码以创建自定义部署步骤之前，必须添加代码文件和程序集引用，并且必须配置这些项目。

#### <a name="to-configure-the-deploymentstepextension-project"></a>配置 DeploymentStepExtension 项目

1. 在**DeploymentStepExtension**项目中，添加两个具有以下名称的代码文件：

    - UpgradeStep

    - DeploymentConfigurationExtension

2. 打开 DeploymentStepExtension 项目的快捷菜单，然后选择 "**添加引用**"。

3. 在 "**框架**" 选项卡上，选中 "system.componentmodel" 程序集对应的复选框。

4. 在 "**扩展**" 选项卡上，选中 "VisualStudio" 程序集对应的复选框，然后选择 **"确定"** 按钮。

#### <a name="to-configure-the-sharepointcommands-project"></a>配置 SharePointCommands 项目

1. 在**SharePointCommands**项目中，添加一个名为命令的代码文件。

2. 在**解决方案资源管理器**中，打开**SharePointCommands**项目节点上的快捷菜单，然后选择 "**添加引用**"。

3. 在 "**扩展**" 选项卡上，选中以下程序集对应的复选框，然后单击 **"选择" "确定"** 按钮

    - Microsoft SharePoint

    - VisualStudio 命令

## <a name="define-the-custom-deployment-step"></a>定义自定义部署步骤
 创建用于定义升级部署步骤的类。 为了定义部署步骤，类实现了 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep> 接口。 每当要定义自定义部署步骤时，都要实现此接口。

#### <a name="to-define-the-custom-deployment-step"></a>定义自定义部署步骤

1. 在**DeploymentStepExtension**项目中，打开 UpgradeStep 代码文件，然后将以下代码粘贴到其中。

    > [!NOTE]
    > 添加此代码后，该项目将会出现一些编译错误，但当你在后续步骤中添加代码时，这些错误将消失。

     [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#1](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/upgradestep.cs#1)]
     [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#1](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/upgradestep.vb#1)]

## <a name="create-a-deployment-configuration-that-includes-the-custom-deployment-step"></a>创建包含自定义部署步骤的部署配置
 为新的部署配置创建项目扩展，其中包括多个内置部署步骤和新的升级部署步骤。 通过创建此扩展，可帮助 SharePoint 开发人员使用 SharePoint 项目中的升级部署步骤。

 为了创建部署配置，类实现了 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 接口。 每当要创建 SharePoint 项目扩展时，都要实现此接口。

#### <a name="to-create-the-deployment-configuration"></a>创建部署配置

1. 在**DeploymentStepExtension**项目中，打开 DeploymentConfigurationExtension 代码文件，然后将以下代码粘贴到其中。

     [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#2](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/deploymentconfigurationextension.cs#2)]
     [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#2](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/deploymentconfigurationextension.vb#2)]

## <a name="create-the-custom-sharepoint-commands"></a>创建自定义 SharePoint 命令
 创建两个调入 SharePoint 服务器对象模型的自定义命令。 一个命令确定解决方案是否已部署;其他命令升级解决方案。

#### <a name="to-define-the-sharepoint-commands"></a>定义 SharePoint 命令

1. 在**SharePointCommands**项目中，打开命令代码文件，然后将以下代码粘贴到其中。

     [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#4](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/SharePointCommands/Commands.cs#4)]
     [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#4](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/sharepointcommands/commands.vb#4)]

## <a name="checkpoint"></a>检查点
 在本演练的此时，自定义部署步骤和 SharePoint 命令的所有代码现在都在项目中。 生成它们以确保在编译时不会出错。

#### <a name="to-build-the-projects"></a>生成项目

1. 在**解决方案资源管理器**中，打开**DeploymentStepExtension**项目的快捷菜单，然后选择 "**生成**"。

2. 打开**SharePointCommands**项目的快捷菜单，然后选择 "**生成**"。

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>创建 VSIX 包以部署扩展
 若要部署扩展，请使用解决方案中的 VSIX 项目创建 VSIX 包。 首先，通过修改 VSIX 项目中的 source.extension.vsixmanifest 文件来配置 VSIX 包。 然后通过生成解决方案创建 VSIX 包。

#### <a name="to-configure-and-create-the-vsix-package"></a>配置和创建 VSIX 包

1. 在**解决方案资源管理器**的 " **UpgradeDeploymentStep** " 项目下，打开**source.extension.vsixmanifest**文件的快捷菜单，然后选择 "**打开**"。

     Visual Studio 将在清单编辑器中打开该文件。 Source.extension.vsixmanifest 文件是所有 VSIX 包都需要的 source.extension.vsixmanifest 文件的基础。 有关此文件的详细信息，请参阅[VSIX 扩展架构1.0 引用](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)。

2. 在 "**产品名称**" 框中，输入**SharePoint 项目的升级部署步骤**。

3. 在 "**作者**" 框中，输入 " **Contoso**"。

4. 在 "**说明**" 框中，输入**提供可在 SharePoint 项目中使用的自定义升级部署步骤**。

5. 在编辑器的 "**资产**" 选项卡中，选择 "**新建**" 按钮。

     此时将显示 "**添加新资产**" 对话框。

6. 在 "**类型**" 列表中，选择 " **VisualStudio. microsoft.visualstudio.mefcomponent**"。

    > [!NOTE]
    > 此值与 `MefComponent` source.extension.vsixmanifest 文件中的元素相对应。 此元素指定 VSIX 包中扩展程序集的名称。 有关详细信息，请参阅[Microsoft.visualstudio.mefcomponent 元素（VSX 架构）](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))。

7. 在 "**源**" 列表中，选择 "**当前解决方案中的项目**"。

8. 在 "**项目**" 列表中，选择 " **DeploymentStepExtension**"，然后选择 "**确定"** 按钮。

9. 在清单编辑器中，再次选择 "**新建**" 按钮。

     此时将显示 "**添加新资产**" 对话框。

10. 在 "**类型**" 列表中 **，输入 "node.js"。**

    > [!NOTE]
    > 此元素指定要包含在 Visual Studio 扩展中的自定义扩展。 有关详细信息，请参阅[资产元素（VSX Schema）](https://msdn.microsoft.com/9fcfc098-edc7-484b-9d4c-acd17829d737)。

11. 在 "**源**" 列表中，选择 "**当前解决方案中的项目**"。

12. 在 "**项目**" 列表中，选择 " **SharePointCommands**"，然后选择 "**确定"** 按钮。

13. 在菜单栏上，选择 "**生成**" "生成  >  **解决方案**"，然后确保解决方案在编译时不会出错。

14. 请确保 UpgradeDeploymentStep 项目的生成输出文件夹现在包含 UpgradeDeploymentStep 文件。

     默认情况下，生成输出文件夹为。包含项目文件的文件夹下的 \bin\Debug 文件夹。

## <a name="prepare-to-test-the-upgrade-deployment-step"></a>准备测试升级部署步骤
 若要测试升级部署步骤，你必须首先将示例解决方案部署到 SharePoint 站点。 首先在 Visual Studio 的实验实例中调试扩展。 然后，创建一个用于测试部署步骤的列表定义和列表实例，然后将其部署到 SharePoint 站点。 接下来，修改列表定义和列表实例，并重新部署它们以演示默认部署过程如何覆盖 SharePoint 站点上的解决方案。

 稍后在本演练中，你将修改列表定义和列表实例，然后将它们升级到 SharePoint 站点。

#### <a name="to-start-debugging-the-extension"></a>开始调试扩展

1. 用管理凭据重启 Visual Studio，然后打开 UpgradeDeploymentStep 解决方案。

2. 在 DeploymentStepExtension 项目中，打开 UpgradeStep 代码文件，然后将一个断点添加到和方法中的第一行代码 `CanExecute` `Execute` 。

3. 选择**F5**键，或在菜单栏上选择 "**调试**" "  >  **开始调试**"，开始调试。

4. Visual Studio 将为 SharePoint Projects\1.0 安装%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Upgrade 部署步骤的扩展，并启动 Visual Studio 的实验实例。 你将在 Visual Studio 的此实例中测试升级部署步骤。

#### <a name="to-create-a-sharepoint-project-with-a-list-definition-and-a-list-instance"></a>使用列表定义和列表实例创建 SharePoint 项目

1. 在 Visual Studio 的实验实例中，在菜单栏上选择 "**文件**" "  >  **新建**  >  **项目**"。

2. 在 "**新建项目**" 对话框中，展开 " **Visual c #** " 节点或**Visual Basic** "节点，展开" **SharePoint** "节点，然后选择" **2010** "节点。

3. 在对话框的顶部，确保 .NET Framework 的版本列表中出现 **.NET Framework 3.5** 。

    和的 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] 项目 [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] 需要此版本的 .NET Framework。

4. 在项目模板列表中，选择 " **SharePoint 2010 项目**"，将项目命名为 " **EmployeesListDefinition**"，然后选择 **"确定"** 按钮。

5. 在 " **SharePoint 自定义向导**" 中，输入要用于调试的站点的 URL。

6. 在 **"什么是此 SharePoint 解决方案的信任级别**" 下，选择 "**部署为场解决方案**" 选项按钮。

   > [!NOTE]
   > 升级部署步骤不支持沙盒解决方案。

7. 选择 **“完成”** 按钮。

    [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]创建 EmployeesListDefinition 项目。

8. 打开 EmployeesListDefinition 项目的快捷菜单，选择 "**添加**"，然后选择 "**新建项**"。

9. 在 "**添加新项-EmployeesListDefinition** " 对话框中，展开 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

10. 选择**列表**项模板，将项目命名为**Employees 列表**，然后选择 "**添加**" 按钮。

     "SharePoint 自定义向导" 随即出现

11. 在 "**选择列表设置**" 页上，验证以下设置，然后选择 "**完成**" 按钮：

    1. **员工列表**显示在 "你**想要为你的列表显示什么名称？"** 框中。

    2. 选择 "**基于以下项创建可自定义的列表：** " 选项按钮。

    3. 在 "**基于以下内容创建可自定义的列表**" 列表中选择**默认值（空白）** 。

       [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]创建具有标题列和一个空实例的 Employees 列表项，并打开列表设计器。

12. 在列表设计器的 "**列**" 选项卡上，选择 "**键入新的或现有的列名称**" 行，然后在 "**列显示名称**" 列表中添加以下列：

    1. 名字

    2. Company

    3. 商务电话

    4. 电子邮件

13. 保存所有文件，然后关闭列表设计器。

14. 在**解决方案资源管理器**中，展开**employees list**节点，然后展开**employees list Instance**子节点。

15. 在*Elements.xml*文件中，将此文件中的默认 xml 替换为以下 xml。 此 XML 将列表的名称更改为**Employees** ，并为名为 Jim Hance 的雇员添加信息。

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

17. 打开 EmployeesListDefinition 项目的快捷菜单，然后选择 "**打开**" 或 "**属性**"。

     "属性设计器" 随即打开。

18. 在 " **SharePoint** " 选项卡上，清除 "**调试后自动收回**" 复选框，然后保存属性。

#### <a name="to-deploy-the-list-definition-and-list-instance"></a>部署列表定义和列表实例

1. 在**解决方案资源管理器**中，选择 " **EmployeesListDefinition** " 项目节点。

2. 在 "**属性**" 窗口中，确保 "**活动部署配置**" 属性设置为 "**默认**"。

3. 选择**F5**键，或在菜单栏上选择 "**调试**" "  >  **开始调试**"。

4. 验证项目是否已成功生成，web 浏览器是否打开 SharePoint 站点，"快速启动" 栏中的 "**列表**" 项是否包括 "新**员工**" 列表，以及 "**雇员**" 列表是否包含 Jim Hance 的条目。

5. 关闭 Web 浏览器。

#### <a name="to-modify-the-list-definition-and-list-instance-and-redeploy-them"></a>修改列表定义和列表实例并重新部署它们

1. 在 EmployeesListDefinition 项目中，打开作为**Employee List 实例**项目项的子项目的*Elements.xml*文件。

2. 删除此 `Data` 元素及其子元素，以从列表中删除 Jim Hance 的条目。

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

4. 打开 "**雇员列表**" 项目项的快捷菜单，然后选择 "**打开**" 或 "**属性**"。

5. 在列表设计器中，选择 "**视图**" 选项卡。

6. 在 "**选定的列**" 列表中，选择 "**附件**"，然后选择 "<" 键将该列移至 "**可用列**" 列表中。

7. 重复上述步骤，将 " **Business Phone** " 列从 "**所选列**" 列表移动到 "**可用列**" 列表。

     此操作从 SharePoint 站点上的 " **Employees** " 列表的默认视图中删除这些字段。

8. 选择**F5**键，或在菜单栏上选择 "**调试**" "  >  **开始调试**"，开始调试。

9. 验证是否出现 "**部署冲突**" 对话框。

     当 Visual Studio 尝试将解决方案（列表实例）部署到已部署该解决方案的 SharePoint 站点时，将显示此对话框。 此对话框在本演练后面的执行升级部署步骤时不会出现。

10. 在 "**部署冲突**" 对话框中，选择 "**自动解决**" 选项按钮。

     Visual Studio 将删除 SharePoint 站点上的列表实例，在项目中部署列表项，然后打开 SharePoint 站点。

11. 在 "快速启动" 栏的 "**列表**" 部分中，选择 "**员工**" 列表，然后验证以下详细信息：

    - "**附件**" 和 "**家庭电话**" 列不会出现在此列表视图中。

    - 列表为空。 当你使用**默认**部署配置来重新部署解决方案时， **Employees**列表已替换为项目中的新的空列表。

## <a name="test-the-deployment-step"></a>测试部署步骤
 你现在已准备好测试升级部署步骤。 首先，将一个项添加到 SharePoint 的列表实例中。 然后，更改列表定义和列表实例，在 SharePoint 站点上升级它们，并确认升级部署步骤不会覆盖新项。

#### <a name="to-manually-add-an-item-to-the-list"></a>手动向列表中添加项

1. 在 SharePoint 站点上的功能区中的 "**列表工具**" 选项卡下，选择 "**项**" 选项卡。

2. 在 "**新建**" 组中，选择 "**新建项**"。

     作为替代方法，你可以选择项列表中的 "**添加新项**" 链接。

3. 在 "**员工-新建项目**" 窗口的 "**标题**" 框中，输入 "**设施经理**"。

4. 在 "**名字**" 框中，输入 " **y**"。

5. 在 "**公司**" 框中，键入**Contoso**。

6. 选择 "**保存**" 按钮，验证新项是否显示在列表中，然后关闭 web 浏览器。

     稍后在本演练中，你将使用此项来验证升级部署步骤不会覆盖此列表中的内容。

#### <a name="to-test-the-upgrade-deployment-step"></a>测试升级部署步骤

1. 在 Visual Studio 的实验实例中，在**解决方案资源管理器**中，打开**EmployeesListDefinition**项目节点的快捷菜单，然后选择 "**属性**"。

    此时将打开属性编辑器/设计器。

2. 在**SharePoint**选项卡上，将 "**活动部署配置**" 属性设置为 "**升级**"。

    此自定义部署配置包括新的升级部署步骤。

3. 打开 "**雇员列表**" 项目项的快捷菜单，然后选择 "**属性**" 或 "**打开**"。

    此时将打开属性编辑器/设计器。

4. 在 "**视图**" 选项卡上，选择 "**电子邮件**" 列，然后选择 **<** 要将该列从 "**所选列**" 列表移动到 "**可用列**" 列表的键。

    此操作从 SharePoint 站点上的 " **Employees** " 列表的默认视图中删除这些字段。

5. 选择**F5**键，或在菜单栏上选择 "**调试**" "  >  **开始调试**"，开始调试。

6. 验证 Visual Studio 的另一个实例中的代码是否在您之前在方法中设置的断点处停止 `CanExecute` 。

7. 再次选择**F5**键，或在菜单栏上选择 "**调试**  >  **继续**"。

8. 验证代码是否在您之前在方法中设置的断点处停止 `Execute` 。

9. 选择**F5**键，或在菜单栏上选择 "**调试**  >  **继续**" "最后一次"。

     Web 浏览器将打开 SharePoint 站点。

10. 在 "快速启动" 区域的 "**列表**" 部分中，选择 "**员工**" 列表，然后验证以下详细信息：

    - 之前手动添加的项（对于 "设备管理器"）仍在列表中。

    - "**业务电话**" 和 "**电子邮件地址**" 列不会出现在此列表视图中。

      **升级**部署配置修改 SharePoint 站点上的现有**Employees**列表实例。 如果使用**默认**部署配置而不是**升级**配置，则会遇到部署冲突。 Visual Studio 将通过替换**Employees**列表解决冲突，并将删除 "设备管理器" 的项。

## <a name="clean-up-the-development-computer"></a>清理开发计算机
 完成升级部署步骤的测试后，从 SharePoint 站点中删除列表实例和列表定义，并从 Visual Studio 中删除部署步骤扩展。

#### <a name="to-remove-the-list-instance-from-the-sharepoint-site"></a>从 SharePoint 站点中删除列表实例

1. 如果列表尚未打开，则打开 SharePoint 站点上的 " **Employees** " 列表。

2. 在 SharePoint 站点上的功能区中，选择 "**列表工具**" 选项卡，然后选择 "**列表**" 选项卡。

3. 在 "**设置**" 组中，选择 "**列表设置**" 项。

4. 在 "**权限和管理**" 下，选择 "**删除此列表**" 命令，选择 **"确定"** 以确认要将列表发送到回收站，然后关闭 web 浏览器。

#### <a name="to-remove-the-list-definition-from-the-sharepoint-site"></a>从 SharePoint 站点中删除列表定义

1. 在 Visual Studio 的实验实例中，在菜单栏上选择 "**生成**  >  **收回**"。

     Visual Studio 从 SharePoint 站点收回列表定义。

#### <a name="to-uninstall-the-extension"></a>卸载扩展

1. 在 Visual Studio 的实验实例中，在菜单栏上选择 "**工具**" "  >  **扩展和更新**"。

     此时，“扩展和更新”**** 对话框打开。

2. 在扩展列表中，选择 " **SharePoint 项目的升级部署步骤**"，然后选择 "**卸载**" 命令。

3. 在出现的对话框中，选择 **"是"** 以确认要卸载扩展，然后选择 "**立即重新启动**" 以完成卸载。

4. 关闭 Visual Studio 的两个实例（在其中打开 UpgradeDeploymentStep 解决方案的实验实例和 Visual Studio 的实例）。

## <a name="see-also"></a>另请参阅
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
