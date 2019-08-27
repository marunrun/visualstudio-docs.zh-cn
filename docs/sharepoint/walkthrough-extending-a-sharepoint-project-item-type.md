---
title: 演练：扩展 SharePoint 项目项类型 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 795cc62ca88f7ede87e978d910d397e0ce6e2ad7
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825975"
---
# <a name="walkthrough-extend-a-sharepoint-project-item-type"></a>演练：扩展 SharePoint 项目项类型
  可以使用**业务数据连接模型**项目项以在 SharePoint 中创建业务数据连接 (BDC) 服务的模型。 默认情况下，通过使用此项目项，创建模型时模型中的数据是不向用户显示。 此外必须在 SharePoint 以使用户能够查看的数据创建外部列表。

 在本演练中，您将创建的扩展**业务数据连接模型**项目项。 开发人员可以使用该扩展在其显示 BDC 模型中的数据的项目中创建外部列表。 本演练演示了下列任务：

- 创建 Visual Studio 扩展将执行两项主要任务：

  - 它将生成 BDC 模型中显示的数据的外部列表。 扩展使用的 SharePoint 项目系统的对象模型来生成*Elements.xml*定义列表的文件。 它还将文件添加到项目，以便与 BDC 模型一起部署。

  - 它将添加到快捷菜单项**业务数据连接模型**项目中的项**解决方案资源管理器**。 开发人员可以单击此菜单项可生成 BDC 模型的外部列表。

- 生成 Visual Studio 扩展 (VSIX) 包将部署扩展插件程序集。

- 测试扩展。

## <a name="prerequisites"></a>系统必备
 需要要完成本演练的开发计算机上安装以下组件：

- 支持的 Microsoft Windows、 SharePoint 和 Visual Studio 版本。

