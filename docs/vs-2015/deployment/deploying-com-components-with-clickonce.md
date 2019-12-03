---
title: 用 ClickOnce 部署 COM 组件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- registration-free COM deployment
- ClickOnce deployment, COM components
- COM components, deploying
- deploying applications [ClickOnce], COM components
- components, deploying
ms.assetid: 1a4c7f4c-7a41-45f2-9af4-8b1666469b89
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6c83367881b7ed6a69fe10af8b7c68eb1692e3e6
ms.sourcegitcommit: 49ebf69986713e440fd138fb949f1c0f47223f23
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74706898"
---
# <a name="deploying-com-components-with-clickonce"></a>使用 ClickOnce 部署 COM 组件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

传统的 COM 组件的部署通常是一件很困难的任务。 组件需要全局注册，因此可能会导致重叠应用程序之间的不良副作用。 这种情况通常并不是 .NET Framework 应用程序中的问题，因为组件完全独立于应用程序或并行兼容。 Visual Studio 允许你在 Windows XP 或更高版本的操作系统上部署隔离的 COM 组件。  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 为部署 .NET 应用程序提供了一种简单且安全的机制。 但是，如果应用程序使用旧的 COM 组件，则需要执行其他步骤来部署它们。 本主题介绍如何部署独立的 COM 组件和引用本机组件（例如，从 Visual Basic 6.0 或视觉对象C++）。  
  
 有关部署独立的 COM 组件的详细信息，请参阅[通过 ClickOnce 和免注册 COM 简化应用部署](/archive/msdn-magazine/2005/april/simplify-app-deployment-with-clickonce-and-registration-free-com)。  
  
## <a name="registration-free-com"></a>免注册 COM  
 免费注册 COM 是一种用于部署和激活隔离的 COM 组件的新技术。 它的工作方式是将所有组件的类型库和注册信息（通常安装在系统注册表中）放到称为清单的 XML 文件中，该文件存储在与应用程序相同的文件夹中。  
  
 隔离 COM 组件要求在开发人员的计算机上注册该组件，但不需要在最终用户的计算机上注册该组件。 若要隔离 COM 组件，只需将其引用的**独立**属性设置为**True**。 默认情况下，此属性设置为**False**，表示它应被视为已注册的 COM 引用。 如果此属性为**True**，则会在生成时为此组件生成清单。 它还会在安装过程中将相应的文件复制到应用程序文件夹。  
  
 当清单生成器遇到独立的 COM 引用时，它会枚举组件的类型库中的所有 `CoClass` 条目，将每个条目与其相应的注册数据相匹配，并为类型库文件中的所有 COM 类生成清单定义。  
  
## <a name="deploying-registration-free-com-components-using-clickonce"></a>使用 ClickOnce 部署免注册 COM 组件  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署技术非常适合用于部署独立的 COM 组件，因为 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 和免注册 COM 都需要组件具有一个清单才能进行部署。  
  
 通常，组件的作者应提供一个清单。 但是，如果不是，则 Visual Studio 可以为 COM 组件自动生成清单。 清单生成在 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 发布过程中执行;有关详细信息，请参阅[发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)。 此功能还允许你利用在早期开发环境（如 Visual Basic 6.0）中创作的旧组件。  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署 COM 组件有两种方式：  
  
- 使用引导程序部署 COM 组件;这适用于所有受支持的平台。  
  
- 使用本机组件隔离（也称为无注册 COM）部署。 但是，这仅适用于 Windows XP 或更高版本的操作系统。  
  
### <a name="example-of-isolating-and-deploying-a-simple-com-component"></a>隔离和部署简单 COM 组件的示例  
 为了演示无注册的 COM 组件部署，此示例将在 Visual Basic 中创建一个基于 Windows 的应用程序，该应用程序引用使用 Visual Basic 6.0 创建的隔离的本机 COM 组件，并使用 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署该组件。  
  
 首先，需要创建本机 COM 组件：  
  
##### <a name="to-create-a-native-com-component"></a>创建本机 COM 组件  
  
1. 使用 Visual Basic 6.0，在 "**文件**" 菜单中依次单击 "**新建**"、"**项目**"。  
  
2. 在 "**新建项目**" 对话框中，选择 " **Visual Basic** " 节点，然后选择**ActiveX DLL**项目。 在“名称”框中键入 `VB6Hello`。  
  
    > [!NOTE]
    > 无注册 COM 仅支持 ActiveX DLL 和 ActiveX 控件项目类型;不支持 ActiveX EXE 和 ActiveX 文档项目类型。  
  
