---
title: 如何：指定生成事件 (Visual Basic) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- pre-build events
- events [Visual Studio], builds
- post-build events
- build events [Visual Studio]
- builds [Visual Studio], events
ms.assetid: 40dc83bf-a7c5-4a14-816a-fa0980b6e4c3
caps.latest.revision: 28
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: c21b50aab30d3ce7603ab8e5f7e6582332e94628
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65685403"
---
# <a name="how-to-specify-build-events-visual-basic"></a>如何：指定生成事件 (Visual Basic)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Basic 中的生成事件可用于运行脚本、宏或用作作为编译过程的一部分的其他操作。 预生成事件发生于编译之前；生成后事件发生于编译之后。  
  
 在“生成事件”对话框中指定生成事件，可从“项目设计器”的“编译”页面获取。  
  
> [!NOTE]
> Visual Basic 速成版不支持输入生成事件。 仅完整版 Visual Studio 产品支持此操作。  
  
## <a name="how-to-specify-pre-build-and-post-build-events"></a>如何指定预生成事件和生成后事件  
  
#### <a name="to-specify-a-build-event"></a>指定生成事件  
  
1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。  
  
2. 单击“编译”选项卡。  
  
3. 单击“生成事件”按钮以打开“生成事件”对话框。  
  
4. 输入预生成操作或生成后操作的命令行参数，然后单击“确定”。  
  
    > [!NOTE]
    > 在运行 .bat 文件的所有生成后命令之前添加 `call` 语句。 例如，`call C:\MyFile.bat` 或 `call C:\MyFile.bat call C:\MyFile2.bat`。  
  
    > [!NOTE]
    > 如果预生成事件或生成后事件未成功完成，可通过使用除零 (0) 之外的代码退出事件操作来终止生成，这表示操作成功。  
  
## <a name="example-how-to-change-manifest-information-using-a-post-build-event"></a>示例:如何使用生成后事件更改清单信息  
 以下过程演示如何使用从生成后事件（项目目录中的 .exe.manifest 文件）调用的 .exe 命令在应用程序清单中设置最低的操作系统版本。 最低的操作系统版本是由四个部分组成的数字组合，例如 4.10.0.0。 为此，该命令将更改清单的 `<dependentOS>` 部分：  
  
```  
<dependentOS>  
   <osVersionInfo>  
      <os majorVersion="4" minorVersion="10" buildNumber="0" servicePackMajor="0" />  
   </osVersionInfo>  
</dependentOS>  
```  
  
#### <a name="to-create-an-exe-command-to-change-the-application-manifest"></a>创建 .exe 命令以更改应用程序清单  
  
1. 为命令创建控制台应用程序。 在“文件”菜单上，单击“新建”，然后单击“项目”。  
  
2. 在“新建项目”对话框的“Visual Basic”节点中，依次选择“Windows”、“控制台应用程序”模板。 将项目命名为 `ChangeOSVersionVB`。  
  
3. 在 Module1.vb 中，将以下行添加到文件顶部的其他 `Imports` 语句中：  
  
   ```  
   Imports System.Xml  
   ```  
  
4. 在 `Sub Main` 中添加下列代码：  
  
   ```  
   Sub Main()  
      Dim applicationManifestPath As String  
      applicationManifestPath = My.Application.CommandLineArgs(0)  
      Console.WriteLine("Application Manifest Path: " & applicationManifestPath.ToString)  
  
      'Get version name  
      Dim osVersion As Version  
      If My.Application.CommandLineArgs.Count >= 2 Then  
         osVersion = New Version(My.Application.CommandLineArgs(1).ToString)  
      Else  
         Throw New ArgumentException("OS Version not specified.")  
      End If  
      Console.WriteLine("Desired OS Version: " & osVersion.ToString())  
  
      Dim document As XmlDocument  
      Dim namespaceManager As XmlNamespaceManager  
      namespaceManager = New XmlNamespaceManager(New NameTable())  
      With namespaceManager  
         .AddNamespace("asmv1", "urn:schemas-microsoft-com:asm.v1")  
         .AddNamespace("asmv2", "urn:schemas-microsoft-com:asm.v2")  
      End With  
  
      document = New XmlDocument()  
      document.Load(applicationManifestPath)  
  
      Dim baseXPath As String  
      baseXPath = "/asmv1:assembly/asmv2:dependency/asmv2:dependentOS/asmv2:osVersionInfo/asmv2:os"  
  
      'Change minimum required OS Version.  
      Dim node As XmlNode  
      node = document.SelectSingleNode(baseXPath, namespaceManager)  
      node.Attributes("majorVersion").Value = osVersion.Major.ToString()  
      node.Attributes("minorVersion").Value = osVersion.Minor.ToString()  
      node.Attributes("buildNumber").Value = osVersion.Build.ToString()  
      node.Attributes("servicePackMajor").Value = osVersion.Revision.ToString()  
  
      document.Save(applicationManifestPath)  
   End Sub  
   ```  
  
    此命令采用两个参数。 第一个参数是应用程序清单的路径（即生成进程在其中创建清单的文件夹，通常为 Projectname.publish）。 第二个参数是新的操作系统版本。  
  
