---
title: 如何：为 ASP.NET 应用程序启用调试 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging ASP.NET Web applications
- Web.config configuration file, debug mode
- debugging [Visual Studio], ASP.NET
ms.assetid: 3beed819-cece-4864-8184-bd410000973a
caps.latest.revision: 40
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 07036fd7c1db7dc8b56502ab9c914f1ba808e876
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65703666"
---
# <a name="how-to-enable-debugging-for-aspnet-applications"></a>如何：为 ASP.NET 应用程序启用调试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要启用调试，必须同时在“项目属性”  页和应用程序的 web.config 文件中启用它。  
  
> [!NOTE]  
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/library/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### <a name="to-enable-aspnet-debugging-in-the-project-properties-visual-basicc"></a>在项目属性中启用 ASP.NET 调试 (Visual Basic/C#)  
  
1. 在 **“解决方案资源管理器”** 中，右键单击 Web 项目的名称，然后选择 **“属性”**。  
  
2. 在项目属性页中，单击 **“Web”** 选项卡。  
  
3. 在“调试器” 下，选中“ASP.NET”  复选框。  
  
### <a name="to-enable-debugging-in-the-webconfig-file"></a>在 web.config 文件中启用调试  
  
1. 通过使用任何标准文本编辑器或 XML 分析器打开 web.config 文件。  
  
    > [!NOTE]  
    > 但是，不可以通过使用 Web 浏览器远程访问该文件。 出于安全原因， [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 将 Microsoft IIS 配置为帮助防止对 Web.config 文件的直接浏览器访问。 如果你尝试使用浏览器访问配置文件，则将遇到 HTTP 访问错误 403（禁止访问）。  
  
2. Web.config 是一个 XML 文件，因此包含使用标记来标记的嵌套节。 查找 `configuration/system.web/compilation` 元素。 如果 compilation 元素不存在，则创建它。  
  
3. 如果 `compilation` 元素不包含 `debug` 特性，请向元素添加该特性。  
  
4. 确保 `debug` 特性值设置为 `true`。  
  
web.config 文件应类似于下面的示例。 请注意，在 configuration 和 system.web 元素之间可存在节  
  
- configuration 和 system.web 元素之间的元素节  
  
- system.web 和 compilation 元素之间的元素节  
  
- compilation 元素可以包含其他特性和元素  
  
## <a name="example"></a>示例  
  
```  
<configuration>  
    ...  
    <system.web>  
        <compilation  
            debug="true"  
            ...  
        >  
        ...  
        </compilation>  
    </system.web>  
</configuration>  
```  
  
## <a name="robust-programming"></a>可靠编程  
[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 会自动检测对 Web.config 文件的任何更改，并应用新的配置设置。 不必重新启动计算机或 IIS 服务器，更改即可生效。  
  
一个网站可包含多个虚拟目录和子目录，而 Web.config 文件可能存在于每个目录中。 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 应用程序从 URL 路径中更高级别的 Web.config 文件中继承设置。 使用分层配置文件可以同时更改若干个 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 应用程序的设置，例如，层次结构下所有应用程序的设置。 但是，如果在层次结构中位于较低位置的文件中设置了 `debug` ，则它将替代较高位置的文件中的值。  
  
例如，可以在 www.microsoft.com/aaa/Web.config 中指定 `debug="true"` ，并且 aaa 文件夹中或 aaa 的任何子文件夹中的所有应用程序都将继承该设置。 因此，如果你[!INCLUDE[vstecasp](../includes/vstecasp-md.md)]应用程序位于 www.microsoft.com/aaa/bbb，它将继承该设置，如将任何[!INCLUDE[vstecasp](../includes/vstecasp-md.md)]www.microsoft.com/aaa/ccc 和 www.microsoft.com/aaa/ddd，等等的应用程序。 唯一的例外情况是其中一个应用程序通过自己的较低级的 Web.config 文件提替代设置。  
  
启用调试模式将极大地影响你的 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 应用程序的性能。 请记住，在部署发布版本的应用程序或进行性能度量之前要禁用调试模式。  
  
## <a name="see-also"></a>请参阅  
[调试 ASP.NET 和 AJAX 应用程序](../debugger/debugging-aspnet-and-ajax-applications.md)  
