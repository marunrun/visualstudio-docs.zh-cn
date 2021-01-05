---
title: 从编辑器扩展访问 DTE 对象
description: 了解如何使用本演练中的代码示例从编辑器扩展访问 DTE 对象。
ms.custom: SEO-VS-2020
ms.date: 04/24/2019
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - getting the DTE object
ms.assetid: c1f40bab-c6ec-45b0-8333-ea5ceb02a39d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1a0ee789590bd411fe7955cf739683d016164f49
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97863720"
---
# <a name="walkthrough-access-the-dte-object-from-an-editor-extension"></a>演练：从编辑器扩展访问 DTE 对象

在 Vspackage 中，可以通过 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> 使用 dte 对象的类型调用方法来获取 dte 对象。 在 Managed Extensibility Framework (MEF) 扩展中，可以导入， <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> 然后 <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> 使用类型调用方法 <xref:EnvDTE.DTE> 。

## <a name="prerequisites"></a>先决条件

要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)。

## <a name="get-the-dte-object"></a>获取 DTE 对象

1. 创建 c # VSIX 项目，并将其命名为 **DTETest**。 添加 **编辑器分类器** 项模板并将其命名为 **DTETest**。

   有关详细信息，请参阅 [使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

::: moniker range=">=vs-2019"

2. 将以下程序集引用添加到项目：

    - VisualStudio 框架
    - VisualStudio. 10.0。

3. 在 *DTETestProvider.cs* 文件中，添加以下 `using` 指令：

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. 在 `DTETestProvider` 类中，导入 <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> 。

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. 在 `GetClassifier()` 方法中，在语句之前添加以下代码 `return` ：

    ```csharp
   ThreadHelper.ThrowIfNotOnUIThread();
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

::: moniker range="vs-2017"

2. 将以下程序集引用添加到项目：

   - EnvDTE
   - VisualStudio 框架

3. 在 *DTETestProvider.cs* 文件中，添加以下 `using` 指令：

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. 在 `DTETestProvider` 类中，导入 <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> 。

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. 在 `GetClassifier()` 方法中，在语句之前添加以下代码 `return` ：

    ```csharp
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

## <a name="see-also"></a>另请参阅

- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
- [使用 DTE 启动 Visual Studio](launch-visual-studio-dte.md)