5. 在 **“生成”** 菜单上，单击 **“生成解决方案”**。  
  
6. 将 .exe 文件复制到目录，例如 `C:\TEMP\ChangeOSVersionVB.exe`。  
  
   接下来，在生成后事件中调用此命令以更改应用程序清单。  
  
#### <a name="to-invoke-a-post-build-event-to-change-the-application-manifest"></a>调用生成后事件以更改应用程序清单  
  
1. 为要发布的项目创建 Windows 应用程序。 在“文件”菜单上，单击“新建”，然后单击“项目”。  
  
2. 在“新建项目”对话框的“Visual Basic”节点中，依次选择“Windows”、“Windows 应用程序”模板。 将项目命名为 `VBWinApp`。  
  
3. 在“解决方案资源管理器”中选择一个项目，然后在“项目”菜单上单击“属性”。  
  
4. 在项目设计器中，转到“发布”页面，并将“发布位置”设置为 `C:\TEMP\`。  
  
5. 单击“立即发布”以发布项目。  
  
     将生成清单文件，并将其置于 `C:\TEMP\VBWinApp_1_0_0_0\VBWinApp.exe.manifest` 中。 若要查看清单，请右键单击该文件，然后依次单击“打开方式”、“从列表中选择程序”、“记事本”。  
  
     在文件中搜索 `<osVersionInfo>` 元素。 例如，版本可能为：  
  
    ```  
    <os majorVersion="4" minorVersion="10" buildNumber="0" servicePackMajor="0" />  
    ```  
  
6. 在项目设计器中，转到“编译”选项卡，然后单击“生成事件”按钮以打开“生成事件”对话框。  
  
7. 在“生成后事件命令行”框中，输入以下命令：  
  
     `C:\TEMP\ChangeOSVersionVB.exe "$(TargetPath).manifest" 5.1.2600.0`  
  
     生成项目时，此命令会将应用程序清单中的最低操作系统版本更改为 5.1.2600.0。  
  
     `$(TargetPath)` 宏表示正在创建的可执行文件的完整路径。 因此，$(TargetPath). 清单将指定在 bin 目录中创建的应用程序清单。 发布操作会将此清单复制到之前设置的发布位置。  
  
8. 再次发布该项目。 转到“发布”页面，然后单击“立即发布”。  
  
     再次查看该清单。 若要查看清单，请转到发布目录、右键单击该文件，然后依次单击“打开方式”、“从列表中选择程序”、“记事本”。  
  
     版本现在应显示为：  
  
    ```  
    <os majorVersion="5" minorVersion="1" buildNumber="2600" servicePackMajor="0" />  
    ```  
  
## <a name="see-also"></a>请参阅  
 [管理编译属性](https://msdn.microsoft.com/94308881-f10f-4caf-a729-f1028e596a2c)   
 [“项目设计器”->“编译”页 (Visual Basic)](../ide/reference/compile-page-project-designer-visual-basic.md)   
 [“项目设计器”->“发布”页](../ide/reference/publish-page-project-designer.md)   
 [预生成事件/生成后事件命令行对话框](../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)   
 [如何：指定生成事件 (C#)](../ide/how-to-specify-build-events-csharp.md)
