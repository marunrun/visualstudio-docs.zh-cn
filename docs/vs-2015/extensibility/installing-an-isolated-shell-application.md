---
title: 安装独立 Shell 应用程序 |Microsoft Docs
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
ms.openlocfilehash: 0adc81cfe9ea4462940c31a02c6429be89709565
ms.sourcegitcommit: 9a66f1c31cc9eba0b5231af72da1d18761a9c56a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2020
ms.locfileid: "75944264"
---
# <a name="installing-an-isolated-shell-application"></a>安装独立 Shell 应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要安装 Shell 应用，必须执行以下步骤。  
  
- 准备解决方案。  
  
- 为应用程序创建 Windows Installer （MSI）包。  
  
- 创建安装引导程序。  
  
  本文档中的所有示例代码均来自[Shell 部署示例](https://code.msdn.microsoft.com/Sample-setup-program-for-81ca73f7)，您可以从 MSDN 网站上的代码库下载该示例。 此示例显示了执行其中每个步骤的结果。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行本主题描述的过程，必须在计算机上安装以下工具。  
  
- Visual Studio SDK  
  
- [WINDOWS INSTALLER XML 工具集](https://documentation.help/WiX-Toolset/index.html/)版本3。6  
  
  该示例还需要 Microsoft 可视化和建模 SDK，这并非所有外壳都需要。  
  
## <a name="preparing-your-solution"></a>准备解决方案  
 默认情况下，Shell 模板构建为 VSIX 包，但此行为主要用于调试目的。 部署 Shell 应用程序时，必须使用 MSI 包，以便在安装过程中进行注册表访问和重启。 若要准备应用程序以进行 MSI 部署，请执行以下步骤。  
  
#### <a name="to-prepare-a-shell-application-for-msi-deployment"></a>为 MSI 部署准备 Shell 应用程序  
  
1. 编辑解决方案中的每个 source.extension.vsixmanifest 文件。  
  
     在 `Identifier` 元素中，添加一个 `InstalledByMSI` 元素和一个 `SystemComponent` 元素，然后将其值设置为 "`true`"。  
  
     这些元素禁止 VSIX 安装程序尝试安装组件，并且用户无法使用 "**扩展和更新**" 对话框来卸载它们。  
  
2. 对于包含 VSIX 清单的每个项目，编辑生成任务，将内容输出到 MSI 将安装到的位置。 在生成输出中包括 VSIX 清单，但不生成 .vsix 文件。  
  
## <a name="creating-an-msi-for-your-shell"></a>为 Shell 创建 MSI  
 为了构建你的 MSI 包，我们建议你使用[Windows Installer 的 XML 工具集](https://documentation.help/WiX-Toolset/index.html)，因为它比标准安装项目提供更大的灵活性。  
  
 在 wsmanconfig.wxs 文件中，设置检测块和 Shell 组件的布局。  
  
 然后，在你的解决方案的 .reg 文件和 ApplicationRegistry 中创建注册表项。  
  
### <a name="detection-blocks"></a>检测块  
 检测块包含一个 `Property` 元素，该元素指定要检测的先决条件，并指定一个 `Condition` 元素，该元素指定在计算机上不存在先决条件时要返回的消息。 例如，Shell 应用程序需要 Microsoft Visual Studio Shell 可再发行组件，并且检测块将类似于以下标记。  
  
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
  
### <a name="layout-of-shell-components"></a>Shell 组件的布局  
 您必须添加元素，以确定要安装的目标目录结构和组件。  
  
##### <a name="to-set-the-layout-of-shell-components"></a>设置 Shell 组件的布局  
  
1. 创建 `Directory` 元素的层次结构，以表示要在目标计算机上的文件系统上创建的所有目录，如下面的示例所示。  
  
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
  
     当指定必须安装的文件时，`Id` 引用这些目录。  
  
2. 按照以下示例所示，识别 Shell 和 Shell 应用程序所需的组件。  
  
    > [!NOTE]
    > 某些元素可能引用其他 wsmanconfig.wxs 文件中的定义。  
  
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
  
    1. `ComponentRef` 元素引用另一个 wsmanconfig.wxs 文件，该文件用于标识当前组件所需的文件。 例如，GeneralProfile 在 HelpAbout 中具有以下定义： wsmanconfig.wxs。  
  
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
  
         `DirectoryRef` 元素指定这些文件在用户计算机上的位置。 `Directory` 元素指定它将安装到子目录中，每个 `File` 元素表示一个生成的文件或作为解决方案一部分存在的文件，并标识在创建 MSI 文件时可在何处找到该文件。  
  
    2. `ComponentGroupRef` 元素引用一组其他组件（或组件和组件组）。 例如，ApplicationGroup 下的 `ComponentGroupRef` 在 wsmanconfig.wxs 中定义如下。  
  
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
    > Shell （独立）应用程序所需的依赖项包括： DebuggerProxy、MasterPkgDef、资源（尤其是 winprf 文件）、应用程序和 PkgDefs。  
  
### <a name="registry-entries"></a>注册表项  
 Shell （独立）项目模板包含用于在安装时合并的注册表项的*项目名称*.reg 文件。 为了进行安装和清理，这些注册表项必须是 MSI 的组成部分。 还必须在 ApplicationRegistry. wsmanconfig.wxs 中创建匹配的注册表块。  
  
##### <a name="to-integrate-registry-entries-into-the-msi"></a>将注册表项集成到 MSI  
  
1. 在**Shell 自定义**文件夹中，打开*项目名称*.reg。  
  
2. 将 $RootFolder $ token 的所有实例替换为目标安装目录的路径。  
  
3. 添加应用程序所需的任何其他注册表项。  
  
4. 打开 ApplicationRegistry. wsmanconfig.wxs。  
  
5. 对于*项目名称*中的每个注册表项，添加相应的注册表块，如以下示例中所示。  
  
    |*ProjectName*.reg|ApplicationRegisty.wxs|  
    |-----------------------|----------------------------|  
    |[HKEY_CLASSES_ROOT\CLSID\\{bb431796-a179-4df7-b65d-c0df6bda7cc6}]<br /><br /> @ = "PhotoStudio DTE Object"|\<RegistryKey Id='DteClsidRegKey' Root='HKCR' Key='$(var.DteClsidRegKey)' Action='createAndRemoveOnUninstall'><br /><br /> \<RegistryValue Type='string' Name='@' Value='$(var.ShortProductName) DTE Object' /><br /><br /> \</RegistryKey >|  
    |[HKEY_CLASSES_ROOT\CLSID\\{bb431796-a179-4df7-b65d-c0df6bda7cc6}\LocalServer32]<br /><br /> @="$RootFolder$\PhotoStudio.exe"|\<RegistryKey Id='DteLocSrv32RegKey' Root='HKCR' Key='$(var.DteClsidRegKey)\LocalServer32' Action='createAndRemoveOnUninstall'><br /><br /> \<RegistryValue Type='string' Name='@' Value='[INSTALLDIR]$(var.ShortProductName).exe' /><br /><br /> \</RegistryKey >|  
  
     在此示例中，DteClsidRegKey 解析为顶部行中的注册表项。 ShortProductName 解析为 `PhotoStudio`。  
  
## <a name="creating-a-setup-bootstrapper"></a>创建安装引导程序  
 仅当安装了所有必备组件时，才会安装完成的 MSI。 若要简化最终用户体验，请在安装应用程序之前创建一个用于收集和安装所有必备组件的安装程序。 若要确保成功安装，请执行以下操作：  
  
- 强制管理员安装。  
  
- 检测是否已安装 Visual Studio Shell （独立）。  
  
- 按顺序运行一条或两条 Shell 安装程序。  
  
- 处理重启请求。  
  
- 运行 MSI。  
  
### <a name="enforcing-installation-by-administrator"></a>强制管理员安装  
 要使安装程序能够访问所需的目录（如\\的目录），此过程是必需的。  
  
##### <a name="to-enforce-installation-by-administrator"></a>强制管理员安装  
  
1. 打开安装项目的快捷菜单，然后选择 "**属性**"。  
  
2. 在 "**配置属性/链接器/清单文件**" 下，将 " **UAC 执行级别**" 设置为 " **requireAdministrator**"。  
  
     此属性将要求程序以管理员身份运行的特性置于嵌入清单文件中。  
  
### <a name="detecting-shell-installations"></a>检测 Shell 安装  
 若要确定是否必须安装 Visual Studio Shell （独立），请先通过检查注册表值 HKLM\Software\Microsoft\DevDiv\vs\Servicing\ShellVersion\isoshell\LCID\Install. 来确定是否已安装该程序。  
  
> [!NOTE]
> Wsmanconfig.wxs 中的 Shell 检测块还读取这些值。  
  
 HKLM\Software\Microsoft\AppEnv\14.0\ShellFolder 指定安装 Visual Studio Shell 的位置，你可以在该位置检查文件。  
  
 有关如何检测 Shell 安装的示例，请参阅 Shell 部署示例中的应用程序的 `GetProductDirFromReg` 函数。  
  
 如果计算机上没有安装包所需的 Visual Studio Shell 中的一个或两个，则必须将其添加到要安装的组件列表。 有关示例，请参阅 Shell 部署示例中 ComponentsPage 的 `ComponentsPage::OnInitDialog` 函数。  
  
### <a name="running-the-shell-installers"></a>运行 Shell 安装程序  
 若要运行 Shell 安装程序，请使用正确的命令行参数调用 Visual Studio Shell 可再发行组件。 至少必须使用命令行参数 **/norestart/q** ，并观察返回代码以确定接下来应执行的操作。 下面的示例运行 Shell （独立）可再发行组件。  
  
```  
dwResult = ExecCmd("Vs_IsoShell.exe /norestart /q", TRUE);  
```  
  
### <a name="running-the-shell-language-pack-installers"></a>运行 Shell 语言包安装程序  
 如果已安装 shell 或 shell，而只是需要语言包，则可以按照以下示例所示安装语言包。  
  
```  
dwResult = ExecCmd("Vs_IsoShellLP.exe /norestart /q", TRUE);  
  
```  
  
### <a name="deciphering-return-values"></a>解密返回值  
 在某些操作系统上，Visual Studio Shell （独立）安装需要重新启动。 此条件可由对 `ExecCmd`的调用的返回代码确定。  
  
|返回值|描述|  
|------------------|-----------------|  
|ERROR_SUCCESS|安装已完成。 你现在可以安装应用程序。|  
|ERROR_SUCCESS_REBOOT_REQUIRED|安装已完成。 您可以在计算机重新启动后安装您的应用程序。|  
|3015|安装正在进行中。 需要重新启动计算机才能继续安装。|  
  
### <a name="handling-restarts"></a>处理重启  
 使用 **/norestart**参数运行 Shell 安装程序时，指定它不会重新启动计算机或要求重新启动计算机。 但是，可能需要重新启动，并且必须确保在计算机重新启动后安装程序继续运行。  
  
 若要正确地处理重启，请确保只将一个安装程序设置为 resume，并正确处理恢复过程。  
  
 如果返回 ERROR_SUCCESS_REBOOT_REQUIRED 或3015，你的代码应在安装继续之前重新启动计算机。  
  
 若要处理重启，请执行以下操作：  
  
- 设置注册表以在 Windows 启动时恢复安装。  
  
- 执行引导程序的双重重启。  
  
- 删除 Shell 安装程序 ResumeData 密钥。  
  
- 重新启动 Windows。  
  
- 重置 MSI 的开始路径。  
  
### <a name="setting-the-registry-to-resume-setup-when-windows-starts"></a>设置注册表以在 Windows 启动时恢复安装程序  
 HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce\ 注册表项在系统启动时以管理权限执行，然后会被清除。 HKEY_CURRENT_USER 包含类似的密钥，但它以普通用户身份运行，不适用于安装。 可以通过在调用安装程序的 RunOnce 密钥中放置一个字符串值来恢复安装。 但是，我们建议使用 **/restart**或类似参数调用安装程序，以通知应用程序正在恢复，而不是启动。 您还可以包括参数以指示您在安装过程中所处的位置，这在可能需要多次重新启动的安装中尤其有用。  
  
 下面的示例演示用于恢复安装的 RunOnce 注册表项值。  
  
 `"c:\MyAppInstaller.exe /restart /SomeOtherDataFlag"`  
  
### <a name="installing-double-restart-of-bootstrapper"></a>安装引导程序的双重重新启动  
 如果直接从 RunOnce 使用安装程序，则桌面无法完全加载。 若要使完整的用户界面可用，必须创建安装程序的另一个执行并结束 RunOnce 实例。  
  
 您必须重新执行安装程序以使其获得正确的权限，并且您必须为其指定足够的信息以了解重启之前的停止位置，如以下示例所示。  
  
```  
if (_cmdLineInfo.IsRestart())  
{  
    TCHAR path[MAX_PATH]={0};  
    GetModuleFileName(NULL, path, MAX_PATH * sizeof(TCHAR));      
    ShellExecute( NULL, _T( "open" ), path, _T("/install"), 0, SW_SHOWNORMAL );  
}  
  
```  
  
### <a name="deleting-the-shell-installer-resumedata-key"></a>删除 Shell 安装程序 ResumeData 密钥  
 Shell 安装程序会将 HKLM\Software\Microsoft\VisualStudio\14.0\Setup\ResumeData 注册表项设置为在重新启动后恢复安装程序的数据。 由于你的应用程序（而不是 Shell 安装程序）正在继续，请删除该注册表项，如以下示例中所示。  
  
```  
CString resumeSetupPath(MAKEINTRESOURCE("SOFTWARE\\Microsoft\\VisualStudio\\14.0\\Setup\\ResumeData"));  
RegDeleteKey(HKEY_LOCAL_MACHINE, resumeSetupPath);  
```  
  
### <a name="restarting-windows"></a>重启 Windows  
 设置所需的注册表项后，您可以重新启动 Windows。 下面的示例为不同的 Windows 操作系统调用 "重新启动" 命令。  
  
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
  
### <a name="resetting-the-start-path-of-msi"></a>正在重置 MSI 的开始路径  
 在重新启动之前，当前目录是安装程序的位置，但在重新启动后，该位置将成为 system32 目录。 安装程序应在每次 MSI 调用之前重置当前目录，如下面的示例所示。  
  
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
 Visual Studio Shell 安装程序返回 ERROR_SUCCESS 后，你可以为应用程序运行 MSI。 由于安装程序提供了用户界面，请在安静模式（ **/q**）和日志记录（ **/l**）下启动 MSI，如以下示例所示。  
  
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
