---
title: DSL 的 MSI 和 VSIX 部署 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 6ce16f06-1978-4e19-8cdc-441ee65a3fb2
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 749763a9a2bb742bb3670050010f497c5c15fba4
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668599"
---
# <a name="msi-and-vsix-deployment-of-a-dsl"></a>DSL 的 MSI 和 VSIX 部署
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以在自己的计算机或其他计算机上安装域特定语言。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 必须已安装在目标计算机上。

## <a name="which"></a>在 VSIX 和 MSI 部署之间选择
 部署域特定语言的方法有两种：

|方法|优点|
|------------|--------------|
|VSX （[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展）|易于部署：从 DslPackage 项目复制并执行 **.vsix**文件。<br /><br /> 有关详细信息，请参阅[使用 VSX 安装和卸载 DSL](#Installing)。|
|MSI （安装程序文件）|-允许用户通过双击 DSL 文件来打开 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。<br />-将图标与目标计算机中的 DSL 文件类型相关联。<br />-将 XSD （XML 架构）与 DSL 文件类型相关联。 这可以避免在将文件加载到 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 时出现警告。<br /><br /> 必须将安装项目添加到解决方案才能创建 MSI。<br /><br /> 有关详细信息，请参阅[使用 MSI 文件部署 DSL](#msi)。|

## <a name="Installing"></a>使用 VSX 安装和卸载 DSL
 此方法安装 DSL 后，用户可以从 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中打开 DSL 文件，但无法从 Windows 资源管理器打开该文件。

#### <a name="to-install-a-dsl-by-using-the-vsx"></a>使用 VSX 安装 DSL

1. 在计算机中，查找 DSL 包项目生成的 **.vsix**文件。

    1. 在**解决方案资源管理器**中，右键单击**DslPackage**项目，然后单击 "**在 Windows 资源管理器中打开文件夹**"。

    2. **@No__t_1 \* \\** _项目_找到文件箱 **。DslPackage**

2. 将 **.vsix**文件复制到要安装 DSL 的目标计算机。 该计算机可以是自己的计算机或其他计算机。

    - 目标计算机必须具有在运行时支持 Dsl 的 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 版本之一。 有关详细信息，请参阅[支持的 Visual Studio 版本 & 建模 SDK](../modeling/supported-visual-studio-editions-for-visualization-amp-modeling-sdk.md)。

    - 目标计算机必须具有**DslPackage\source.extensions.manifest**中指定的其中一个 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 版本。

3. 在目标计算机上，双击 **.vsix**文件。

     “” 将会打开并安装扩展。

4. 启动或重启 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]。

5. 若要测试 DSL，请使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 创建新文件，该文件具有你为 DSL 定义的扩展。

#### <a name="to-uninstall-a-dsl-that-was-installed-by-using-vsx"></a>卸载使用 VSX 安装的 DSL

1. 在 "**工具**" 菜单上，单击 "**扩展管理器**"。

2. 展开“已安装的扩展”。

3. 选择在其中定义 DSL 的扩展，然后单击 "**卸载**"。

   在极少数情况下，有错误的扩展无法加载并在错误窗口中创建报告，但不显示在扩展管理器中。 在这种情况下，可以通过从以下位置删除文件来删除扩展：

   *LocalAppData* **\Microsoft\VisualStudio\10.0\Extensions**

## <a name="msi"></a>在 MSI 中部署 DSL
 通过为 DSL 定义 MSI （Windows Installer）文件，可以允许用户通过 Windows 资源管理器打开 DSL 文件。 你还可以将图标和简短说明与你的文件扩展名相关联。 此外，MSI 还可以安装可用于验证 DSL 文件的 XSD。 如果需要，可以将其他组件添加到将在其中同时安装的 MSI。

 有关 MSI 文件和其他部署选项的详细信息，请参阅[部署应用程序、服务和组件](../deployment/deploying-applications-services-and-components.md)。

 若要生成 MSI，请将安装项目添加到 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 解决方案中。 创建安装项目最简单的方法是使用 CreateMsiSetupProject.tt 模板，该模板可从[VMSDK 站点](http://go.microsoft.com/fwlink/?LinkID=186128)下载。

#### <a name="to-deploy-a-dsl-in-an-msi"></a>在 MSI 中部署 DSL

1. 在扩展清单中设置 `InstalledByMsi`。 这会阻止除 MSI 之外安装和卸载 VSX。 如果你将在 MSI 中包含其他组件，则这一点非常重要。

   1. 打开 DslPackage\source.extension.tt

   2. 在 `<SupportedProducts>` 之前插入以下行：

       ```
       <InstalledByMsi>true</InstalledByMsi>
       ```

2. 在 Windows 资源管理器中创建或编辑将表示 DSL 的图标。 例如，编辑**DslPackage\Resources\File.ico**

3. 请确保 DSL 的以下属性是正确的：

   - 在 DSL 资源管理器中，单击 "根" 节点，然后在属性窗口中查看：

       - 描述

       - Version

   - 单击 "**编辑器**" 节点，然后在 "属性窗口中，单击"**图标**"。 设置值以引用**DslPackage\Resources**中的图标文件，如**file .ico**

   - 在 "**生成**" 菜单上，打开**Configuration Manager**，然后选择要生成的配置，例如 "**发布**" 或 "**调试**"。

4. 请参阅[可视化和建模 SDK 主页](http://go.microsoft.com/fwlink/?LinkID=186128)，然后在 "**下载**" 选项卡上下载**CreateMsiSetupProject.tt**。

5. 将**CreateMsiSetupProject.tt**添加到 Dsl 项目。

    [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 将创建一个名为 **.vdproj**的文件。

6. 在 Windows 资源管理器中，将 Dsl \\ * .vdproj 复制到名为 Setup 的新文件夹。

    （如果需要，现在可以从 Dsl 项目中排除 CreateMsiSetupProject.tt。）

7. 在**解决方案资源管理器**中，将**安装程序 \\** 作为现有项目添加 \* .vdproj。

8. 在 "**项目**" 菜单上，单击 "**项目依赖项**"。

    在 "**项目依赖项**" 对话框中，选择 "安装" 项目。

    选中 " **DslPackage**" 旁边的框。

9. 重新生成解决方案。

10. 在 Windows 资源管理器中，在安装项目中找到生成的 MSI 文件。

     将 MSI 文件复制到要安装 DSL 的计算机。 双击 MSI 文件。 安装程序将运行。

11. 在目标计算机上，创建一个具有 DSL 文件扩展名的新文件。 验证：

    - 在 Windows 资源管理器列表视图中，该文件将显示您定义的图标和说明。

    - 双击该文件时，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 启动，然后在 DSL 编辑器中打开 DSL 文件。

    如果愿意，可以手动创建安装项目，而不是使用文本模板。 有关包括此过程的演练，请参阅[可视化和建模 SDK 实验室](http://go.microsoft.com/fwlink/?LinkId=208878)的第5章。

#### <a name="to-uninstall-a-dsl-that-was-installed-from-an-msi"></a>卸载从 MSI 安装的 DSL

1. 在 Windows 中，打开 "**程序和功能**" 控制面板。

2. 卸载 DSL。

3. 重新启动 Visual Studio。
