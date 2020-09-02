---
title: 自定义 RequireJS 的 IntelliSense |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 2be07ef8-9c08-444b-a21a-22a4fe6386a3
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 279ac7737460c90f86918ae673e8f64ef1215546
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72665885"
---
# <a name="customizing-intellisense-for-requirejs"></a>为 RequireJS 自定义 IntelliSense
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

从 Visual Studio 2013 Update 4 开始，支持对常用 RequireJS JavaScript 文件和模块化加载程序的支持。 RequireJS 使定义代码模块之间的依赖关系和仅在需要时动态加载模块更容易了。 编写使用 RequireJS 的 JavaScript 代码时，会针对你从你的模块定义中引用的模块或通过调用 `require()` 从你的代码中引用的模块提供 IntelliSense 建议。

 默认情况下，Visual Studio 支持非常基本的配置，以支持 RequireJS，但常见的做法是设置你自己的自定义配置设置（即为库定义别名）。 本主题介绍可用于自定义 Visual Studio 几种不同方法，以用于你的项目的独特设置。

 本主题介绍如何执行以下操作：

- 在 ASP.NET 项目中自定义 RequireJS

- 在 JSProj 项目中自定义用于生成 Apache Cordova 应用、Windows 应用商店应用和 LightSwitch HTML 应用的 RequireJS

## <a name="customize-requirejs-in-aspnet-projects"></a>在 ASP.NET 项目中自定义 RequireJS
 你的当前 JavaScript 文件引用名为 require.js 的文件时，将自动启用对 RequireJS 的支持（有关详细信息，请参阅 [JavaScript IntelliSense](../ide/javascript-intellisense.md) 中的“确定 IntelliSense 上下文”部分）。 在 ASP.NET 项目中，引用 require.js 通常是使用 _references.js 文件中的///指令来完成的 \<reference/> 。

### <a name="configure-the-data-main-attribute-in-an-aspnet-project"></a>在 ASP.NET 项目中配置 data-main 属性
 为了准确地模拟运行应用时应用的工作情况，JavaScript 编辑器需要知道在设置 require.js 时应首先加载什么文件。 通常使用引用 require.js 的脚本元素上的 `data-main` 属性在你的应用程序 HTML 文件中对此进行配置，如下所示。

```html
<script src="js/require.js" data-main="js/app.js"></script>
```

 在此示例中，data-main (js/app.js) 引用的脚本在 require.js 后立即加载。 立即加载的文件是首次使用) 配置 RequireJS 使用 (的最佳位置 `require.config()` 。若要告诉 JavaScript 编辑器要 `data-main` 在应用程序中使用的文件，请添加 `data-main` 属性，然后修改在 \<reference/> 应用程序中引用 require.js 的///指令。 例如，可以使用以下指令：

```javascript
/// <reference path="js/require.js" data-main="js/app.js" />
```

### <a name="configure-the-application-start-page-in-an-aspnet-project"></a>在 ASP.NET 项目中配置应用程序起始页
 应用运行时，RequireJS 假定文件的相对路径 (例如 "... \\ "路径) 相对于加载 require.js 库的 HTML 文件。 在 Visual Studio 编辑器中编写 ASP.NET 项目的代码时，此起始页是未知的，你需要告知编辑器使用相对文件路径时要使用什么起始页。 为此，请将 `start-page` 属性添加到/// \<reference/> 指令中。

```javascript
/// <reference path="js/require.js" data-main="js/app.js" start-page="/app/index.html" />
```

 `start-page` 属性指定运行应用时在浏览器中看到的页面的 URL。

## <a name="customize-requirejs-in-jsproj-projects"></a>在 JSProj 项目中自定义 RequireJS
 生成 Apache Cordova 应用、基于 HTML 的 Windows 应用商店应用或 LightSwitch HTML 应用时，使用 JSProj 项目（项目文件以 .jsproj 扩展名结尾）。 与 ASP.NET 项目不同，这些项目从项目中存在的 HTML 文件读取对 .js 文件的引用。 因此，在 JSProj 项目中编辑 JavaScript 时，你将看到，如果当前正在编辑 JavaScript 文件在另一个也引用 require.js 的 HTML 文件中被引用，将启用对 RequireJS 的支持。

 JSProj 项目文件中不需要 ASP.NET 项目所需的自定义步骤。 也就是说，会自动加载引用 require.js 的脚本标记上的 `data-main` 属性使用的脚本文件以配置 require.js。 引用 require.js 的 HTML 文件还用作应用程序的起始页。

## <a name="see-also"></a>另请参阅
 [JavaScript IntelliSense](../ide/javascript-intellisense.md)
