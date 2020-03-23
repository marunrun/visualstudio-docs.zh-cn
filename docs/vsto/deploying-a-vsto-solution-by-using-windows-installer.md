---
title: 使用 Windows 安装程序部署用于办公室解决方案的可视化工作室工具
ms.date: 08/18/2010
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, setup project
- Office development in Visual Studio, MSI
- deploying applications [Office development in Visual Studio], setup project
- deploying applications [Office development in Visual Studio], MSI
- ClickOnce deployment [Office development in Visual Studio], MSI
- publishing Office solutions [Office development in Visual Studio], setup project
- Office applications [Office development in Visual Studio], MSI
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 876781cb6967f5d10dddccd54a46e218170445ab
ms.sourcegitcommit: 92361aac3665a934faa081e1d1ea89a067b01c5b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/17/2020
ms.locfileid: "79432197"
---
# <a name="deploying-a-visual-studio-tools-for-office-solution-using-windows-installer"></a>使用 Windows 安装程序部署用于办公室解决方案的可视化工作室工具

## <a name="summary"></a>总结

了解如何使用可视化工作室安装程序项目部署适用于 Office （VSTO） 的 Microsoft 可视化工作室工具外接程序或文档级解决方案。

伍特·范·武格特，代码顾问

泰德·帕蒂森，泰德·帕蒂森集团

本文由 Microsoft 在原始作者的许可下更新。

**适用于：** 办公室视觉工作室工具，微软办公室，微软视觉工作室。

## <a name="overview"></a>概述

您可以使用 Windows 安装程序包开发 VSTO 解决方案并部署解决方案。 此讨论包括部署简单 Office 外接程序的步骤。

## <a name="deployment-methods"></a>部署方法

ClickOnce 可轻松用于为加载项和解决方案创建设置。 但是，它无法安装需要管理权限（如计算机级加载项）的加载项。

可以使用 Windows 安装程序安装需要管理权限的加载项，但创建安装程序确实需要付出更多努力。

有关如何使用 ClickOnce 部署 VSTO 解决方案的概述，请参阅[使用 ClickOnce 部署 Office 解决方案](deploying-an-office-solution-by-using-clickonce.md)。

## <a name="deploying-office-solutions-that-target-the-vsto-runtime"></a>部署面向 VSTO 运行时的 Office 解决方案

单击"一次"和"Windows 安装程序"包需要在安装 Office 解决方案时执行相同的基本任务。

1. 在用户计算机上安装必备组件。
2. 部署解决方案的特定组件。
3. 对于外接程序，请创建注册表项。
4. 信任解决方案以允许其执行。

### <a name="required-prerequisite-components-on-the-target-computer"></a>目标计算机上的必需先决条件组件

下面是计算机上必须安装的软件列表才能运行 VSTO 解决方案：

- 微软 Office 2010 或更新。
- 微软 .NET 框架 4 或更新。
- Microsoft Visual Studio 2010 Tools for Office Runtime。
  运行时提供了一个管理加载项和文档级解决方案的环境。 运行时的版本确实随 Microsoft Office 一起发布，但您可能希望使用外接程序重新分发特定版本。
- 如果您不使用嵌入式互操作类型，则为 Microsoft Office 的主互操作程序集。
- 项目引用的任何实用程序程序集。

### <a name="specific-components-for-the-solution"></a>解决方案的特定组件

安装程序包必须将这些组件安装到用户的计算机：

- 如果创建文档级解决方案，则为 Microsoft Office 文档。
- 自定义程序集及其所需的任何程序集。
- 其他组件，如配置文件。
- 应用程序清单 （.清单）。
- 部署清单 （.vsto）。

### <a name="registry-entries-for-add-ins"></a>外接程序的注册表项

Microsoft Office 使用注册表项查找和加载加载加载加载项。这些注册表项应作为部署过程的一部分创建。 有关这些注册表项的详细信息，请参阅[VSTO 加载项的注册表项](registry-entries-for-vsto-add-ins.md)。

