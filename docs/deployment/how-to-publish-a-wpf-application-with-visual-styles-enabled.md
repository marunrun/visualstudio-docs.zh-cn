---
title: 如何-发布启用了视觉样式的 WPF 应用程序 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 73b22b02-fc75-42aa-82d3-51fdcaf8e5c8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 21c94cc7ab97070b138cbae108c617094faf09b5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85382206"
---
# <a name="how-to-publish-a-wpf-application-with-visual-styles-enabled"></a>如何：发布启用了视觉样式的 WPF 应用程序

视觉样式使公共控件的外观可以根据用户选择的主题进行更改。 默认情况下，不会为 Windows Presentation Foundation (WPF) 应用程序启用视觉样式，因此你必须手动启用它们。 但是，为 WPF 应用程序启用视觉样式并发布解决方案会导致错误。 本主题介绍如何解决此错误以及用于发布启用了视觉样式的 WPF 应用程序的过程。 有关视觉样式的详细信息，请参阅 [视觉样式概述](/windows/desktop/Controls/visual-styles-overview)。 有关错误消息的详细信息，请参阅 [排查 ClickOnce 部署中的特定错误](../deployment/troubleshooting-specific-errors-in-clickonce-deployments.md)。

 若要解决此错误并发布解决方案，您必须执行以下任务：

