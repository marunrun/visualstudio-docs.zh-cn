---
title: 使用 Windows Installer 部署 VSTO 解决方案
description: 了解如何使用 Visual Studio 安装程序项目部署适用于 Office (VSTO) 外接程序或文档级解决方案的 Microsoft Visual Studio 工具。
ms.custom: SEO-VS-2020
titleSuffix: ''
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
ms.openlocfilehash: e49705c99801cd6e09f4bf6d9be3c411cc2c53e3
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2020
ms.locfileid: "96846540"
---
# <a name="deploying-a-vsto-solution-using-windows-installer"></a>使用 Windows Installer 部署 VSTO 解决方案

## <a name="summary"></a>总结

了解如何使用 Visual Studio 安装程序项目部署适用于 Office (VSTO) 外接程序或文档级解决方案的 Microsoft Visual Studio 工具。

Wouter van Vugt，代码顾问

李小明 Pattison，李小明 Pattison Group

此文章已由 Microsoft 使用原始作者的权限进行了更新。

**适用于：** Visual Studio Tools for Office、Microsoft Office Microsoft Visual Studio。

## <a name="overview"></a>概述

可以通过使用 Windows Installer 包来开发 VSTO 解决方案并部署解决方案。 本讨论包含部署简单 Office 外接程序的步骤。

## <a name="deployment-methods"></a>部署方法

可以轻松地使用 ClickOnce 创建外接程序和解决方案的设置。 但是，它不能安装需要管理特权的外接程序，如计算机级外接程序。

需要管理权限的外接程序可以通过使用 Windows Installer 进行安装，但它确实需要更多的精力才能创建安装程序。

有关如何使用 ClickOnce 部署 VSTO 解决方案的概述，请参阅 [使用 Clickonce 部署 Office 解决方案](deploying-an-office-solution-by-using-clickonce.md)。

## <a name="deploying-office-solutions-that-target-the-vsto-runtime"></a>部署以 VSTO 运行时为目标的 Office 解决方案

在安装 Office 解决方案时，ClickOnce 和 Windows Installer 包需要执行相同的基本任务。

1. 在用户计算机上安装必备组件。
2. 部署解决方案的特定组件。
3. 对于外接程序，请创建注册表项。
4. 信任解决方案以允许它执行。

### <a name="required-prerequisite-components-on-the-target-computer"></a>目标计算机上所需的必备组件

下面是必须在计算机上安装的软件的列表，才能运行 VSTO 解决方案：

- Microsoft Office 2010 或更高版本。
- Microsoft .NET Framework 4 或更高版本。
- Microsoft Visual Studio 2010 Tools for Office Runtime。
  运行时提供了一个管理外接程序和文档级解决方案的环境。 运行时版本与 Microsoft Office 一起提供，但你可能希望使用外接程序重新发布特定的版本。
- 如果不使用嵌入的互操作类型，则为 Microsoft Office 的主互操作程序集。
- 项目引用的任何实用工具程序集。

### <a name="specific-components-for-the-solution"></a>解决方案的特定组件

安装程序包必须将这些组件安装到用户的计算机上：