显示自定义窗体区域的 Outlook 加载项需要允许标识窗体区域的其他注册表项。 有关注册表项的详细信息，请参阅[Outlook 窗体区域的注册表项](registry-entries-for-vsto-add-ins.md#OutlookEntries)。

文档级解决方案不需要任何注册表项。 相反，文档内的属性用于查找自定义项。 有关这些属性的详细信息，请参阅[自定义文档属性概述](custom-document-properties-overview.md)。

### <a name="trusting-the-vsto-solution"></a>信任 VSTO 解决方案

为了运行自定义项，计算机必须信任解决方案。 可以通过使用证书对清单进行签名、创建包含列表的信任关系或将其安装到计算机上的受信任位置来信任外接程序。

有关如何获取签名证书的详细信息，请参阅[单击"一次部署"和"身份验证"。](../deployment/clickonce-and-authenticode.md) 有关信任解决方案的详细信息，请参阅[使用包含列表信任办公室解决方案](trusting-office-solutions-by-using-inclusion-lists.md)。 您可以在 Windows 安装程序文件中添加包含列表条目，并包含自定义操作。 有关启用包含列表的详细信息，请参阅[如何：配置包含列表安全性](how-to-configure-inclusion-list-security.md)。

如果未使用这两个选项，则向用户显示信任提示，以让他们决定是否信任解决方案。

有关与文档级解决方案相关的安全性的详细信息，请参阅[授予文档信任](granting-trust-to-documents.md)。

## <a name="creating-a-basic-installer"></a>创建基本安装程序

"设置"和"部署"项目模板包含在可供下载的[Microsoft 可视化工作室安装程序项目](https://marketplace.visualstudio.com/items?itemName=visualstudioclient.MicrosoftVisualStudio2017InstallerProjects)扩展中。

要为 Office 解决方案创建安装程序，必须完成以下任务：

- 添加将部署的 Office 解决方案的组件。
- 对于应用程序级加载项，请配置注册表项。
- 配置必备组件，以便可以在最终用户计算机上安装这些组件。
- 配置启动条件以验证所需的必备组件是否可用。 如果未安装所有必需的先决条件，则启动条件可用于阻止安装。

第一步是创建设置项目。

### <a name="to-create-the-addin-setup-project"></a>创建添加设置项目

1. 打开要部署的 Office 添加项目。 在此示例中，我们使用名为 ExcelAddIn 的 Excel 外接程序。
2. 打开"办公室项目"后，在 **"文件**"菜单上展开 **"添加"，** 然后单击 **"新项目**"以添加新项目。
::: moniker range="=vs-2017"
3. 在"**添加新项目"** 对话框中，在 **"项目类型"** 窗格中展开**其他项目类型**，然后展开 **"设置和部署"，** 然后选择**可视化工作室安装程序**。
4. 在 **"模板"** 窗格中，从**可视化工作室安装**的模板组中选择 **"设置项目**"。
::: moniker-end
::: moniker range="=vs-2019"
3. 在"**添加新项目**"对话框中，选择 **"设置项目"** 模板。
4. 单击“下一步”****。
::: moniker-end

5. 在 **"名称**"框中，键入**OfficeAddInsetup**。
::: moniker range="=vs-2017"
6. 单击 **"打开"** 以创建新的设置项目。
::: moniker-end
::: moniker range="=vs-2019"
6. 单击 **"创建**"以创建新的设置项目。
::: moniker-end

可视化工作室为新的设置项目打开文件系统资源管理器。 文件系统资源管理器允许您将文件添加到设置项目。

   ![设置项目的文件系统资源管理器屏幕截图](media/setup-project-figure-1.png)

   **图 1：设置项目的文件系统资源管理器**

安装程序项目需要部署 ExcelAddIn。 您可以通过将 ExcelAddIn 项目输出添加到安装程序项目来配置此任务的设置项目。

### <a name="to-add-the-exceladdin-project-output"></a>添加 ExcelAddIn 项目输出

1. 在**解决方案资源管理器**中，右键单击**OfficeAddInSetup**，单击 **"添加**"，然后单击 **"项目输出**"。
2. 在 **"添加项目输出组"** 对话框中，从项目列表中选择**ExcelAddIn**和**主输出**。
3. 单击"**确定"** 将项目输出添加到设置项目。

    ![设置项目添加项目输出组对话框的屏幕截图](media/setup-project-figure-2.png)

    **图 2：设置项目 添加项目输出组对话框**

安装程序项目需要部署部署清单和应用程序清单。 从 ExcelAddIn 项目的输出文件夹中将这两个文件作为独立文件添加到安装程序项目中。

### <a name="to-add-the-deployment-and-application-manifests"></a>添加部署和应用程序清单

1. 在**解决方案资源管理器**中，右键单击**OfficeAddInSetup，** 单击"**添加**"，然后单击"**文件**"。
2. 在"**添加文件"** 对话框中，导航到**ExcelAddIn**输出目录。 通常，输出目录是项目根目录的**bin\\发布**子文件夹，具体取决于所选的生成配置。
3. 选择**ExcelAddIn.vsto**和**ExcelAddIn.dll.清单**文件，然后单击 **"打开"** 以将这两个文件添加到设置项目中。

    ![应用程序和部署清单的屏幕截图在解决方案资源管理器中](media/setup-project-figure-3.jpg)

    **图 3：解决方案资源管理器中外接程序的应用程序和部署清单**

引用 ExcelAddIn 包括 ExcelAddIn 需要的所有组件。 必须排除这些组件并使用先决条件包进行部署，以允许正确注册它们。 此外，在安装开始之前，必须显示并接受软件许可条款。

### <a name="to-exclude-the-exceladdin-project-dependencies"></a>排除 ExcelAddIn 项目依赖项

1. 在**解决方案资源管理器**中，在**OfficeAddInSetup**节点中，选择 **"检测到的依赖项"** 项下的所有依赖项项，但**Microsoft .NET 框架**或任何以**\*结尾的程序集除外。公用事业.dll**. 实用程序程序集旨在与应用程序一起部署。
2. 右键单击组并选择 **"属性**"。
3. 在 **"属性"** 窗口中，将 **"排除"** 属性更改为**True**以从设置项目中排除从属程序集。 确保不排除任何实用程序程序集。

    ![解决方案资源管理器的屏幕截图，显示要排除的依赖项](media/setup-project-figure-4.jpg)

    **图 4：排除依赖项**

您可以通过添加安装程序（也称为引导程序）来配置 Windows 安装程序包以安装必备组件。 此设置程序可以安装先决条件组件，此过程称为引导。

对于**ExcelAddIn，** 必须先安装这些先决条件，然后才能正确运行外接程序：

- Office 解决方案所针对的 Microsoft .NET 框架版本。
- Microsoft Visual Studio 2010 Tools for Office Runtime。

将从属组件配置为先决条件

1. 在**解决方案资源管理器**中，右键单击**OfficeAddInSetup**项目并选择**属性**。
2. 将显示 **"OfficeAddInSetup 属性页**"对话框。
3. 单击 **"先决条件"** 按钮。
4. 在"先决条件"对话框中，选择正确的版本的 .NET 框架和适用于 Office 运行时的 Microsoft 可视化工作室工具。

    ![先决条件对话框的屏幕截图](media/setup-project-figure-5.png)

    **图 5：先决条件对话框**

    > [!NOTE]
    >可视化工作室安装程序项目中已配置的一些必备包取决于所选的生成配置。 您必须为使用的每个生成配置选择正确的必备组件。

Microsoft Office 使用注册表项查找加载项。 HKEY\_CURRENT\_用户配置单元中的键用于为每个用户注册外接程序。 HKEY\_LOCAL\_MACHINE 配置单元下的键用于为计算机的所有用户注册外接程序。 有关注册表项的详细信息，请参阅[VSTO 加载项的注册表项](registry-entries-for-vsto-add-ins.md)。

### <a name="to-configure-the-registry"></a>配置注册表

1. 在**解决方案资源管理器**中，右键单击**OfficeAddInSetup**。
2. 展开**视图**。
3. 单击**注册表**以打开注册表编辑器窗口。
4. 在**注册表（OfficeAddInSetup）编辑器中**，展开**HKEY\_LOCAL\_MACHINE，** 然后**展开软件**。
5. 删除在**\[\]** **HKEY\_LOCAL\_MACHINE\\软件**下找到的制造商密钥 。
6. 扩展**\_HKEY\_CURRENT 用户**，然后**扩展软件**。
7. 删除在**\[\] ** **HKEY\_CURRENT\_USER\\软件**下找到的制造商密钥。
8. 要添加外接程序安装的注册表项，请右键单击 **"用户/计算机 Hive"** 键，请选择 **"新建密钥**"。 使用文本**软件**为新密钥的名称。 右键点击新创建**的软件**密钥，并创建一个新的密钥与文本**微软**。
9. 使用类似的过程创建外接程序注册所需的整个密钥层次结构：

    **\\用户/机器蜂巢软件\\微软\\办公室\\\\Excel 加载\\项示例公司.ExcelAddIn**

    公司名称通常用作外接程序名称的前缀，以提供唯一性。

10. 右键单击**示例公司.ExcelAddIn**键，选择 **"新建**"，然后单击**字符串值**。 使用名称的文本**说明**。
11. 使用此步骤可以添加另外三个值：
    - 类型**字符串**的**友好名称**
    - **DWORD**类型的**加载行为**
    - 类型**字符串****的清单**

12. 右键单击注册表编辑器中的 **"描述"** 值，然后单击 **"属性窗口**"。 在 **"属性"窗口中**，为"值"属性输入**Excel 演示添加。**
13. 在注册表编辑器中选择 **"友好名称**"键。 在**属性窗口中**，将**值**属性更改为**Excel 演示添加。**
14. 在注册表编辑器中选择**LoadBehavior**键。 在 **"属性"窗口中**，将 **"值"** 属性更改为**3。** LoadBehavior 的值 3 指示应在启动主机应用程序时加载外接程序。 有关加载行为的详细信息，请参阅[VSTO 加载项的注册表项](registry-entries-for-vsto-add-ins.md)。

15. 在注册表编辑器中选择 **"清单**"键。 在 **"属性"窗口中**，将 **"值"** 属性更改为**文件：//[目标ID_ExcelAddIn.vsto_vsto）本地**

    ![注册表编辑器的屏幕截图](media/setup-project-figure-6.png)

    **图 6：设置注册表项**

      VSTO 运行时使用此注册表项来查找部署清单。 [目标]宏将替换为将外接程序安装到的文件夹。 宏将包含尾随的 * 字符，因此部署清单的文件名应为 ExcelAddIn.vsto，而不显示 * 字符。
      **vstolocal**后缀告诉 VSTO 运行时，外接程序应从此位置加载，而不是 ClickOnce 缓存。 删除此后修复程序将导致运行时将自定义项复制到 ClickOnce 缓存中。

   >[!WARNING]
   >您应该非常小心在可视化工作室的注册表编辑器。 例如，如果您不小心为错误的密钥设置了 DeleteAtUn 安装，则可以删除注册表的活动部分，从而使用户计算机处于不一致甚至更糟的损坏状态。

64 位版本的 Office 将使用 64 位注册表配置单元来查找加载项。要在 64 位注册表配置单元下注册加载项，必须仅将安装程序项目的目标平台设置为 64 位。

1. 在解决方案资源管理器中选择**OfficeAddInSetup**项目。
2. 转到 **"属性"** 窗口并将**TargetPlatform**属性设置为**x64**。

为 32 位和 64 位版本的 Office 安装外接程序需要创建两个单独的 MSI 包。 一个用于 32 位，一个用于 64 位。

  ![属性窗口的屏幕截图，显示用于向 64 位 Office 注册加载项的目标平台](media/setup-project-figure-7.jpg)

  **图 7：用于在 64 位 Office 注册加载项的目标平台**

如果 MSI 包用于安装外接程序或解决方案，则无需安装所需的先决条件即可安装。 如果未安装先决条件，则可以使用 MSI 中的启动条件来阻止外接程序安装。

### <a name="configure-a-launch-condition-to-detect-the-vsto-runtime"></a>配置启动条件以检测 VSTO 运行时

1. 在**解决方案资源管理器**中，右键单击**OfficeAddInSetup**。
2. 展开**视图**。
3. 单击 **"启动条件**"。
4. 在**启动条件（OfficeAddInSetup）编辑器中**，右键单击**目标计算机上的"要求"，** 然后单击"**添加注册表启动条件**"。 此搜索条件可以在注册表中搜索 VSTO 运行时安装的密钥。 然后，通过命名属性向安装程序的各个部分提供密钥的值。 启动条件使用搜索条件定义的属性来检查特定值。
5. 在**启动条件（OfficeAddInSetup）编辑器中**，选择 **"搜索注册表项1"** 搜索条件，右键单击条件，然后选择 **"属性窗口**"。

6. 在 **"属性"** 窗口中，设置以下属性：
   1. 将 **（名称）** 的值设置为**搜索 VSTO 2010 运行时**。
   2. 将**属性**的值更改为**VSTORUNTIMEREDIST**。
   3. 将**RegKey**的值设置为**软件\\微软\\VSTO 运行时\\设置 v4R**
   4. 将**根**属性设置为**vsdrrHKLM**。
   5. 将 **"值"** 属性更改为**版本**。

7. 在**启动条件（OfficeAddInSetup）编辑器中**，选择 **"条件1**启动条件"，右键单击条件，然后选择 **"属性窗口**"。
8. 在“属性”窗口中，设置以下属性：
   1. 将 **（名称）** 设置为**验证 VSTO 2010 运行时可用性**。
   2. 将**条件**的值更改为**\>VSTORUNTIMEREDIST ="10.0.30319"**
   3. 将**InstallURL**属性留空。
   4. 将 **"消息**设置为**可视化工作室 2010"未安装用于办公室运行时的工具。请运行安装程序.exe 以安装外接程序**。

        ![验证运行时可用性启动条件的属性窗口屏幕截图](media/setup-project-figure-8.jpg)

        **图 8：验证运行时可用性启动条件的属性窗口**

 上述启动条件显式检查由引导程序包安装 VSTO 运行时是否存在。

### <a name="configure-a-launch-condition-to-detect-the-vsto-runtime-installed-by-office"></a>配置启动条件以检测 Office 安装的 VSTO 运行时

1. 在**启动条件（OfficeAddInSetup）编辑器中**，右键单击 **"搜索目标计算机**"，然后单击"**添加注册表搜索**"。
2. 选择 **"搜索注册表项1"** 搜索条件，右键单击条件，然后选择 **"属性窗口**"。
3. 在 **"属性"** 窗口中，设置以下属性：
    1. 将 **（名称）** 的值设置为**搜索 Office VSTO 运行时**。
    2. 将**属性**的值更改为**Office Runtime**。
    3. 将**RegKey**的值设置为**软件\\微软\\VSTO 运行时\\设置 v4**。
    4. 将**根**属性设置为**vsdrrHKLM**。
    5. 将 **"值"** 属性更改为**版本**。

4. 在**启动条件（OfficeAddInSetup）编辑器中**，选择 **"验证 VSTO 2010 运行时可用性**启动条件"，右键单击条件，然后选择 **"属性窗口**"。

5. 将**条件**属性的值更改为**VSTORUNTIMEREDIST \>= "10.0.30319" 或 OFFICERUNTIME\>= "10.0.21022"。** 根据外接程序所需的运行时版本，版本号可能会有所不同。

    ![启动条件的属性窗口屏幕截图](media/setup-project-figure-9.jpg)
  
    **图 9：通过 Redist 或 Office 启动条件验证运行时可用性的属性窗口**

如果外接程序的目标是 .NET 框架 4 或更新，则可以将引用的主互通程序集 （PIA） 中的类型嵌入到 VSTO 程序集中。

要通过执行以下步骤来检查 Interop 类型是否会嵌入到外接程序中：

1. 展开解决方案资源管理器中的参考节点
2. 选择其中一个 PIA**引用，例如**Office 。
3. 通过点击 F4 或从"程序集"上下文菜单中选择"属性"来查看属性窗口。
4. 检查属性**嵌入互操作类型的值**。

如果该值设置为**True，** 则嵌入类型，您可以向下跳到[**"新建设置项目**](#to-build-the-setup-project)"部分。

有关详细信息，请参阅[类型等效和嵌入式互操作类型](/dotnet/framework/interop/type-equivalence-and-embedded-interop-types)

### <a name="to-configure-launch-conditions-to-detect-that-for-office-pias"></a>配置启动条件以检测 Office PIA 的启动条件

1. 在**启动条件（OfficeAddInSetup）编辑器中**，右键单击**目标计算机上的"要求"，****然后单击"添加 Windows 安装程序启动条件**"。 此启动条件通过搜索特定组件 ID 来搜索 Office PIA。
2. 右键单击 **"搜索组件 1"** 并单击 **"属性"窗口**以显示启动条件的属性。
3. 在**属性窗口中**，设置以下属性：

    1. 将 **（名称）** 属性的值更改为 **"搜索办公室共享 PIA"**
    2. 将组件**ID**的值更改为正在使用的 Office 组件的组件 ID。 您可以在下表中找到组件 ID 列表，例如 **{64E2917E-AA13-4CA4-BFFE-EA6EDA3AFCB4}。**
    3. 将**属性**属性的值更改为**HASSHAREDPIA**。

4. 在**启动条件（OfficeAddInSetup）编辑器中**，右键单击 **"条件 1"，** 然后单击 **"属性"窗口**以显示启动条件的属性。

5. 更改**条件1**的这些属性 ：

    1. 将 **（名称）** 更改为**验证办公室共享 PIA 可用性**。
    2. 将**条件**更改为**HASSHAREDPIA**。
    3. 将**安装 Url**留空。
    4. 将**消息**更改为**与 Excel 交互所需的组件不可用。请运行 setup.exe**。

    ![验证办公室共享 PIA 启动条件的属性窗口屏幕截图](media/setup-project-figure-10.jpg)
  
    **图 10：验证办公室共享 PIA 启动条件的属性窗口**

### <a name="component-ids-of-the-primary-interop-assemblies-for-microsoft-office"></a>微软办公室主交互程序集的组件 ID

|主互操作程序集|Office 2010|Office 2013|办公室 2013 （64 位）|Office 2016|办公室 2016 （64 位）|
|------------------------|------------------------|------------------------|------------------------|------------------------|------------------------|
|Excel|[EA7564AC-C67D-4868-BE5C-26E4FC2223FF]|[C8A65ABE-3270-4FD7-B854-50C8082C8F39]|[E3BD1151-B9CA-4D45-A77E-51A6E0ED322A]|C4ACE6DB-AA99-401F-8BE6-8784BD09F003*|[C4ACE6DB-AA99-401F-8BE6-8784BD09F003]|
|InfoPath|{4153F732-D670-4E44-8AB7-500F2B576BDA]|[0F825A16-25B2-4771-A497-FC8AF3B355D8]|[C5BBD36E-B320-47EF-A512-556B99CB7E41]|-|-|
|Outlook|{1D844339-3DAE-413E-BC13-62D6A52816B2]|[F9F828D5-9F0B-46F9-9E3E-9C59F3C5E136]|{7824A03F-28CC-4371-BC54-93D15EFC1E7F]|[7C6D92EF-7B45-46E5-8670-819663220E4E]|[7C6D92EF-7B45-46E5-8670-819663220E4E]|
|PowerPoint|[EECBA6B8-3A62-44AD-99EB-866625466F9]|{813139AD-6DAB-4DD-8C6D-0CA30D073B41}|{05758318-BCFD-4288-AD8D-81185841C235}|[E0A76492-0FD5-4EC2-8570-AE1BAA61DC88]|[E0A76492-0FD5-4EC2-8570-AE1BAA61DC88]|
|Visio|{3EA123B5-6316-452E-9D51-A489E06E2347}|[C1713368-12A8-41F1-ACA1-934B01AD6EEB]|[2CC0B221-22D2-4C15-A9FB-DE818E51AF75]|{2D4540EC-2C88-4C28-AE88-2614B5460648]|{2D4540EC-2C88-4C28-AE88-2614B5460648]|
|Word|[8B74A499-37F8-4DEA-B5A0-D72FC501CEFA]|[9FE736B7-B1EE-410C-8D07-082891C3DAC8]|[13C07AF5-B206-4A48-BB5B-B8022333E3CA]|[DC5CCACD-A7AC-4FD3-9F70-9454B5DE5161]|[DC5CCACD-A7AC-4FD3-9F70-9454B5DE5161]|
|微软表格 2.0|[B2279272-3FD2-434D-B94E-E4E0F8561AC4]|[B2279272-3FD2-434D-B94E-E4E0F8561AC4]|[A5A30117-2D2A-4C5C-B3C8-8897AC32C2AC]|-|-|
|Microsoft Graph|{011B9112-EBB1-4A6C-86CB-C2FDC9EA7B0E}|{52DA4B37-B8EB-4B7F-89C1-824654CE4C70}|{24706F33-F0CE-4EB4-BC91-9E935394F510]|-|-|
|智能标记 (Smart Tag)|{7102C98C-EF47-4F04-A227-FE33650BF954]|{487A7921-EB3A-4262-BB5B-A5736B732486}|[74EFC1F9-747D-4867-B951-EFCF29F51AF7]|-|-|
|办公室共享|[64E2917E-AA13-4CA4-BFFE-EA6EDA3AFCB4]|{6A174BDB-0049-4D1C-86EF-3114CB0C4C4E]|{76601EBB-44A7-49EE-8DE3-7B7B9D7EB05]|{625F5772-C1B3-497E-8ABE-7254EDB00506]|{625F5772-C1B3-497E-8ABE-7254EDB00506]|
|Project|{957A4EC0-E67B-4E86-A383-6AF7270B216A}|[1C50E422-24FA-44A9-A120-E88280C8C341]|{706D7F44-8231-489D-9B25-3025ADE9F114]|{107BCD9A-F1DC-4004-A444-33706FC10058}|{107BCD9A-F1DC-4004-A444-33706FC10058}|

  ![最终启动条件的屏幕截图](media/setup-project-figure-11.jpg)

  **图11：最终发射条件**

您可以进一步优化 ExcelAddIn 安装的启动条件。 例如，检查是否安装了实际的目标 Office 应用程序可能很有用。

### <a name="to-build-the-setup-project"></a>生成设置项目

1. 在**解决方案资源管理器**中，右键单击**OfficeAddInSetup**项目，然后单击 **"生成**"。
2. 使用**Windows 资源管理器**，导航到**OfficeAddInSetup**项目的输出目录，然后转到"发布"或"调试"文件夹，具体取决于所选的生成配置。 将所有文件从文件夹复制到用户可以访问的位置。

测试 ExcelAddIn 设置

1. 导航到将**OfficeAddInSetup**复制到的位置。
2. 双击 setup.exe 文件以安装**OfficeAddInSetup**外接程序。 接受显示的任何软件许可条款，并完成设置向导以在用户计算机上安装外接程序。

Excel Office 解决方案应从设置期间指定的位置安装和运行。

## <a name="additional-requirements-for-document-level-solutions"></a>文档级解决方案的其他要求

在 Windows 安装程序安装程序项目中，部署文档级解决方案需要几个不同的配置步骤。

以下是部署文档级解决方案所需的基本步骤的列表：

- 创建可视化工作室设置项目。
- 添加文档级解决方案的主要输出。 主输出还包括 Microsoft Office 文档。
- 将部署和应用程序清单添加为松散文件。
- 从安装程序包中排除从属组件（任何实用程序程序集除外）。
- 配置必备包。
- 配置启动条件。
- 生成设置项目并将结果复制到部署位置。
- 通过执行设置在用户计算机上部署文档级解决方案。
- 如果需要，更新自定义文档属性。

### <a name="changing-the-location-of-the-deployed-document"></a>更改已部署文档的位置

Office 文档中的属性用于查找文档级别解决方案。 如果文档安装到与 VSTO 程序集相同的文件夹中，则无需进行任何更改。 但是，如果将其安装到不同的文件夹，则这些属性需要在设置期间更新。

有关这些文档属性的详细信息，请参阅[自定义文档属性概述](custom-document-properties-overview.md)。

要更改这些属性，需要在设置期间使用自定义操作。

下面的示例使用称为 ExcelWorkbookProject 的文档级解决方案和称为 ExcelWorkbook安装程序的设置项目。 ExcelWorkbook安装程序项目使用上述步骤进行配置，但设置注册表项除外。

将自定义操作项目添加到可视化工作室解决方案

1. 通过右键单击**解决方案资源管理器**中的**Office 文档部署项目**，将新的 .NET 控制台项目添加到解决方案中
2. 展开 **"添加"** 并单击 **"新项目**"。
3. 选择控制台应用模板并命名项目 **"添加自定义自定义操作**"。

    ![解决方案资源管理器的屏幕截图 - 添加自定义自定义操作](media/setup-project-figure-15.jpg)
  
    **图 12：解决方案资源管理器 - 添加自定义自定义操作**

4. 添加对这些程序集的引用：
    1. System.ComponentModel
    2. System.Configuration.Install
    3. 微软.VisualStudio.工具.应用程序
    4. Microsoft.VisualStudio.Tools.Applications.ServerDocument

5. 将此代码复制到Program.cs或程序.vb

```csharp
    using System;
    using System.IO;
    using System.Collections;
    using System.ComponentModel;
    using System.Configuration.Install;
    using Microsoft.VisualStudio.Tools.Applications;
    using Microsoft.VisualStudio.Tools.Applications.Runtime;

    namespace AddCustomizationCustomAction
    {
        [RunInstaller(true)]
        public class AddCustomizations : Installer
        {
            public AddCustomizations() : base() { }

            public override void Install(IDictionary savedState)
            {
                base.Install(savedState);

                //Get the CustomActionData Parameters
                string documentLocation = Context.Parameters.ContainsKey("documentLocation") ? Context.Parameters["documentLocation"] : String.Empty;
                string assemblyLocation = Context.Parameters.ContainsKey("assemblyLocation") ? Context.Parameters["assemblyLocation"] : String.Empty;
                string deploymentManifestLocation = Context.Parameters.ContainsKey("deploymentManifestLocation") ? Context.Parameters["deploymentManifestLocation"] : String.Empty;
                Guid solutionID = Context.Parameters.ContainsKey("solutionID") ? new Guid(Context.Parameters["solutionID"]) : new Guid();

                string newDocLocation = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments), Path.GetFileName(documentLocation));

                try
                {
                    //Move the file and set the Customizations
                    if (Uri.TryCreate(deploymentManifestLocation, UriKind.Absolute, out Uri docManifestLocationUri))
                    {
                        File.Move(documentLocation, newDocLocation);
                        ServerDocument.RemoveCustomization(newDocLocation);
                        ServerDocument.AddCustomization(newDocLocation, assemblyLocation,
                                                        solutionID, docManifestLocationUri,
                                                        true, out string[] nonpublicCachedDataMembers);
                    }
                    else
                    {
                        LogMessage("The document could not be customized.");
                    }
                }
                catch (ArgumentException)
                {
                    LogMessage("The document could not be customized.");
                }
                catch (DocumentNotCustomizedException)
                {
                    LogMessage("The document could not be customized.");
                }
                catch (InvalidOperationException)
                {
                    LogMessage("The customization could not be removed.");
                }
                catch (IOException)
                {
                    LogMessage("The document does not exist or is read-only.");
                }
            }

            public override void Rollback(IDictionary savedState)
            {
                base.Rollback(savedState);
                DeleteDocument();
            }
            public override void Uninstall(IDictionary savedState)
            {
                base.Uninstall(savedState);
                DeleteDocument();
            }
            private void DeleteDocument()
            {
                string documentLocation = Context.Parameters.ContainsKey("documentLocation") ? Context.Parameters["documentLocation"] : String.Empty;

                try
                {
                    File.Delete(Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments), Path.GetFileName(documentLocation)));
                }
                catch (Exception)
                {
                    LogMessage("The document doesn't exist or is read-only.");
                }
            }
            private void LogMessage(string Message)
            {
                if (Context.Parameters.ContainsKey("LogFile"))
                {
                    Context.LogMessage(Message);
                }
            }

            static void Main() { }
            }
    }
```

要将自定义添加到文档，您需要具有 VSTO 文档级解决方案的解决方案 ID。 此值将从可视化工作室项目文件中检索。

检索解决方案 ID

1. 在 **"生成**"菜单上，单击 **"生成解决方案**"以生成文档级解决方案，并将解决方案 ID 属性添加到项目文件中。
2. 在**解决方案资源管理器**中，右键单击文档级项目**ExcelWorkbook 项目**
3. 单击 **"卸载项目"** 从可视化工作室内部访问项目文件。

    ![解决方案资源管理器卸载 Excel 文档解决方案的屏幕截图](media/setup-project-figure-16.jpg)

    **图 13：卸载 Excel 文档解决方案**

4. 在**解决方案资源管理器**中，右键单击**ExcelWorkbook 项目**，然后单击 **"编辑ExcelWorkbookProject.vbproj"** 或 **"编辑 ExcelWorkbookProject.csproj**"。
5. 在**ExcelWorkbook 项目**编辑器中，在**属性组**元素中找到**解决方案ID**元素。
6. 复制此元素的 GUID 值。

    ![检索解决方案 ID](media/setup-project-figure-17.jpg)

    **图 14：检索解决方案 ID**

7. 在**解决方案资源管理器**中，右键单击**ExcelWorkbook 项目**，然后单击 **"重新加载项目**"。
8. 在对话框中单击 **"是**"，该对话框显示关闭**ExcelWorkbook 项目**编辑器。
9. **解决方案 ID**将在安装自定义操作中使用。

最后一步是为**安装**和**卸载**步骤配置自定义操作。

### <a name="to-configure-the-setup-project"></a>配置设置项目

1. 在**解决方案资源管理器**中，右键单击**ExcelWorkbook安装程序**，展开 **"添加"** 并单击 **"项目输出**"。
2. 在"**添加项目输出组"** 对话框中，在 **"项目**"列表中，单击"**添加自定义自定义操作**"。
3. 选择 **"主输出**"并单击"**确定**"以关闭对话框，并将包含自定义操作的程序集添加到设置项目中。

    ![文档清单自定义操作的屏幕截图 - 添加项目输出组窗口](media/setup-project-figure-18.jpg)

    **图 15：文档清单自定义操作 - 添加项目输出组**

4. 在**解决方案资源管理器**中，右键单击**ExcelWorkbook 安装程序**。
5. 展开**视图**并单击 **"自定义操作**"。
6. 在**自定义操作（ExcelWorkbook安装程序）** 编辑器中，右键单击 **"自定义操作"，** 然后单击"**添加自定义操作**"。
7. 在 **"项目中选择项目**"对话框中，在"**查找"** 列表中单击 **"应用程序文件夹**"。 **从 AddCustomCustomAction（活动）中选择主输出，** 然后单击 **"确定"** 将自定义操作添加到安装步骤。
8. 在 **"安装"节点**下，右键单击**AddCustomAction（活动）的主输出**，然后单击 **"重命名**"。 将自定义操作 **"将文档复制到"我的文档"并附加自定义项**。
9. 在**卸载节点**下，右键单击**AddCustomAction（活动）的主输出**，然后单击 **"重命名**"。 命名自定义操作**从"文档"文件夹中删除文档**。

    ![文档清单自定义操作窗口的屏幕截图](media/setup-project-figure-19.jpg)

    **图 16：文档清单自定义操作**

10. 在**自定义操作 （ExcelWorkbook安装程序）** 编辑器中，右键单击 **"将文档复制到"我的文档"并附加自定义项**，然后单击"**属性窗口**"。
11. 在 **"自定义操作数据****属性**"窗口中，输入自定义 DLL 的位置、部署清单和 Microsoft Office 文档的位置。 还需要解决方案 ID。
12. 如果要将任何设置错误记录到文件，请包括 LogFile 参数。
s
    ``` text
    /assemblyLocation="[INSTALLDIR]ExcelWorkbookProject.dll" /deploymentManifestLocation="[INSTALLDIR]ExcelWorkbookProject.vsto" /documentLocation="[INSTALLDIR]ExcelWorkbookProject.xlsx" /solutionID="Your Solution ID" /LogFile="[TARGETDIR]Setup.log"
    ```

    ![将文档复制到"我的文档属性"窗口的自定义操作的屏幕截图](media/setup-project-figure-20.jpg)

    **图 17：将文档复制到我的文档的自定义操作**

13. 卸载的自定义操作需要文档的名称，您可以通过**在"自定义操作数据"** 中使用相同的文档定位参数来提供

    ``` text
    /documentLocation="[INSTALLDIR]ExcelWorkbookProject.xlsx"
    ```

14. 编译和部署**ExcelWorkbook 安装程序**项目。
15. 查看 **"我的文档"** 文件夹，然后打开 ExcelWorkbookProject.xlsx 文件。

## <a name="additional-resources"></a>其他资源

[如何：安装用于办公室运行时的可视化工作室工具](how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)

[办公室主互通程序集](office-primary-interop-assemblies.md)

[VSTO 外接程序的注册表项](registry-entries-for-vsto-add-ins.md)

[Custom Document Properties Overview](custom-document-properties-overview.md)

[在 Windows 注册表中指定窗体区域](/office/vba/outlook/concepts/creating-form-regions/specifying-form-regions-in-the-windows-registry)

[向文档授予信任](granting-trust-to-documents.md)

## <a name="about-the-authors"></a>关于作者

Wouter van Vugt 是 Microsoft MVP，拥有 Office 开放 XML 技术，是专注于创建具有 SharePoint、Microsoft Office 和相关 .NET 技术的 Office 业务应用程序 （OBA） 的独立顾问。
沃特是开发商社区网站（如[OpenXmlDeveloper.org](http://openxmldeveloper.org/)和[MSDN）](/previous-versions/office/developer/office-2007/bb879915(v=office.12))的频繁贡献者。 他发表了几篇白皮书和文章，以及一本在线文章，名为"打开 XML：解释电子书"。
Wouter 是 Code-Counsel 的创始人，这家荷兰公司专注于通过各种渠道提供尖端技术内容。 你可以通过阅读他的博客和访问[代码顾问网站](http://www.code-counsel.net/)来了解更多关于伍特的信息。

泰德·帕蒂森是 SharePoint MVP、作者、培训师和泰德·帕蒂森集团的创始人。 2005 年秋季，Ted 被 Microsoft 的开发人员平台福音组聘用，为 Windows SharePoint 服务 3.0 和 Microsoft Office SharePoint Server 2007 撰写了 Ascend 开发人员培训课程。 从那时起，Ted 一直专注于对专业开发人员进行 SharePoint 2007 技术教育。 Ted 为 Microsoft 出版社撰写了一本名为《Windows SharePoint 服务 3.0》的书，该书重点介绍了如何使用 SharePoint 作为构建业务解决方案的开发平台。 Ted 还为 MSDN 杂志撰写了一个标题为"办公空间"的面向开发人员的专栏。
