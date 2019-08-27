---
title: MSI 和 VSIX 部署 DSL 的 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 6ce16f06-1978-4e19-8cdc-441ee65a3fb2
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 3aaaf704e1ad8880ef7768ef9d7a23d325882a15
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62422560"
---
# <a name="msi-and-vsix-deployment-of-a-dsl"></a>DSL 的 MSI 和 VSIX 部署
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在你自己的计算机上或其他计算机上，可以安装特定于域的语言。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 已必须在目标计算机上安装。  
  
## <a name="which"></a> VSIX 和 MSI 部署之间进行选择  
 有两种部署域特定语言的方法：  
  
|方法|优点|  
|------------|--------------|  
|VSX ([!INCLUDE[vsprvs](../includes/vsprvs-md.md)]扩展)|非常易于部署：复制并执行 **.vsix** DslPackage 项目中的文件。<br /><br /> 有关详细信息请参阅[安装和卸载 DSL 使用 VSX](#Installing)。|  
|MSI （安装程序文件）|-允许用户打开[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]通过双击 DSL 文件。<br />-将图标与目标计算机中的 DSL 文件类型关联。<br />-将与 DSL 的文件类型关联的 XSD （XML 架构）。 这可以避免警告，当文件被加载到[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。<br /><br /> 必须将安装项目添加到解决方案以创建 MSI。<br /><br /> 有关详细信息，请参阅[使用 MSI 文件部署 DSL](#msi)。|  
  
## <a name="Installing"></a> 安装和使用 VSX 卸载 DSL  
 此方法安装 DSL 时，用户可以在打开 DSL 文件[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，但无法从 Windows 资源管理器中打开该文件。  
  
#### <a name="to-install-a-dsl-by-using-the-vsx"></a>若要使用 VSX 安装 DSL  
  
1. 在您的计算机，找到 **.vsix**由 DSL 包项目生成的文件。  
  
    1. 在中**解决方案资源管理器**，右键单击**DslPackage**项目，并单击**在 Windows 资源管理器中打开文件夹**。  
  
    2. 找到的文件**bin\\\*\\**_YourProject_**。DslPackage.vsix**  
  
2. 复制 **.vsix**到目标计算机，你想要安装 DSL 的文件。 该计算机可以是自己的计算机或其他计算机。  
  
    - 目标计算机必须具有的版本之一[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]Dsl 支持在运行时。 有关详细信息，请参阅[的可视化和建模 SDK 支持 Visual Studio 版本](../modeling/supported-visual-studio-editions-for-visualization-amp-modeling-sdk.md)。  
  
    - 目标计算机必须具有的版本之一[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]中指定**DslPackage\source.extensions.manifest**。  
  
3. 在目标计算机上，双击 **.vsix**文件。  
  
     “” 将会打开并安装扩展。  
  
4. 启动或重启 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]。  
  
5. 若要测试 DSL，请使用[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]若要创建新的文件扩展名为你的 DSL 定义。  
  
#### <a name="to-uninstall-a-dsl-that-was-installed-by-using-vsx"></a>若要卸载使用 VSX 安装 DSL  
  
1. 上**工具**菜单上，单击**扩展管理器**。  
  
2. 展开“已安装的扩展” 。  
  
3. 选择该扩展在其中定义 DSL，然后单击**卸载**。  
  
   在极少数情况下，有错误的扩展无法加载并在错误窗口中创建报告，但不显示在扩展管理器中。 在这种情况下，可以通过从以下位置删除文件来删除扩展：  
  
   *LocalAppData* **\Microsoft\VisualStudio\10.0\Extensions**  
  
## <a name="msi"></a> 部署在 MSI 中的 DSL  
 通过定义用于 DSL 的 MSI （Windows 安装程序） 文件，可以允许用户从 Windows 资源管理器中打开 DSL 文件。 您还可以在文件扩展名关联的图标和简短说明。 此外，MSI 可以安装一个可以用来验证 DSL 文件的 XSD。 如果你想，您可以将其他组件添加到将安装在同一时间的 MSI。  
  
 有关 MSI 文件和其他部署选项的详细信息，请参阅[部署应用程序、 服务和组件](../deployment/deploying-applications-services-and-components.md)。  
  
 若要生成 MSI，你的安装项目添加到你[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]解决方案。 创建安装项目的最简单方法是使用 CreateMsiSetupProject.tt 模板，您可以从下载[VMSDK 站点](http://go.microsoft.com/fwlink/?LinkID=186128)。  
  
#### <a name="to-deploy-a-dsl-in-an-msi"></a>若要部署在 MSI 中的 DSL  
  
1. 设置`InstalledByMsi`扩展清单中。 这会阻止 VSX 正在安装和卸载 MSI 除外。 这是重要信息： 如果将 MSI 中包括其他组件。  
  
   1. 打开 DslPackage\source.extension.tt  
  
   2. 插入以下行之前`<SupportedProducts>`:  
  
       ```  
       <InstalledByMsi>true</InstalledByMsi>  
       ```  
  
2. 创建或编辑图标来表示你在 Windows 资源管理器的 DSL。 例如，编辑**DslPackage\Resources\File.ico**  
  
3. 请确保你的 DSL 的以下属性正确：  
  
   - 在 DSL 资源管理器中单击根节点，并在属性窗口中，查看：  
  
       - 描述  
  
       - Version  
  
   - 单击**编辑器**节点，在属性窗口中，单击**图标**。 设置要引用的图标文件中的值**DslPackage\Resources**，如**File.ico**  
  
   - 上**构建**菜单中，打开**Configuration Manager**，然后选择你想要构建，例如配置**版本**或**调试**.  
  
4. 转到[可视化和建模 SDK 主页](http://go.microsoft.com/fwlink/?LinkID=186128)，并从**下载**选项卡上，下载**CreateMsiSetupProject.tt**。  
  
5. 添加**CreateMsiSetupProject.tt**到 Dsl 项目。  
  
    [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 将创建名为的文件**CreateMsiSetupProject.vdproj**。  
  
6. 在 Windows 资源管理器，复制 Dsl\\\*.vdproj 到新的文件夹名为安装程序。  
  
    （如果你想，您现在可以排除 CreateMsiSetupProject.tt 从 Dsl 项目。）  
  
7. 在中**解决方案资源管理器**，添加**安装程序\\\*.vdproj**作为现有项目。  
  
8. 上**项目**菜单上，单击**项目依赖项**。  
  
    在中**项目依赖项**对话框框中，选择安装项目。  
  
    选中此框旁边**DslPackage**。  
  
9. 重新生成解决方案。  
  
10. 在 Windows 资源管理器，找到安装程序项目中生成的 MSI 文件。  
  
     将 MSI 文件复制到你想要安装 DSL 的计算机。 双击该 MSI 文件。 在运行安装程序。  
  
11. 在目标计算机中，创建具有 DSL 的文件扩展名的新文件。 验证：  
  
    - 在 Windows 资源管理器列表视图中，该文件将显示带图标和您定义的说明。  
  
    - 双击该文件时[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]启动，并在 DSL 的编辑器中打开 DSL 文件。  
  
    如果您愿意，你可以安装项目手动创建，而不是使用文本模板。 包括此过程的演练，请参阅第 5 章[可视化和建模 SDK 实验室](http://go.microsoft.com/fwlink/?LinkId=208878)。  
  
#### <a name="to-uninstall-a-dsl-that-was-installed-from-an-msi"></a>若要卸载从 MSI 安装的 DSL  
  
1. 在 Windows 中，打开**程序和功能**控制面板。  
  
2. 卸载 DSL。  
  
3. 重新启动 Visual Studio。
