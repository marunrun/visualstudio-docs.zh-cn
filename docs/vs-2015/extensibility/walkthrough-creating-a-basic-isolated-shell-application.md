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
ms.openlocfilehash: e92fa99a266dc1d1b537387f3dae848a6ecb285d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63442281"
---
# <a name="walkthrough-creating-a-basic-isolated-shell-application"></a>演练：创建基本的独立的 Shell 应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练演示如何创建独立的 shell 解决方案，自定义帮助关于工具窗口，并创建安装独立的 shell 的安装程序。  
  
## <a name="prerequisites"></a>系统必备  
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。 若要部署独立的 shell，还必须使用 Visual Studio Shell （独立） 可再发行组件包。  
  
## <a name="creating-an-isolated-shell-solution"></a>创建独立的 Shell 解决方案  
 本部分演示如何使用 Visual Studio Shell 独立的项目模板来创建独立的 shell 的解决方案。 该解决方案包含以下项目：  
  
- *SolutionName*。AboutBoxPackage 项目，可用于自定义帮助的 / 关于框的外观。  
  
- ShellExtensionsVSIX 项目，其中包含定义独立的 shell 应用程序的不同组件的 source.extension.vsixmanifest 文件。  
  
- *SolutionName*项目中，它将生成调用独立的 shell 应用程序的可执行文件。 此项目包含的外壳自定义设置文件夹，它允许你自定义外观和行为的独立的 shell 应用程序。  
  
- *SolutionName* UI 项目，生成附属程序集，用于定义活动菜单命令和可本地化的字符串。  
  
#### <a name="to-create-a-basic-isolated-shell-solution"></a>若要创建基本的独立的 shell 的解决方案  
  
1. 打开 Visual Studio 并创建一个新项目。  
  
2. 在中**新的项目**窗口中，展开**其他项目类型**，然后**扩展性**。 选择**Visual Studio Shell 独立**项目模板。  
  
3. 将项目命名`MyVSShellStub`和指定的位置。 请确保**创建解决方案目录**处于选中状态，然后依次**确定**。  
  
     新解决方案将出现在**解决方案资源管理器**。  
  
4. 生成解决方案并启动调试独立的 shell 应用程序。  
  
     将显示在 Visual Studio 独立 shell。 标题栏中读取**MyVSShellStub**。 标题栏图标是从 \MyVSShellStub\Resource Files\ApplicationIcon.ico 生成。  
  
## <a name="customizing-the-application-name-and-icon"></a>自定义应用程序名称和图标  
 您可能想要设置你的应用程序外观的标题栏中使用你的公司和其徽标的名称。 以下步骤说明如何更改名称和通过更改包定义文件，MyVSShellStub.Application.pkgdef 自定义应用程序标题栏中显示的图标。  
  
#### <a name="to-customize-the-application-name-and-icon"></a>若要自定义应用程序名称和图标  
  
1. 在 MyVSShellStub 项目中，打开 \Shell Customization\MyVSShellStub.Application.pkgdef。  
  
2. 更改`AppName`元素的值为 **"AppName"="Fabrikam 音乐编辑器"**  
  
3. 若要更改应用程序图标，将复制到 \MyVSShellStub\MyVSShellStub\MyVSShellStub\ 目录的不同的图标。 现有的 ApplicationIcon.ico 文件重命名为 ApplicationIcon1.ico。 新文件重命名为 ApplicationIcon.ico。  
  
4. 生成解决方案并启动调试。 独立的 shell 会显示 IDE。 标题栏中的新图标旁边**Fabrikam 音乐编辑器**。  
  
## <a name="customizing-the-default-web-browser-home-page"></a>自定义默认 Web 浏览器主页  
 本部分演示如何更改默认主页**Web 浏览器**通过更改包定义文件的窗口。  
  
#### <a name="to-customize-the-default-web-browser-home-page"></a>若要自定义默认 Web 浏览器主页  
  
1. 在 MyVSShellStub.Application.pkgdef 文件中，更改`DefaultHomePage`元素的值为"<http://www.microsoft.com>"。  
  
2. 重新生成 MyVSShellStub 项目。  
  
3. 生成解决方案并启动调试。  
  
4. 在中**视图 / 其他 Windows**，单击**Web 浏览器**。 **Web 浏览器**窗口会显示 Microsoft Corporation 主页。  
  
## <a name="removing-the-print-command"></a>删除打印命令  
 独立的 shell UI 项目中的.vsct 文件包含一窗体的声明`<Define name=No_`*元素*`>`，其中*元素*是一个标准的 Visual Studio 菜单和命令。  
  
 如果在声明未被注释掉，将从独立 shell 中排除该菜单或命令。 相反，如果声明已被注释，菜单或命令包含在独立 shell。  
  
 在以下步骤中，在.vsct 文件中取消打印命令。  
  
#### <a name="to-remove-the-print-command"></a>若要删除的打印命令  
  
