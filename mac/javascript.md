---
title: JavaScript 和 TypeScript
description: 有关 Visual Studio for Mac 中 JavaScript 支持的信息
author: sayedihashimi
ms.author: sayedha
ms.date: 05/03/2018
ms.technology: vs-ide-general
ms.assetid: 61432695-5B12-4257-B250-48D37EED106D
ms.openlocfilehash: 7ffe24d26af91d7d6733ec1540c2f2d810425e1e
ms.sourcegitcommit: 9a227faafdd0bad6f017ace607dc61eb56b32d72
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/21/2019
ms.locfileid: "71175418"
---
# <a name="javascript-and-typescript-support"></a>JavaScript 和 TypeScript 支持

Visual Studio for Mac 通过语法突出显示、代码格式设置和 IntelliSense 提供对 JavaScript 和 TypeScript 的支持。

![typescript 编辑器支持](/media/tsjseditor-2019.gif)

有关编写 JavaScript 的详细信息，请参阅[编写 JavaScript 代码](/scripting/javascript/writing-javascript-code)指南。

## <a name="adding-a-javascript-file"></a>添加 JavaScript 文件

通常通过“新建文件”对话框将 JavaScript 文件添加到 ASP.NET Core 项目  。 要添加 javascript 文件，右键单击项目并转到“添加”>“新建文件”  ：

![将新建文件添加到项目中](media/javascript-image1.png)

从“新建文件”对话框选择“Web > 空 JS 文件”或“Web > TypeScript 文件”    。 为文件命名，然后选择“新建”  ：

![从模板创建新的 typescript 文件](media/javascript-image2.png)

## <a name="intellisense"></a>IntelliSense

Visual Studio for Mac 使用 [JavaScript Language Service](/visualstudio/ide/javascript-intellisense) 提供 IntelliSense，为用户在编写代码时提供智能代码完成、参数信息和成员列表。

Visual Studio for Mac 中的 JavaScript IntelliSense 可以基于类型推理、JSDoc 或 TypeScript 声明。

- **类型推理** - 对象类型是通过周围的代码上下文推出的。 有关详细信息，请参阅[基于类型推理的 IntelliSense](/visualstudio/ide/javascript-intellisense#intellisense-based-on-type-inference) 的 Visual Studio 部分。
- **JSDoc** - 有时类型推理不提供正确的类型信息。 在这些情况下，类型信息可以由 [JSDoc](https://jsdoc.app/about-getting-started.html) 注释显式提供。 有关详细信息，请参阅[基于 JSDoc 的 IntelliSense](/visualstudio/ide/javascript-intellisense#intellisense-based-on-jsdoc) 的 Visual Studio 部分
- **TypeScript 声明文件** - `.d.ts` 文件用于提供 JavaScript IntelliSense 的值。 该文件中声明的类型可用作 JSDoc 注释的类型。 有关详细信息，请参阅[基于 TypeScript 声明文件的 IntelliSense](/visualstudio/ide/javascript-intellisense#intellisense-based-on-typescript-declaration-files) 的 Visual Studio 部分

    ![添加 typescript 定义文件](media/javascript-type-intellisense-2019.gif)

## <a name="see-also"></a>请参阅

- [JavaScript IntelliSense（Windows 上的 Visual Studio）](/visualstudio/ide/javascript-intellisense)
