---
title: 演练：创建基本的独立 Shell 应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, walkthroughs
- Shell [Visual Studio], walkthroughs
- walkthroughs [Visual Studio], isolated shell-based application
ms.assetid: 8b12e223-aae3-4c23-813d-ede1125f5f69
caps.latest.revision: 55
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b6dc84dd8d9f19012c4d09ba9bfd974ec181b9f6
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74291266"
---
# <a name="walkthrough-creating-a-basic-isolated-shell-application"></a>演练：创建基本的独立 Shell 应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练演示如何创建独立的 shell 解决方案，自定义 "帮助" 窗口，并创建安装独立 shell 的安装程序。  
  
## <a name="prerequisites"></a>先决条件  
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)。 若要部署独立 shell，还必须使用 Visual Studio Shell （独立）可再发行组件包。  
  
## <a name="creating-an-isolated-shell-solution"></a>创建独立 Shell 解决方案  
 本部分演示如何使用 Visual Studio Shell 独立项目模板来创建独立的 shell 解决方案。 该解决方案包含以下项目：  
  
- *解决方案名称*。AboutBoxPackage 项目，可用于自定义 "帮助/关于" 框的外观。  
  
- ShellExtensionsVSIX 项目，其中包含定义独立 shell 应用程序的不同组件的 source.extension.vsixmanifest 文件。  
  
- *解决方案名称*项目，该项目生成调用独立 shell 应用程序的可执行文件。 此项目包含 Shell 自定义文件夹，可用于 customiz 隔离 Shell 应用程序的外观和行为。  
  
- *解决方案名称*UI 项目，该项目生成定义活动菜单命令和可本地化字符串的附属程序集。  
  
#### <a name="to-create-a-basic-isolated-shell-solution"></a>创建基本的独立 shell 解决方案  
  
1. 打开 Visual Studio 并创建一个新项目。  
  
2. 在 "**新建项目**" 窗口中，展开 "**其他项目类型**"，然后展开 "可**扩展性**"。 选择 " **Visual Studio Shell 独立**项目模板"。  
  
3. 将项目命名为 `MyVSShellStub` 并指定位置。 请确保已选中 "**创建解决方案的目录**"，然后单击 **"确定"** 。  
  
     新解决方案将显示在**解决方案资源管理器**中。  
  
4. 生成解决方案并开始调试独立 shell 应用程序。  
  
     将显示 Visual Studio 独立 shell。 标题栏将读取**MyVSShellStub**。 标题栏图标是从 \MyVSShellStub\Resource Files\ApplicationIcon.ico. 生成的。  
  
## <a name="customizing-the-application-name-and-icon"></a>自定义应用程序名称和图标  
 您可能想要使用您的公司名称及其在标题栏中的徽标来标记您的应用程序。 以下步骤演示如何通过更改包定义文件 MyVSShellStub 更改显示在自定义应用程序标题栏中的名称和图标。  
  
#### <a name="to-customize-the-application-name-and-icon"></a>自定义应用程序名称和图标  
  
1. 在 MyVSShellStub 项目中，打开 \Shell Customization\MyVSShellStub.Application.pkgdef。  
  
2. 将 `AppName` 元素值更改为 **"AppName" = "Fabrikam 音乐编辑器"**  
  
3. 若要更改应用程序图标，请将不同的图标复制到 \MyVSShellStub\MyVSShellStub\MyVSShellStub\ 目录中。 将现有的 ApplicationIcon 文件重命名为 ApplicationIcon1。 将新文件重命名为 ApplicationIcon。  
  
4. 生成解决方案并启动调试。 随即出现隔离 shell IDE。 标题栏的 " **Fabrikam 音乐编辑器**" 的旁边有新图标。  
  
## <a name="customizing-the-default-web-browser-home-page"></a>自定义默认的 Web 浏览器主页  
 本部分演示如何通过更改包定义文件来更改**Web 浏览器**窗口的默认主页。  
  
#### <a name="to-customize-the-default-web-browser-home-page"></a>自定义默认的 Web 浏览器主页  
  