3. 在**解决方案资源管理器**中，双击 " **Class1** " 打开文本编辑器。  
  
4. 在 Class1 中，将以下代码添加到 `New` 方法的生成代码之后：  
  
    ```  
    Public Sub SayHello()  
       MsgBox "Message from the VB6Hello COM component"  
    End Sub  
    ```  
  
5. 生成组件。 在 "**生成**" 菜单中，单击 "**生成解决方案**"。  
  
> [!NOTE]
> 免注册 COM 仅支持 Dll 和 COM 控件项目类型。 不能对无注册 COM 使用 Exe。  
  
 现在，你可以创建基于 Windows 的应用程序并向其添加对 COM 组件的引用。  
  
##### <a name="to-create-a-windows-based-application-using-a-com-component"></a>使用 COM 组件创建基于 Windows 的应用程序  
  
1. 使用 Visual Basic，在 "**文件**" 菜单中依次单击 "**新建**"、"**项目**"。  
  
2. 在 "**新建项目**" 对话框中，选择 " **Visual Basic** " 节点，然后选择 " **Windows 应用程序**"。 在“名称”框中键入 `RegFreeComDemo`。  
  
3. 在**解决方案资源管理器**中，单击 "**显示所有文件**" 按钮以显示项目引用。  
  
4. 右键单击 "**引用**" 节点，然后从上下文菜单中选择 "**添加引用**"。  
  
5. 在 "**添加引用**" 对话框中，单击 "**浏览**" 选项卡，导航到 "VB6Hello"，然后选择它。  
  
    "引用" 列表中将出现一个**VB6Hello**引用。  
  
6. 指向 "**工具箱**"，选择一个 "**按钮**" 控件，然后将其拖到 " **Form1** " 窗体。  
  
7. 在 "**属性**" 窗口中，将按钮的**Text**属性设置为 " **Hello**"。  
  
8. 双击该按钮添加处理程序代码，然后在代码文件中添加代码，使处理程序按如下所示进行读取：  
  
   ```  
   Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
       Dim VbObj As New VB6Hello.Class1  
       VbObj.SayHello()  
   End Sub  
   ```  
  
9. 运行该应用程序。 从 "**调试**" 菜单中，单击 "**启动调试**"。  
  
   接下来，需要隔离控件。 您的应用程序使用的每个 COM 组件都在您的项目中表示为 COM 引用。 这些引用在 "**解决方案资源管理器**" 窗口中的 "**引用**" 节点下可见。 （请注意，可以直接使用 "**项目**" 菜单上的 "**添加引用**" 命令来添加引用，也可以通过将 ActiveX 控件拖到窗体上来间接添加引用。）  
  
   以下步骤演示如何隔离 COM 组件和发布包含独立控件的更新应用程序：  
  
##### <a name="to-isolate-a-com-component"></a>隔离 COM 组件  
  
1. 在**解决方案资源管理器**的 "**引用**" 节点中，选择**VB6Hello**引用。  
  
2. 在 "**属性**" 窗口中，将**隔离**属性的值从**False**更改为**True**。  
  
3. 在 "**生成**" 菜单中，单击 "**生成解决方案**"。  
  
   现在，按 F5 后，应用程序将按预期方式工作，但它现在正在无注册 COM 下运行。 为了证明这一点，请尝试在 Visual Studio IDE 之外注销 VB6Hello 组件并运行 RegFreeComDemo1。 这次单击该按钮时，它仍然有效。 如果暂时重命名应用程序清单，则会再次失败。  
  
> [!NOTE]
> 可以通过暂时取消注册 COM 组件来模拟该组件。 打开命令提示符，通过键入 "`cd /d %windir%\system32`"，然后通过键入 `regsvr32 /u VB6Hello.dll`取消注册该组件。 您可以通过键入 `regsvr32 VB6Hello.dll`重新注册它。  
  
 最后一步是使用 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]发布应用程序：  
  
##### <a name="to-publish-an-application-update-with-an-isolated-com-component"></a>使用独立的 COM 组件发布应用程序更新  
  
1. 在 "**生成**" 菜单中，单击 "**发布 RegFreeComDemo**"。  
  
    此时，将显示发布向导。  
  
2. 在发布向导中，指定本地计算机磁盘上的位置，您可以在该位置访问和检查已发布的文件。  
  
