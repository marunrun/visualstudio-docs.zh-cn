---
title: 调整到编辑器的旧版代码 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - adapters
ms.assetid: a208d38e-9bea-41c9-9fe2-38bd86a359cb
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0bb90723a72c10dbf6cfda5edd4aa68f71f1c6b9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68184921"
---
# <a name="adapting-legacy-code-to-the-editor"></a>根据编辑器调整旧代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 编辑器具有许多功能，可以从现有代码组件访问。 以下说明介绍如何改编非 MEF 组件，例如，VSPackage，使用编辑器的功能。 此外说明了如何使用适配器来托管和非托管代码中获取的编辑器中的服务。  
  
## <a name="editor-adapters"></a>编辑器适配器  
 编辑器适配器或填充程序，还公开的类和接口中的编辑器对象的包装类则<xref:Microsoft.VisualStudio.TextManager.Interop>API。 可以使用的适配器，例如移动非编辑器服务之间、 Visual Studio shell 命令和编辑器服务。 （这是在编辑器在 Visual Studio 中的当前托管方式。）适配器还可在旧版编辑器和语言服务扩展在 Visual Studio 中正常工作。  
  
## <a name="using-editor-adapters"></a>使用编辑器适配器  
 <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>提供新的编辑器接口和旧接口之间进行切换的方法和还创建适配器的方法。  
  
 如果将此服务在 MEF 组件部分中，可以将服务导入，如下所示。  
  
```  
[Import(typeof(IVsEditorAdaptersFactoryService))]  
internal IVsEditorAdaptersFactoryService editorFactory;  
```  
  
 如果你想要在非 MEF 组件中使用此服务，请按照本主题后面的"使用 Visual Studio 编辑器服务在非 MEF 组件"部分中的说明。  
  
## <a name="switching-between-the-new-editor-api-and-the-legacy-api"></a>新的编辑器 API 和旧版 API 之间进行切换  
 使用以下方法编辑器对象和旧版接口之间进行切换。  
  
|方法|转换|  
|------------|----------------|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetBufferAdapter%2A>|将转换<xref:Microsoft.VisualStudio.Text.ITextBuffer>到<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetDataBuffer%2A>|将转换<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>到<xref:Microsoft.VisualStudio.Text.ITextBuffer>。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetDocumentBuffer%2A>|将转换<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>到<xref:Microsoft.VisualStudio.Text.ITextBuffer>。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetViewAdapter%2A>|将转换<xref:Microsoft.VisualStudio.Text.Editor.ITextView>到<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetWpfTextView%2A>|将转换<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>到<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView>。|  
  
## <a name="creating-adapters"></a>创建适配器  
 使用以下方法创建的旧接口的适配器。  
  
|方法|转换|  
|------------|----------------|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsCodeWindowAdapter%2A>|创建 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextBufferAdapter%2A>|创建<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>为指定<xref:Microsoft.VisualStudio.Utilities.IContentType>。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextBufferAdapter%2A>|创建 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextBufferCoordinatorAdapter%2A>|创建 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator>。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextViewAdapter%2A>|创建<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>为<xref:Microsoft.VisualStudio.Text.Editor.ITextViewRoleSet>。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextViewAdapter%2A>|创建 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>。|  
  
## <a name="creating-adapters-in-unmanaged-code"></a>在非托管代码中创建适配器  
 注册适配器的所有类是在本地共同创建的可以通过使用实例化`VsLocalCreateInstance()`函数。  
  
 通过使用 vsshlids.h 文件中定义的 Guid 创建所有适配器...Visual Studio SDK 安装的 \VisualStudioIntegration\Common\Inc\ 文件夹。 若要创建的 VsTextBufferAdapter 实例，请使用下面的代码。  
  
```  
IVsTextBuffer *pBuf = NULL;  
VsLocalCreateInstance(CLSID_VsTextBuffer, NULL, CLSCTX_INPROC_SERVER, IID_IVsTextBuffer, (void**)&pBuf);  
```  
  
## <a name="creating-adapters-in-managed-code"></a>在托管代码中创建适配器  
 在托管代码中，你可以共同创建适配器，所述的非托管代码的方式相同。 此外可以使用允许你创建并与适配器交互的 MEF 服务。 获取适配器的这种方式使不是共同创建时具有的更精细地控制。  
  
