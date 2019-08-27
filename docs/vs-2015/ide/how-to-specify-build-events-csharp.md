---
title: 如何：指定生成事件 (C#) |Microsoft Docs
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
ms.assetid: b4ce1ad9-5215-4b6f-b6a2-798b249aa335
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f77a6b9b655cc7dfbf0639a81d7d350b904ce82a
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435229"
---
# <a name="how-to-specify-build-events-c"></a>如何：指定生成事件 (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用生成事件，可以指定生成开始之前或生成完成之后运行的命令。 只有当生成成功到达生成过程中的这些时间点时，才执行生成事件。  
  
 项目生成时，预先生成事件将添加到名为 PreBuildEvent.bat 的文件，而后期生成事件将添加到名为 PostBuildEvent.bat 的文件。 若要确保错误检查，请向生成步骤中添加自己的错误检查命令。  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="how-to-specify-pre-build-and-post-build-events"></a>如何指定预生成事件和生成后事件  
  
#### <a name="to-specify-a-build-event"></a>指定生成事件  
  
1. 在“解决方案资源管理器”中，选择要为其指定生成事件的项目。  
  
2. 在“项目”菜单上，单击“属性”。  
  
3. 选择“生成事件”选项卡。  
  
4. 在“预先生成事件命令行”框中指定生成事件的语法。  
  
    > [!NOTE]
    > 如果项目是最新的且没有触发任何生成，则不会运行预生成事件。  
  
5. 在“后期生成事件命令行”框中指定生成事件的语法。  
  
    > [!NOTE]
    > 在运行 .bat 文件的所有生成后命令之前添加 `call` 语句。 例如，`call C:\MyFile.bat` 或 `call C:\MyFile.bat call C:\MyFile2.bat`。  
  
6. 在“运行后期生成事件”框中，指定运行后期生成事件的条件。  
  
    > [!NOTE]
    > 若要添加长语法，或从[预先生成事件/后期生成事件命令行对话框](../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)中选择任何生成宏，请单击省略号按钮 (…) 以显示编辑框。  
  
     生成事件语法可以包含命令提示符处或 .bat 文件中有效的任何命令。 批处理文件名的前面应带有 `call`，以确保执行后面的所有命令。  
  
     注意：如果预先生成事件或后期生成事件不能成功完成，可以通过使事件操作退出来终止生成，并显示指示操作成功的代码零 (0) 以外的其他代码。  
  
## <a name="example-how-to-change-manifest-information-by-using-a-post-build-event"></a>示例:如何通过使用生成后事件更改清单信息  
 下面的过程说明如何使用从后期生成事件（项目目录中的 .exe.manifest 文件）中调用的 .exe 命令设置应用程序清单中的操作系统最低版本。 最低的操作系统版本是由四个部分组成的数字组合，例如 4.10.0.0。 为此，该命令将更改清单的 `<dependentOS>` 部分：  
  
```  
<dependentOS>  
   <osVersionInfo>  
      <os majorVersion="4" minorVersion="10" buildNumber="0" servicePackMajor="0" />  
   </osVersionInfo>  
</dependentOS>  
```  
  
#### <a name="to-create-an-exe-command-to-change-the-application-manifest"></a>创建 .exe 命令以更改应用程序清单  
  
1. 为命令创建控制台应用程序。 在“文件”菜单中，指向“新建”，然后单击“项目”。  
  
2. 在“新建项目”对话框中，展开“Visual C#”，单击“Windows”，然后单击“控制台应用程序”模板。 将项目命名为 `ChangeOSVersionCS`。  
  
3. 在 Program.cs 中，将以下行添加到文件顶部的其他 `using` 语句：  
  
   ```  
   using System.Xml;  
   ```  
  
4. 在 `ChangeOSVersionCS` 命名空间中，将 `Program` 类实现替换为以下代码：  
  
   ```  
   class Program  
   {  
      /// <summary>  
      /// This function will set the minimum operating system version for a ClickOnce application.  
      /// </summary>  
      /// <param name="args">  
      /// Command Line Arguments:  
      /// 0 - Path to application manifest (.exe.manifest).  
      /// 1 - Version of OS  
      ///</param>  
      static void Main(string[] args)  
      {  
         string applicationManifestPath = args[0];  
         Console.WriteLine("Application Manifest Path: " + applicationManifestPath);  
  
         // Get version name.  
         Version osVersion = null;  
         if (args.Length >=2 ){  
            osVersion = new Version(args[1]);  
         }else{  
            throw new ArgumentException("OS Version not specified.");  
         }  
         Console.WriteLine("Desired OS Version: " + osVersion.ToString());  
  
         XmlDocument document;  
         XmlNamespaceManager namespaceManager;  
         namespaceManager = new XmlNamespaceManager(new NameTable());  
         namespaceManager.AddNamespace("asmv1", "urn:schemas-microsoft-com:asm.v1");  
         namespaceManager.AddNamespace("asmv2", "urn:schemas-microsoft-com:asm.v2");  
  
         document = new XmlDocument();  
         document.Load(applicationManifestPath);  
  
         string baseXPath;  
         baseXPath = "/asmv1:assembly/asmv2:dependency/asmv2:dependentOS/asmv2:osVersionInfo/asmv2:os";  
  
         // Change minimum required operating system version.  
         XmlNode node;  
         node = document.SelectSingleNode(baseXPath, namespaceManager);  
         node.Attributes["majorVersion"].Value = osVersion.Major.ToString();  
         node.Attributes["minorVersion"].Value = osVersion.Minor.ToString();  
         node.Attributes["buildNumber"].Value = osVersion.Build.ToString();  
         node.Attributes["servicePackMajor"].Value = osVersion.Revision.ToString();  
  
         document.Save(applicationManifestPath);  
      }  
   }  
   ```  
  
    此命令采用两个参数：应用程序清单的路径（即生成进程在其中创建清单的文件夹，通常为 Projectname.publish），以及新的操作系统版本。  
  
5. 生成项目。 在 **“生成”** 菜单上，单击 **“生成解决方案”**。  
  
6. 将 .exe 文件复制到目录，例如 `C:\TEMP\ChangeOSVersionVB.exe`。  
  
   然后，在后期生成事件中调用此命令以修改应用程序清单。  
  
#### <a name="to-invoke-a-post-build-event-to-modify-the-application-manifest"></a>调用后期生成事件以修改应用程序清单  
  
1. 为要发布的项目创建 Windows 应用程序。 在“文件”菜单中，指向“新建”，然后单击“项目”。  
  
2. 在“新建项目”对话框中，展开“Visual C#”，单击“Windows”，然后单击“Windows 窗体应用程序”模板。 将项目命名为 `CSWinApp`。  
  
3. 在“解决方案资源管理器”中选择一个项目，然后在“项目”菜单上单击“属性”。  
  
4. 在项目设计器中，转到“发布”页，并将“发布位置”设置为 `C:\TEMP\`。  
  
5. 单击“立即发布”以发布项目。  
  
     将生成清单文件，并将其置于 `C:\TEMP\CSWinApp_1_0_0_0\CSWinApp.exe.manifest` 中。 若要查看该清单，请右键单击该文件，单击“打开方式”，选择“从列表中选择程序”，然后单击“记事本”。  
  
     在文件中搜索 `<osVersionInfo>` 元素。 例如，版本可能为：  
  
    ```  
    <os majorVersion="4" minorVersion="10" buildNumber="0" servicePackMajor="0" />  
    ```  
  
6. 在项目设计器中，单击“生成事件”选项卡，然后单击“编辑后期生成”按钮。  
  
7. 在“后期生成事件命令行”框中，键入以下命令：  
  
     `C:\TEMP\ChangeOSVersionCS.exe "$(TargetPath).manifest" 5.1.2600.0`  
  
     生成项目时，此命令会将应用程序清单中的最低操作系统版本更改为 5.1.2600.0。  
  
     由于 `$(TargetPath)` 宏表示所创建的可执行文件的完整路径，因此 `$(TargetPath)`.manifest 将指定在 bin 目录中创建的应用程序清单。 发布操作会将此清单复制到之前设置的发布位置。  
  
8. 再次发布该项目。 转到“发布”页面，然后单击“立即发布”。  
  
     再次查看该清单。 若要查看清单，请打开发布目录，右键单击该文件，单击“打开方式”，选择“从列表中选择程序”，然后单击“记事本”。  
  
     版本现在应显示为：  
  
    ```  
    <os majorVersion="5" minorVersion="1" buildNumber="2600" servicePackMajor="0" />  
    ```  
  
## <a name="see-also"></a>请参阅  
 [“项目设计器”->“生成事件”页 (C#)](../ide/reference/build-events-page-project-designer-csharp.md)   
 [预生成事件/生成后事件命令行对话框](../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)   
 [如何：指定生成事件 (Visual Basic)](../ide/how-to-specify-build-events-visual-basic.md)   
 [编译和生成](../ide/compiling-and-building-in-visual-studio.md)
