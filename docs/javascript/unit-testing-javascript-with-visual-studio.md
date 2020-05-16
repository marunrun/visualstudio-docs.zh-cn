---
title: 对 JavaScript 和 TypeScript 代码进行单元测试
description: Visual Studio 支持使用针对 Visual Studio 的 Node.js 工具对 JavaScript 和 TypeScript 代码进行单元测试
ms.date: 06/06/2018
ms.topic: conceptual
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 792c74a3b5da5ed6528fa3919a0c60625d1a38ef
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77071942"
---
# <a name="unit-testing-javascript-and-typescript-in-visual-studio"></a>在 Visual Studio 中对 JavaScript 和 TypeScript 代码进行单元测试

通过针对 Visual Studio 的 Node.js 工具可以在无需切换到命令提示符的情况下，使用一些常用 JavaScript 框架写入和运行单元测试。

支持的框架：
* Mocha ([mochajs.org](https://mochajs.org/))
* Jasmine ([Jasmine.github.io](https://jasmine.github.io/))
* Tape ([github.com/substack/tape](https://github.com/substack/tape))
* Jest ([jestjs.io](https://jestjs.io/))
* 导出运行程序（此框架特定于针对 Visual Studio 的 Node.js 工具）

> [!WARNING]
> 磁带的问题当前阻止磁带测试运行。 如果合并 [PR #361](https://github.com/substack/tape/pull/361)，则应解决此问题。

如果你常用的框架不受支持，请参阅[添加对单元测试框架的支持](#addingFramework)，获取有关添加支持的信息。

## <a name="write-unit-tests"></a>写入单元测试

将单元测试添加到项目之前，请确保要使用的框架已本地安装在项目中。 使用 [npm 包安装窗口](npm-package-management.md#npmInstallWindow)可以轻松完成此操作。

向项目添加单元测试的首选方法是在项目中创建“测试”文件夹并将其设置为项目属性中的测试根  。 还需要选择想要使用的测试框架。

![设置测试根和测试框架](../javascript/media/unit-test-project-properties.png)

可以使用“添加新项”对话框，将简单的空白测试添加到项目  。 同一项目中同时支持 JavaScript 和 TypeScript。

![添加新单元测试](../javascript/media/unit-test-add-new-item.png)

对于 Mocha 单元测试，请使用以下代码：

```javascript
var assert = require('assert');

describe('Test Suite 1', function() {
    it('Test 1', function() {
        assert.ok(true, "This shouldn't fail");
    })

    it('Test 2', function() {
        assert.ok(1 === 1, "This shouldn't fail");
        assert.ok(false, "This should fail");
    })
})
```

如果尚未在项目属性中设置单元测试选项，则必须确保“属性”窗口中的“测试框架”属性设为适用于单元测试文件的正确测试框架   。 这通过单元测试文件模板自动完成。

![测试框架](../javascript/media/UnitTestsFrameworkMocha.png)

> [!Note]
> 单元测试选项将优先于单个文件的设置。

打开测试资源管理器（选择“测试” **“Windows”** “测试资源管理器”）后，Visual Studio 发现并显示测试 >    >   。 如果开始未显示测试，则重新生成项目以刷新列表。

![测试资源管理器](../javascript/media/UnitTestsDiscoveryMocha.png)

> [!NOTE]
> 请勿在 tsconfig.json 中使用 `outdir` 或 `outfile`，因为测试资源管理器无法在 TypeScript 文件中找到单元测试  。

## <a name="run-tests"></a>运行测试

可以在 Visual Studio 2017 中运行测试，或从命令行运行测试。

### <a name="run-tests-in-visual-studio-2017"></a>在 Visual Studio 2017 中运行测试

可以通过在测试资源管理器中单击“全部运行”链接运行测试  。 或者，可以选择一个或多个测试或组，右键单击并从快捷菜单选择“运行所选测试”，从而运行测试  。 后台运行测试，测试资源管理器自动更新并显示结果。 此外，还可以通过选择“调试所选测试”调试所选测试  。

> [!Warning]
> 使用 Node 8+ 调试单元测试仅适用于 JavaScript 测试文件，TypeScript 测试文件命中断点失败。 一种变通方法是使用 `debugger` 关键字。

> [!NOTE]
> 我们当前不支持分析测试或代码覆盖率。

### <a name="run-tests-from-the-command-line"></a>从命令行运行测试

可以使用以下命令从适用于 Visual Studio 2017 的[开发人员命令提示](/dotnet/framework/tools/developer-command-prompt-for-vs)运行测试：

```
vstest.console.exe <path to project file>\NodejsConsoleApp23.njsproj /TestAdapterPath:<VisualStudioFolder>\Common7\IDE\Extensions\Microsoft\NodeJsTools\TestAdapter
```

该命令显示类似下面的输出：

```
Microsoft (R) Test Execution Command Line Tool Version 15.5.0
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...
Processing: NodejsConsoleApp23\NodejsConsoleApp23\UnitTest1.js
  Creating TestCase:NodejsConsoleApp23\NodejsConsoleApp23\UnitTest1.js::Test Suite 1 Test 1::mocha
  Creating TestCase:NodejsConsoleApp23\NodejsConsoleApp23\UnitTest1.js::Test Suite 1 Test 2::mocha
Processing finished for framework of Mocha
Passed   Test Suite 1 Test 1
Standard Output Messages:
 Using default Mocha settings
 1..2
 ok 1 Test Suite 1 Test 1

Failed   Test Suite 1 Test 2
Standard Output Messages:
 not ok 1 Test Suite 1 Test 2
   AssertionError [ERR_ASSERTION]: This should fail
       at Context.<anonymous> (NodejsConsoleApp23\NodejsConsoleApp23\UnitTest1.js:10:16)

Total tests: 2. Passed: 1. Failed: 1. Skipped: 0.
Test Run Failed.
Test execution time: 1.5731 Seconds
```

> [!NOTE]
> 如果收到指示无法找到 vstest.console.exe 的错误，请确保已打开开发人员命令提示，而不是常规的命令提示符  。

## <a name="add-support-for-a-unit-test-framework"></a><a name="addingFramework"></a>添加对单元测试框架的支持

可以通过使用 JavaScript 实现发现和执行逻辑添加对其他测试框架的支持。 可以通过在以下位置添加名为测试框架的文件夹执行此操作：

`<VisualStudioFolder>\Common7\IDE\Extensions\Microsoft\NodeJsTools\TestAdapter\TestFrameworks`

此文件夹必须包含与导出以下两个函数的文件名称相同的 JavaScript 文件：

* `find_tests`
* `run_tests`

有关 `find_tests` 和 `run_tests` 实现的示例，请参阅 Mocha 单元测试框架实现：

`<VisualStudioFolder>\Common7\IDE\Extensions\Microsoft\NodeJsTools\TestAdapter\TestFrameworks\mocha\mocha.js`

Visual Studio 启动时开始发现可用测试框架。 如果在 Visual Studio 运行时添加框架，请重启 Visual Studio 检测框架。 但是，对实现做出更改时无需重启。

## <a name="unit-tests-in-other-project-types"></a>其他项目类型中的单元测试
并不局限于在 Node.js 项目中编写单元测试。 将 TestFramework 和 TestRoot 属性添加到任何 C# 或 Visual Basic 项目时，将枚举这些测试，并且可使用“测试资源管理器”窗口运行它们。

为实现此操作，请在解决方案资源管理器中右键单击项目节点，选择“卸载项目”  ，然后选择“编辑项目”  。 然后在项目文件中，将以下两个元素添加到属性组中。

> [!NOTE]
> 确保未对要添加元素的属性组指定条件。
> 这可能会导致意外行为。

```xml
<PropertyGroup>
    <JavaScriptTestRoot>tests\</JavaScriptTestRoot>
    <JavaScriptTestFramework>Tape</JavaScriptTestFramework>
</PropertyGroup>
```

接下来，将测试添加到指定的测试根文件夹，它们将可以在“测试资源管理器”窗口中运行。 如果最初未显示它们，可能需要重新生成项目。

### <a name="unit-test-net-core-and-net-standard"></a>对 .NET Core 和 .NET Standard 进行单元测试
除了上述属性之外，你还需要安装 NuGet 包[Microsoft.JavaScript.UnitTest](https://www.nuget.org/packages/Microsoft.JavaScript.UnitTest/) 并设置以下属性：

```xml
<PropertyGroup>
    <GenerateProgramFile>false</GenerateProgramFile>
</PropertyGroup>
```

一些测试框架可能需要额外的 npm 包来进行测试检测。 例如，jest 需要 jest-editor-support npm 包。 如果需要，请查看特定框架的文档。
