---
title: 安装独立的 Shell 应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Shell [Visual Studio], deploying shell-based applications
- Visual Studio shell, deploying shell-based applications
ms.assetid: 33416226-9083-41b5-b153-10d2bf35c012
caps.latest.revision: 41
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 60862d631d93788f10c372310da9eb3d181943ef
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63414546"
---
# <a name="installing-an-isolated-shell-application"></a>安装独立的 Shell 应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要安装的 Shell 应用程序必须执行以下步骤。  
  
- 准备你的解决方案。  
  
- 创建你的应用程序的 Windows Installer (MSI) 包。  
  
- 创建安装程序引导程序。  
  
  本文档中的示例代码的所有来自[Shell 部署示例](http://go.microsoft.com/fwlink/?LinkId=262245)，可以从 MSDN 网站上的代码库下载。 此示例演示执行每个步骤的结果。  
  
## <a name="prerequisites"></a>系统必备  
 若要执行本主题介绍的过程，必须在计算机上安装以下工具。  
  
- Visual Studio SDK  
  
- [Windows Installer XML 工具集](http://go.microsoft.com/fwlink/?LinkId=82720)版本 3.6  
  
  此示例还要求 Microsoft 可视化和建模 SDK，这不是所有外壳都需要。  
  
## <a name="preparing-your-solution"></a>准备你的解决方案  
 默认情况下，Shell 模板构建到 VSIX 包，但此行为旨在主要用于调试目的。 外壳应用程序部署时，必须使用 MSI 包以在安装过程中允许进行注册表访问和重新启动的。 若要准备 MSI 部署应用程序，请执行以下步骤。  
  
#### <a name="to-prepare-a-shell-application-for-msi-deployment"></a>若要准备 MSI 部署一个外壳应用程序  
  
1. 编辑你的解决方案中每个的.vsixmanifest 文件。  
  
     在中`Identifier`元素中，添加`InstalledByMSI`元素和一个`SystemComponent`元素，然后将其值设置为`true`。  
  
     这些元素可防止 VSIX 安装程序尝试从使用卸载安装您的组件和用户**扩展和更新**对话框。  
  
2. 有关每个项目包含 VSIX 清单，请编辑生成任务输出内容将在其中安装 MSI 的位置。 包括在 VSIX 清单中生成输出，但不生成.vsix 文件。  
  
## <a name="creating-an-msi-for-your-shell"></a>为你的 Shell 中创建 MSI  
 若要生成 MSI 包，我们建议你使用[Windows Installer XML 工具集](http://go.microsoft.com/fwlink/?LinkId=82720)因为它提供更大的灵活性比标准安装程序项目。  
  
 在 Product.wxs 文件中，设置检测块和外壳程序组件的布局。  
  
 在你的解决方案的.reg 文件和 ApplicationRegistry.wxs 中，然后创建注册表项。  
  
### <a name="detection-blocks"></a>检测块  
 检测块组成`Property`元素，用于指定进行检测的先决条件和`Condition`元素，它指定要返回到系统必备组件未存在于计算机上的消息。 例如，外壳应用程序将需要可再发行组件，在 Microsoft Visual Studio Shell，检测块将类似于下面的标记。  
  
```xml  
<Property Id="ISOSHELLSFX">  
  <RegistrySearch Id="IsoShellSfx" Root="HKLM" Key="Software\Microsoft\DevDiv\vs\Servicing\\$(var.ShellVersion)\IsoShell\$(var.ProductLanguage)" Name="Install" Type="raw" />  
</Property>  
<Property Id="INTSHELLSFX">  
  <RegistrySearch Id="IntShellSfx" Root="HKLM" Key="SOFTWARE\Microsoft\DevDiv\vs\Servicing\$(var.ShellVersion)\devenv\$(var.ProductLanguage)" Name="Install" Type="raw" />  
</Property>  
  
<Condition Message="This application requires $(var.IsoShellName).  Please install $(var.IsoShellName) then run this installer again.">  
  <![CDATA[Installed OR ISOSHELLSFX]]>  
</Condition>  
<Condition Message="This application requires $(var.IntShellName).  Please install $(var.IntShellName) then run this installer again.">  
  <![CDATA[Installed OR INTSHELLSFX]]>  
</Condition>  
  
```  
  
### <a name="layout-of-shell-components"></a>外壳程序组件的布局  
 您必须添加元素来标识目标目录结构和要安装的组件。  
  
##### <a name="to-set-the-layout-of-shell-components"></a>若要设置布局的外壳程序组件  
  
1. 创建层次结构的`Directory`元素来表示所有要在目标计算机上，在文件系统上创建如下例所示的目录。  
  
    ```xml  
    <Directory Id="TARGETDIR" Name="SourceDir">  
      <Directory Id="ProgramFilesFolder">  
        <Directory Id="CompanyDirectory" Name="$(var.CompanyName)">  
          <Directory Id="INSTALLDIR" Name="$(var.FullProductName)">  
            <Directory Id="ExtensionsFolder" Name="Extensions" />  
            <Directory Id="Folder1033" Name="1033" />  
          </Directory>  
        </Directory>  
      </Directory>  
      <Directory Id="ProgramMenuFolder">  
        <Directory Id="ApplicationProgramsFolder" Name="$(var.FullProductName)"/>  
      </Directory>  
    </Directory>  
    ```  
  
     这些目录到引用的`Id`时指定必须安装的文件。  
  
2. 标识外壳和外壳应用程序需要，如以下示例所示的组件。  
  
    > [!NOTE]
    > 某些元素可以引用其他.wxs 文件中定义。  
  
    ```xml  
    <Feature Id="ProductFeature" Title="$(var.ShortProductName)Shell" Level="1">  
      <ComponentGroupRef Id="ApplicationGroup" />  
      <ComponentGroupRef Id="HelpAboutPackage" />  
      <ComponentRef Id="GeneralProfile" />  
      <ComponentGroupRef Id="EditorAdornment"/>        
      <ComponentGroupRef Id="SlideShowDesignerGroup"/>  
  
      <!-- Note: The following ComponentGroupRef is required to pull in generated authoring from project references. -->  
      <ComponentGroupRef Id="Product.Generated" />  
    </Feature>  
    ```  
  
    1. `ComponentRef`元素引用另一个标识当前组件所需文件的.wxs 文件。 例如，GeneralProfile HelpAbout.wxs 中具有以下定义。  
  
        ```xml  
        <Fragment Id="FragmentProfiles">  
          <DirectoryRef Id="INSTALLDIR">  
            <Directory Id="ProfilesFolder" Name="Profiles">  
              <Component Id='GeneralProfile' Guid='*'>  
                <File Id='GeneralProfile' Name='General.vssettings' DiskId='1' Source='$(var.BuildOutputDir)Profiles\General.vssettings' KeyPath='yes' />  
              </Component>  
            </Directory>  
          </DirectoryRef>  
        </Fragment>  
        ```  
  
         `DirectoryRef`元素指定在用户的计算机上转这些文件。 `Directory`元素指定，则将安装到子目录，而每台`File`元素表示的文件生成或，作为解决方案的一部分存在，并且标识该文件可以找到创建的 MSI 文件时。  
  
    2. `ComponentGroupRef`元素表示一组的其他组件 （或组件以及组件组）。 例如， `ComponentGroupRef` ApplicationGroup 下定义，如下所示 Application.wxs 中。  
  
        ```xml  
        <ComponentGroup Id="ApplicationGroup">  
          <ComponentGroupRef Id="DebuggerProxy" />  
          <ComponentRef Id="MasterPkgDef" />  
          <ComponentRef Id="SplashResource" />  
          <ComponentRef Id="IconResource" />  
          <ComponentRef Id="WinPrfResource" />  
          <ComponentRef Id="AppExe" />  
          <ComponentRef Id="AppConfig" />  
          <ComponentRef Id="AppPkgDef" />  
          <ComponentRef Id="AppPkgDefUndef" />  
          <ComponentRef Id="$(var.ShortProductName)UI1033" />  
          <ComponentRef Id="ApplicationShortcut"/>  
          <ComponentRef Id="ApplicationRegistry"/>  
        </ComponentGroup>  
        ```  
  
    > [!NOTE]
    > Shell （独立） 应用程序必需的依赖项是：DebuggerProxy，MasterPkgDef，资源 （尤其是.winprf 文件），应用程序和 PkgDefs。  
  
### <a name="registry-entries"></a>注册表项  
 Shell （独立） 项目模板包括*ProjectName*合并安装上的注册表项的.reg 文件。 这些注册表项必须是安装和清理目的的 MSI 的一部分。 此外必须在 ApplicationRegistry.wxs 中创建匹配的注册表基块。  
  
##### <a name="to-integrate-registry-entries-into-the-msi"></a>若要将集成到 MSI 的注册表项  
  
1. 在中**外壳自定义设置**文件夹中，打开*ProjectName*。 地区  
  
2. $RootFolder$ 令牌的所有实例都替换为目标安装目录的路径。  
  
3. 添加应用程序所需的任何其他注册表项。  
  
4. 打开 ApplicationRegistry.wxs。  
  
5. 为在每个注册表条目*ProjectName*.reg，添加相应的注册表块，如以下示例所示。  
  
    |*ProjectName*.reg|ApplicationRegisty.wxs|  
    |-----------------------|----------------------------|  
    |[HKEY_CLASSES_ROOT\CLSID\\{bb431796-a179-4df7-b65d-c0df6bda7cc6}]<br /><br /> @="PhotoStudio DTE Object"|\<RegistryKey Id='DteClsidRegKey' Root='HKCR' Key='$(var.DteClsidRegKey)' Action='createAndRemoveOnUninstall'><br /><br /> \<RegistryValue Type='string' Name='@' Value='$(var.ShortProductName) DTE Object' /><br /><br /> \</RegistryKey>|  
    |[HKEY_CLASSES_ROOT\CLSID\\{bb431796-a179-4df7-b65d-c0df6bda7cc6}\LocalServer32]<br /><br /> @="$RootFolder$\PhotoStudio.exe"|\<RegistryKey Id='DteLocSrv32RegKey' Root='HKCR' Key='$(var.DteClsidRegKey)\LocalServer32' Action='createAndRemoveOnUninstall'><br /><br /> \<RegistryValue Type='string' Name='@' Value='[INSTALLDIR]$(var.ShortProductName).exe' /><br /><br /> \</RegistryKey>|  
  
     在此示例中，Var.DteClsidRegKey 解析为最上面一行中的注册表项。 Var.ShortProductName 解析为`PhotoStudio`。  
  
## <a name="creating-a-setup-bootstrapper"></a>创建安装程序引导程序  
 仅当首次安装所有必备组件，将安装已完成的 MSI。 若要简化最终用户体验，创建收集并安装你的应用程序之前安装所有必备组件的安装程序。 若要确保成功安装，请执行以下操作：  
  
- 强制执行由管理员安装。  
  
- 检测是否安装了 Visual Studio Shell （独立）。  
  
- 按顺序运行一个或两个命令行程序安装程序。  
  
- 处理重新启动请求。  
  
- 运行 MSI。  
  
### <a name="enforcing-installation-by-administrator"></a>强制执行由管理员安装  
 此过程需启用安装程序来访问所需的目录，如 \Program Files\\。  
  
##### <a name="to-enforce-installation-by-administrator"></a>若要强制执行由管理员安装  
  
1. 打开安装项目的快捷菜单，然后选择**属性**。  
  
2. 下**配置属性 / 链接器 / 清单文件**，请设置**UAC 执行级别**到**requireAdministrator**。  
  
     此属性将放到嵌入的清单文件，以管理员身份运行该程序所需的属性。  
  
### <a name="detecting-shell-installations"></a>检测 Shell 安装  
 若要确定是否必须安装 Visual Studio Shell （独立），请首先确定是否已安装通过检查 HKLM\Software\Microsoft\DevDiv\vs\Servicing\ShellVersion\isoshell\LCID\Install 的注册表值。  
  
> [!NOTE]
> 由 Shell 检测块中 Product.wxs 还读取这些值。  
  
 HKLM\Software\Microsoft\AppEnv\14.0\ShellFolder 指定的位置的已安装 Visual Studio Shell，并可以检查那里文件。  
  
 有关如何检测 Shell 安装的示例，请参阅`GetProductDirFromReg`Utilities.cpp Shell 部署示例中的函数。  
  
 如果一个或两个为包所需的 Visual Studio Shell 的计算机上未安装，必须将它们添加到要安装的组件列表。 有关示例，请参阅`ComponentsPage::OnInitDialog`ComponentsPage.cpp Shell 部署示例中的函数。  
  
### <a name="running-the-shell-installers"></a>运行命令行程序安装程序  
 若要运行的命令行程序安装程序，请使用正确的命令行自变量调用 Visual Studio Shell 可再发行组件。 至少，必须使用命令行参数 **/norestart /q**并留意其中的返回代码，以确定应如何处理下一步。 下面的示例运行 Shell （独立） 可再发行组件。  
  
```  
dwResult = ExecCmd("Vs_IsoShell.exe /norestart /q", TRUE);  
```  
  
### <a name="running-the-shell-language-pack-installers"></a>运行 Shell 语言包安装程序  
 如果您改为查找已安装的命令行程序或 shell，只需要一种语言包，则可以如以下示例所示安装语言包。  
  
```  
dwResult = ExecCmd("Vs_IsoShellLP.exe /norestart /q", TRUE);  
  
```  
  
### <a name="deciphering-return-values"></a>解密的返回值  
 在某些操作系统上的 Visual Studio Shell （独立） 安装需要重新启动。 此条件可通过对调用的返回代码确定`ExecCmd`。  
  
|返回值|描述|  
|------------------|-----------------|  
|ERROR_SUCCESS|安装已完成。 现在可以安装你的应用程序。|  
|ERROR_SUCCESS_REBOOT_REQUIRED|安装已完成。 重新启动计算机后，你可以安装你的应用程序。|  
|3015|安装正在进行中。 重新启动计算机才能继续安装。|  
  
### <a name="handling-restarts"></a>处理重新启动  
 通过使用运行程序安装程序时 **/norestart**参数，指定它不会重新启动计算机，或者要求重新启动计算机。 但是，可能需要重新启动，并且必须确保您的安装程序将继续后重新启动计算机。  
  
 若要正确地处理重新启动，请确保安装程序的只有一个是组恢复和恢复进程会得到正确处理。  
  
 如果返回 ERROR_SUCCESS_REBOOT_REQUIRED 或 3015 时，你的代码在安装继续前应重新启动计算机。  
  
 若要处理的重启，请执行以下操作：  
  
- 设置注册表以继续安装，Windows 启动时。  
  
- 执行双引导程序重新启动。  
  
- 删除命令行程序安装程序 ResumeData 密钥。  
  
- 重启 Windows。  
  
- 重置的 MSI 开始路径。  
  
### <a name="setting-the-registry-to-resume-setup-when-windows-starts"></a>当 Windows 启动时恢复安装程序将注册表设置  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce\ 注册表项在使用管理权限的系统启动时执行，然后清除。 HKEY_CURRENT_USER 包含类似的密钥，但它以普通用户身份运行，并不适用于安装。 可以通过将一个字符串值放入 RunOnce 项调用您的安装程序继续安装。 但是，我们建议使用调用安装程序**重启**或类似的参数，以通知它正在恢复而不启动该应用程序。 此外可以包含参数来指示安装过程中，这可能需要多次重新启动的安装中特别有用的。  
  
 下面的示例显示了用于恢复安装 RunOnce 注册表项值。  
  
 `"c:\MyAppInstaller.exe /restart /SomeOtherDataFlag"`  
  
### <a name="installing-double-restart-of-bootstrapper"></a>安装双引导程序重新启动  
 如果直接从 RunOnce 使用安装程序，则在桌面上不能完全加载。 若要使完整的用户界面，必须创建另一个执行安装程序并结束 RunOnce 实例。  
  
 必须重新执行安装程序，以便获取正确的权限，并必须为其提供足够的信息来了解您停止的位置之前重新启动，如以下示例所示。  
  
```  
if (_cmdLineInfo.IsRestart())  
{  
    TCHAR path[MAX_PATH]={0};  
    GetModuleFileName(NULL, path, MAX_PATH * sizeof(TCHAR));      
    ShellExecute( NULL, _T( "open" ), path, _T("/install"), 0, SW_SHOWNORMAL );  
}  
  
```  
  
### <a name="deleting-the-shell-installer-resumedata-key"></a>正在删除命令行程序安装程序 ResumeData 密钥  
 程序安装程序设置 HKLM\Software\Microsoft\VisualStudio\14.0\Setup\ResumeData 注册表项与要重启后继续运行安装程序数据。 由于应用程序时，不程序安装程序，正在继续，删除该注册表项，如以下示例所示。  
  
```  
CString resumeSetupPath(MAKEINTRESOURCE("SOFTWARE\\Microsoft\\VisualStudio\\14.0\\Setup\\ResumeData"));  
RegDeleteKey(HKEY_LOCAL_MACHINE, resumeSetupPath);  
```  
  
### <a name="restarting-windows"></a>正在重启 Windows  
 设置必需的注册表项后，可以重新启动 Windows。 下面的示例调用不同的 Windows 操作系统的重新启动命令。  
  
```  
OSVERSIONINFO ov;  
HANDLE htoken ;  
//Ask for the SE_SHUTDOWN_NAME token as this is needed by the thread calling for a system shutdown.  
if (OpenProcessToken(GetCurrentProcess(), TOKEN_ADJUST_PRIVILEGES | TOKEN_QUERY, &htoken))  
{  
    LUID luid ;  
    LookupPrivilegeValue(NULL, SE_SHUTDOWN_NAME, &luid) ;  
    TOKEN_PRIVILEGES    privs ;  
    privs.Privileges[0].Luid = luid ;  
    privs.PrivilegeCount = 1 ;  
    privs.Privileges[0].Attributes = SE_PRIVILEGE_ENABLED ;  
    AdjustTokenPrivileges(htoken, FALSE, &privs, 0, (PTOKEN_PRIVILEGES) NULL, 0) ;  
}   
  
//Use InitiateSystemShutdownEx to avoid unexpected restart message box  
try  
{              
    if ( (ov.dwMajorVersion > 5) || ( (ov.dwMajorVersion == 5) && (ov.dwMinorVersion  > 0) ))  
    {  
        bExitWindows = InitiateSystemShutdownEx(0, _T(""), 0, TRUE, TRUE, REASON_PLANNED_FLAG);  
    }  
    else  
    {  
#pragma prefast(suppress:380,"ignore warning about legacy api")  
        bExitWindows = InitiateSystemShutdown(0, _T(""), 0, TRUE, TRUE);  
    }  
}  
catch(...)  
{  
    //advapi32.dll call not available! Will not restart!  
}  
  
```  
  
### <a name="resetting-the-start-path-of-msi"></a>重置 MSI 起始的路径  
 重新启动之前, 的当前目录是你的安装程序的位置，但是，重启后，位置将成为 system32 目录。 如以下示例所示，安装程序应重置之前每个 MSI 调用时，在当前目录。  
  
```  
CString GetSetupPath()  
{  
    TCHAR file[MAX_PATH];  
    GetModuleFileName(NULL, file, MAX_PATH * sizeof(TCHAR));  
    CString path(file);  
    int fpos = path.ReverseFind('\\');  
    if (fpos != -1)  
    {  
        path = path.Left(fpos + 1);  
    }  
  
    return path;  
}  
  
```  
  
### <a name="running-the-application-msi"></a>运行应用程序 MSI  
 Visual Studio Shell 安装程序将返回 ERROR_SUCCESS 后，你可以为应用程序运行 MSI。 因为您的安装程序会向用户界面，在静默模式下启动 MSI (**/q**) 和使用日志记录 (**/L**)，如下面的示例所示。  
  
```cpp#  
TCHAR temp[MAX_PATH];  
GetTempPath(MAX_PATH, temp);  
  
CString boutiqueInstallCmd, msi, log;  
CString cmdLine(MAKEINTRESOURCE("msiexec /q /I %s /L*vx %s REBOOT=ReallySuppress"));  
CString name(MAKEINTRESOURCE("PhotoStudioIntShell.msi"));  
log.Format(_T("\"%s%s.log\""), temp, name);  
msi.Format(_T("\"%s%s\""), GetSetupPath(), name);  
boutiqueInstallCmd.Format(cmdLine, msi, log);  
  
//TODO: You can use MSI API to gather and present install progress feedback from your MSI.  
dwResult = ExecCmd(boutiqueInstallCmd, FALSE);  
```  
  
## <a name="see-also"></a>请参阅  
 [演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)