1. 在 MyVSShellStub 文件中，将 `DefaultHomePage` 元素值更改为 "<https://www.microsoft.com>"。  
  
2. 重新生成 MyVSShellStub 项目。  
  
3. 生成解决方案并启动调试。  
  
4. 在**视图/其他窗口**中，单击 " **Web 浏览器**"。 **Web 浏览器**窗口显示 Microsoft Corporation 主页。  
  
## <a name="removing-the-print-command"></a>删除打印命令  
 独立 shell UI 项目中的 .vsct 文件包含一组格式为 `<Define name=No_`*元素*`>`的声明，其中*Element*是标准 Visual Studio 菜单和命令之一。  
  
 如果声明为取消注释，则从独立 shell 中排除该菜单或命令。 相反，如果声明了声明，则菜单或命令将包含在独立 shell 中。  
  
 在下面的步骤中，将在 .vsct 文件中取消注释 "打印" 命令。  
  
#### <a name="to-remove-the-print-command"></a>删除 "打印" 命令  
  
1. 验证 "**打印**" 命令显示在独立 shell 应用程序的 "**文件**" 菜单上。  
  
2. 在 MyVSShellStubUI 项目中，打开 \Resource Files\MyVSShellStubUI.vsct 进行编辑。  
  
3. 取消注释此行：  
  
    ```  
    <!-- <Define name="No_PrintChildrenCommand"/> -->  
    ```  
  
4. 这会删除 "打印" 命令。  
  
5. 开始调试隔离 shell 应用程序。 验证 "**文件/打印**" 命令是否已消失。  
  
## <a name="removing-features-from-the-isolated-shell"></a>从独立 Shell 删除功能  
 如果你不想在自定义的独立 shell 应用程序中使用这些功能，则可以通过编辑 .pkgundef 文件来删除加载到 Visual Studio 中的某些包。 在 $RootKey $ \Packages 注册表项的一个子项中指定包。  
  
> [!NOTE]
> 若要查找 Visual Studio 功能的 Guid，请参阅[Visual Studio 功能的包 guid](../extensibility/package-guids-of-visual-studio-features.md)。  
  
 下面的过程演示如何从独立 shell 删除 XML 编辑器。  
  
#### <a name="to-remove-the-xml-editor"></a>删除 XML 编辑器  
  
1. 打开 MyVSShellStub 项目的 "Shell 自定义文件夹" 中的 MyVSShellStub 文件。  
  
2. 取消注释以下行：  
  
     [$RootKey $ \Packages\\{87569308-4813-40a0-9cd0-d7a30838ca3f}]  
  
3. 重新生成解决方案并开始调试独立 shell。 打开 XML 文件，例如，\MyVSShellStub\MyVSShellStub\MyVSShellStubUI\MyVSShellStubUI.vsct。 验证文件中的 XML 关键字不是着色，并且在行上键入 "<" 不会显示 XML 工具提示。  
  
## <a name="customizing-the-helpabout-box"></a>自定义 "帮助/关于" 框  
 您可以自定义 "帮助/关于" 框，它是作为独立 shell 项目模板的一部分创建的。  
  
#### <a name="to-customize-the-company-name"></a>自定义公司名称  
  
1. 公司名称、版权信息、产品版本和产品说明可在 \Properties\AssemblyInfo.cs 文件中的 MyVSShellStub AboutBoxPackage 项目中找到。 打开此文件。  
  
2. 将 `AssemblyCompany` 值更改为**fabrikam**，将 `AssemblyProduct` 和 `AssemblyTitle` 值更改为**fabrikam 音乐编辑器**，将 `AssemblyCopyright` 值更改为 "**版权所有© Fabrikam 2015**：  
  
    ```  
    [assembly: AssemblyTitle("Fabrikam Music Editor")]  
    [assembly: AssemblyDescription("")]  
    [assembly: AssemblyConfiguration("")]  
    [assembly: AssemblyCompany("Fabrikam")]  
    [assembly: AssemblyProduct("Fabrikam Music Editor")]  
    [assembly: AssemblyCopyright("Copyright © Fabrikam 2015")] [assembly: AssemblyCompany("Fabrikam")]  
    [assembly: AssemblyProduct("Fabrikam Music Editor ")]  
    [assembly: AssemblyCopyright("Copyright © Fabrikam 2015”)]  
    ```  
  