3. 单击“完成”以发布应用程序。  
  
   如果检查已发布的文件，则会注意到包含 sysmon 文件。 此控件完全独立于此应用程序，这意味着，如果最终用户的计算机使用其他版本的控件，则它不能干扰此应用程序。  
  
## <a name="referencing-native-assemblies"></a>引用本机程序集  
 Visual Studio 支持对本机 Visual Basic 6.0 或C++程序集的引用;此类引用称为本机引用。 可以通过验证引用是否设置为**本机**或**ActiveX**来判断引用是否为本机引用。  
  
 若要添加本机引用，请使用 "**添加引用**" 命令，然后浏览到该清单。 某些组件将清单置于 DLL 中。 在这种情况下，只需选择 DLL 本身，Visual Studio 就会将其添加为本机引用（如果它检测到组件包含嵌入的清单）。 如果清单中列出的所有依赖文件或程序集位于与引用组件相同的文件夹中，则它也会自动包括这些文件或程序集。  
  
 利用 COM 控制隔离，可以轻松地部署没有清单的 COM 组件。 但是，如果使用清单提供组件，则可以直接引用清单。 事实上，应始终使用组件作者提供的清单，而不是使用**独立**的属性。  
  
## <a name="limitations-of-registration-free-com-component-deployment"></a>免注册 COM 组件部署的限制  
 无注册 COM 比传统部署技术提供明显的优点。 但是，还应指出一些限制和注意事项。最大限制是它仅适用于 Windows XP 或更高版本。 无需注册的 COM 的实现需要更改在核心操作系统中加载组件的方式。 遗憾的是，免费的 COM 没有下级支持层。  
  
 并非每个组件都适用于无注册 COM。 如果满足以下任一条件，则组件不适合：  
  
- 组件是进程外服务器。 不支持 EXE 服务器;仅支持 Dll。  
  
- 组件是操作系统的一部分，或者是系统组件，例如 XML、Internet Explorer 或 Microsoft 数据访问组件（MDAC）。 应遵循组件作者的再分发策略;咨询供应商。  
  
- 组件是应用程序的一部分，如 Microsoft Office。 例如，不应尝试隔离 Microsoft Excel 对象模型。 这是 Office 的一部分，只能在安装了完整 Office 产品的计算机上使用。  
  
- 组件用于作为外接程序或管理单元（例如，Office 外接程序或 Web 浏览器中的控件）。 此类组件通常需要宿主环境定义的某种注册方案，而该方案超出了清单本身的范围。  
  
- 组件管理系统的物理或虚拟设备，例如，打印后台处理程序的设备驱动程序。  
  
- 该组件是可再发行的数据访问。 数据应用程序通常需要安装单独的数据访问可再发行组件，才能运行。 不应尝试隔离某些组件，如 Microsoft ADO 数据控件、Microsoft OLE DB 或 Microsoft 数据访问组件（MDAC）。 相反，如果应用程序使用 MDAC 或 SQL Server Express，则应将其设置为必备组件;请参阅[如何：使用 ClickOnce 应用程序安装必备组件](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)。  
  
  在某些情况下，组件的开发人员可能会将其重新设计为免注册 COM。 如果无法做到这一点，则仍可使用引导程序通过标准注册方案生成并发布依赖于它们的应用程序。 有关详细信息，请参阅[创建引导程序包](../deployment/creating-bootstrapper-packages.md)。  
  
  每个应用程序只能隔离一个 COM 组件。 例如，不能将同一 COM 组件与属于同一应用程序的两**个不同类库**项目隔离开来。 这样做会导致生成警告，并且应用程序在运行时将无法加载。 为了避免此问题，Microsoft 建议你将 COM 组件封装在一个类库中。  
  
  开发人员的计算机上需要进行 COM 注册，即使应用程序的部署不需要注册也是如此。 `Isolated` 属性要求在开发人员的计算机上注册 COM 组件，以便在生成过程中自动生成清单。 无注册捕获功能可在生成过程中调用自注册。 此外，类型库中未显式定义的任何类将不会反映在清单中。 将 COM 组件与预先存在的清单（如本机引用）结合使用时，可能不需要在开发时注册该组件。 但是，如果组件是 ActiveX 控件并且你想要将其包含在 "**工具箱**" 和 "Windows 窗体设计器" 中，则需要注册。  
  
## <a name="see-also"></a>请参阅  
 [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)
