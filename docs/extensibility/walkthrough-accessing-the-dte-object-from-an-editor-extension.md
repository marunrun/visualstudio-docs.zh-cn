---
title: 从编辑器扩展器访问 DTE 对象
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
ms.openlocfilehash: e37bdb21b7c8132f0dfb166d19e03d36e838245d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697661"
---
# <a name="walkthrough-access-the-dte-object-from-an-editor-extension"></a>演练：从编辑器扩展器访问 DTE 对象

在 VSPackages 中，可以通过使用 DTE 对象<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A>的类型调用 方法来获取 DTE 对象。 在托管扩展性框架 （MEF） 扩展中，可以导入<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>然后使用 类型<xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A><xref:EnvDTE.DTE>调用 方法。

## <a name="prerequisites"></a>先决条件

要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[可视化工作室 SDK](../extensibility/visual-studio-sdk.md)。

## <a name="get-the-dte-object"></a>获取 DTE 对象

1. 创建一个 C# VSIX 项目并将其命名为**DTETest**。 添加**编辑器分类器**项目模板并将其命名为**DTETest**。

   有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

::: moniker range=">=vs-2019"

2. 向项目添加以下程序集引用：

    - 微软.VisualStudio.shell.Framework.Framework
    - 微软.VisualStudio.shell.不可改变.10.0

3. 在*DTETestProvider.cs*文件中，添加以下`using`指令：

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. 在`DTETestProvider`类中，导入<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>。

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. 在`GetClassifier()`方法中，在`return`语句之前添加以下代码：

    ```csharp
   ThreadHelper.ThrowIfNotOnUIThread();
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

::: moniker range="vs-2017"

2. 向项目添加以下程序集引用：

   - EnvDTE
   - 微软.VisualStudio.shell.Framework.Framework

3. 在*DTETestProvider.cs*文件中，添加以下`using`指令：

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. 在`DTETestProvider`类中，导入<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>。

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. 在`GetClassifier()`方法中，在`return`语句之前添加以下代码：

    ```csharp
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

## <a name="see-also"></a>请参阅

- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
- [使用 DTE 启动 Visual Studio](launch-visual-studio-dte.md)