- Microsoft Office 文档（如果创建文档级解决方案）。
- 自定义程序集和它所需要的任何程序集。
- 其他组件，如配置文件。
- 应用程序清单)  (。
- 部署清单 ( .vsto) 。

### <a name="registry-entries-for-add-ins"></a>外接程序的注册表项

Microsoft Office 使用注册表项来查找和加载外接程序。这些注册表项应作为部署过程的一部分进行创建。 有关这些注册表项的详细信息，请参阅 [VSTO 外接程序的注册表项](registry-entries-for-vsto-add-ins.md)。

显示自定义窗体区域的 Outlook 外接程序需要其他注册表项，以允许识别窗体区域。 有关注册表项的详细信息，请参阅 [Outlook 窗体区域的注册表项](registry-entries-for-vsto-add-ins.md#OutlookEntries)。

文档级解决方案不需要任何注册表项。 而是使用文档中的属性来查找自定义项。 有关这些属性的详细信息，请参阅 [自定义文档属性概述](custom-document-properties-overview.md)。

### <a name="trusting-the-vsto-solution"></a>信任 VSTO 解决方案

若要运行自定义项，解决方案必须受计算机的信任。 可以通过使用证书对清单进行签名、使用包含列表创建信任关系或将其安装到计算机上的受信任位置，来信任外接程序。

有关如何获取用于签名的证书的详细信息，请参阅 [ClickOnce 部署和验证码](../deployment/clickonce-and-authenticode.md)。 有关信任解决方案的详细信息，请参阅 [使用包含列表信任 Office 解决方案](trusting-office-solutions-by-using-inclusion-lists.md)。 可以在 Windows Installer 文件中添加包含自定义操作的包含列表项。 有关启用包含列表的详细信息，请参阅 [如何：配置包含列表安全性](how-to-configure-inclusion-list-security.md)。

如果这两个选项都不使用，则向用户显示信任提示，让他们决定是否信任解决方案。

有关与文档级解决方案相关的安全性的详细信息，请参阅向 [文档授予信任](granting-trust-to-documents.md)。

## <a name="creating-a-basic-installer"></a>创建基本安装程序

安装和部署项目模板包含在可供下载的 [Microsoft Visual Studio 安装程序项目](https://marketplace.visualstudio.com/items?itemName=visualstudioclient.MicrosoftVisualStudio2017InstallerProjects) 扩展中。

若要创建 Office 解决方案的安装程序，必须完成以下任务：

- 添加将部署的 Office 解决方案的组件。
- 对于应用程序级外接程序，请配置注册表项。
- 配置必备组件，以便可以将其安装在最终用户计算机上。
- 配置启动条件以验证所需的必备组件是否可用。 如果未安装所有必需的必备组件，则启动条件可用于阻止安装。

第一步是创建安装项目。

### <a name="to-create-the-addin-setup-project"></a>创建外接程序安装项目

1. 打开要部署的 Office 外接程序项目。 在此示例中，我们使用了一个名为 ExcelAddIn 的 Excel 外接程序。
2. 打开 Office 项目后，在 " **文件** " 菜单上，展开 " **添加** "，然后单击 " **新建项目** " 添加新项目。
::: moniker range="=vs-2017"
3. 在 "**添加新项目**" 对话框中，展开 **"项目类型"** 窗格中的 "**其他项目类型**"，展开 "**安装和部署**"，然后选择 " **Visual Studio 安装程序**"。
4. 在 "**模板**" 窗格中，从 " **Visual Studio 已安装** 的模板" 组中选择 "**安装项目**"。
::: moniker-end
::: moniker range="=vs-2019"
3. 在 " **添加新项目** " 对话框中，选择 " **安装" 项目** 模板。
4. 单击 **“下一步”** 。
::: moniker-end

5. 在 " **名称** " 框中，键入 **officeaddinsetup "**。
::: moniker range="=vs-2017"
6. 单击 " **打开** " 以创建新的安装项目。
::: moniker-end
::: moniker range="=vs-2019"
6. 单击 " **创建** " 创建新的安装项目。
::: moniker-end

Visual Studio 将打开新安装项目的文件系统资源管理器。 文件系统资源管理器允许您将文件添加到安装项目。

   ![安装程序项目的文件系统资源管理器的屏幕截图](media/setup-project-figure-1.png)

   **图1：安装项目的文件系统资源管理器**

安装项目需要部署 ExcelAddIn。 可以通过将 ExcelAddIn 项目输出添加到安装项目来为此任务配置安装项目。

### <a name="to-add-the-exceladdin-project-output"></a>添加 ExcelAddIn 项目输出

1. 在 **解决方案资源管理器** 中，右键单击 **officeaddinsetup "**，单击" **添加** "，然后单击" **项目输出**"。
2. 在 " **添加项目输出组** " 对话框中，从 "项目" 列表中选择 " **ExcelAddIn** "，并选择 " **主输出**"。
3. 单击 **"确定"** ，将项目输出添加到安装项目。

    ![安装项目 "添加项目输出组" 对话框的屏幕截图](media/setup-project-figure-2.png)

    **图2：安装项目 "添加项目输出组" 对话框**

安装项目需要部署部署清单和应用程序清单。 将这两个文件作为独立文件从 ExcelAddIn 项目的输出文件夹添加到安装项目。

### <a name="to-add-the-deployment-and-application-manifests"></a>添加部署和应用程序清单

1. 在 **解决方案资源管理器** 中，右键单击 **officeaddinsetup "**，单击" **添加**"，然后单击" **文件**"。
2. 在 " **添加文件** " 对话框中，导航到 " **ExcelAddIn** " 输出目录。 通常，输出目录是项目根目录的 **bin \\ release** 子文件夹，具体取决于所选的生成配置。
3. 选择 **ExcelAddIn** 和 **ExcelAddIn.dll .manifest** 文件，然后单击 " **打开** " 将这两个文件添加到安装项目。

    ![解决方案资源管理器中的应用程序和部署清单的屏幕截图](media/setup-project-figure-3.jpg)

    **图3：解决方案资源管理器中的外接程序的应用程序和部署清单**

引用 ExcelAddIn 包含 ExcelAddIn 所需的所有组件。 必须使用先决条件包排除并部署这些组件，以允许正确注册这些组件。 此外，在安装开始之前，必须显示并接受软件许可条款。

### <a name="to-exclude-the-exceladdin-project-dependencies"></a>排除 ExcelAddIn 项目依赖项

1. 在 **解决方案资源管理器** 的 " **officeaddinsetup"** "节点中，选择"**检测到的依赖** 项 "项下的" 所有依赖项 "项， **Microsoft .NET 框架** 或以 **\*.Utilities.dll** 结尾的任何程序集除外。 实用程序程序集与应用程序一起部署。
2. 右键单击该组，然后选择 " **属性**"。
3. 在 " **属性** " 窗口中，将 " **排除** " 属性更改为 " **True** "，以从安装项目中排除依赖程序集。 请确保不排除任何实用工具程序集。

    ![显示要排除的依赖项的解决方案资源管理器屏幕截图](media/setup-project-figure-4.jpg)

    **图4：排除依赖项**

可以通过添加安装程序（也称为 "引导程序"）将 Windows Installer 包配置为安装必备组件。 此安装程序可以安装系统必备组件，这是一个称为 "引导" 的进程。

对于 **ExcelAddIn**，必须先安装这些必备组件，然后才能正常运行外接程序：

- Office 解决方案面向的 Microsoft .NET Framework 版本。
- Microsoft Visual Studio 2010 Tools for Office Runtime。

配置依赖组件为系统必备组件

1. 在 **解决方案资源管理器** 中，右键单击 **officeaddinsetup "** 项目，然后选择" **属性**"。
2. 此时将显示 " **Officeaddinsetup" 属性页** "对话框。
3. 单击 " **必备项** " 按钮。
4. 在 "系统必备" 对话框中，选择正确的 .NET Framework 版本和 Office 运行时 Microsoft Visual Studio 工具。

    !["必备组件" 对话框的屏幕截图](media/setup-project-figure-5.png)

    **图5： "系统必备" 对话框**

    > [!NOTE]
    >Visual Studio 安装程序项目中配置的某些必备组件包依赖于所选的生成配置。 你必须为你使用的每个生成配置选择正确的必备组件。

Microsoft Office 使用注册表项查找外接程序。 HKEY \_ 当前 \_ 用户配置单元中的密钥用于为每个单独的用户注册外接程序。 HKEY \_ 本地计算机 hive 下的密钥 \_ 用于为计算机的所有用户注册外接程序。 有关注册表项的详细信息，请参阅 [VSTO 外接程序的注册表项](registry-entries-for-vsto-add-ins.md)。

### <a name="to-configure-the-registry"></a>配置注册表

1. 在 **解决方案资源管理器** 中，右键单击 **officeaddinsetup "**。
2. 展开 " **视图**"。
3. 单击 " **注册表** "，打开 "注册表编辑器" 窗口。
4. 在 **注册表 (officeaddinsetup ")** 编辑器中，依次展开" HKEY "、" **\_ 本地 \_ 计算机** "和" **软件**"。
5. 删除 **\[ 制造商 \]**？在 **HKEY \_ 本地 \_ 计算机 \\ 软件** 下找到的密钥。
6. 展开 " **HKEY \_ 当前 \_ 用户** " 和 " **软件**"。
7. 删除 **HKEY " \_ 当前 \_ 用户 \\ 软件**" 下的 **\[ 制造商 \]** 密钥。
8. 若要为外接程序安装添加注册表项，请右键单击 **用户/计算机 Hive** 键，然后选择 " **新项**"。 使用文本 **软件** 作为新密钥的名称。 右键单击新创建的 **软件** 密钥，并使用文本 **Microsoft** 创建新密钥。
9. 使用类似的过程创建外接程序注册所需的整个密钥层次结构：

    **用户/计算机 Hive \\ Software \\ Microsoft \\ Office \\ Excel \\ Addins \\ samplecompany.exceladdin 注册表项. ExcelAddIn**

    公司名称通常用作外接程序名称的前缀，以提供唯一性。

10. 右键单击 " **ExcelAddIn** " 项，选择 " **新建**"，然后单击 " **字符串值**"。 使用名称的文本 **说明** 。
11. 使用此步骤添加三个更多值：
    - **字符串** 类型的 **FriendlyName**
    - **DWORD** 类型的 **LoadBehavior**
    - **字符串** 类型的 **清单**

12. 在注册表编辑器中右键单击 **说明** 值，然后单击 " **属性窗口**"。 在 " **属性" 窗口** 中，为 "值" 属性输入 **Excel Demo AddIn** 。
13. 在注册表编辑器中选择 **FriendlyName** 项。 在 " **属性" 窗口** 中，将 " **值** " 属性更改为 **Excel Demo 外接** 程序。
14. 在注册表编辑器中选择 " **LoadBehavior** " 项。 在 " **属性" 窗口** 中，将 " **值** " 属性更改为 **3。** LoadBehavior 的值3指示加载项应在宿主应用程序启动时加载。 有关加载行为的详细信息，请参阅 [VSTO 外接程序的注册表项](registry-entries-for-vsto-add-ins.md)。

15. 在注册表编辑器中选择 **清单** 键。 在 " **属性" 窗口** 中，将 " **值** " 属性更改为 **file：///[TARGETDIR] ExcelAddIn | vstolocal**

    ![注册表编辑器的屏幕截图](media/setup-project-figure-6.png)

    **图6：设置注册表项**

      VSTO 运行时使用此注册表项来查找部署清单。 [TARGETDIR] 宏将替换为将外接程序安装到的文件夹。 该宏将包含尾随 \ 字符，因此部署清单的文件名应为 ExcelAddIn，不含 \ 字符。
      **Vstolocal** 后缀通知 VSTO 运行时外接程序应从此位置加载（而不是 ClickOnce 缓存）。 删除此后缀将导致运行时将自定义项复制到 ClickOnce 缓存中。

   >[!WARNING]
   >在 Visual Studio 中，你应非常小心地处理注册表编辑器。 例如，如果你无意中为错误的键设置了 DeleteAtUninstall，则可能会删除注册表的活动部分，使用户计算机处于不一致的状态，甚至更糟糕的状态。

64位版本的 Office 将使用64位注册表配置单元查找外接程序。若要在64位注册表配置单元中注册外接程序，则必须将安装项目的目标平台设置为仅64位。

1. 在解决方案资源管理器中选择 **officeaddinsetup "** 项目。
2. 中转到 " **属性** " 窗口，并将 **TargetPlatform** 属性设置为 **x64**。

若要为32位和64位版本的 Office 安装外接程序，将需要你创建两个单独的 MSI 包。 一个用于32位，另一个用于64位。

  !["属性" 窗口的屏幕截图，显示用于注册64位 Office 外接程序的目标平台](media/setup-project-figure-7.jpg)

  **图7：用于注册64位 Office 外接程序的目标平台**

如果使用 MSI 包安装外接程序或解决方案，则无需安装所需的必备软件即可进行安装。 如果未安装系统必备组件，则可以使用 MSI 中的启动条件来阻止外接程序安装。

### <a name="configure-a-launch-condition-to-detect-the-vsto-runtime"></a>配置启动条件以检测 VSTO 运行时

1. 在 **解决方案资源管理器** 中，右键单击 **officeaddinsetup "**。
2. 展开 " **视图**"。
3. 单击 " **启动条件**"。
4. 在 " **启动条件" (officeaddinsetup ")** " 编辑器中，右键单击 " **目标计算机上的要求**"，然后单击 " **添加注册表启动条件**"。 此搜索条件可以在注册表中搜索 VSTO 运行时安装的键。 然后，可通过命名属性对安装程序的各个部分使用该密钥的值。 启动条件使用由搜索条件定义的属性来检查某个值。
5. 在 " **启动条件 (officeaddinsetup" ")** 编辑器中，选择" **搜索 RegistryEntry1** "搜索条件，右键单击该条件，然后选择" **属性窗口**"。

6. 在 " **属性** " 窗口中，设置以下属性：
   1. 将 **(名称)** 的值设置为 **搜索 VSTO 2010 运行时**。
   2. 将 **属性** 的值更改为 **VSTORUNTIMEREDIST**。
   3. 将 **RegKey** 的值设置为 **软件 \\ Microsoft \\ VSTO 运行时安装 \\ v4R**
   4. 将 **根** 属性设置为 " **vsdrrHKLM**"。
   5. 将 " **值** " 属性更改为 " **版本**"。

7. 在 " **启动条件" (officeaddinsetup ")** " 编辑器中，选择 " **Condition1** " 启动条件，右键单击该条件，然后选择 " **属性窗口**"。
8. 在“属性”窗口中，设置以下属性：
   1. 设置 **(名称)** 以 **验证 VSTO 2010 运行时可用性**。
   2. 将 **条件** 的值更改为 **VSTORUNTIMEREDIST \> = "10.0.30319"**
   3. 将 **InstallURL** 属性留空。
   4. 将 **消息** 设置为 **未安装 Visual Studio 2010 Tools for Office Runtime。请运行 Setup.exe 以安装外接程序**。

        ![验证运行时可用性启动条件的 "属性" 窗口的屏幕截图](media/setup-project-figure-8.jpg)

        **图8：验证运行时可用性启动条件的 "属性" 窗口**

 上面的启动条件在引导程序包安装时，显式检查 VSTO 运行时是否存在。

### <a name="configure-a-launch-condition-to-detect-the-vsto-runtime-installed-by-office"></a>配置启动条件以检测 Office 安装的 VSTO 运行时

1. 在 " **启动条件" (officeaddinsetup ")** " 编辑器中，右键单击 " **搜索目标计算机**"，然后单击 " **添加注册表搜索**"。
2. 选择 " **搜索 RegistryEntry1** " 搜索条件，右键单击该条件，然后选择 " **属性窗口**"。
3. 在 " **属性** " 窗口中，设置以下属性：
    1. 将 **(名称)** 的值设置为 **搜索 Office VSTO 运行时**。
    2. 将 **属性** 的值更改为 **OfficeRuntime**。
    3. 将 **RegKey** 的值设置为 **软件 \\ Microsoft \\ VSTO 运行时安装程序 \\ v4**。
    4. 将 **根** 属性设置为 " **vsdrrHKLM**"。
    5. 将 " **值** " 属性更改为 " **版本**"。

4. 在 " **启动条件" (officeaddinsetup ")** " 编辑器中，选择前面定义的 " **验证 VSTO 2010 运行时可用性** " 启动条件，右键单击该条件，然后选择 " **属性窗口**"。

5. 将 **Condition** 属性的值更改为 **VSTORUNTIMEREDIST \> = "10.0.30319" 或 OFFICERUNTIME \> = "10.0.21022"**。 版本号可能不同，具体取决于外接程序所需的运行时版本。

    ![启动条件的 "属性" 窗口的屏幕截图](media/setup-project-figure-9.jpg)
  
    **图9：通过再发行或 Office 启动条件验证运行时可用性的属性窗口**

如果外接程序针对 .NET Framework 4 或更高版本，则引用的主互操作程序集 (PIA) 内的类型可以嵌入 VSTO 程序集。

若要通过执行以下步骤来检查是否将在外接程序中嵌入互操作类型：

1. 展开 "引用" 节点解决方案资源管理器
2. 选择其中一个 PIA 引用，例如 " **Office**"。
3. 按 F4 或从程序集上下文菜单中选择 "属性"，查看 "属性" 窗口。
4. 检查 " **嵌入互操作类型**" 属性的值。

如果将该值设置为 **True**，则将嵌入这些类型，您可以跳到 [**来生成安装项目**](#to-build-the-setup-project) 部分。

有关详细信息，请参阅 [类型等效性和嵌入的互操作类型](/dotnet/framework/interop/type-equivalence-and-embedded-interop-types)

### <a name="to-configure-launch-conditions-to-detect-that-for-office-pias"></a>配置启动条件以检测 Office Pia 的情况

1. 在 " **启动条件" (officeaddinsetup ")** " 编辑器中，右键单击 " **目标计算机上的要求**"，然后 **单击 "添加 Windows Installer 启动条件**"。 此启动条件通过搜索特定组件 ID 搜索 Office PIA。
2. 右键单击 " **搜索 Component1** "，然后单击 " **属性窗口** " 以显示启动条件的属性。
3. 在 " **属性" 窗口** 中，设置以下属性：

    1. 将 **(名称)** 属性的值更改为 "**搜索 Office 共享 PIA** "
    2. 将组件 Id 的值 **更改为你** 正在使用的 Office 组件的组件 Id。 可以在下表中找到组件 Id 的列表，例如 **{64E2917E-AA13-4CA4-BFFE-EA6EDA3AFCB4}**。
    3. 将 **属性** 属性的值更改为 **HASSHAREDPIA**。

4. 在 " **启动条件" (officeaddinsetup ")** " 编辑器中，右键单击 " **Condition1** "，然后单击 " **属性窗口** " 以显示启动条件的属性。

5. 更改 **Condition1** 的以下属性：

    1. 更改 **(名称)** **验证 Office 共享 PIA 可用性**。
    2. 将 **条件** 更改为 **HASSHAREDPIA**。
    3. 将 **InstallUrl** 留空。
    4. 将 **消息** 更改为 **与 Excel 交互所需的组件不可用。请运行 setup.exe**。

    ![验证 Office 共享 PIA 启动条件的 "属性" 窗口的屏幕截图](media/setup-project-figure-10.jpg)
  
    **图10：验证 Office 共享 PIA 启动条件的 "属性" 窗口**

### <a name="component-ids-of-the-primary-interop-assemblies-for-microsoft-office"></a>Microsoft Office 的主互操作程序集的组件 Id

|主互操作程序集|Office 2010|Office 2013|Office 2013 (64) |Office 2016|Office 2016 (64) |
|------------------------|------------------------|------------------------|------------------------|------------------------|------------------------|
|Excel|{EA7564AC-C67D-4868-BE5C-26E4FC2223FF}|{C8A65ABE-3270-4FD7-B854-50C8082C8F39}|{E3BD1151-B9CA-4D45-A77E-51A6E0ED322A}|C4ACE6DB-AA99-401F-8BE6-8784BD09F003}|{C4ACE6DB-AA99-401F-8BE6-8784BD09F003}|
|InfoPath|{4153F732-D670-4E44-8AB7-500F2B576BDA}|{0F825A16-25B2-4771-A497-FC8AF3B355D8}|{C5BBD36E-B320-47EF-A512-556B99CB7E41}|-|-|
|Outlook|{1D844339-3DAE-413E-BC13-62D6A52816B2}|{F9F828D5-9F0B-46F9-9E3E-9C59F3C5E136}|{7824A03F-28CC-4371-BC54-93D15EFC1E7F}|{7C6D92EF-7B45-46E5-8670-819663220E4E}|{7C6D92EF-7B45-46E5-8670-819663220E4E}|
|PowerPoint|{EECBA6B8-3A62-44AD-99EB-8666265466F9}|{813139AD-6DAB-4DDD-8C6D-0CA30D073B41}|{05758318-4288 BCFD-AD8D-81185841C235}|{E0A76492-0FD5-4EC2-8570-AE1BAA61DC88}|{E0A76492-0FD5-4EC2-8570-AE1BAA61DC88}|
|Visio|{3EA123B5-6316-452E-9D51-A489E06E2347}|{C1713368-12A8-41F1-ACA1-934B01AD6EEB}|{2CC0B221-22D2-4C15-A9FB-DE818E51AF75}|{2D4540EC-2C88-4C28-AE88-2614B5460648}|{2D4540EC-2C88-4C28-AE88-2614B5460648}|
|Word|{8B74A499-37F8-4DEA-B5A0-D72FC501CEFA}|{9FE736B7-B1EE-410C-8D07-082891C3DAC8}|{13C07AF5-B206-4A48-BB5B-B8022333E3CA}|{DC5CCACD-A7AC-4FD3-9F70-9454B5DE5161}|{DC5CCACD-A7AC-4FD3-9F70-9454B5DE5161}|
|Microsoft Forms 2。0|{B2279272-3FD2-434D-B94E-E4E0F8561AC4}|{B2279272-3FD2-434D-B94E-E4E0F8561AC4}|{A5A30117-2D2A-4C5C-B3C8-8897AC32C2AC}|-|-|
|Microsoft Graph|{011B9112-EBB1-4A6C-86CB-C2FDC9EA7B0E}|{52DA4B37-B8EB-4B7F-89C1-824654CE4C70}|{24706F33-F0CE-4EB4-BC91-9E935394F510}|-|-|
|智能标记 (Smart Tag)|{7102C98C-EF47-4F04-A227-FE33650BF954}|{487A7921-EB3A-4262-BB5B-A5736B732486}|{74EFC1F9-747D-4867-B951-EFCF29F51AF7}|-|-|
|Office 共享|{64E2917E-AA13-4CA4-BFFE-EA6EDA3AFCB4}|{6A174BDB-0049-4D1C-86EF-3114CB0C4C4E}|{76601EBB-44A7-49EE-8DE3-7B7B9D7EBB05}|{625F5772-C1B3-497E-8ABE-7254EDB00506}|{625F5772-C1B3-497E-8ABE-7254EDB00506}|
|项目|{957A4EC0-E67B-4E86-A383-6AF7270B216A}|{1C50E422-24FA-44A9-A120-E88280C8C341}|{706D7F44-8231-489D-9B25-3025ADE9F114}|{107BCD9A-F1DC-4004-A444-33706FC10058}|{107BCD9A-F1DC-4004-A444-33706FC10058}|

  ![最终启动条件的屏幕截图](media/setup-project-figure-11.jpg)

  **图11：最终启动条件**

可以进一步优化 ExcelAddIn 安装的启动条件。 例如，检查是否安装了实际的目标 Office 应用程序可能会很有用。

### <a name="to-build-the-setup-project"></a>生成安装项目

1. 在 **解决方案资源管理器** 中，右键单击 **officeaddinsetup "** 项目，然后单击" **生成**"。
2. 使用 **Windows 资源管理器**，导航到 **officeaddinsetup "** 项目的输出目录，然后转到" 发布 "或" 调试 "文件夹，具体取决于所选的生成配置。 将文件夹中的所有文件复制到用户可以访问的位置。

测试 ExcelAddIn 安装程序

1. 导航到将 **officeaddinsetup "** 复制到的位置。
2. 双击 setup.exe 文件以安装 **officeaddinsetup "** 外接程序。 接受显示的任何软件许可条款，然后完成安装向导以在用户计算机上安装加载项。

Excel Office 解决方案应在安装过程中指定的位置安装和运行。

## <a name="additional-requirements-for-document-level-solutions"></a>文档级解决方案的其他要求

部署文档级解决方案需要在 Windows Installer 安装项目中执行几个不同的配置步骤。

下面是部署文档级解决方案所需的基本步骤列表：

- 创建 Visual Studio 安装程序项目。
- 添加文档级解决方案的主输出。 主输出还包括 Microsoft Office 文档。
- 将部署和应用程序清单作为松散文件添加。
- 除) 的任何实用工具程序集之外，从安装程序包中排除依赖组件 (。
- 配置必备组件包。
- 配置启动条件。
- 生成安装项目并将结果复制到部署位置。
- 通过执行安装程序在用户计算机上部署文档级解决方案。
- 如果需要，请更新自定义文档属性。

### <a name="changing-the-location-of-the-deployed-document"></a>更改已部署文档的位置

Office 文档中的属性用于查找文档级解决方案。 如果将文档安装到与 VSTO 程序集相同的文件夹中，则不需要进行任何更改。 但是，如果将其安装到不同的文件夹，则需要在安装过程中更新这些属性。

有关这些文档属性的详细信息，请参阅 [自定义文档属性概述](custom-document-properties-overview.md)。

若要更改这些属性，需要在安装过程中使用自定义操作。

下面的示例使用名为 ExcelWorkbookProject 的文档级解决方案和一个名为 ExcelWorkbookSetup 的安装项目。 使用上述相同步骤配置 ExcelWorkbookSetup 项目，但设置注册表项除外。

将自定义操作项目添加到 Visual Studio 解决方案

1. 通过右键单击 "**解决方案资源管理器** 中的 **Office 文档部署项目**，将新的 .net 控制台项目添加到解决方案中。
2. 展开 " **添加** "，然后单击 " **新建项目**"。
3. 选择 "控制台应用程序" 模板，并将项目命名为 " **AddCustomizationCustomAction**"。

    ![解决方案资源管理器的屏幕截图-AddCustomizationCustomAction](media/setup-project-figure-15.jpg)
  
    **图12：解决方案资源管理器 AddCustomizationCustomAction**

4. 添加对这些程序集的引用：
    1. System.ComponentModel
    2. System.Configuration.Install
    3. VisualStudio。
    4. Microsoft.VisualStudio.Tools.Applications.ServerDocument

5. 将此代码复制到 Program.cs 或 Program .vb

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

若要将自定义项添加到文档，需要具有 VSTO 文档级解决方案的解决方案 ID。 将从 Visual Studio 项目文件中检索此值。

检索解决方案 ID

1. 在 " **生成** " 菜单上，单击 " **生成解决方案** " 以生成文档级解决方案，并将 "解决方案 ID" 属性添加到项目文件。
2. 在 **解决方案资源管理器** 中，右键单击文档级项目 **ExcelWorkbookProject**
3. 单击 " **UnloadProject** " 可从 Visual Studio 内部访问项目文件。

    ![卸载 Excel 文档解决方案的解决方案资源管理器屏幕截图](media/setup-project-figure-16.jpg)

    **图13：卸载 Excel 文档解决方案**

4. 在 **解决方案资源管理器** 中，右键单击 " **ExcelWorkbookProject** "，然后单击 "EditExcelWorkbookProject **" 或 "** **.vbproj** "。
5. 在 **ExcelWorkbookProject** 编辑器中，找到 **PropertyGroup** 元素中的 **SolutionID** 元素。
6. 复制此元素的 GUID 值。

    ![检索 SolutionID](media/setup-project-figure-17.jpg)

    **图14：检索 SolutionID**

7. 在 **解决方案资源管理器** 中，右键单击 **ExcelWorkbookProject** ，然后单击 " **重新加载项目**"。
8. 在出现的对话框中单击 **"是"** 以关闭 " **ExcelWorkbookProject** 编辑器"。
9. **解决方案 ID** 将用于安装自定义操作。

最后一步是配置用于 **安装** 和 **卸载** 步骤的自定义操作。

### <a name="to-configure-the-setup-project"></a>配置安装程序项目

1. 在 **解决方案资源管理器** 中，右键单击 **ExcelWorkbookSetup**，展开 " **添加** "，然后单击 " **项目输出**"。
2. 在 " **添加项目输出组** " 对话框的 " **项目** " 列表中，单击 " **AddCustomizationCustomAction**"。
3. 选择 " **主输出** "，然后单击 **"确定"** 以关闭对话框，并将包含自定义操作的程序集添加到安装项目。

    ![文档清单自定义操作-"添加项目输出组" 窗口的屏幕截图](media/setup-project-figure-18.jpg)

    **图15：文档清单自定义操作-添加项目输出组**

4. 在 **解决方案资源管理器** 中，右键单击 **ExcelWorkbookSetup**。
5. 展开 " **视图** "，然后单击 " **自定义操作**"。
6. 在 " **自定义操作 (ExcelWorkbookSetup")** 编辑器中，右键单击 " **自定义操作** "，然后单击 " **添加自定义操作**"。
7. 在 " **选择项目中的项** " 对话框的 " **查找范围** " 列表中，单击 " **应用程序文件夹**"。 选择 **AddCustomizationCustomAction (active) 中的 "主输出** "，然后单击 **"确定"** 将自定义操作添加到安装步骤。
8. 在 " **安装" 节点** 下，右键单击 " **AddCustomizationCustomAction (Active)** 中的" 主输出 "，然后单击" **重命名**"。 命名自定义操作 **将文档复制到 "我的文档" 并附加自定义**。
9. 在 " **卸载" 节点** 下，右键单击 " **AddCustomizationCustomAction (Active) 中的" 主输出** "，然后单击" **重命名**"。 命名自定义操作 **从文档文件夹中删除文档**。

    ![文档清单自定义操作窗口的屏幕截图](media/setup-project-figure-19.jpg)

    **图16：文档清单自定义操作**

10. 在 " **自定义操作 (ExcelWorkbookSetup")** 编辑器中，右键单击 **"将文档复制到我的文档" 并附加自定义** ，然后单击 " **属性窗口**"。
11. 在 **CustomActionData** 的 " **属性** " 窗口中，输入自定义 DLL 的位置、部署清单和 Microsoft Office 文档的位置。 还需要 SolutionID。
12. 如果要将任何安装错误记录到文件中，请包含 LogFile 参数。
s
    ``` text
    /assemblyLocation="[INSTALLDIR]ExcelWorkbookProject.dll" /deploymentManifestLocation="[INSTALLDIR]ExcelWorkbookProject.vsto" /documentLocation="[INSTALLDIR]ExcelWorkbookProject.xlsx" /solutionID="Your Solution ID" /LogFile="[TARGETDIR]Setup.log"
    ```

    ![用于将文档复制到我的文档的自定义操作屏幕截图属性窗口](media/setup-project-figure-20.jpg)

    **图17：用于将文档复制到我的文档的自定义操作**

13. 用于卸载的自定义操作需要文档的名称，你可以通过在 **CustomActionData** 中使用相同的 documentLocation 参数提供该文档

    ``` text
    /documentLocation="[INSTALLDIR]ExcelWorkbookProject.xlsx"
    ```

14. 编译并部署 **ExcelWorkbookSetup** 项目。
15. 在 **"我的文档** " 文件夹中查找，打开 ExcelWorkbookProject.xlsx 文件。

## <a name="additional-resources"></a>其他资源

[如何：安装 Visual Studio Tools for Office 运行时](how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)

[Office Primary Interop Assemblies](office-primary-interop-assemblies.md)

[VSTO 外接程序的注册表项](registry-entries-for-vsto-add-ins.md)

[Custom Document Properties Overview](custom-document-properties-overview.md)

[在 Windows 注册表中指定窗体区域](/office/vba/outlook/concepts/creating-form-regions/specifying-form-regions-in-the-windows-registry)

[Granting Trust to Documents](granting-trust-to-documents.md)

## <a name="about-the-authors"></a>关于作者

Wouter van Vugt 是 Microsoft MVP，具有 Office Open XML 技术，以及一个独立的顾问，重点介绍如何创建 Office Business Applications (Oba) SharePoint、Microsoft Office 以及相关的 .NET 技术。
Wouter 是开发人员社区网站（如 [MSDN](/previous-versions/office/developer/office-2007/bb879915(v=office.12))）的常见参与者。 他发布了若干白皮书和文章，以及标题为 "Open XML：说明电子书" 的书籍。
Wouter 是代码顾问的创始人，这是一家荷兰公司，致力于通过各种渠道交付先进的技术内容。 若要了解有关 Wouter 的详细信息，请阅读他的博客。

李小明 Pattison 是一个 SharePoint MVP、作者、培训师和李小明 Pattison 组的创始人。 在2005的秋季，李小明由 Microsoft 的开发人员平台推广组雇用，为 Windows SharePoint Services 3.0 和 Microsoft Office SharePoint Server 2007 编写递增开发人员培训课程。 自那时起，李小明已经完全专注于专业开发人员对 SharePoint 2007 技术的培训。 在 Windows SharePoint Services 3.0 中，李小明撰写了 Microsoft 新闻书籍，重点介绍如何使用 SharePoint 作为构建业务解决方案的开发平台。 李小明还为名为 "办公空间" 的 MSDN 杂志写入一个以开发人员为中心的列。
