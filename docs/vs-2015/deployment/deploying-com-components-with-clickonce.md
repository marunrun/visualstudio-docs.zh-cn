---
title: 使用 ClickOnce 部署 COM 组件 |Microsoft Docs
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
ms.openlocfilehash: 282945f473f2799b92b24321383190ca38557cbc
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63422774"
---
# <a name="deploying-com-components-with-clickonce"></a>使用 ClickOnce 部署 COM 组件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

旧的 COM 组件的部署具有传统上是一个困难的任务。 组件需要全局注册，因此可能会导致重叠的应用程序之间的意外副作用。 这种情况下通常不是.NET Framework 应用程序中的问题由于完全独立于应用程序或组件的并行兼容。 Visual Studio，可部署在 Windows XP 或更高版本的操作系统上的独立的 COM 组件。  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 提供了一种简单而安全的机制，用于部署.NET 应用程序。 但是，如果您的应用程序使用旧的 COM 组件，您需要采取其他步骤进行部署。 本主题介绍如何部署独立的 COM 组件并引用本机组件 (例如，从 Visual Basic 6.0 或视觉对象C++)。  
  
 有关部署独立的 COM 组件的详细信息，请参阅"使用简化应用程序部署[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]和免注册 COM"处[ https://msdn.microsoft.com/magazine/msdn-magazine-issues.aspx ](https://msdn.microsoft.com/magazine/msdn-magazine-issues.aspx)。  
  
## <a name="registration-free-com"></a>免注册 COM  
 免注册 COM 是一项新技术用于部署和激活隔离的 COM 组件。 其工作方式是将所有组件的类型库和通常安装到名为一个清单，为 XML 文件在系统注册表的注册信息存储在应用程序所在的文件夹中。  
  
 隔离的 COM 组件需要它在开发人员计算机上注册，但它不需要最终用户的计算机上注册。 若要隔离 COM 组件，您只需设置它的引用**独立**属性设置为**True**。 默认情况下，此属性设置为**False**，指示，它应被视为已注册的 COM 引用。 如果此属性为 **，则返回 True**，它会导致要在生成时生成此组件的清单。 它还会导致在安装过程中要复制到应用程序文件夹的相应文件。  
  
 当清单生成器遇到独立的 COM 引用时，它将枚举所有的`CoClass`中组件的类型库，其对应的注册数据，每一项匹配和生成的项清单的所有 COM 定义类型库文件中的类。  
  
## <a name="deploying-registration-free-com-components-using-clickonce"></a>免注册 COM 组件使用 ClickOnce 部署  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署技术非常适合于部署独立的 COM 组件，因为两者[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]和免注册 COM 需要一个组件，为了部署具有清单。  
  
 通常情况下，该组件的作者应提供一个清单。 如果没有，但是，Visual Studio 是能够生成自动为 COM 组件的清单。 清单生成执行期间[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]发布过程; 有关详细信息，请参阅[发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)。 此功能还允许你利用在早期开发环境，如 Visual Basic 6.0 中编写的旧组件。  
  
 有两种方法的[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署 COM 组件：  
  
- 使用引导程序来部署您的 COM 组件;这适用于所有受支持的平台。  
  
- 使用本机组件隔离 (也称为免注册 COM) 部署。 但是，这仅适用于 Windows XP 或更高版本的操作系统。  
  
### <a name="example-of-isolating-and-deploying-a-simple-com-component"></a>隔离和部署简单的 COM 组件的示例  
 为了演示免注册 COM 组件部署，此示例将在引用使用 Visual Basic 6.0 中，创建独立本机 COM 组件的 Visual Basic 中创建基于 Windows 的应用程序并将其使用部署[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]。  
  
 首先需要创建本机 COM 组件：  
  
##### <a name="to-create-a-native-com-component"></a>若要创建的本机 COM 组件  
  
1. 从使用 Visual Basic 6.0**文件**菜单上，单击**新建**，然后**项目**。  
  
2. 在中**新的项目**对话框中，选择**Visual Basic**节点，然后选择**ActiveX DLL**项目。 在“名称”框中键入 `VB6Hello`。  
  
    > [!NOTE]
    > 使用免注册 COM; 支持仅 ActiveX DLL 和 ActiveX 控件的项目类型不支持 ActiveX EXE 和 ActiveX 文档项目类型。  
  
3. 在中**解决方案资源管理器**，双击**Class1.vb**打开文本编辑器。  
  
4. 在 Class1.vb，为生成的代码后面添加以下代码`New`方法：  
  
    ```  
    Public Sub SayHello()  
       MsgBox "Message from the VB6Hello COM component"  
    End Sub  
    ```  
  
5. 生成的组件。 从**构建**菜单上，单击**生成解决方案**。  
  
> [!NOTE]
> 免注册 COM 支持仅 Dll 和 COM 控制项目类型。 您不能使用免注册 com Exe  
  
 现在可以创建基于 Windows 的应用程序，并向其添加对 COM 组件的引用。  
  
##### <a name="to-create-a-windows-based-application-using-a-com-component"></a>若要创建基于 Windows 的应用程序使用 COM 组件  
  
1. 使用 Visual Basic 中，从**文件**菜单上，单击**新建**，然后**项目**。  
  
2. 在中**新的项目**对话框中，选择**Visual Basic**节点，然后选择**Windows 应用程序**。 在“名称”框中键入 `RegFreeComDemo`。  
  
3. 在中**解决方案资源管理器**，单击**显示所有文件**按钮以显示项目引用。  
  
4. 右键单击**引用**节点，然后选择**添加引用**从上下文菜单。  
  
5. 在中**添加引用**对话框中，单击**浏览**选项卡上，导航至 VB6Hello.dll，然后选择它。  
  
    一个**vb6hello**引用将出现在引用列表。  
  
6. 指向**工具箱**，选择**按钮**控件，并将其拖到**Form1**窗体。  
  
7. 在中**属性**窗口中，设置按钮的**文本**属性设置为**Hello**。  
  
8. 双击按钮以添加处理程序代码，并在代码文件中，添加代码，因此处理程序读取，如下所示：  
  
   ```  
   Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
       Dim VbObj As New VB6Hello.Class1  
       VbObj.SayHello()  
   End Sub  
   ```  
  
9. 运行该应用程序。 从**调试**菜单上，单击**开始调试**。  
  
   接下来需要隔离控件。 每个应用程序使用的 COM 组件是在项目中表示为 COM 引用。 下可以看到这些引用**引用**中的节点**解决方案资源管理器**窗口。 (请注意，您可以添加引用直接使用**添加引用**命令**项目**菜单中，或间接通过将 ActiveX 控件拖到窗体上。)  
  
   以下步骤演示如何隔离的 COM 组件和发布更新的应用程序包含独立的控件：  
  
##### <a name="to-isolate-a-com-component"></a>若要隔离 COM 组件  
  
1. 在中**解决方案资源管理器**，在**引用**节点中，选择**vb6hello**引用。  
  
2. 在中**属性**窗口中，更改的值**独立**属性从**False**到**True**。  
  
3. 从**构建**菜单上，单击**生成解决方案**。  
  
   现在，当按 F5，应用程序按预期工作，但它现在运行下免注册 com。 为了证明这一点，请尝试注销 VB6Hello.dll 组件并运行 Visual Studio IDE 外部 RegFreeComDemo1.exe。 这一次单击按钮时，它仍然适用。 如果您暂时重命名应用程序清单，它将再次失败。  
  
> [!NOTE]
> 您可以通过暂时注销模拟 COM 组件不存在。 打开命令提示符处，转到您的系统文件夹中，通过键入`cd /d %windir%\system32`，然后通过键入注销该组件`regsvr32 /u VB6Hello.dll`。 通过键入可以再次注册该`regsvr32 VB6Hello.dll`。  
  
 最后一步是发布应用程序使用[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]:  
  
##### <a name="to-publish-an-application-update-with-an-isolated-com-component"></a>若要发布使用独立的 COM 组件的应用程序更新  
  
1. 从**构建**菜单上，单击**发布 RegFreeComDemo**。  
  
    出现“发布向导”。  
  
2. 在发布向导中，在本地计算机的磁盘，则可以访问并检查已发布的文件中指定的位置。  
  
3. 单击“完成”以发布应用程序。  
  
   如果您检查已发布的文件，您将注意 sysmon.ocx 文件是包含。 该控件是控件的完全独立于此应用程序，这意味着，如果最终用户的计算机已使用不同版本的另一个应用程序，将不会影响与此应用程序。  
  
## <a name="referencing-native-assemblies"></a>引用本机程序集  
 Visual Studio 支持对本机 Visual Basic 6.0 的引用或C++程序集;此类引用称为本机引用。 可以告知是否为本机引用通过验证，其**文件类型**属性设置为**本机**或**ActiveX**。  
  
 若要添加本机引用，请使用**添加引用**命令，然后浏览到该清单。 某些组件将放置在 DLL 内部的清单。 在这种情况下，只需选择 DLL 本身和 Visual Studio 会将其添加为本机引用如果检测到该组件包含嵌入的清单。 Visual Studio 还会自动将任何依赖文件或程序集是否引用的组件所在的文件夹的清单中列出。  
  
 COM 控件隔离轻松部署尚不具有清单的 COM 组件。 但是，如果使用清单提供了一个组件，您可以直接引用清单。 实际上，应始终使用尽可能而不是使用由该组件的作者提供的清单**独立**属性。  
  
## <a name="limitations-of-registration-free-com-component-deployment"></a>免注册 COM 组件部署的限制  
 免注册 COM 提供了明确优于传统的部署技术。 但是，有一些限制和注意事项还应指出。最大限制是，这仅适用 Windows XP 或更高版本。 免注册 COM 实现所需的核心操作系统中加载组件的方式的更改。 遗憾的是，免注册 com。 没有低级别的支持层  
  
 不是每个组件是合适的候选项的免注册 com。 如果下列任何条件成立，组件不合适：  
  
- 该组件是一个进程外服务器。 不支持 EXE 服务器;支持仅 Dll。  
  
- 该组件为操作系统的一部分，或者系统组件，如 XML、 Internet Explorer 或 Microsoft 数据访问组件 (MDAC)。 应遵循组件作者; 的重新分发策略请咨询供应商。  
  
- 该组件是应用程序，例如 Microsoft Office 的一部分。 例如，您不应尝试隔离 Microsoft Excel 对象模型。 这是 Office 的一部分，可以仅在计算机上安装的完整 Office 产品。  
  
- 该组件用于作为外接程序或管理单元中，例如 Office 外接程序或 Web 浏览器中的控件。 此类组件通常需要某种类型的定义不在范围内的清单本身的宿主环境的注册方案。  
  
- 该组件管理系统，例如，设备驱动程序的打印后台处理程序的物理或虚拟设备。  
  
- 该组件是可再发行组件的数据访问。 数据应用程序通常需要单独的数据的访问可再发行组件才能运行安装。 不应尝试隔离组件，如 Microsoft ADO 数据控件、 Microsoft OLE DB 或 Microsoft 数据访问组件 (MDAC)。 相反，如果你的应用程序使用 MDAC 或 SQL Server Express，您应该将它们设置为系统必备组件;请参阅[如何：与 ClickOnce 应用程序一起安装的必备组件](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)。  
  
  在某些情况下，可能会使组件开发人员重新设计免注册 com。 如果无法做到这一点，仍可以生成和发布应用程序依赖于它们通过使用引导程序的标准注册方案。 有关详细信息，请参阅[创建引导程序包](../deployment/creating-bootstrapper-packages.md)。  
  
  COM 组件仅可隔离每个应用程序的一次。 例如，不能将同一 COM 组件的两个不同隔离**类库**属于同一个应用程序的项目。 执行此操作将导致生成警告，并在应用程序将无法在运行时加载。 若要避免此问题，Microsoft 建议您封装单个类库中的 COM 组件。  
  
  即使应用程序的部署不需要注册，有开发人员的计算机需要注册，在 COM 中的几种方案。 `Isolated`属性需要开发人员的计算机上注册的 COM 组件，以便自动在生成过程生成清单。 没有注册捕获功能，在生成过程中调用自注册。 此外，类型库中未显式定义的任何类不会反映在清单中。 与预先存在的清单，本机引用，如使用 COM 组件时该组件可能不需要在开发时注册。 但是，注册是必需的如果该组件是 ActiveX 控件，并且你想要将其包含在**工具箱**和 Windows 窗体设计器。  
  
## <a name="see-also"></a>请参阅  
 [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)
