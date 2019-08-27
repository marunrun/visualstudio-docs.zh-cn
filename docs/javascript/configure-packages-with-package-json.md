---
title: 使用 package.json 配置 npm 包
description: 使用 package.json 指定 npm 包版本
ms.date: 09/06/2018
ms.topic: conceptual
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 652ff7b0380fc03a3f9c8155a2f8696d9dfee5b9
ms.sourcegitcommit: 7fbfb2a1d43ce72545096c635df2b04496b0be71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67692375"
---
# <a name="packagejson-configuration"></a>package.json 配置

开发包含大量 npm 包的 Node.js 应用时，如果更新了一个或多个包，则在生成项目时遇到警告或错误的情况并不罕见。 有时，会出现版本冲突或者包版本已弃用的情况。 以下是一些快速提示，可帮助配置 [package.json](https://docs.npmjs.com/files/package.json) 文件，并了解显示警告或错误时所发生的情况。 这并不是 package.json 的完整指南，而只是着重介绍了 npm 包版本控制  。

npm 包版本控制系统具有严格的规则。 版本格式符合以下规则：

```
[major].[minor].[patch]
```

假设应用中有一个 5.2.1 版本的包。 主版本为 5，次版本为 2，修补程序为 1。

* 在主版本更新中，包包含不可后向兼容的新功能，即中断性变更。
* 在次要版本更新中，向包添加了与早期包版本后向兼容的新功能。
* 在修补程序更新中，包含了一个或多个 Bug 修复。 Bug 修复始终后向兼容。

值得注意是，npm 包的某些功能具有依赖项。 例如，若要将 TypeScript 编译器包 (ts-loader) 的新功能用于 webpack，可能还需要更新 webpack npm 包和 webpack-cli 包。

为了帮助管理包版本控制，npm 支持可在 package.json 中使用的多种表示法  。 可以使用这些表示法控制要在应用中接受的包更新类型。

假设正在使用 React，并且需要包含 react 和 react-dom npm 包   。 可以在 package.json 文件中以多种方式指定它  。 例如，可以如下所示，指定使用包的确切版本。

  ```json
  "dependencies": {
    "react": "16.4.2",
    "react-dom": "16.4.2",
  },
  ```

使用之前的表示法，npm 将始终获得指定的确切版本 16.4.2。

可以使用特殊的表示法来限制修补程序更新的更新（Bug 修复）。 在此示例中：

  ```json
  "dependencies": {
    "react": "~16.4.2",
    "react-dom": "~16.4.2",
  },
  ```

使用波形符 (~) 告知 npm 仅在修补包后更新该包。 因此，npm 可以将 react 16.4.2 更新为 16.4.3（或 16.4.4 等），但它不会接受对主版本或次要版本的更新。 因此，16.4.2 不会更新为 16.5.0。

也可使用脱字号 (^) 指定 npm 可以更新次要版本号。

  ```json
  "dependencies": {
    "react": "^16.4.2",
    "react-dom": "^16.4.2",
  },
  ```

使用这种表示法，npm 可以将 react 16.4.2 更新为 16.5.0（或 16.5.1、16.6.0 等），但它不接受对主要版本的更新。 因此，16.4.2 不会更新为 17.0.0。

npm 更新包时，会生成一个 package-lock.json 文件，该文件列出应用中使用的实际 npm 包（包括所有嵌套包）版本  。 虽然 package.json 控制应用的直接依赖项，但它不控制嵌套依赖项（特定 npm 包所需的其他 npm 包）  。 如果需要确保其他开发人员和测试人员使用你正在使用的确切包（包括嵌套包），可以在开发周期中使用 package-lock.json 文件  。 有关详细信息，请参阅 npm 文档中的 [package-lock.json](https://docs.npmjs.com/files/package-lock.json)。

对于 Visual Studio，未将 package-lock.json 文件添加到项目中，但可在项目文件夹中找到它  。
