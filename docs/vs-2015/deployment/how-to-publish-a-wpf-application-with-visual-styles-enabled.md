---
title: 如何：发布启用了视觉样式的 WPF 应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
ms.assetid: 73b22b02-fc75-42aa-82d3-51fdcaf8e5c8
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c3691f782f317667b56f6bf3641c0f4c6a703eda
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697573"
---
# <a name="how-to-publish-a-wpf-application-with-visual-styles-enabled"></a>如何：发布启用了视觉样式的 WPF 应用程序

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

视觉样式可启用常用控件以基于用户选择的主题更改的外观。 默认情况下，视觉样式未启用的 Windows Presentation Foundation (WPF) 应用程序中，因此你必须手动启用它们。 但是，启用视觉样式的 WPF 应用程序，然后发布该解决方案将导致错误。 本主题介绍如何解决此错误，发布启用了视觉样式的 WPF 应用程序的过程。 视觉样式的详细信息，请参阅[视觉样式概览](https://msdn.microsoft.com/5b5d7bb6-684f-478d-bf5f-b8d18bbcff2e)。 有关错误消息的详细信息，请参阅[ClickOnce 部署中的故障排除特定错误](../deployment/troubleshooting-specific-errors-in-clickonce-deployments.md)。

 若要解决此错误并发布解决方案，必须执行以下任务：

- [将解决方案发布不使用视觉样式已启用](#BKMK_publishsolwovs)。

- [创建清单文件](#BKMK_CreateManifest)。

- [将清单文件嵌入到已发布解决方案的可执行文件](#BKMK_embedmanifest)。

- [应用程序和部署清单签名](#BKMK_signappdeplyman)。

  然后，您可以将已发布的文件移动到要从中安装应用程序的最终用户的位置。

## <a name="BKMK_publishsolwovs"></a> 将解决方案发布不使用视觉样式已启用

1. 请确保你的项目不具有视觉样式已启用。 首先，检查你的项目的清单文件的以下 XML。 然后，如果存在 XML，则请将带有注释标记的 XML。

     默认情况下不启用视觉样式。

    ```xml
    <dependency>
        <dependentAssembly>
          <assemblyIdentity
              type="win32"
              name="Microsoft.Windows.Common-Controls"
              version="6.0.0.0"
              processorArchitecture="*"
              publicKeyToken="6595b64144ccf1df"
              language="*" />
        </dependentAssembly>
      </dependency>
    ```

     以下过程介绍如何打开与项目关联的清单文件。

    **若要在 Visual Basic 项目中打开清单文件**

    1. 在菜单栏上依次选择**项目**， _ProjectName_**属性**，其中*ProjectName*是 WPF 项目的名称。

         WPF 项目的属性页会显示。

    2. 上**应用程序**选项卡上，选择**查看 Windows 设置**。

         在中打开 app.manifest 文件**代码编辑器**。

    **若要在 C# 项目中打开清单文件**

    1. 在菜单栏上依次选择**项目**， _ProjectName_**属性**，其中*ProjectName*是 WPF 项目的名称。

         WPF 项目的属性页会显示。

    2. 上**应用程序**选项卡上，记下的清单字段中显示的名称。 这是清单的与你的项目相关联的名称。

        > [!NOTE]
        > 如果**使用默认设置嵌入清单**或**创建应用程序而无需清单**出现在清单的字段中，不启用了可视样式。 如果清单文件的名称出现在清单字段，请继续执行此过程的下一步。

    3. 在中**解决方案资源管理器**，选择**显示所有文件**（)。

         此按钮将显示所有项目项，其中包括已排除，以及通常处于隐藏状态。 清单文件显示为一个项目项。

2. 生成和发布你的解决方案。 有关如何发布解决方案的详细信息，请参阅[如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

## <a name="BKMK_CreateManifest"></a> 创建清单文件

1. 将以下 XML 粘贴到记事本文件。

     此 XML 描述包含支持视觉样式的控件的程序集。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
     <asmv1:assembly manifestVersion="1.0"
         xmlns="urn:schemas-microsoft-com:asm.v1"
         xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"
         xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <dependency>
        <dependentAssembly>
          <assemblyIdentity
            type="win32"
            name="Microsoft.Windows.Common-Controls"
            version="6.0.0.0"
            processorArchitecture="*"
            publicKeyToken="6595b64144ccf1df"
            language="*" />
        </dependentAssembly>
      </dependency>
    </asmv1:assembly>
    ```

2. 在记事本中，单击**文件**，然后单击**另存为**。

3. 在中**另存为**对话框中**另存为类型**下拉列表中，选择**的所有文件**。

4. 在中**文件名**框中，将文件命名并追加 **.manifest**到的文件的名称的末尾。 例如： **themes.manifest**。

5. 选择**浏览文件夹**按钮，选择任何文件夹，然后单击**保存**。

    > [!NOTE]
    > 剩余过程假设此文件的名称是**themes.manifest**和您的计算机上的文件保存到 C:\temp 目录。

## <a name="BKMK_embedmanifest"></a> 将清单文件嵌入到已发布解决方案的可执行文件

1. 打开**Visual Studio 命令提示符**。

    有关如何打开详细信息**Visual Studio 命令提示符**，请参阅[命令提示](https://msdn.microsoft.com/library/94fcf524-9045-4993-bfb2-e2d8bad44219)。

   > [!NOTE]
   > 剩余的步骤使你的解决方案有关的以下假设：
   >
   > - 解决方案的名称是**MyWPFProject**。
   > - 该解决方案位于以下目录中： `%UserProfile%\Documents\Visual Studio 2010\Projects\`。
   >
   > - 该解决方案发布到以下目录： `%UserProfile%\Documents\Visual Studio 2010\Projects\publish`。
   > - 最新版本的发布的应用程序文件位于以下目录中： `%UserProfile%\Documents\Visual Studio 2010\Projects\publish\Application Files\WPFApp_1_0_0_0`
   >
   > 无需使用的名称或上面所述的目录位置。 名称和位置上面所述仅用于说明发布你的解决方案所需的步骤。

2. 在命令提示符下，将更改为包含已发布的应用程序文件的最新版本的目录的路径。 下面的示例演示了此步骤。

   ```
   cd "%UserProfile%\Documents\Visual Studio 2010\Projects\MyWPFProject\publish\Application Files\WPFApp_1_0_0_0"
   ```

3. 在命令提示符下运行以下命令以将清单文件嵌入到应用程序的可执行文件。

   ```
   mt –manifest c:\temp\themes.manifest –outputresource:MyWPFApp.exe.deploy
   ```

## <a name="BKMK_signappdeplyman"></a> 对应用程序和部署清单进行签名

1. 在命令提示符处，运行以下命令以删除`.deploy`从当前目录中的可执行文件的扩展。

   ```
   ren MyWPFApp.exe.deploy MyWPFApp.exe
   ```

   > [!NOTE]
   > 此示例假定只有一个文件具有`.deploy`文件扩展名。 请确保重命名此目录中的所有文件具有`.deploy`文件扩展名。

2. 在命令提示符下运行以下命令，应用程序清单进行签名。

   ```
   mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx
   ```

   > [!NOTE]
   > 此示例假定使用签名清单`.pfx`项目文件。 如果不签名的清单，则可以省略`–cf`此示例中使用的参数。 如果您要签署的证书需要密码的清单，指定`–password`选项 (`For example: mage –u MyWPFApp.exe.manifest –cf ..\..\..\MyWPFApp_TemporaryKey.pfx – password Password`)。

3. 在命令提示符处，运行以下命令来添加`.deploy`扩展到您在此过程的上一步骤中重命名文件的名称。

   ```
   ren MyWPFApp.exe MyWPFApp.exe.deploy
   ```

   > [!NOTE]
   > 此示例假定只有一个文件具有`.deploy`文件扩展名。 请确保重命名以前此目录中的所有文件`.deploy`文件扩展名。

4. 在命令提示符下运行以下命令部署清单进行签名。

   ```
   mage -u ..\..\MyWPFApp.application -appm MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx
   ```

   > [!NOTE]
   > 此示例假定使用签名清单`.pfx`项目文件。 如果不签名的清单，则可以省略`–cf`此示例中使用的参数。 如果您要签署的证书需要密码的清单，指定`–password`选项，如本例所示：`For example: mage –u MyWPFApp.exe.manifest –cf ..\..\..\MyWPFApp_TemporaryKey.pfx – password Password`。

   执行这些步骤后，您可以将已发布的文件移动到要从中安装应用程序的最终用户的位置。 如果你想要经常更新解决方案，可以将这些命令移到一个脚本，并运行该脚本每次发布新版本。

## <a name="see-also"></a>请参阅

[ClickOnce 部署中的特定错误的疑难解答](../deployment/troubleshooting-specific-errors-in-clickonce-deployments.md)
[视觉样式概述](https://msdn.microsoft.com/5b5d7bb6-684f-478d-bf5f-b8d18bbcff2e)
[命令提示](https://msdn.microsoft.com/library/94fcf524-9045-4993-bfb2-e2d8bad44219)