3. 若要添加产品说明，请将 `AssemblyDescription` 值更改为**Fabrikam 音乐编辑器的说明。** ：  
  
    ```  
    [assembly: AssemblyDescription("The description of Fabrikam Music editor.”)]  
    ```  
  
4. 开始调试，在独立 shell 应用程序中，打开 "**帮助/关于**" 框。 应会看到已更改的字符串。 "帮助/关于" 框的标题与 AssemblyInfo.cs 中的 `AssemblyTitle` 值相同。  
  
5. "**帮助"/"关于**" 框本身的属性位于 MyVSShellStub. AboutBoxPackage\AboutBox.xaml 文件中。 若要更改 "帮助/关于" 框的宽度，请转到 `AboutDialogStyle` 块并将 `Width` 属性设置为200：  
  
    ```  
    <Style x:Key="AboutDialogStyle" TargetType="Window">  
        <Setter Property="Height" Value="Auto" />  
        <Setter Property="Width" Value="200" />  
        <Setter Property="ShowInTaskbar" Value="False" />  
        <Setter Property="ResizeMode" Value="NoResize" />  
        <Setter Property="WindowStyle" Value="SingleBorderWindow" />  
        <Setter Property="SizeToContent" Value="Height" />  
    </Style>  
    ```  
  
6. 重新生成解决方案并开始调试独立 shell。 "帮助"/"关于" 框应该大致为正方形。  
  