1. 确认**打印**命令显示在**文件**独立的 shell 应用程序中的菜单。  
  
2. 在 MyVSShellStubUI 项目中，打开 \Resource Files\MyVSShellStubUI.vsct 进行编辑。  
  
3. 取消注释以下行：  
  
    ```  
    <!-- <Define name="No_PrintChildrenCommand"/> -->  
    ```  
  
4. 这会删除打印命令。  
  
5. 开始调试独立的 shell 应用程序。 确认**文件 / 打印**命令将消失。  
  
## <a name="removing-features-from-the-isolated-shell"></a>从独立 Shell 中删除功能  
 您可删除部分使用 Visual Studio 编辑.pkgundef 文件，如果不希望这些功能在自定义独立的 shell 应用程序中加载的包。 一个 $RootKey$ \Packages 注册表项的子项中指定的包。  
  
> [!NOTE]
> 若要查找的 Guid 的 Visual Studio 功能，请参阅[包的 Guid 的 Visual Studio 功能](../extensibility/package-guids-of-visual-studio-features.md)。  
  
 以下过程说明如何删除 XML 编辑器与独立 shell。  
  
#### <a name="to-remove-the-xml-editor"></a>若要删除的 XML 编辑器  
  
1. 在 MyVSShellStub 项目的命令行程序自定义文件夹中打开 MyVSShellStub.pkgundef 文件。  
  
2. 取消注释以下行：  
  
     [$RootKey$\Packages\\{87569308-4813-40a0-9cd0-d7a30838ca3f}]  
  
3. 重新生成解决方案并启动调试的独立的 shell。 打开 XML 文件，例如，\MyVSShellStub\MyVSShellStub\MyVSShellStubUI\MyVSShellStubUI.vsct。 验证文件中的 XML 关键字不颜色区分，键入"<"在行上不会使 XML 工具提示。  
  
## <a name="customizing-the-helpabout-box"></a>自定义帮助 / 关于框  
 你可以自定义帮助/关于框中，这将创建为独立的 shell 项目模板的一部分。  
  
#### <a name="to-customize-the-company-name"></a>若要自定义公司名称  
  
1. 公司名称、 版权信息、 产品版本和产品说明 \Properties\AssemblyInfo.cs 文件中找到 MyVSShellStub.AboutBoxPackage 项目中。 打开此文件。  
  
2. 更改`AssemblyCompany`值设为**Fabrikam**，则`AssemblyProduct`并`AssemblyTitle`值到**Fabrikam 音乐编辑器**，并`AssemblyCopyright`值设为**版权所有 ©Fabrikam 2015**:  
  
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
  
3. 若要添加的产品的说明，请更改`AssemblyDescription`值设为**Fabrikam 音乐编辑器的说明。**:  
  
    ```  
    [assembly: AssemblyDescription("The description of Fabrikam Music editor.”)]  
    ```  
  
4. 开始调试并在独立的 shell 应用程序，打开**帮助 / 关于**框。 你应看到已更改的字符串。 帮助的 / 关于框的标题等同于`AssemblyTitle`AssemblyInfo.cs 中的值。  
  
5. 属性**帮助/关于**MyVSShellStub.AboutBoxPackage\AboutBox.xaml 文件中找到框本身。 若要更改帮助的 / 关于框的宽度，请转到`AboutDialogStyle`阻止并设置`Width`到 200 个属性：  
  
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
  
6. 重新生成解决方案并启动调试的独立的 shell。 帮助/关于框应为大约正方形。  
  
