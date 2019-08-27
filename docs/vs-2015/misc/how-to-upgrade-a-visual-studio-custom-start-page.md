---
title: 如何：升级自定义起始页 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
ms.assetid: 78342ce6-36c8-485b-a5f6-760e7a420a26
caps.latest.revision: 8
manager: jillfra
ms.openlocfilehash: abe1013d37db43114f3970f12b1a0d1f08b07a4e
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63446462"
---
# <a name="how-to-upgrade-a-visual-studio-custom-start-page"></a>如何：升级 Visual Studio 自定义起始页
你可以通过下列步骤将 Visual Studio 2010 或 Visual Studio 2012 的自定义起始页升级到 Visual Studio 2015。

> [!WARNING]
> 在此过程中升级的自定义起始页是用 Visual Studio 库上的 [自定义起始页](http://visualstudiogallery.msdn.microsoft.com/f655a5dc-1a2d-4eca-b774-76c352c03b87) 模板创建的。 你的起始页可能具有需要升级的其他功能。

### <a name="to-upgrade-a-custom-start-page-to-visual-studio-2015"></a>将自定义起始页升级到 Visual Studio 2015

1. 请确保已安装了 Visual Studio 2015 和 Visual Studio 2015 SDK。 你可以从 [Microsoft Visual Studio 2013 SDK](https://my.visualstudio.com/Downloads?pid=1436)下载 VSSDK。

2. 打开你的自定义模板项目。 你将看到一条消息，提示你将要升级该项目。 单击“确定”  并等待升级完成。

3. 在起始页项目和控件项目的项目属性中，请确保目标框架版本至少为 .NET Framework 4.5。

4. 在起始页项目的项目属性的调试类别中，设置指向 devenv.exe 的 Visual Studio 2015 版本的路径。

5. 在这两个项目的项目引用中，删除对 Microsoft.VisualStudio.Shell.11.0 的引用并添加对 Microsoft.VisualStudio.Shell.14.0 的引用。

6. 使用 XML 编辑器打开 StartPage.xaml 并进行以下更改：

    1. 更新命名空间。 将以下行：

        ```

        xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.11.0"
         xmlns:vsfxim="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.Immutable.11.0"
        xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.11.0"
        ```

         更改为以下内容：

        ```

        xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.142.0"
         xmlns:vsfxim="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.Immutable.14.0"
        xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
        ```

7. 打开 MyControl.xaml，并将命名空间引用从 `xmlns:vs="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.11.0"` 更改为 `xmlns:vs="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"` 。