---
title: JavaScript IntelliSense
ms.date: 06/28/2017
ms.topic: conceptual
ms.technology: vs-javascript
helpviewer_keywords:
- IntelliSense [JavaScript]
- <reference> JavaScript XML tag
- JavaScript Code Editor
- XML code comments, JavaScript IntelliSense
- reference JavaScript XML tag
- JavaScript, IntelliSense
- code comments, JavaScript IntelliSense
- JavaScript, reference groups
- JavaScript Editor
- reference directives [JavaScript]
- JavaScript, XML documentation comments
- reference groups [JavaScript]
- JavaScript, reference directives
- IntelliSense [JavaScript], about
- IntelliSense extensibility [JavaScript]
- XML documentation comments [JavaScript]
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6ee40d877af75469dcc1abc176d67f43c8bdcfb3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62538169"
---
# <a name="javascript-intellisense"></a>JavaScript IntelliSense

Visual Studio 提供了功能强大、即时可用的 JavaScript 编辑体验。 借助于基于 TypeScript 的语言服务所提供的支持，Visual Studio 提供功能更丰富的 IntelliSense、现代 JavaScript 功能支持，以及改进的工作效率功能（如“转到定义”、重构等）。

> [!NOTE]
> 自 Visual Studio 2017 起，JavaScript 语言服务为语言服务使用新引擎（名为“Salsa”）。 本文中包含详细信息，你还可参阅此[博客文章](https://devblogs.microsoft.com/visualstudio/previewing-salsa-javascript-language-service-visual-studio-15/)。 全新的编辑体验也几乎适用于 Visual Studio Code。 请参阅 [VS Code 文档](https://code.visualstudio.com/docs/languages/javascript)，了解详细信息。

有关 Visual Studio 的常规 IntelliSense 功能的详细信息，请参阅[使用 IntelliSense](../ide/using-intellisense.md)。

## <a name="whats-new-in-the-javascript-language-service-in-visual-studio-2017"></a>Visual Studio 2017 中 JavaScript 语言服务的新增功能

自 Visual Studio 2017 起，JavaScript IntelliSense 将显示更多有关参数和成员列表的信息。 此新信息由 TypeScript 语言服务提供，该服务在后台使用静态分析来更好地了解使用者的代码。

TypeScript 使用多个源来构建此信息：

- [基于类型推理的 IntelliSense](#TypeInference)
- [基于 JSDoc 的 IntelliSense](#JsDoc)
- [基于 TypeScript 声明文件的 IntelliSense](#TsDeclFiles)
- [自动获取类型定义](#Auto)

<a name="TypeInference"></a>

### <a name="intellisense-based-on-type-inference"></a>基于类型推理的 IntelliSense

在 JavaScript 中，通常没有可用的显式类型信息。 好在一般情况下可根据周围的代码上下文，轻松推导出类型。
此过程称为“类型推理”。

对于变量或属性，类型通常是用于对其进行初始化的值类型或最新的赋值。

```js
var nextItem = 10;
nextItem; // here we know nextItem is a number

nextItem = "box";
nextItem; // now we know nextItem is a string
```

对于函数，可以从 return 语句中推断返回类型。

当前无法对函数参数进行推理，但是可使用 JSDoc 或 TypeScript .d.ts 文件解决此问题（请参阅后面的部分）。

此外，还有针对以下内容的专门推导：

- “ES3 style”类（用构造函数和原型属性的赋值来指定）。
- CommonJS 样式模块模式（指定为 `exports` 对象上的属性赋值或对 `module.exports` 属性的赋值）。

```js
function Foo(param1) {
    this.prop = param1;
}
Foo.prototype.getIt = function () { return this.prop; };
// Foo will appear as a class, and instances will have a 'prop' property and a 'getIt' method.

exports.Foo = Foo;
// This file will appear as an external module with a 'Foo' export.
// Note that assigning a value to "module.exports" is also supported.
```

<a name="JsDoc"></a>

### <a name="intellisense-based-on-jsdoc"></a>基于 JSDoc 的 IntelliSense

在类型推理不提供所需类型信息（或支持文档）的情况下，可通过 JSDoc 注释显式提供类型信息。  例如，若要为部分声明的对象提供特定类型，可使用 `@type` 标记，如下所示：

```js
/**
 * @type {{a: boolean, b: boolean, c: number}}
 */
var x = {a: true};
x.b = false;
x. // <- "x" is shown as having properties a, b, and c of the types specified
```

如前文所述，无法对函数参数进行推理。 但是，还可以使用 JSDoc `@param` 标记向函数参数添加类型。

```js
/**
 * @param {string} param1 - The first argument to this function
 */
function Foo(param1) {
    this.prop = param1; // "param1" (and thus "this.prop") are now of type "string".
}
```

请参阅 [JavaScript 中的 JSDoc 支持](https://github.com/Microsoft/TypeScript/wiki/JsDoc-support-in-JavaScript)了解当前支持的 JsDoc 注释。

<a name="TsDeclFiles"></a>
### <a name="intellisense-based-on-typescript-declaration-files"></a>基于 TypeScript 声明文件的 IntelliSense

由于 JavaScript 和 TypeScript 现基于同一语言服务，因此它们能够以更丰富的方式进行交互。 例如，可以为在 .d.ts 文件（详细信息）中声明的值提供 JavaScript IntelliSense（请参阅 [TypeScript 文档](https://www.typescriptlang.org/docs/handbook/declaration-files/introduction.html)），而且在 TypeScript 中声明的类型（如接口和类）可用作 JsDoc 注释中的类型。

下面是一个简单的示例，其中演示 TypeScript 定义文件通过接口向同一项目的 JavaScript 文件提供此类类型信息（使用 `JsDoc` 标记）。

![TypeScript 定义文件](https://raw.githubusercontent.com/wiki/Microsoft/TypeScript/images/decl1.png)

<a name="Auto"></a>
### <a name="automatic-acquisition-of-type-definitions"></a>自动获取类型定义

在 TypeScript 世界中，最常用的 JavaScript 库的 API 由 .d.ts 文件描述，此类定义最常见的存储库位于 [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped)。

默认情况下，Salsa 语言服务将尝试检测正在使用的 JavaScript 库，并自动下载和引用用于描述库的对应 .d.ts 文件，以提供更丰富的 IntelliSense。 文件将下载到用户文件夹下的缓存中，位置为 %LOCALAPPDATA%\Microsoft\TypeScript。

> [!NOTE]
> 如果使用的是 tsconfig.json 配置文件，此功能在默认情况下为“禁用”，但可将其设置为“启用”，如下所述。

目前，自动检测适用于从 npm（通过读取 package.json 文件）、Bower（通过读取 bower.json 文件）下载的依赖项，以及项目中与大致前 400 个最常用的 JavaScript 库的列表匹配的松散文件。 例如，如果项目中有 jquery-1.10.min.js，将提取并加载 jquery.d.ts 文件，从而提供更好的编辑体验。 .d.ts 文件不会对项目产生任何影响。

如果不想使用自动获取，可通过添加配置文件来禁用它，如下所述。 仍可直接在项目中手动放置要使用的定义文件。

## <a name="see-also"></a>请参阅

- [使用 IntelliSense](../ide/using-intellisense.md)
- [JavaScript 支持 (Visual Studio for Mac)](/visualstudio/mac/javascript)