- [在未启用视觉样式的情况下发布解决方案](#publish-the-solution-without-visual-styles-enabled)。

- [创建清单文件](#create-a-manifest-file)。

- 将[清单文件嵌入到已发布解决方案的可执行文件中](#embed-the-manifest-file-into-the-executable-file-of-the-published-solution)。

- [对应用程序和部署清单进行签名](#sign-the-application-and-deployment-manifests)。

  然后，你可以将已发布的文件移动到你希望最终用户安装该应用程序的位置。

## <a name="publish-the-solution-without-visual-styles-enabled"></a>在未启用视觉样式的情况下发布解决方案

1. 确保你的项目未启用视觉样式。 首先，检查项目的清单文件中是否有以下 XML。 然后，如果 XML 存在，则用注释标记将 XML 括起来。

     默认情况下，不启用视觉样式。

    ```xml
    <dependency>
        <dependentAssembly>
            <assemblyIdentity type="win32" name="Microsoft.Windows.Common-Controls" version="6.0.0.0" processorArchitecture="*" publicKeyToken="6595b64144ccf1df" language="*" />
        </dependentAssembly>
    </dependency>
    ```

     下面的过程演示如何打开与项目关联的清单文件。

    **在 Visual Basic 项目中打开清单文件**

    1. 在菜单栏上，依次选择 "项目"、"**项目***名称***属性**"，其中，*项目*名称是您的 WPF 项目的名称。

         显示 WPF 项目的属性页。

    2. 在 " **应用程序** " 选项卡上，选择 " **查看 Windows 设置**"。

         App.config 文件将在 **代码编辑器**中打开。

    **在 c # 项目中打开清单文件**

    1. 在菜单栏上，依次选择 "项目"、"**项目***名称***属性**"，其中，*项目*名称是您的 WPF 项目的名称。

         显示 WPF 项目的属性页。

    2. 在 " **应用程序** " 选项卡上，记下 "清单" 字段中显示的名称。 这是与你的项目关联的清单的名称。

        > [!NOTE]
        > 如果 "清单" 字段中显示 **带有默认设置的嵌入清单** ，或 " **创建不带清单的应用程序** "，则不会启用视觉样式。 如果清单文件的名称出现在清单字段中，则继续执行此过程中的下一步。

    3. 在“解决方案资源管理器”中，选择“显示所有文件”********。

         此按钮显示所有项目项，包括已排除的项目项和通常隐藏的项目项。 清单文件显示为项目项。

2. 生成并发布解决方案。 有关如何发布解决方案的详细信息，请参阅 [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

## <a name="create-a-manifest-file"></a>创建清单文件

1. 将以下 XML 粘贴到记事本文件中。

     此 XML 介绍包含支持视觉样式的控件的程序集。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <asmv1:assembly manifestVersion="1.0"
        xmlns="urn:schemas-microsoft-com:asm.v1"
        xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"
        xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <dependency>
            <dependentAssembly>
                <assemblyIdentity type="win32" name="Microsoft.Windows.Common-Controls" version="6.0.0.0" processorArchitecture="*" publicKeyToken="6595b64144ccf1df" language="*" />
            </dependentAssembly>
        </dependency>
    </asmv1:assembly>
    ```

2. 在记事本中，单击 " **文件**"，然后单击 " **另存为**"。

3. 在 " **另存为** " 对话框的 " **保存类型** " 下拉列表中，选择 " **所有文件**"。

4. 在 " **文件名" 框中** ，将文件命名为，并将 *.manifest* 附加到文件名的末尾。 例如： *themes*。

5. 选择 " **浏览文件夹** " 按钮，选择任意文件夹，然后单击 " **保存**"。

    > [!NOTE]
    > 其余过程假设此文件的名称为 *themes* ，并将文件保存到计算机上的 *C：\temp* 目录。

## <a name="embed-the-manifest-file-into-the-executable-file-of-the-published-solution"></a>将清单文件嵌入到已发布解决方案的可执行文件中

1. 打开 **Visual Studio 命令提示符**。

    有关如何打开 **Visual Studio 命令提示符**的详细信息，请参阅 [命令](/dotnet/framework/tools/developer-command-prompt-for-vs)提示符。

   > [!NOTE]
   > 其余步骤对您的解决方案进行了以下假设：
   >
   > - 解决方案的名称为 **MyWPFProject**。
   > - 此解决方案位于以下目录中： `%UserProfile%\Documents\Visual Studio 2010\Projects\` 。
   >
   > - 解决方案发布到以下目录： `%UserProfile%\Documents\Visual Studio 2010\Projects\publish` 。
   > - 发布的应用程序文件的最新版本位于以下目录中： `%UserProfile%\Documents\Visual Studio 2010\Projects\publish\Application Files\WPFApp_1_0_0_0`
   >
   > 你不必使用上述名称或目录位置。 上面所述的名称和位置仅用于说明发布解决方案所需的步骤。

2. 在命令提示符下，更改包含已发布应用程序文件的最新版本的目录的路径。 下面的示例演示了此步骤。

   ```cmd
   cd "%UserProfile%\Documents\Visual Studio 2010\Projects\MyWPFProject\publish\Application Files\WPFApp_1_0_0_0"
   ```

3. 在命令提示符下，运行以下命令，将清单文件嵌入到应用程序的可执行文件中。

   ```cmd
   mt -manifest c:\temp\themes.manifest -outputresource:MyWPFApp.exe.deploy
   ```

## <a name="sign-the-application-and-deployment-manifests"></a>对应用程序和部署清单进行签名

1. 在命令提示符下，运行以下命令以从当前目录中的可执行文件中删除 *.deploy* 扩展。

   ```cmd
   ren MyWPFApp.exe.deploy MyWPFApp.exe
   ```

   > [!NOTE]
   > 此示例假定只有一个文件具有 *.deploy* 文件扩展名。 请确保在此目录中重命名具有 *.deploy* 文件扩展名的所有文件。

2. 在命令提示符下，运行以下命令对应用程序清单进行签名。

   ```cmd
   mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx
   ```

   > [!NOTE]
   > 此示例假设你使用项目的 *.pfx* 文件对清单进行签名。 如果不对清单进行签名，则可以省略 `-cf` 本示例中使用的参数。 如果要使用要求密码的证书对清单进行签名，请将选项指定 `-password` (`For example: mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx - password Password`) 。

3. 在命令提示符下，运行以下命令，将 *.deploy* 扩展名添加到在此过程的前一步骤中重命名的文件的名称。

   ```
   ren MyWPFApp.exe MyWPFApp.exe.deploy
   ```

   > [!NOTE]
   > 此示例假定只有一个文件具有 *.deploy* 文件扩展名。 请确保在此目录中重命名以前具有 *.deploy* 文件扩展名的所有文件。

4. 在命令提示符下，运行以下命令对部署清单进行签名。

   ```
   mage -u ..\..\MyWPFApp.application -appm MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx
   ```

   > [!NOTE]
   > 此示例假设你使用项目的 *.pfx* 文件对清单进行签名。 如果不对清单进行签名，则可以省略 `-cf` 本示例中使用的参数。 如果要使用要求密码的证书对清单进行签名，请指定 `-password` 选项，如以下示例中所示： `For example: mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx - password Password` 。

   执行这些步骤后，可以将已发布的文件移动到希望最终用户安装应用程序的位置。 如果你打算经常更新解决方案，则可以将这些命令移动到脚本中，并在每次发布新版本时运行该脚本。

## <a name="see-also"></a>另请参阅

-[ClickOnce 部署中的特定错误的疑难解答](../deployment/troubleshooting-specific-errors-in-clickonce-deployments.md)
- [视觉样式概述](/windows/desktop/Controls/visual-styles-overview)
- [启用视觉样式](/windows/desktop/Controls/cookbook-overview)
- [命令提示](/dotnet/framework/tools/developer-command-prompt-for-vs)
