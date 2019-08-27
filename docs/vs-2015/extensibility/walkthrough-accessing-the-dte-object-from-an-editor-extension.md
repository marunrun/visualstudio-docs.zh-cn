---
title: 演练：从编辑器扩展访问 DTE 对象 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - getting the DTE object
ms.assetid: c1f40bab-c6ec-45b0-8333-ea5ceb02a39d
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4b14b59465b94ddd0a09748f0e309166bf3d4114
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68148879"
---
# <a name="walkthrough-accessing-the-dte-object-from-an-editor-extension"></a>演练：通过编辑器扩展访问 DTE 对象
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Vspackage 中，您可以通过调用中获取 DTE 对象<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A>与 DTE 对象类型的方法。 在 Managed Extensibility Framework (MEF) 扩展中，您可以导入<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>，然后调用<xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A>方法的类型与<xref:EnvDTE.DTE>。  
  
## <a name="prerequisites"></a>系统必备  
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。  
  
## <a name="getting-the-dte-object"></a>获取 DTE 对象  
  
#### <a name="to-get-the-dte-object-from-the-serviceprovider"></a>若要从该服务提供商获取 DTE 对象  
  
1. 创建一个名为 C# VSIX 项目`DTETest`。 添加编辑器分类器项模板并将其命名`DTETest`。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。  
  
2. 添加对项目的以下程序集引用：  
  
    - EnvDTE  
  
    - EnvDTE80  
  
    - Microsoft.VisualStudio.Shell.Immutable.10.0  
  
3. 转到 DTETest.cs 文件，并添加以下`using`指令：  
  
    ```csharp  
    using EnvDTE;  
    using EnvDTE80;  
    using Microsoft.VisualStudio.Shell;  
  
    ```  
  
4. 在中`GetDTEProvider`类中，导入<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>。  
  
    ```csharp  
    [Import]  
    internal SVsServiceProvider ServiceProvider = null;  
  
    ```  
  
5. 在 `GetClassifier()` 方法中，添加以下代码。  
  
    ```csharp  
    DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));  
  
    ```  
  
6. 如果您必须使用<xref:EnvDTE80.DTE2>接口，可以强制转换为它的 DTE 对象。  
  
## <a name="see-also"></a>请参阅  
 [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