- [!include[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)] 本演练使用**VSIX 项目**中此 SDK 来创建 VSIX 包来部署项目项模板。 有关详细信息，请参阅[扩展 Visual Studio 中的 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

  了解以下概念很有帮助，但不是必需，若要完成本演练：

- 中的 BDC 服务[!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)]。 有关详细信息，请参阅[BDC 体系结构](http://go.microsoft.com/fwlink/?LinkId=177798)。

- BDC 模型的 XML 架构。 有关详细信息，请参阅[BDC 模型基础结构](http://go.microsoft.com/fwlink/?LinkId=177799)。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练中，您需要创建两个项目：

- 若要创建要部署项目项扩展的 VSIX 包一个 VSIX 项目。

- 一个用于实现项目项扩展的库项目。

  首先演练创建项目。

#### <a name="to-create-the-vsix-project"></a>若要创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件”   > “新建”   > “项目”  。

3. 在中**新的项目**对话框框中，展开**Visual C#** 或**Visual Basic**节点，然后选择**扩展性**节点。

    > [!NOTE]
    > **扩展性**节点是安装 Visual Studio SDK 的情况下才可用。 有关详细信息，请参阅本主题前面的先决条件部分。

4. 在顶部的列表**新的项目**对话框框中，选择 **.NET Framework 4.5**。

     SharePoint 工具扩展需要在此版本的.NET Framework 的功能。

5. 选择**VSIX 项目**模板。

6. 在中**名称**框中，输入**GenerateExternalDataLists**，然后选择**确定**按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将添加**GenerateExternalDataLists**投影到**解决方案资源管理器**。

7. 如果未自动打开 source.extension.vsixmanifest 文件，请在 GenerateExternalDataLists 项目中，打开其快捷菜单，然后选择**打开**

8. 验证是否 source.extension.vsixmanifest 文件中有一个非空白条目 （输入 Contoso） 的作者字段中，保存该文件，并将其然后关闭。

#### <a name="to-create-the-extension-project"></a>若要创建扩展项目

1. 在中**解决方案资源管理器**，打开快捷菜单**GenerateExternalDataLists**解决方案节点，选择**添加**，然后选择**新项目**.

2. 在中**添加新项目**对话框框中，展开**Visual C#** 或**Visual Basic**节点，然后选择**Windows**节点。

3. 在顶部的对话框的列表中选择 **.NET Framework 4.5**。

4. 在项目模板列表中，选择**类库**。

5. 在中**名称**框中，输入**BdcProjectItemExtension**，然后选择**确定**按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将添加**BdcProjectItemExtension**到解决方案并打开默认 Class1 代码文件。

6. 从项目中删除的 Class1 代码文件。

## <a name="configure-the-extension-project"></a>配置扩展项目
 编写代码以创建项目项扩展之前，添加代码文件和程序集引用的扩展项目。

#### <a name="to-configure-the-project"></a>若要配置项目

1. 在 BdcProjectItemExtension 项目中，添加具有以下名称的两个文件：

    - ProjectItemExtension

    - GenerateExternalDataLists

2. 选择 BdcProjectItemExtension 项目，然后在菜单栏上选择**项目** > **添加引用**。

3. 下**程序集**节点，选择**Framework**节点，然后选择复选框为每个以下程序集：

    - System.ComponentModel.Composition

    - WindowsBase

4. 下**程序集**节点，选择**扩展**节点，并选择复选框为以下程序集：

    - Microsoft.VisualStudio.SharePoint

5. 选择**确定**按钮。

## <a name="define-the-project-item-extension"></a>定义项目项扩展
 创建一个定义的扩展类**业务数据连接模型**项目项。 若要定义扩展，此类应实现<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension>接口。 实现此接口，只要您想要扩展现有的项目项类型。

#### <a name="to-define-the-project-item-extension"></a>若要定义项目项扩展

1. 将以下代码粘贴到 ProjectItemExtension 代码文件。

    > [!NOTE]
    > 添加此代码后，项目将有某些编译错误。 在后续步骤中添加代码时，这些错误将消失。

     [!code-csharp[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#1](../sharepoint/codesnippet/CSharp/generateexternaldatalists/bdcprojectitemextension/projectitemextension.cs#1)]
     [!code-vb[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#1](../sharepoint/codesnippet/VisualBasic/generateexternaldatalists/bdcprojectitemextension/projectitemextension.vb#1)]

## <a name="create-the-external-data-lists"></a>创建外部数据列表
 添加的分部定义`GenerateExternalDataListsExtension`BDC 模型中创建的外部数据列表的每个实体的类。 若要创建外部数据列表，此代码将首先通过分析 BDC 模型文件中的 XML 数据读取 BDC 模型中的实体数据。 然后，它创建 BDC 模型为基础，并将此列表实例添加到项目的列表实例。

#### <a name="to-create-the-external-data-lists"></a>若要创建外部数据列表

1. 将以下代码粘贴到 GenerateExternalDataLists 代码文件。

     [!code-vb[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#2](../sharepoint/codesnippet/VisualBasic/generateexternaldatalists/bdcprojectitemextension/generateexternaldatalists.vb#2)]
     [!code-csharp[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#2](../sharepoint/codesnippet/CSharp/generateexternaldatalists/bdcprojectitemextension/generateexternaldatalists.cs#2)]

## <a name="checkpoint"></a>检查点
 此时在演练中，项目项扩展的所有代码都现项目中。 生成解决方案以确保该项目在编译时没有错误。

#### <a name="to-build-the-solution"></a>生成解决方案

1. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

## <a name="create-a-vsix-package-to-deploy-the-project-item-extension"></a>创建 VSIX 包来部署项目项扩展
 若要将扩展部署，使用 VSIX 项目在解决方案中创建 VSIX 包。 首先，通过修改包含在 VSIX 项目的 source.extension.vsixmanifest 文件中配置 VSIX 包。 然后，通过生成解决方案中创建 VSIX 包。

#### <a name="to-configure-and-create-the-vsix-package"></a>若要配置和创建 VSIX 包

1. 在中**解决方案资源管理器**，在 GenerateExternalDataLists 项目中，打开 source.extension.vsixmanifest 文件中的快捷菜单，然后选择**打开**。

     Visual Studio 清单编辑器中打开该文件。 在 source.extension.vsixmanifest 文件是 extension.vsixmanifest 文件的基础所需的所有 VSIX 包。 有关此文件的详细信息，请参阅[VSIX 扩展架构 1.0 参考](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)。

2. 在中**产品名称**框中，输入**外部数据列表生成器**。

3. 在中**作者**框中，输入**Contoso**。

4. 在中**描述**框中，输入**的业务数据连接模型可用于生成外部数据列表的项目项的扩展**。

5. 上**资产**选项卡的编辑器中，选择**新建**按钮。

     **添加新资产**对话框随即出现。

6. 在中**类型**列表中，选择**Microsoft.VisualStudio.MefComponent**。

    > [!NOTE]
    > 此值对应于`MefComponent`extension.vsixmanifest 文件中的元素。 此元素指定 VSIX 包中的扩展插件程序集名称。 有关详细信息，请参阅[MEFComponent 元素 （VSX 架构）](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))。

7. 在中**源**列表中，选择**当前解决方案中的项目**。

8. 在中**项目**列表中，选择**BdcProjectItemExtension**，然后选择**确定**按钮。

9. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

10. 请确保项目编译和生成未出现错误。

11. 请确保 GenerateExternalDataLists 项目的生成输出文件夹现在包含 GenerateExternalDataLists.vsix 文件。

     默认情况下，生成输出文件夹是...包含项目文件的文件夹下的 \bin\Debug 文件夹。

## <a name="test-the-project-item-extension"></a>测试项目项扩展
 现在您就可以测试项目项扩展。 首先，开始调试 Visual Studio 的实验实例中的扩展项目。 然后，使用 Visual Studio 的实验实例中扩展插件生成 BDC 模型的外部列表。 最后，打开要验证它按预期方式工作的 SharePoint 站点上的外部列表。

#### <a name="to-start-debugging-the-extension"></a>若要开始调试扩展

1. 如有必要，使用管理凭据，重新启动 Visual Studio，然后打开 GenerateExternalDataLists 解决方案。

2. 在 BdcProjectItemExtension 项目中，打开 ProjectItemExtension 代码文件，并将断点添加到中的代码行`Initialize`方法。

3. 打开 GenerateExternalDataLists 代码文件，并将断点添加到代码中的第一行`GenerateExternalDataLists_Execute`方法。

4. 开始调试通过选择**F5**关键的或在菜单栏中选择**调试** > **开始调试**。

     Visual Studio 会将扩展安装到 %UserProfile%\AppData\Local\Microsoft\VisualStudio\10.0Exp\Extensions\Contoso\External 数据列表 Generator\1.0 并启动 Visual Studio 的实验实例。 在 Visual Studio 的此实例中，将测试项目项。

#### <a name="to-test-the-extension"></a>若要测试此扩展

1. 在实验实例中的 Visual Studio 中，在菜单栏上，选择**文件** > **新建** > **项目**。

2. 在**新的项目**对话框框中，展开**模板**节点，展开**Visual C#** 节点，展开**SharePoint**节点，然后选择**2010年**。

3. 在顶部的对话框的列表中，请确保 **.NET Framework 3.5**处于选中状态。 为项目[!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)]需要此版本的.NET Framework。

4. 在项目模板列表中，选择**SharePoint 2010 项目**。

5. 在中**名称**框中，输入**SharePointProjectTestBDC**，然后选择**确定**按钮。

6. 在 SharePoint 自定义向导中，输入你想要使用以进行调试，请选择该站点的 URL**部署为场解决方案**，然后选择**完成**按钮。

7. 打开 SharePointProjectTestBDC 项目的快捷菜单中，选择**外**，然后选择**新项**。

8. 在中**添加 NewItem-SharePointProjectTestBDC**对话框框中，展开已安装的语言节点，展开**SharePoint**节点。

9. 选择**2010年**节点，然后选择**业务数据连接模型 （仅场解决方案）** 模板。

10. 在中**名称**框中，输入**TestBDCModel**，然后选择**添加**按钮。

11. 验证中设置的断点处停止 Visual Studio 的其他实例中的代码`Initialize`ProjectItemExtension 代码文件的方法。

12. 在 Visual Studio 的已停止实例中，选择**F5**键，或在菜单栏上选择**调试** > **继续**继续调试项目。

13. 在 Visual Studio 的实验实例中，选择**F5**密钥，或在菜单栏上依次选择**调试** > **开始调试**生成、 部署和运行**TestBDCModel**项目。

     指定用于调试的 SharePoint 站点的默认页将打开 web 浏览器。

14. 确认**列出了**部分的快速启动区域中尚不包含基于项目中的默认 BDC 模型的列表。 通过使用 SharePoint 用户界面或通过使用项目项扩展，必须先创建一个外部数据的列表。

15. 关闭 Web 浏览器。

16. 在有 TestBDCModel 项目打开的 Visual Studio 的实例中，打开快捷菜单**TestBDCModel**中的节点**解决方案资源管理器**，然后选择**生成外部数据列表**。

17. 验证中设置的断点处停止 Visual Studio 的其他实例中的代码`GenerateExternalDataLists_Execute`方法。 选择**F5**密钥，或在菜单栏上依次选择**调试** > **继续**继续调试项目。

18. Visual Studio 的实验实例中添加列表实例名为**Entity1DataList** TestBDCModel 到项目中和实例还会生成一项功能，名为**功能 2**的列表实例。

19. 选择**F5**密钥，或在菜单栏上依次选择**调试** > **开始调试**生成、 部署和运行 TestBDCModel 项目。

     Web 浏览器会打开用于调试的 SharePoint 站点的默认页面。

20. 在中**列出了**部分的快速启动区域中，选择**Entity1DataList**列表。

21. 验证列表中包含名为 Identifier1 和 Message，除了具有 Identifier1 值 0 和 Hello World 消息值的一项的列。

     **业务数据连接模型**项目模板生成的默认 BDC 模型提供所有这些数据。

22. 关闭 Web 浏览器。

## <a name="clean-up-the-development-computer"></a>清理开发计算机
 测试项目项扩展完成后，从 SharePoint 站点中删除的外部列表和 BDC 模型，并从 Visual Studio 中删除项目项扩展。

#### <a name="to-remove-the-external-data-list-from-the-sharepoint-site"></a>若要从 SharePoint 站点中删除外部数据列表

1. 在 SharePoint 站点的快速启动区域中，选择**Entity1DataList**列表。

2. 在功能区中的 SharePoint 站点上，选择**列表**选项卡。

3. 上**列表**选项卡上，在**设置**组中，选择**列表设置**。

4. 下**权限和管理**，选择**删除此列表**，然后选择**确定**以确认你想要将此列表发送到回收站。

5. 关闭 Web 浏览器。

#### <a name="to-remove-the-bdc-model-from-the-sharepoint-site"></a>若要从 SharePoint 站点中删除 BDC 模型

1. 在实验实例中的 Visual Studio 中，在菜单栏上，选择**构建** > **Retract**。

     Visual Studio 从 SharePoint 站点中删除 BDC 模型。

#### <a name="to-remove-the-project-item-extension-from-visual-studio"></a>若要从 Visual Studio 中删除项目项扩展

1. 在实验实例中的 Visual Studio 中，在菜单栏上，选择**工具** > **扩展和更新**。

     此时，“扩展和更新”  对话框打开。

2. 在扩展的列表，选择**外部的数据列表生成器**，然后选择**卸载**按钮。

3. 在出现的对话框中，选择**是**以确认你想要卸载扩展。

4. 选择**立即重新启动**以完成卸载。

5. 关闭 Visual Studio （实验实例和在其中 GenerateExternalDataLists 解决方案已打开的实例） 的两个实例。

## <a name="see-also"></a>请参阅
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
- [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
