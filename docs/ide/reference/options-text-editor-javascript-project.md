---
title: “选项”>“文本编辑器”>“JavaScript”>“项目”
ms.date: 1/15/2019
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Project.General
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Project
- VS.ToolsOptionsPages.Text_Editor.TypeScript.Project.General
- VS.ToolsOptionsPages.Text_Editor.TypeScript.Project
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 190cbdb2a8096415985d83fc525b997572d252c2
ms.sourcegitcommit: ce1ab8a25c66a83e60eab80ed8e1596fe66dd85c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2019
ms.locfileid: "68605930"
---
# <a name="options-text-editor-javascript-project"></a>“选项”>“文本编辑器”>“JavaScript”>“项目”

使用“选项”对话框中的“项目”页，可以指定代码编辑器中的 JavaScript 和 TypeScript 项目选项   。 要访问此页，请先依次选择菜单栏中的“工具” > “选项”，再依次展开“文本编辑器” > “JavaScript/TypeScript” > “项目”      。

## <a name="project-analysis-options"></a>项目分析选项

这些选项用于确定编辑器如何分析项目、报告诊断信息和提供改进建议。 通过选中或取消选中这些选项，可以指定编辑器如何处理这些情况。

### <a name="uielement-list"></a>UIElement 列表

- **仅分析包含在编辑器中打开的文件的项目**
- **仅报告在编辑器中打开的文件的诊断信息**
- **提供不属于更正的可能改进建议**

## <a name="virtual-projects-in-solution-explorer"></a>解决方案资源管理器中的虚拟项目

使用这些选项，可以选择是否在解决方案加载或未加载后显示虚拟项目。

## <a name="compile-on-save"></a>在保存时编译

这些选项用于确定是否自动编译不属于项目的 TypeScript 文件。 请先选中复选框，再选择要使用的代码生成类型。

### <a name="uielement-list"></a>UIElement 列表

- **对不属于项目的模块使用 AMD 代码生成**
- **对不属于项目的模块使用 CommonJS 代码生成**
- **对不属于项目的模块使用 UMD 代码生成**
- **对不属于项目的模块使用 System 代码生成**
- **对不属于项目的模块使用 ES2015 代码生成**

## <a name="ecmascript-version-for-files-that-are-not-part-of-a-project"></a>不属于项目的文件的 ECMAScript 版本

使用这些选项，可以选择不属于项目的文件的 ECMAScript 版本。 可以选择“ECMAScript 3”  、“ECMAScript 5”  或“ECMAScript 6”  。

## <a name="jsx-emit-for-tsx-files-that-are-not-part-of-a-project"></a>不属于项目的 TSX 文件的 JSX 发出内容

这些选项用于确定编辑器如何处理不属于项目的 TypeScript 文件。

### <a name="uielement-list"></a>UIElement 列表

|选项|说明|
|------------|-----------------|
|**React 框架**|在你选中此选项后，代码编辑器会发出 .js  文件扩展名。|
|**Preserve**|在你选中此选项后，代码编辑器会在输出中保留 JSX，并发出 .jsx  文件扩展名。|

## <a name="see-also"></a>请参阅

- [“选项”对话框 ->“环境”->“常规”](../../ide/reference/general-environment-options-dialog-box.md)