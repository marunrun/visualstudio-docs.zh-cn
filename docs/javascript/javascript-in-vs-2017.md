---
title: JavaScript
ms.date: 01/15/2019
ms.technology: vs-javascript
ms.topic: conceptual
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 74dca14c-5071-416f-a92b-d09f95e3dfb8
caps.latest.revision: 1
author: bowdenk7
ms.author: wilkelly
manager: jillfra
ms.openlocfilehash: 2a0d3657843dcf282e5c9aab8609efe5f9611965
ms.sourcegitcommit: 9eff8371b7a79a637ebb6850f775dd3eed343d8b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/03/2020
ms.locfileid: "78234951"
---
# <a name="javascript-in-visual-studio-2017"></a>Visual Studio 2017 中的 JavaScript

JavaScript 是 Visual Studio 中的一级语言。 当你在 Visual Studio IDE 中编写 JavaScript 代码时，你可以使用该标准编辑帮助（代码片段，IntelliSense 等等）的大部分或全部。 对于许多应用程序类型和服务，可以编写 JavaScript 代码。

> [!NOTE]
> 我们汇集了整个社区的力量，将所有 Microsoft JavaScript API 参考（超过 500 页）从 docs.microsoft.com 重定向到其 MDN 对应位置，以使 [MDN Web 文档](https://developer.mozilla.org/en-US/)成为 Web 的一站式首要开发资源。 有关详细信息，请参阅此[公告](https://blogs.windows.com/msedgedev/2018/06/26/chakra-docs-mdn-web-docs/)。

## 对 ECMAScript 2015 (ES6) 和更高版本的 <a name="ES6"></a> 支持

Visual Studio 现在支持 ECMAScript 语言更新（例如 ECMAScript 2015/2016）的语法。

### <a name="what-is-ecmascript-2015"></a>什么是 ECMAScript 2015？

JavaScript 作为一种编程语言仍在不断更新，而 [TC39](https://www.ecma-international.org/memento/tc39-m.htm) 是负责进行更新的委员会。
ECMAScript 2015 是对 JavaScript 语言的更新，提供了有帮助的新语法和功能。 要深入了解 ES6 的功能，请查看[此](http://es6-features.org/#Constants)引用站点。

除了支持 ECMAScript 2015，Visual Studio 还支持 ECMAScript 2016，并会在发布 ECMAScript 的将来版本后提供对这些版本的支持。 要与 TC39 和 ECMAScript 中的最新更改保持同步，请关注它们在 [github](https://github.com/tc39) 上的文章。

### <a name="transpile-javascript"></a>转译 JavaScript

JavaScript 的常见问题在于，用户想使用最新的 ES6+ 语言功能（因为它们能提高效率），但是运行时环境（通常是浏览器）尚不支持这些新功能。 这意味着，用户必须弄清楚哪种浏览器支持哪些功能（可能会非常繁琐乏味），或者，需要一种方法将 ES6+ 代码转换为目标运行时了解的版本（通常是 ES5）。 将代码转换为运行时可以理解的版本通常称为“转译”。

TypeScript 的主要功能之一是可以将 ES6+ 代码转译为 ES5 或 ES3，以便用户可以编写使自己最为高效的代码，但同时仍可以在任意平台上运行代码。 因为 [!include[vs_dev15](../../docs/misc/includes/vs_dev15_md.md)] 中的 JavaScript 使用与 TypeScript 相同的语言服务，因此也可以利用 ES6+ 到 ES5 的转译。

在设置转译之前，需要对配置选项进行一定的了解。
通过 `tsconfig.json` 文件配置 TypeScript。
如果没有此类文件，则使用某些默认值。
出于兼容性原因，这些默认值在仅存在 JavaScript 文件（或还有 `.d.ts` 文件）的上下文中是不同的。
若要编译 JavaScript 文件，则必须添加 `tsconfig.json` 文件并显式设置某些选项。

Tsconfig 文件的必需设置如下：

- `allowJs`：必须将此值设置为 `true`，才能识别 JavaScript 文件。 默认值为 `false`，因为 TypeScript 编译为 JavaScript，并且编译器不应包含刚刚编译的文件。
- `outDir`：应将此值设置为未包含在项目中的位置，这样就不会检测已发出 JavaScript 文件并将文件添加到项目中（请参阅 `exclude`）。
- `module`：如果使用的是模块，此设置会指示编译器已发出代码应使用哪种模块格式（例如，用于节点的 `commonjs`，或 Browserify 等捆绑程序）。
- `exclude`：此设置指明不要在项目中添加的文件夹。
应向此设置添加输出位置和非项目文件夹（如 `node_modules` 或 `temp`）。
- `enableAutoDiscovery`：此设置按上面所述启用自动检测和下载定义文件。
- `compileOnSave`：此设置指示编译器是否只要在 Visual Studio 中保存源文件时就应重新编译。
- `typeAcquisition`：这组设置控制自动类型获取的行为（[这一部分](/visualstudio/ide/javascript-intellisense#Auto)进一步说明了这一点）

为了将 JavaScript 文件转换为 CommonJS 模块并将其放置在 `./out` 文件夹中，可以使用以下 `tsconfig.json` 文件：

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "allowJs": true,
    "outDir": "out"
  },
  "exclude": [
    "node_modules",
    "wwwroot",
    "out"
  ],
  "compileOnSave": true,
  "typeAcquisition": {
    "enable": true
  }
}
```

在准备好设置的情况下，如果存在一个源文件 (`./app.js`) 并包含多个 ECMAScript 2015 语言功能，如下所示：

```js
import {Subscription} from 'rxjs/Subscription';  // ES6 import

class Foo {  // ES6 Class
    sayHi(name) {
        return `Hi ${name}, welcome to Salsa!`;  // ES6 template string
    }
}

export let sqr = x => x * x;  //ES6 export, let, and arrow function
export default Subscription;  //ES6 default export
```

则文件将被发送至面向 ECMAScript 5（默认值）的 `./out/app.js`，如下所示：

```js
"use strict";
var Subscription_1 = require('rxjs/Subscription');
var Foo = (function () {
    function Foo() {
    }
    Foo.prototype.sayHi = function (name) {
        return "Hi " + name + ", welcome to Salsa!";
    };
    return Foo;
}());
exports.sqr = function (x) { return x * x; };
Object.defineProperty(exports, "__esModule", { value: true });
exports.default = Subscription_1.Subscription;
```

## <a name="better-intellisense"></a>更好的 IntelliSense

[!include[vs_dev15](../../docs/misc/includes/vs_dev15_md.md)] 中的 JavaScript IntelliSense 现将显示有关参数和成员列表的详细信息。 此新信息由 TypeScript 语言服务提供，该服务在后台使用静态分析来更好地了解使用者的代码。 可以在[此处](/visualstudio/ide/javascript-intellisense/)阅读有关新的 IntelliSense 体验及其工作原理的详细信息。

## <a name="JSX"></a>JSX 语法支持

[!include[vs_dev15](../../docs/misc/includes/vs_dev15_md.md)] 中的 JavaScript 提供丰富的 JSX 语法支持。 JSX 是允许在 JavaScript 文件中使用 HTML 标记的语法集。

下图显示了在 `comps.tsx` TypeScript 文件中定义 React 组件，然后从 `app.jsx` 文件中使用此组件，通过 IntelliSense 在 JSX 表达式中实现补全和记录。
此处不需要 TypeScript，此特定示例刚好包含了一些 TypeScript 代码。

![JSX 语法](../javascript/media/js-react.png)

> [!NOTE]
> 若要将 JSX 语法转换为 React 调用，必须将 `"jsx": "react"` 设置添加到 `tsconfig.json` 文件中的 `compilerOptions`。

在生成时在 `./out/app.js' 处创建的 JavaScript 文件包含代码：

```js
"use strict";
var comps_1 = require('./comps');
var x = React.createElement(comps_1.RepoDisplay, {description: "test"});
```

## <a name="configure-your-javascript-project"></a>配置 JavaScript 项目

语言服务由静态分析提供支持，这意味着它会分析源代码（而不实际执行代码），以返回 IntelliSense 结果并提供其他编辑功能。
因此，项目上下文中包含的文件的数量越多、文件大小越大，在分析过程中使用的内存和 CPU 就越多。
因此，对项目形状做出了几个默认假设：

- `package.json` 和 `bower.json` 列出了项目所使用的依赖项，并且这些项默认包含在自动类型获取 (ATA) 中
- 顶层 `node_modules` 文件夹包含库源代码，并且其内容默认不包括在项目上下文中
- 所有其他 `.js`、`.jsx`、`.ts` 和 `.tsx` 文件都可能是你自己的  源文件之一，并且必须包含在项目上下文中

在大多数情况下，使用默认项目配置就能打开项目并获得极佳的体验。 但是，在较大项目或具有不同文件夹结构的项目中，可能需要进一步配置语言服务，才能更好地仅专注于你自己的源文件。

### <a name="override-defaults"></a>替代默认值

可以通过将 `tsconfig.json` 文件添加到项目根目录来替代默认配置。
`tsconfig.json` 有多个不同的选项，可以操纵项目上下文。
下面列出了其中几个选项，但要获取一整套可用选项，请[参阅架构存储](http://json.schemastore.org/tsconfig)。

## <a name="important-tsconfigjson-options"></a>重要的 `tsconfig.json` 选项

```json
{
  "compilerOptions": {
    "allowJs": true,          // include .js and .jsx in project context (defaults to only .ts and .tsx)
    "noEmit": true            // turns off downlevel compiler
  },
  "files": [],                // list of explicit files to include in the project context. Highest priority.
  "include": [],              // list of folders or glob patterns to include in the project context.
  "exclude": [],              // list of folders or glob patterns to exclude. Overridden by files array.
  "typeAcquisition": {
    "enable": true,           // Defaulted to "false" with a tsconfig. Enables better IntelliSense in JS.
    "include": [ "jquery" ],  // Specific libs to fetch .d.ts files that weren't picked up by ATA
    "exclude": [ "node" ]     // Specific libs to not fetch .d.ts files for
  }
}
```

### <a name="example-project-configuration"></a>示例项目配置

提供具有以下设置的项目：

- 项目的源文件位于 `wwwroot/js`
- 项目的 lib 文件位于 `wwwroot/lib`
- `bootstrap`、`jquery`、`jquery-validation` 和 `jquery-validation-unobtrusive` 在 `bower.json` 中列出
- `kendo-ui` 已手动添加到 lib文件夹

![文件夹结构](../javascript/media/js-folderstructure.png)

可以使用以下 `tsconfig.json` 来确保语言服务仅分析 `js` 文件夹中的源文件，但仍然提取 `.d.ts` 文件并将其用于 `lib` 文件夹中的库。

```json
{
  "compilerOptions": {
    "allowJs": true,
    "noEmit": true
  },
  "exclude": ["wwwroot/lib"],  //ignore lib folders, we will get IntelliSense via ATA
  "typeAcquisition": {
    "enable": true,
    "include": [ "kendo-ui" ]  //kendo-ui wasn't added via bower, so we need to list it here
  }
}
```

## <a name="troubleshooting-the-javascript-language-service-has-been-disabled-for-the-following-projects"></a>故障排除 已为以下项目禁用 JavaScript language service
打开一个含有大量内容的 JavaScript 项目时，可能会收到一条消息，内容为“已为以下项目禁用 JavaScript language service”。 出现大量 JavaScript 源的最常见原因是由于包含源代码超过 20MB 项目限制的库。

优化项目的简单方法是在项目根目录中添加 `tsconfig.json` 文件，让语言服务知道可以放心忽略哪些文件。 使用以下示例排除存储库的最常见目录：

```json
{
  "compilerOptions": {
    "allowJs": true,
    "allowSyntheticDefaultImports": true,
    "maxNodeModuleJsDepth": 2,
    "noEmit": true,
    "skipLibCheck": true
  },
  "exclude": [
    "**/bin",
    "**/bower_components",
    "**/jspm_packages",
    "**/node_modules",
    "**/obj",
    "**/platforms"
  ]
}
```

根据需要添加更多目录。 其他一些示例包括“vendor”或“wwwroot/lib”目录。

> [!NOTE]
> 也可使用编译器属性 `disableSizeLimit` 来禁用 20MB 检查限制。 使用此属性时请特别小心，因为禁用该限制可能会导致语言服务故障。

## <a name="notable-changes-from-visual-studio-2015"></a>Visual Studio 2015 中的显著更改

由于 [!include[vs_dev15](../../docs/misc/includes/vs_dev15_md.md)] 中拥有全新的语言服务，因此，有几个与之前的体验不同或之前的体验中没有的行为。
最显著的更改是将 VSDoc 替换为 JSDoc、删除自定义 `.intellisense.js` 扩展和特定代码模式的有限 IntelliSense。

### <a name="no-more-references-or-_referencesjs"></a>不再具有 `///<references/>` 或 `_references.js`

以前，在任何时候要了解 IntelliSense 作用域中有哪些文件的过程相当复杂。 有时，需要所有文件都位于作用域，其他情况下则不需要，但这会导致涉及手动引用管理的复杂配置。 今后，无需再考虑引用管理，因此也无需对引用、注释或`_references.js` 文件添加三斜杠。

有关 IntelliSense 工作原理的详细信息，请参阅 [JavaScript IntelliSense](/visualstudio/ide/javascript-intellisense/) 页。

### <a name="vsdoc"></a>VSDoc

XML 文档注释（有时称为 VSDoc）以前可用于修饰包含额外可强化 IntelliSense 结果的数据的源代码。
为支持更易于编写并且是 JavaScript 公认标准的 [JSDoc](https://jsdoc.app/about-getting-started.html)，不再支持 VSDoc。

### <a name="intellisensejs-extensions"></a>`.intellisense.js` 扩展

以前，可以创建 [IntelliSense 扩展](https://msdn.microsoft.com/library/hh874692.aspx)，通过此扩展可以为第三方库添加自定义完成结果。
这些扩展难以编写并且安装和引用它们也很繁琐，因此，以后的新语言服务不再支持这些文件。
作为更简单的替代方法，可以编写 TypeScript 定义文件，来提供与旧版 `.intellisense.js` 扩展相同的 IntelliSense 优势。
可以在[此处](http://www.typescriptlang.org/docs/handbook/declaration-files/introduction.html)了解有关声明 (`.d.ts`) 文件创作的详细信息。

### <a name="unsupported-patterns"></a>不支持的模式

由于新语言服务由静态分析（而不是执行引擎）提供支持（请阅读[此问题](https://github.com/Microsoft/TypeScript/issues/4789)获取有关差异的信息），因此，存在几种无法再检测到的 JavaScript 模式。
最常见的模式是“expando”模式。
当前语言服务无法向在声明后附加属性的对象提供 IntelliSense。
例如：

```js
var obj = {};
obj.a = 10;
obj.b = "hello world";
obj. // IntelliSense won't show properties a or b
```

可以通过在对象创建期间声明属性来避免此问题：

```js
var obj = {
    "a": 10,
    "b": "hello world"
}
obj. // IntelliSense shows properties a and b
```

还可以添加 JSDoc 注释，如下所示：

```js
/**
 * @type {{a: number, b: string}}
 */
var obj = {};
obj.a = 10;
obj.b = "hello world";
obj. // IntelliSense shows properties a and b
```
