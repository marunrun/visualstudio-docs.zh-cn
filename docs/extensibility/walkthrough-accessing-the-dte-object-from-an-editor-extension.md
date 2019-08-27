---
title: 从编辑器扩展访问 DTE 对象
ms.date: 04/24/2019
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - getting the DTE object
ms.assetid: c1f40bab-c6ec-45b0-8333-ea5ceb02a39d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1fb22793c3bfa805fae11c8bbea7f07c06fd5a85
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322789"
---
# <a name="walkthrough-access-the-dte-object-from-an-editor-extension"></a>演练：从编辑器扩展访问 DTE 对象

在 Vspackage 中，您可以通过调用中获取 DTE 对象<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A>与 DTE 对象类型的方法。 在 Managed Extensibility Framework (MEF) 扩展中，您可以导入<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>，然后调用<xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A>方法的类型与<xref:EnvDTE.DTE>。

## <a name="prerequisites"></a>系统必备

要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。

## <a name="get-the-dte-object"></a>获取 DTE 对象

1. 创建C#VSIX 项目并将其命名**DTETest**。 添加**编辑器分类器**项模板并将其命名**DTETest**。

   有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

::: moniker range=">=vs-2019"

2. 将添加到项目的以下程序集引用：

    - Microsoft.VisualStudio.Shell.Immutable.10.0

3. 在中*DTETestProvider.cs*文件中，添加以下`using`指令：

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. 在中`DTETestProvider`类中，导入<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>。

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. 在中`GetClassifier()`方法中，添加以下代码之前`return`语句：

    ```csharp
   ThreadHelper.ThrowIfNotOnUIThread();
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

::: moniker range="vs-2017"

2. 添加对项目的以下程序集引用：

   - EnvDTE
   - Microsoft.VisualStudio.Shell.Framework

3. 在中*DTETestProvider.cs*文件中，添加以下`using`指令：

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. 在中`DTETestProvider`类中，导入<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>。

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. 在中`GetClassifier()`方法中，添加以下代码之前`return`语句：

    ```csharp
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

## <a name="see-also"></a>请参阅

- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
- [启动 Visual Studio 中使用 DTE](launch-visual-studio-dte.md)