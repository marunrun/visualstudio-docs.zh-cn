---
title: 使旧代码适应编辑器 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184921"
---
# <a name="adapting-legacy-code-to-the-editor"></a>根据编辑器调整旧代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 编辑器提供了许多可以从现有代码组件访问的功能。 下面的说明演示如何调整非 MEF 组件（例如 VSPackage）以使用编辑器功能。 说明还演示了如何使用适配器在托管和非托管代码中获取编辑器的服务。  
  
## <a name="editor-adapters"></a>编辑器适配器  
 编辑器适配器（或填充程序）是编辑器对象的包装器，它们也公开 API 中的类和接口 <xref:Microsoft.VisualStudio.TextManager.Interop> 。 可以使用适配器在非编辑器服务之间移动，例如 Visual Studio shell 命令和编辑器服务。  (这是当前在 Visual Studio 中承载该编辑器的方式。 ) 适配器还允许旧编辑器和语言服务扩展在 Visual Studio 中正常工作。  
  
## <a name="using-editor-adapters"></a>使用编辑器适配器  
 <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>提供一些方法，这些方法可在新的编辑器接口和旧接口之间切换，还提供用于创建适配器的方法。  
  
 如果在 MEF 组件部分中使用此服务，可以按如下所示导入服务。  
  
```  
[Import(typeof(IVsEditorAdaptersFactoryService))]  
internal IVsEditorAdaptersFactoryService editorFactory;  
```  
  
 如果要在非 MEF 组件中使用此服务，请按照本主题后面的 "在非 MEF 组件中使用 Visual Studio 编辑器服务" 一节中的说明进行操作。  
  
## <a name="switching-between-the-new-editor-api-and-the-legacy-api"></a>在新编辑器 API 和旧 API 之间切换  
 使用以下方法在编辑器对象和旧接口之间切换。  
  
|方法|转换|  
|------------|----------------|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetBufferAdapter%2A>|将 <xref:Microsoft.VisualStudio.Text.ITextBuffer> 转换为 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetDataBuffer%2A>|将 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> 转换为 <xref:Microsoft.VisualStudio.Text.ITextBuffer>。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetDocumentBuffer%2A>|将 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> 转换为 <xref:Microsoft.VisualStudio.Text.ITextBuffer>。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetViewAdapter%2A>|将 <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 转换为 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetWpfTextView%2A>|将 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 转换为 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView>。|  
  
## <a name="creating-adapters"></a>创建适配器  
 使用以下方法为旧版接口创建适配器。  
  
|方法|转换|  
|------------|----------------|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsCodeWindowAdapter%2A>|创建 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextBufferAdapter%2A>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>为指定的创建 <xref:Microsoft.VisualStudio.Utilities.IContentType> 。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextBufferAdapter%2A>|创建 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextBufferCoordinatorAdapter%2A>|创建 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator>。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextViewAdapter%2A>|为 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 创建一个 <xref:Microsoft.VisualStudio.Text.Editor.ITextViewRoleSet>。|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextViewAdapter%2A>|创建 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>。|  
  
## <a name="creating-adapters-in-unmanaged-code"></a>在非托管代码中创建适配器  
 所有适配器类都注册为本地可创建的，并且可以使用函数进行实例化 `VsLocalCreateInstance()` 。  
  
 所有适配器都是使用中 vsshlids 文件中定义的 Guid 创建的。Visual Studio SDK 安装的 \VisualStudioIntegration\Common\Inc\ 文件夹。 若要创建 VsTextBufferAdapter 的实例，请使用以下代码。  
  
```  
IVsTextBuffer *pBuf = NULL;  
VsLocalCreateInstance(CLSID_VsTextBuffer, NULL, CLSCTX_INPROC_SERVER, IID_IVsTextBuffer, (void**)&pBuf);  
```  
  
## <a name="creating-adapters-in-managed-code"></a>在托管代码中创建适配器  
 在托管代码中，你可以采用与非托管代码所述相同的方式来创建适配器。 你还可以使用 MEF 服务，该服务允许你创建适配器并与之进行交互。 通过这种方式，适配器可以实现比共同创建适配器更精细的控制。  
  
#### <a name="to-create-an-adapter-for-ivstextview"></a>为 IVsTextView 创建适配器  
  
1. 添加对 Microsoft.VisualStudio.Editor.dll 的引用。 请确保将 `CopyLocal` 设置为 `false`。  
  
2. 实例化 <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> ，如下所示。  
  
    ```  
    using Microsoft.VisualStudio.Editor;  
    ...  
    IVsEditorAdaptersFactoryService adapterFactoryService = ComponentModel.GetService<IVsEditorAdaptersFactoryService>();  
    ```  
  
3. 调用 `CreateX()` 方法。  
  
    ```  
    adapterFactoryService.CreateTextViewAdapter(textView);  
    ```  
  
## <a name="using-the-visual-studio-editor-directly-from-unmanaged-code"></a>直接从非托管代码使用 Visual Studio 编辑器  
 VisualStudio 命名空间和 VSEditor 命名空间都将可调用 COM 的接口作为 IVx * 接口公开提供。 例如，IVxTextBuffer 接口是接口的 COM 版本。 VisualStudio 接口是接口的 COM 版本。 <xref:Microsoft.VisualStudio.Text.ITextBuffer> 从中 `IVxTextBuffer` ，你可以访问缓冲快照、修改缓冲区、侦听缓冲区中的文本更改事件，并创建跟踪点和跨度。 以下步骤演示如何 `IVxTextBuffer` 从访问 `IVsTextBuffer` 。  
  
#### <a name="to-get-an-ivxtextbuffer"></a>获取 IVxTextBuffer  
  
1. IVx * 接口的定义位于中的 VSEditor 文件中。Visual Studio SDK 安装的 \VisualStudioIntegration\Common\Inc\ 文件夹。  
  
2. 以下代码使用方法实例化文本缓冲区 `IVsUserData->GetData()` 。 在下面的代码中， `pData` 是指向对象的指针 `IVsUserData` 。  
  
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
 如果你有一个不使用 MEF 的现有托管代码组件，并且你想要使用 Visual Studio 编辑器的服务，则必须添加对包含 ComponentModelHost VSPackage 的程序集的引用并获取其 SComponentModel 服务。  
  
#### <a name="to-consume-visual-studio-editor-components-from-a-non-mef-component"></a>从非 MEF 组件使用 Visual Studio 编辑器组件  
  
1. 向中的 Microsoft.VisualStudio.ComponentModelHost.dll 程序集添加引用。Visual Studio 安装的 \Common7\IDE\ 文件夹。 请确保将 `CopyLocal` 设置为 `false`。  
  
2. 将私有 `IComponentModel` 成员添加到要在其中使用 Visual Studio 编辑器服务的类，如下所示。  
  
    ```  
    using Microsoft.VisualStudio.ComponentModelHost;  
    ....  
    private IComponentModel componentModel;  
    ```  
  
3. 在组件的初始化方法中实例化组件模型。  
  
    ```  
    componentModel =  
     (IComponentModel)Package.GetGlobalService(typeof(SComponentModel));  
    ```  
  
4. 此后，你可以通过对所需服务调用方法获取任何一个 Visual Studio 编辑器服务 `IComponentModel.GetService<T>()` 。  
  
    ```  
    textBufferFactoryService =  
         componentModel.GetService<ITextBufferFactoryService>();     
    ```
