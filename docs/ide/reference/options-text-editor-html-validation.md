---
title: “选项”>“文本编辑器”>“HTML (Web 窗体)”>“验证”
ms.date: 1/15/2019
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.HTML.Validation
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d06674d476dd671f715d2f4c88bdd23852f78687
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62778474"
---
# <a name="options-text-editor-html-web-forms-validation"></a>“选项”>“文本编辑器”>“HTML (Web 窗体)”>“验证”

使用“验证”选项页，可以设置 HTML 编辑器首选如何检查文档中 HTML 标记的语法。 若要访问此页，请先依次选择菜单栏中的“工具” > “选项”，再依次展开“文本编辑器” > “HTML (Web 窗体)” > “验证”。

## <a name="validation"></a>验证

- **使用 doctype 检测验证架构**

   架构用于确定在此架构中有效的元素、属性和大小写。 架构还用于确定 IntelliSense 中可用的标记和属性。

   如果希望 Visual Studio 使用页面的 <!DOCTYPE> 声明和 html 元素内容来确定架构，请选中此选项。 例如，如果你选中此选项，且页面中有声明 `<!DOCTYPE html>`，Visual Studio 就会使用 HTML5 架构。 不过，如果 html 标记有 xmlns 属性（如 `<html xmlns="http://www.w3.org/1999/xhtml">`），Visual Studio 就会使用 XHTML5 架构。

- **找不到 doctype 时的目标**

   选择在页面中没有 <!DOCTYPE> 声明时依据的验证架构。

  - **显示错误**

     选中此复选框即可启用验证。 如果你取消选中此复选框，编辑器就不会标记验证错误。

     使用其他复选框，可以通过指定要让编辑器标记的各类错误来微调验证。

     > [!NOTE]
     > 某些架构不提供标记各个错误类型的选项。 例如，如果你选择“XHTML 1.1”作为目标架构，所有选项复选框都会遭禁用。 在此示例中，编辑器会标记所有类型的错误。

## <a name="see-also"></a>请参阅

- [“选项”对话框 ->“环境”->“常规”](../../ide/reference/general-environment-options-dialog-box.md)