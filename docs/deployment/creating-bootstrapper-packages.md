---
title: 创建引导程序包
ms.date: 05/02/2018
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [Visual Studio], prerequisites
- deploying applications [Visual Studio], custom prerequisites
- prerequisites, custom
- RedistList file
- custom prerequisites
- redistributables list
ms.assetid: ba1a785b-693d-446b-bcae-b88cadee73d1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3dc22b775af048cc3138d6930a835a00c9d97b2a
ms.sourcegitcommit: 9cfd3ef6c65f671a26322320818212a1ed5955fe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68533336"
---
# <a name="create-bootstrapper-packages"></a>创建引导程序包
安装程序是可配置为检测并安装可再发行组件（如 Windows Installer (.msi) 文件和可执行程序）的一般安装程序。 安装程序也称为“引导程序”。 它通过一组 XML 清单进行编程，这些清单指定用于管理组件安装的元数据。  ClickOnce 的 "**必备**组件" 对话框中显示的每个可再发行组件 (即必备组件) 都是一个引导程序包。 一个引导程序包是一组目录和文件，其中包含用于说明系统必备组件的安装方式的清单文件。

引导程序首先检测是否已安装所有系统必备组件。 如果未安装系统必备组件，引导程序将首先显示相关许可协议。 接着，在最终用户接受许可协议后，将开始安装相应的系统必备组件。 否则，如果检测到所有的系统必备组件，引导程序将直接启动应用程序的安装程序。

## <a name="create-custom-bootstrapper-packages"></a>创建自定义引导程序包
您可以使用 Visual Studio 中的 XML 编辑器生成引导程序清单。 若要查看创建引导程序包的示例, 请参阅[演练:使用隐私提示](../deployment/walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt.md)创建自定义引导程序。

若要创建引导程序包, 必须创建产品清单, 并为组件的每个本地化版本创建包清单。

* Product 清单*product .xml*包含包的任何非特定语言的元数据。 它包含可再发行组件的所有本地化版本通用的元数据。  若要创建此文件, [请参阅如何:创建产品清单](../deployment/how-to-create-a-product-manifest.md)。

* 包清单 ( *package*) 包含特定于语言的元数据;它通常包含本地化的错误消息。 必须至少为组件的每个本地化版本提供一个程序包清单。 若要创建此文件, [请参阅如何:创建包清单](../deployment/how-to-create-a-package-manifest.md)。

在创建这两个文件之后，请将产品清单文件放置在一个依据自定义引导程序命名的文件夹中。 程序包清单文件将放置到一个依据区域设置命名的文件夹中。 例如，如果程序包清单文件针对的是英语版的再发行程序，请将该文件放置在一个名为 en 的文件夹中。 对于每个区域设置（如 ja 代表日语，de 代表德语）重复此过程。 最终的自定义引导程序包的文件夹结构将如下所示。

```
CustomBootstrapperPackage
  product.xml
  CustomBootstrapper.msi
  de
    eula.rtf
    package.xml
  en
    eula.rtf
    package.xml
  ja
    eula.rtf
    package.xml
```

接下来, 将可再发行文件复制到引导程序文件夹位置。 有关详细信息，请参阅[如何：创建已本地化的引导程序包](../deployment/how-to-create-a-localized-bootstrapper-package.md)。

```
*\Program Files (x86)\Microsoft SDKs\ClickOnce Bootstrapper*
```

或者, 对于较旧版本的 Visual Studio

```
*\Program Files\Microsoft Visual Studio 14.0\SDK\Bootstrapper\Packages*
```

或

```
*\Program Files (x86)\Microsoft Visual Studio 14.0\SDK\Bootstrapper\Packages*
```

还可以从以下注册表项中的**路径**值找到引导程序文件夹位置:

```
*HKLM\Software\Microsoft\GenericBootstrapper*
```

在 64 位系统上，请使用以下注册表项：

```
*HKLM\Software\Wow6432Node\Microsoft\GenericBootstrapper*
```

每个可再发行组件均位于程序包目录下它们自己的子文件夹中。 产品清单和可再发行文件必须放入此子文件夹中。 组件的本地化版本和包清单必须放入按照区域性名称命名的子文件夹中。

在将这些文件复制到引导程序文件夹中之后，相应的引导程序包将自动出现在 Visual Studio 的“系统必备”对话框中。 如果自定义引导程序包未显示，请关闭并重新打开“系统必备”对话框。 有关详细信息，请参阅 [“系统必备”对话框](../ide/reference/prerequisites-dialog-box.md)。

下表显示由引导程序自动填充的属性。

|Property|描述|
|--------------|-----------------|
|ApplicationName|应用程序的名称。|
|ProcessorArchitecture|可执行文件的目标平台的处理器和每字位数。 包括以下值：<br /><br /> -   Intel<br />-   IA64<br />-   AMD64|
|[Version9x](/windows/desktop/Msi/version9x)|Microsoft Windows 95、Windows 98 或 Windows ME 操作系统的版本号。 版本的语法是 Major.Minor.ServicePack。|
|[VersionNT](/windows/desktop/Msi/versionnt)|Windows NT、Windows 2000、Windows XP、Windows Vista、Windows Server 2008 或 Windows 7 操作系统的版本号。 版本的语法是 Major.Minor.ServicePack。|
|[VersionMSI](/windows/desktop/Msi/versionmsi)|要在安装过程中运行的 Windows Installer 程序集 (msi) 的版本。|
|[AdminUser](/windows/desktop/Msi/adminuser)|如果用户具有管理员特权，则设置此属性。 值为 true 或 false。|
|InstallMode|安装模式指示需要安装组件的位置。 包括以下值：<br /><br /> -   HomeSite - 从供应商的网站安装系统必备组件。<br />-   SpecificSite - 从选定的位置安装系统必备组件。<br />-   SameSite - 从与应用程序相同的位置安装系统必备组件。|

## <a name="separate-redistributables-from-application-installations"></a>独立于应用程序安装的可再发行组件
你可以阻止在安装项目中部署可再发行文件。 为此，请在 .NET Framework 目录的 RedistList 文件夹中创建一个可再发行文件列表：

`%ProgramFiles%\Microsoft.NET\RedistList`

可再发行组件列表是一个 XML 文件, 您应该使用以下格式命名该文件:*公司名称 >。\< \<组件名称 >。RedistList*。 举例来说，如果组件名为 DataWidgets 且由 Acme 开发，则使用 Acme.DataWidgets.RedistList.xml。 可再发行文件列表的内容的示例可能像下面这样：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<FileList Redist="Acme.DataWidgets" >
<File AssemblyName="Acme.DataGrid" Version="1.0.0.0" PublicKeyToken="b03f5f7f11d50a3a" Culture="neutral" ProcessorArchitecture="MSIL" InGAC="true" />
</FileList>
```

## <a name="see-also"></a>请参阅
- [如何：使用 ClickOnce 应用程序安装必备组件](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)
- [“系统必备”对话框](../ide/reference/prerequisites-dialog-box.md)
- [产品和包架构引用](../deployment/product-and-package-schema-reference.md)
- [使用 Visual Studio 2005 引导程序来开始安装](http://go.microsoft.com/fwlink/?LinkId=107537)