## <a name="before-you-deploy-the-isolated-shell-application"></a>部署独立 Shell 应用程序之前  
 可以在具有 Visual Studio Shell （独立）可再发行组件包的任何计算机上安装独立 shell 应用程序。 有关可再发行组件包的详细信息，请参阅[Visual Studio 扩展性下载](https://go.microsoft.com/fwlink/?LinkID=119298)网站。  
  
## <a name="deploying-the-isolated-shell-application"></a>部署独立 Shell 应用程序  
 通过创建安装项目，将独立 shell 应用程序部署到目标计算机。 你必须指定以下内容：  
  
- 目标计算机上的文件夹和文件的布局。  
  
- 保证 .NET Framework 和 Visual Studio shell 运行时安装在目标计算机上的启动条件。  
  
  在以下过程中，你将需要在你的计算机上安装 InstallShield 有限版。  
  
#### <a name="to-create-the-setup-project"></a>创建安装项目  
  
1. 在**解决方案资源管理器**中，右键单击 "解决方案" 节点，然后单击 "**添加新项目**"。  
  
2. 在 "**新建项目**" 对话框中，展开 "**其他项目类型**"，然后选择 "**安装和部署**"。 选择 InstallShield 模板。 将新项目命名为 "`MySetup`"，然后单击 **"确定"** 。  
  
3. 如果已安装 InstallShield 有限版，则继续下一步。  
  
    如果尚未安装 InstallShield 有限版，将显示 "InstallShield 下载" 页。 按照说明下载并安装产品，选择与你的 Visual Studio 版本兼容的 InstallShield 版本。 必须决定是注册 InstallShield 安装还是将其用作评估版。 完成安装后，必须重启 Visual Studio。  
  
   > [!IMPORTANT]
   > 必须以管理员身份启动 Visual Studio，然后才能创建 InstallShield 项目。 如果不这样做，则在生成项目时将会收到错误。  
  
   后续步骤演示了如何配置安装项目。  
  
> [!IMPORTANT]
> 在配置安装项目之前，请确保已生成独立 shell 项目的 "发布" 配置。  
  
#### <a name="to-configure-the-setup-project"></a>配置安装程序项目  
  
1. 在**解决方案资源管理器**的 " **mysetup.bat** " 项目下，选择 "**项目助手**"。 在 "**项目助手**" 窗口的底部，选择 "**应用程序信息**"。 输入**fabrikam**作为公司名称，并输入**fabrikam 音乐编辑器**作为应用程序名称。 选择**项目助手**右下方的向前箭头。  
  
2. 如果**你的应用程序要求在计算机上安装任何软件**，请选择 **"是**"，然后选择 " **Microsoft .NET Framework 4.5 Full Package**"。  
  
3. 选择窗口底部的 "**应用程序文件**" 按钮，并确保已选中 " **Fabrikam 音乐编辑器**" 文件夹。  
  
4. 选择 "**添加文件**" 按钮。 在 "**添加文件**" 对话框中，添加**MyVSShellStub\Release**文件夹中的以下文件：  
  
    1. MyVSShellStub.exe.config  
  
    2. DebuggerProxy.dll  
  
    3. DebuggerProxy.dll.manifest  
  
    4. MyVSShellStub.pkgdef  
  
    5. MyVSShellStub.pkgundef  
  
    6. MyVSShellStub.winprf  
  
    7. 闪现  
  
5. 单击 "**添加项目输出**" 按钮，然后添加**MyVSShellStub/Primary Output**。 单击" **确定**"。  
  
6. 在左窗格中的 "**目标计算机**" 下，右键单击 " **Fabrikam 音乐编辑器 [INSTALLDIR]** " 节点，并添加一个名为 "**扩展**" 的**新文件夹**。  
  
7. 右键单击左窗格中的 "**扩展**" 节点，然后添加名为 "**应用程序**" 的新文件夹。  
  
8. 选择**应用程序**文件夹，然后单击 "**添加项目输出**" 按钮，然后从 MyVSShellStub AboutBoxPackage 项目选择主输出。  
  
9. 单击 "**添加文件**" 按钮，然后从 \MyVSShellStub\Release\Extensions\Application\ 文件夹中添加以下文件：  
  
    - MyVSShellStub.AboutBoxPackage.pkgdef  
  
    - MyVSShellStub.Application.pkgdef  
  
10. 右键单击左窗格中的 " **Fabrikam 音乐编辑器 [INSTALLDIR]** " 节点，然后添加名为**1033**的新文件夹。  
  
11. 选择1033文件夹，然后单击 "**添加项目输出**" 按钮，然后选择 MyVSShellStubUI 项目的主输出。  
  
12. 转到 "**应用程序快捷方式**" 窗口。  
  
13. 单击 "**新建**" 创建快捷方式，然后选择 " **[ProgramFilesFolder] \Fabrikam\Fabrikam 音乐 Editor\MyVSShellStub.Primary 输出**"。  
  
14. 转到 "**安装访谈**" 窗格。  
  
15. 将所有项目设置为 "**否**"。  
  
16. 在**解决方案资源管理器**的 mysetup.bat 项目中，打开 "**定义安装要求和操作 \ 要求**"。 此时将打开 "**要求**" 窗口。  
  
17. 右键单击 "**系统软件要求**" 并选择 "**创建新启动条件**"。 **系统搜索向导**随即出现。  
  
18. 在 "**你想要查找什么？** " 窗格中，选择下拉列表中的 "**注册表项**"，然后单击 "**下一步**"。  
  
19. 在 "**你希望如何查找它？** " 窗格中，选择 " **HKEY_LOCAL_MACHINE** " 作为注册表根目录。 为64位系统输入**SOFTWARE\Wow6432Node\Microsoft\DevDiv\vs\Servicing\14.0\isoshell** ，为32位系统输入**SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\isoshell** ，并输入**Install**作为注册表值。 单击“下一步”。  
  
20. 在 "**你希望如何处理值？"** 窗格中，输入**此产品需要安装 Visual Studio 2015 隔离 Shell 可再发行组件。** 作为显示文本，然后单击 "**完成**"。  
  
21. 重新生成独立 shell 解决方案以创建安装项目。  
  
     可以在以下文件夹中找到 setup.exe 文件：  
  
     \MyVSShellStub\MySetup\MySetup\Express\SingleImage\DiskImages\DISK1  
  
## <a name="testing-the-installation-program"></a>测试安装程序  
 若要测试安装，请将 setup.exe 文件复制到另一台计算机，然后运行安装程序可执行文件。 你应该能够运行独立 shell 应用程序。