#### <a name="to-create-an-adapter-for-ivstextview"></a>若要为 IVsTextView 创建适配器  
  
1. 添加对 Microsoft.VisualStudio.Editor.dll 的引用。 请确保`CopyLocal`设置为`false`。  
  
2. 实例化<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>，按如下所示。  
  
    ```  
    using Microsoft.VisualStudio.Editor;  
    ...  
    IVsEditorAdaptersFactoryService adapterFactoryService = ComponentModel.GetService<IVsEditorAdaptersFactoryService>();  
    ```  
  
3. 调用 `CreateX()` 方法。  
  
    ```  
    adapterFactoryService.CreateTextViewAdapter(textView);  
    ```  
  
## <a name="using-the-visual-studio-editor-directly-from-unmanaged-code"></a>使用非托管代码中直接在 Visual Studio 编辑器  
 Microsoft.VisualStudio.Platform.VSEditor 命名空间和 Microsoft.VisualStudio.Platform.VSEditor.Interop 命名空间作为 IVx * 接口公开可调用 COM 接口。 例如，Microsoft.VisualStudio.Platform.VSEditor.Interop.IVxTextBuffer 接口是 COM 版本<xref:Microsoft.VisualStudio.Text.ITextBuffer>接口。 从`IVxTextBuffer`，可以有权访问缓冲区快照、 修改缓冲区、 侦听的文本更改事件对缓冲区，以及创建跟踪点和跨度。 以下步骤演示如何访问`IVxTextBuffer`从`IVsTextBuffer`。  
  
#### <a name="to-get-an-ivxtextbuffer"></a>若要获取 IVxTextBuffer  
  
1. IVx * 接口的定义是在 VSEditor.h 文件...Visual Studio SDK 安装的 \VisualStudioIntegration\Common\Inc\ 文件夹。  
  
2. 通过使用下面的代码实例化的文本缓冲区`IVsUserData->GetData()`方法。 在下面的代码中，`pData`是一个指向`IVsUserData`对象。  
  
    ```  
    #include <textmgr.h>  
    #include <VSEditor.h>  
    #include <vsshlids.h>  
  
    CComPtr<IVsTextBuffer> pVsTextBuffer;  
    CComPtr<IVsUserData> pData;  
    CComPtr<IVxTextBuffer> pVxBuffer;  
    ...  
    if (SUCCEEDED(pVsTextBuffer->QueryInterface(IID_IVsUserData, &pData))  
    {  
        CComVariant vt;  
        if (SUCCEEDED(pData->GetData(GUID_VxTextBuffer, &vt)) &&  
        (vt.Type == VT_UNKNOWN) && (vt.punkVal != NULL))  
        {  
            vt.punkVal->QueryInterface(IID_IVxTextBuffer, (void**)&pVxBuffer);  
        }  
    }  
    ```  
  
## <a name="using-visual-studio-editor-services-in-a-non-mef-component"></a>在非 MEF 组件中使用 Visual Studio 编辑器服务  
 如果您有现有的托管的代码组件不使用 MEF，并且你想要使用 Visual Studio 编辑器的服务，必须添加对包含 ComponentModelHost VSPackage 的程序集的引用，并获取其 SComponentModel 服务。  
  
#### <a name="to-consume-visual-studio-editor-components-from-a-non-mef-component"></a>若要使用 Visual Studio 编辑器组件从非 MEF 组件  
  
1. 添加对中的 Microsoft.VisualStudio.ComponentModelHost.dll 程序集的引用...Visual Studio 安装的 \Common7\IDE\ 文件夹。 请确保`CopyLocal`设置为`false`。  
  
2. 添加一个私有`IComponentModel`到想要使用 Visual Studio 编辑器服务，按如下所示的类的成员。  
  
    ```  
    using Microsoft.VisualStudio.ComponentModelHost;  
    ....  
    private IComponentModel componentModel;  
    ```  
  
3. 实例化组件的初始化方法中的组件模型。  
  
    ```  
    componentModel =  
     (IComponentModel)Package.GetGlobalService(typeof(SComponentModel));  
    ```  
  
4. 在此之后，可以调用可获取 Visual Studio 编辑器服务的任何一个`IComponentModel.GetService<T>()`所需的服务的方法。  
  
    ```  
    textBufferFactoryService =  
         componentModel.GetService<ITextBufferFactoryService>();     
    ```
