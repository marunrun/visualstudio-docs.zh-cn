---
title: 部署自定义起始页 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- package start page
- deploy start page
ms.assetid: 4a7eb360-de83-41d5-be53-3cfb160d19f9
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1cdd172c2960024da8b12735764161d36498c4e2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68162094"
---
# <a name="deploying-custom-start-pages"></a>部署自定义起始页
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用 VSIX 部署或将文件复制到目标计算机上的正确位置，你可以部署自定义起始页。  
  
## <a name="vsix-deployment-by-using-the-start-page-project-template"></a>使用起始页项目模板的 VSIX 部署  
 当使用起始页项目模板，创建一个起始页，然后生成项目时，Visual Studio 创建可以分发的.vsix 文件。 打包.vsix 文件中的启动页提供了部署，具体取决于您的目标受众的以下选项：  
  
- 在网络共享上或在公共网站上，可以将.vsix 文件。 在有人打开文件时，会自动安装启动页。  
  
- 可以上传到.vsix 文件[Visual Studio Marketplace](https://marketplace.visualstudio.com/) Web 站点，以便用户可以使用来安装它**扩展管理器**。  
  
  起始页项目模板创建一份默认 Visual Studio 起始页，以便您可以修改副本，并保留原始。  
  
  你可以通过使用获取起始页项目模板**扩展管理器**或通过从 Web 站点下载它。  
  
## <a name="vsix-deployment-without-using-the-start-page-project-template"></a>而无需使用起始页项目模板的 VSIX 部署  
 成功的 VSIX 部署需要在 VSIX 注册过程和识别的文件夹中安装的扩展**扩展管理器**。 由于起始页项目模板已指定正确的文件夹中，我们建议要打包为 VSIX 部署扩展时使用它。 但是，如果你不能在其中使用该模板的用例，您可以创建 VSIX 部署而无需使用它。  
  
 若要创建 VSIX 部署而无需使用起始页项目模板，首先创建这两种方式之一中的启动页的.vsix 文件：  
  
- 通过将自定义起始页文件添加到一个空的 VSIX 项目。 有关详细信息，请参阅[VSIX 项目模板](../extensibility/vsix-project-template.md)。  
  
- 通过手动创建.vsix 文件。 有关详细信息，请参阅[如何：手动将扩展打包 （VSIX 部署）](../misc/how-to-manually-package-an-extension-vsix-deployment.md)。  
  
  Visual studio 能够识别启动页上，`Content Element`必须包含的 VSIX 清单`CustomExtension Element`具有`Type`属性设置为`"StartPage"`。 使用 VSIX 部署安装起始页扩展将出现在**自定义起始页**上列出**启动**选项页中以 **[安装的扩展]** *扩展插件名称*。  
  
  如果起始页包中包含的程序集，必须添加绑定路径注册，以便它们可用于 Visual Studio 将启动。 若要执行此操作，请确保您的包，包括具有以下信息的.pkgdef 文件。  
  
```  
[$RootKey$\BindingPaths\{Insert a new GUID here}]  
"$PackageFolder$"=""  
```  
  
### <a name="vsix-deployment-for-all-users"></a>所有用户的的 VSIX 部署  
 默认情况下，在 VSIX 包中部署的扩展插件安装仅为当前用户。 您可以通过创建的所有用户部署的目标计算机的所有用户都使起始页安装。  
  
##### <a name="to-create-an-all-users-deployment"></a>若要创建的所有用户部署  
  
1. 在代码视图中打开 extension.vsixmanifest 文件。  
  
2. 在中`Identifier`vsix 清单中，元素添加`AllUsers`元素的值为`true`。  
  
    ```  
    <AllUsers>true</AllUsers>  
    ```  
  
     这将导致 vsix 安装程序提示输入管理员权限，然后将文件安装到 \Common7\IDE\Extensions。  
  
3. 打开.pkgdef 文件。  
  
4. 修改.pkgdef 设置默认起始页在 HKLM 下的添加以下内容，其中*MyStartPage.xaml*是包含你的起始页.xaml 文件的名称。  
  
     [$RootKey$\StartPage\Default]  
  
     "Uri"="$PackageFolder$\\*MyStartPage.xaml*"  
  
     这将告知 Visual 花了在新的起始页位置中进行查找。  
  
## <a name="file-copy-deployment"></a>文件复制部署  
 不需要创建要部署自定义起始页的.vsix 文件。 相反，您可以直接在用户的 \StartPages\ 文件夹复制标记和支持文件。 **自定义起始页**上列出**启动**选项页列出了该文件夹，以及该路径中的每个.xaml 文件 — 例如，%USERPROFILE%\My Documents\Visual Studio *版本*\StartPages\\*文件名*.xaml。 如果你的起始页包含对专用程序集的引用，必须将它们复制并将其粘贴在 \PrivateAssemblies\ 文件夹中。  
  
 若要分发而无需打包创建起始页中的.vsix 文件，建议使用基本的文件的复制策略，例如，批处理脚本或任何其他部署技术，它允许您将文件放入所需的目录。  
  
#### <a name="to-manually-install-a-custom-start-page"></a>若要手动安装自定义起始页  
  
1. 复制的.xaml 文件，包含起始页标记，以及任何支持文件以外的程序集，并将其粘贴在用户的 \StartPages\ 文件夹中。  
  
2. 如果启动页需要程序集，将它们复制并粘贴在...\\ *Visual Studio 安装文件夹*\Common7\IDE\PrivateAssemblies\\。  
  
3. 在中**自定义起始页**上列出**启动**选项页上，选择新的起始页。 有关详细信息，请参阅[自定义起始页](../ide/customizing-the-start-page-for-visual-studio.md)。  
  
## <a name="see-also"></a>请参阅  
 [自定义起始页](../ide/customizing-the-start-page-for-visual-studio.md)   
 [将用户控件添加到起始页](../extensibility/adding-user-control-to-the-start-page.md)