## <a name="before-you-deploy-the-isolated-shell-application"></a>在部署独立的 Shell 应用程序之前  
 可以在具有 Visual Studio Shell （独立） 可再发行组件包的任何计算机上安装独立的 shell 应用程序。 有关可再发行组件包的详细信息，请参阅[Visual Studio 扩展性下载](http://go.microsoft.com/fwlink/?LinkID=119298)网站。  
  
## <a name="deploying-the-isolated-shell-application"></a>部署独立的 Shell 应用程序  
 通过创建安装项目部署到目标计算机在独立的 shell 应用程序。 必须指定以下操作：  
  
- 文件夹和目标计算机上的文件的布局。  
  
- 在目标计算机上安装了保证.NET Framework 和 Visual Studio shell 运行时的启动条件。  
  
  在下面的过程需要在计算机上安装 InstallShield Limited Edition。  
  
#### <a name="to-create-the-setup-project"></a>若要创建安装项目  
  
1. 在中**解决方案资源管理器**，右键单击解决方案节点，然后单击**添加新项目**。  
  
2. 在中**新的项目**对话框框中，展开**其他项目类型**，然后选择**安装和部署**。 选择 InstallShield 模板。 将新项目命名`MySetup`，然后单击**确定**。  
  
3. 如果已安装 InstallShield Limited Edition，则继续下一步。  
  
    如果尚未安装 InstallShield Limited Edition，将显示 InstallShield 下载页。 按照说明下载并安装该产品，选择与你的 Visual Studio 版本兼容的 InstallShield 的版本。 您必须决定是要注册的 InstallShield 安装，或者使用它以评估方式。 完成安装之后，必须重新启动 Visual Studio。  
  
   > [!IMPORTANT]
   > 在创建 InstallShield 项目之前，必须以管理员身份启动 Visual Studio。 如果不这样做，则会出现错误，生成项目时。  
  
   后续步骤演示如何配置安装程序项目。  
  
> [!IMPORTANT]
> 请确保在配置安装项目之前构建独立的 shell 项目的发布配置至少一次。  
  
#### <a name="to-configure-the-setup-project"></a>若要配置安装项目  
  
1. 在中**解决方案资源管理器**下**MySetup**项目中，选择**项目助手**。 上的下一行**项目助手**窗口中，选择**应用程序信息**。 输入**Fabrikam**作为你的公司名称和**Fabrikam 音乐编辑器**作为你的应用程序名称。 选择右下角的向前箭头**项目助手**。  
  
2. 选择**是**下**应用程序是否需要在计算机上安装任何软件？** ，然后选择**完整 Microsoft.NET Framework 4.5 的程序包**。  
  
3. 选择**应用程序文件**按钮在窗口的底部，请确保**Fabrikam 音乐编辑器**选择文件夹。  
  
4. 选择**将文件添加**按钮。 在中**添加文件**对话框框中，添加以下文件从**MyVSShellStub\Release**文件夹：  
  
    1. MyVSShellStub.exe.config  
  
    2. DebuggerProxy.dll  
  
    3. DebuggerProxy.dll.manifest  
  
    4. MyVSShellStub.pkgdef  
  
    5. MyVSShellStub.pkgundef  
  
    6. MyVSShellStub.winprf  
  
    7. Splash.bmp  
  
5. 单击**添加项目输出**按钮，然后添加**MyVSShellStub/主输出**。 单击 **“确定”**。  
  
6. 在左窗格中下,**目标计算机**，右键单击**Fabrikam 音乐编辑器 [INSTALLDIR]** 节点，并添加**新文件夹**名为**扩展**.  
  
7. 右键单击**扩展**的左窗格中的节点，并添加名为的新文件夹**应用程序**。  
  
8. 选择**应用程序**文件夹，然后单击**添加项目输出**按钮，然后选择从 MyVSShellStub.AboutBoxPackage 项目主输出。  
  
9. 单击**将文件添加**按钮，然后从 \MyVSShellStub\Release\Extensions\Application\ 文件夹添加以下文件：  
  
    - MyVSShellStub.AboutBoxPackage.pkgdef  
  
    - MyVSShellStub.Application.pkgdef  
  
10. 右键单击**Fabrikam 音乐编辑器 [INSTALLDIR]** 的左窗格中的节点，并添加名为的新文件夹**1033年**。  
  
11. 选择 1033年文件夹，然后单击**添加项目输出**按钮，然后选择从 MyVSShellStubUI 项目主输出。  
  
12. 将移动到**应用程序快捷方式**窗口。  
  
13. 单击**新建**若要创建快捷方式，然后选择 **[ProgramFilesFolder] \Fabrikam\Fabrikam Music Editor\MyVSShellStub.Primary Output**。  
  
14. 将移动到**安装访谈**窗格。  
  
15. 将所有项都设置为**否**。  
  
16. 在中**解决方案资源管理器**，在 MySetup 项目中，打开**定义安装程序要求和操作 \ 要求**。 **要求**窗口随即打开。  
  
17. 右键单击**系统软件要求**，然后选择**创建新的启动条件**。 **系统搜索向导**出现。  
  
18. 在**要查找什么？** 窗格中，选择**注册表条目**在下拉列表中，单击**下一步**。  
  
19. 在**要如何查找？** 窗格中，选择**HKEY_LOCAL_MACHINE**作为注册表根。 输入**SOFTWARE\Wow6432Node\Microsoft\DevDiv\vs\Servicing\14.0\isoshell**适用于 64 位系统或**SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\isoshell**对于 32 位系统，并输入**安装**作为注册表值。 单击 **“下一步”**。  
  
20. 在中**你想要使用的值执行操作？** 窗格中，输入**本产品需要 Visual Studio 2015 独立 Shell 可再发行组件安装。** 作为显示文本，然后单击**完成**。  
  
21. 重新生成独立的 shell 解决方案，以创建安装项目。  
  
     可以在以下文件夹中找到 setup.exe 文件：  
  
     \MyVSShellStub\MySetup\MySetup\Express\SingleImage\DiskImages\DISK1  
  
## <a name="testing-the-installation-program"></a>测试安装程序  
 若要测试安装程序，请将 setup.exe 文件复制到另一台计算机并运行安装程序可执行文件。 您应能够运行独立的 shell 应用程序。
