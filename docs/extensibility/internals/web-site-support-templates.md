---
title: 网站支持模板 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- we site projects, templates
ms.assetid: 37173c97-486b-4b3c-8ed3-cf5890c4de23
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8e9229a2614d2d797a5a2159df5b18a92850edbd
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323280"
---
# <a name="web-site-support-templates"></a>网站支持模板
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 网站项目和项模板提供加速开发过程无需从头开始创建新网站项目和项的可重用和可自定义网站项目和项存根。 有关详细信息[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]模板，请参阅[创建项目和项模板](../../ide/creating-project-and-item-templates.md)。

## <a name="project-template-folder"></a>项目模板文件夹
 Web 项目模板通常安装在 [*Visual Studio 安装路径*] \Common7\IDE\ProjectTemplates\Web\\，每个同名 web 编程语言的子文件夹中。

## <a name="project-file"></a>项目文件
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成的开发环境 (IDE) 作为一种方法将模板映射到正确的项目类型需要项目文件扩展名。 Web 项目没有项目文件，因为注册 dummy 项目文件扩展名.webproj 将模板映射到项目类型。

 （可选） 的语言名称字符串可以添加到模板中，若要启用 Web 项目系统中设置语言默认**添加新项**对话框中的项基于该模板。 字符串必须是该文件的第一行。 它必须匹配下 AddItemLanguageName 中 IntelliSense 引擎注册，注册的名称和项目 Subtype(VsTemplate) 下注册的名称。 有关详细信息，请参阅[网站支持属性](../../extensibility/internals/web-site-support-attributes.md)。

 如果字符串不存在，Web 项目系统会尝试确定基于页面的项目模板添加到 Web 项目的语言属性和文件扩展的默认语言。

## <a name="project-templates"></a>项目模板
 使用网站项目模板来构建新网站以响应**新的 Web 站点**命令**文件**菜单。 目前支持三个网站项目类型：

- 空网站项目

- 网站项目

- Web 服务项目

### <a name="empty-web-site-projects"></a>空网站项目
 这些文件创建新的空网站以响应**空网站**命令，选择后，会出现**文件** > **新的 Web 站点**:

- EmptyWeb.vstemplate

     引导用户创建新的空网站模板文件。

- EmptyWeb.webproj

     此文件是项目模板系统的项目。 它满足 EmptyWeb.vstemplate 文件中的项目文件引用。

### <a name="web-site-projects"></a>网站项目
 这些文件创建新网站以响应**ASP.NET Web 站点**命令，选择后，会出现**文件** > **新的 Web 站点**:

- Default.aspx

     新的 Web 站点默认主页。 Language 特性指定源代码语言，并 CodeFile 特性指定包含与此页关联的代码隐藏代码的依赖文件。

- Default.aspx。*扩展*

     包含默认主页上的代码隐藏代码的依赖文件。 代码隐藏语言决定*扩展*此文件。

- web.config

     根 web.site 配置文件。

- WebApplication.vstemplate

     确定网站解决方案的内容并强制 App_Data 文件夹创建的模板文件。

- WebApplication.webproj

     此文件是项目模板系统的项目。 它满足 WebApplication.vstemplate 文件中的项目文件引用。

### <a name="web-service-projects"></a>Web 服务项目
 这些文件创建新网站以响应**ASP.NET Web 服务**命令，选择后，会出现**文件** > **新的 Web 站点**:

- Service.asmx

     新的 Web 服务的 HTML 页。 语言特性指定源代码语言和代码隐藏特性指定包含与此服务关联的代码隐藏代码的依赖文件。

- 服务。 *extension*

     实现服务类的依赖文件。 代码隐藏语言决定*扩展*此文件。

- web.config

- 根 web.site 配置文件。

- WebService.vstemplate

     确定网站解决方案的内容并强制 App_Data 和 App_Code 文件夹创建的模板文件。 该服务。*扩展*文件复制到 App_Code 文件夹。

- WebService.webproj

     此文件是项目模板系统的项目。 它满足 WebService.vstemplate 文件中的项目文件引用。

## <a name="project-item-template-folder"></a>项目项模板文件夹
 Web 项目项模板通常安装在 [*Visual Studio 安装路径*] \Common7\IDE\ItemTemplates\Web\\，每个命名其 web 编程语言的子文件夹中。

## <a name="project-item-templates"></a>项目项模板
 网站项目项模板用于将新的 Web 页面添加到响应中的 Web 站点**添加现有项**命令。 目前支持这些类型的网页：

- 新的类

- 新的 HTML 页面

- 新 Web 窗体

- 新的主页面

### <a name="new-class"></a>新的类
 此模板创建新的源文件的空类定义以响应**添加新的类**命令。

- 类。 *extension*

     实现了空的类的源文件。 代码隐藏语言决定*扩展*此文件。

- Class.vstemplate

     模板文件，创建的源文件，并确定其内容。

### <a name="new-html-page"></a>新的 HTML 页面
 此模板创建新的 Web 页以响应**添加新的 HTML 页面**命令。

- HTMLPage.htm

     Web 页面的起始内容。 此 Web 页面通常具有任何关联的代码隐藏依赖文件。 若要创建智能页关联的代码隐藏文件，请改为使用 Web 窗体模板。

- HTMLPage.vstemplate

     创建 Web 页并确定其内容的模板文件。

### <a name="new-webform"></a>新 web 窗体
 此模板创建新的智能网页以响应**添加新 Web 窗体**命令。

 若要创建依赖的代码隐藏源文件，请选择**将代码放在单独的文件**。 否则，单个网页将创建一个带有空的脚本块，但不\<%page%> 指令来挂接依赖文件。

 若要创建所选的母版页的内容页，选择**选择母版页**。

- WebForm.aspx

     Web 页面的起始内容。 此 Web 页面具有任何关联的代码隐藏依赖文件。

- WebForm_cb.aspx

     Web 页面的起始内容。 此 Web 页面有一个关联的代码隐藏依赖文件。

- 代码隐藏文件。 *extension*

     实现 web 窗体类的依赖文件。 代码隐藏语言决定*扩展*此文件。

- ContentPage.aspx

     作为内容页面的网页的起始内容。 此 Web 页面具有任何关联的代码隐藏依赖文件。

- ContentPage_cb.aspx

     作为内容页面的网页的起始内容。 此 Web 页面有一个关联的代码隐藏依赖文件。

- WebForm.vstemplate

     确定新的 web 页面和其依赖的文件的内容模板文件。

### <a name="new-master-page"></a>新的母版页
 此模板创建新的主页面，以响应**添加新的主页面**命令。

 若要创建依赖的代码隐藏源文件，请选择**将代码放在单独的文件**。 否则单个网页将创建一个带有空的脚本块，但不\<%page%> 指令来挂接依赖文件。

- MasterPage.master

     母版页的起始内容。 此母版页具有任何关联的代码隐藏依赖文件。

- MasterPage_cb.master

     母版页的起始内容。 此母版页有一个关联的代码隐藏依赖文件。

- 代码隐藏文件。*扩展*

     实现主页面类中的依赖文件。 代码隐藏语言决定*扩展*此文件。

- MasterPage.vstemplate

     确定新的主页面和其依赖的文件的内容模板文件。

## <a name="see-also"></a>请参阅
- [网站支持](../../extensibility/internals/web-site-support.md)