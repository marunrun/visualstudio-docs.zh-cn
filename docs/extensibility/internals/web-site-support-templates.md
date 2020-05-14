---
title: 网站支持模板 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- we site projects, templates
ms.assetid: 37173c97-486b-4b3c-8ed3-cf5890c4de23
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0e3c139ae6f2f9ec618e6382a1551a9e35eee7ec
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703453"
---
# <a name="web-site-support-templates"></a>网站支持模板
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]网站项目和项目模板提供可重用和可自定义的网站项目和项目存根，通过消除从头开始创建新网站项目和项目的需求来加快开发过程。 有关[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]模板的详细信息，请参阅[创建项目和项目模板](../../ide/creating-project-and-item-templates.md)。

## <a name="project-template-folder"></a>项目模板文件夹
 Web 项目模板通常安装在 [*可视化工作室安装路径*][公共7_IDE_ProjectTemplates]Web\\上，每个模板都位于以 Web 编程语言命名的子文件夹中。

## <a name="project-file"></a>项目文件
 集成[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]开发环境 （IDE） 需要项目文件扩展名作为将模板映射到正确项目类型的一种方式。 由于 Web 项目没有项目文件，因此注册了虚拟项目文件扩展名 .webproj 以将模板映射到项目类型。

 或者，可以将语言名称字符串添加到模板中，以使 Web 项目系统能够根据模板为项目在"**添加新项目"** 对话框中设置语言默认值。 字符串必须是文件的第一行。 它必须与 IntelliSense 引擎注册中在 AddItem语言名称下注册的名称和在项目子类型（VsTemplate）下注册的名称相匹配。 有关详细信息，请参阅[网站支持属性](../../extensibility/internals/web-site-support-attributes.md)。

 如果字符串不存在，Web 项目系统将尝试根据项目模板添加到 Web 项目的页面的语言属性和文件扩展名来确定默认语言。

## <a name="project-templates"></a>项目模板
 网站项目模板用于生成新网站以响应 **"文件**"菜单上**的"新建网站"** 命令。 当前支持三种网站项目类型：

- 空网站项目

- 网站项目

- Web 服务项目

### <a name="empty-web-site-projects"></a>空网站项目
 这些文件创建一个新的空网站，以响应**空网站**命令，该命令在选择 **"文件** > **新网站**"后可用：

- 空Web.vstemplate

     指导创建新空网站的模板文件。

- 空Web.webproj

     此文件是项目模板系统的项目。 它满足 EmptyWeb.vstemplate 文件中的项目文件引用。

### <a name="web-site-projects"></a>网站项目
 这些文件创建一个新的网站，以响应**ASP.NET网站**命令，该命令在选择 **"文件** > **新网站**"后可用：

- Default.aspx

     新网站的默认主页。 语言属性指定代码背后语言，CodeFile 属性指定包含与此页面关联的代码后面的从属文件。

- 默认值.aspx。*扩展*

     包含默认主页的代码后面代码的从属文件。 代码背后语言确定此文件的*扩展名*。

- web.config

     根网站配置文件。

- Web应用程序.vstemplate

     模板文件，用于确定网站解决方案的内容并强制创建App_Data文件夹。

- Web应用程序.webproj

     此文件是项目模板系统的项目。 它满足 WebApplication.vstemplate 文件中的项目文件引用。

### <a name="web-service-projects"></a>Web 服务项目
 这些文件创建一个新的网站，以响应**ASP.NET Web 服务**命令，该命令在选择 **"文件** > **新网站**"后可用：

- 服务.asmx

     新 Web 服务的 HTML 页。 语言属性指定代码背后语言，Code背后属性指定包含与此服务关联的代码后面的从属文件。

- 服务。 *扩展*

     实现服务类的从属文件。 代码背后语言确定此文件的*扩展名*。

- web.config

- 根网站配置文件。

- WebService.vstemplate

     模板文件，用于确定网站解决方案的内容并强制创建App_Data和App_Code文件夹。 服务。*扩展文件*将复制到App_Code文件夹。

- WebService.webproj

     此文件是项目模板系统的项目。 它满足 WebService.vstemplate 文件中的项目文件引用。

## <a name="project-item-template-folder"></a>项目模板文件夹
 Web 项目项模板通常安装在 [*可视化工作室安装路径*] [公共7_IDE_ItemTemplates]Web\\中，每个模板都位于以 Web 编程语言命名的子文件夹中。

## <a name="project-item-templates"></a>项目项目模板
 网站项目项目模板用于向网站添加新网页以响应 **"添加现有项目"** 命令。 当前支持这些类型的网页：

- 新类

- 新的 HTML 页面

- 新 Web 窗体

- 新母版页

### <a name="new-class"></a>新类
 此模板创建一个新的源文件，用于定义一个空类以响应 **"添加新类"** 命令。

- 类。 *扩展*

     实现空类的源文件。 代码背后语言确定此文件的*扩展名*。

- 类.vstemplate

     创建源文件并确定其内容的模板文件。

### <a name="new-html-page"></a>新的 HTML 页面
 此模板创建一个新网页以响应 **"添加新 HTML 页"** 命令。

- HTMLPage.htm

     网页的起始内容。 此网页通常没有关联的代码背后的从属文件。 要使用关联的代码背后文件创建智能页面，请使用 Web 窗体模板。

- HTMLPage.vstemplate

     创建网页并确定其内容的模板文件。

### <a name="new-webform"></a>新 Web 表单
 此模板创建一个新的智能网页以响应 **"添加新 Web 窗体"** 命令。

 要创建源文件背后的从属代码，请选择**将代码放在单独的文件中**。 否则，将创建一个 Web 页，该网页具有空脚本块\<，并且没有 %Page %> 指令来挂接从属文件。

 要为所选母版页创建内容页，请选择 **"选择母版页**"。

- WebForm.aspx

     网页的起始内容。 此网页没有关联的代码背后的从属文件。

- WebForm_cb.aspx

     网页的起始内容。 此网页具有关联的代码背后相关文件。

- 代码后面。 *扩展*

     实现 Webform 类的从属文件。 代码背后语言确定此文件的*扩展名*。

- 内容页.aspx

     网页的起始内容作为内容页。 此网页没有关联的代码背后的从属文件。

- ContentPage_cb.aspx

     网页的起始内容作为内容页。 此网页具有关联的代码背后相关文件。

- WebForm.vstemplate

     确定新网页及其从属文件（如果有）内容的模板文件。

### <a name="new-master-page"></a>新母版页
 此模板创建一个新的母版页以响应 **"添加新母版页"** 命令。

 要创建源文件背后的从属代码，请选择**将代码放在单独的文件中**。 否则，将创建一个 Web 页，该网页具有空脚本\<块，并且没有 %Page %> 指令来挂接从属文件。

- 母版

     母版页的起始内容。 此母版页没有关联的代码背后的从属文件。

- MasterPage_cb.master

     母版页的起始内容。 此母版页具有关联的代码背后从属文件。

- 代码后面。*扩展*

     实现母版页类的从属文件。 代码背后语言确定此文件的*扩展名*。

- 母版页面.vstemplate

     确定新母版页及其从属文件（如果有）内容的模板文件。

## <a name="see-also"></a>请参阅
- [网站支持](../../extensibility/internals/web-site-support.md)
