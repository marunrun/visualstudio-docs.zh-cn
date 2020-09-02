---
title: 如何：注册编辑器文件类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - register file types
ms.assetid: 54846779-8290-48de-90ab-81011559d9a5
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8d22e61d88b5f6e3959a369f6957efbc824384b2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204122"
---
# <a name="how-to-register-editor-file-types"></a>如何：注册编辑器文件类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

注册编辑器文件类型最简单的方法是使用作为托管包框架的一部分提供的注册属性 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] (MPF) 类。 如果在本机中实现包 [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] ，还可以编写注册编辑器和关联扩展的注册表脚本。  
  
## <a name="registration-using-mpf-classes"></a>使用 MPF 类注册  
  
#### <a name="to-register-editor-file-types-using-mpf-classes"></a>使用 MPF 类注册编辑器文件类型  
  
1. <xref:Microsoft.VisualStudio.Shell.ProvideEditorExtensionAttribute>在 VSPackage 的类中为编辑器提供相应的参数。  
  
    ```  
    [Microsoft.VisualStudio.Shell.ProvideEditorExtensionAttribute(typeof(EditorFactory), ".Sample", 32,   
         ProjectGuid = "{A2FE74E1-B743-11d0-AE1A-00A0C90FFFC3}",   
         TemplateDir = "..\\..\\Templates",   
         NameResourceID = 106)]  
    ```  
  
     Where "。示例 "是为此编辑器注册的扩展，" 32 "是其优先级别。  
  
     `projectGuid`是在中定义的杂项文件类型的 GUID <xref:Microsoft.VisualStudio.VSConstants.CLSID.MiscellaneousFilesProject_guid> 。 提供了其他文件类型，因此，生成的文件不会成为生成过程的一部分。  
  
     `TemplateDir` 表示包含托管基本编辑器示例附带的模板文件的文件夹。  
  
     `NameResourceID` 在 BasicEditorUI 项目的 Resources .h 文件中定义，并将编辑器标识为 "My Editor"。  
  
2. 重写 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 方法。  
  
     在方法的实现中 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> ，调用 <xref:Microsoft.VisualStudio.Shell.Package.RegisterEditorFactory%2A> 方法并传递编辑器工厂的实例，如下所示。  
  
    ```  
    protected override void Initialize()  
    {  
        Trace.WriteLine (string.Format(CultureInfo.CurrentCulture,   
        "Entering Initialize() of: {0}", this.ToString()));  
        base.Initialize();  
           //Create Editor Factory  
        editorFactory = new EditorFactory(this);  
        base.RegisterEditorFactory(editorFactory);  
    }  
    ```  
  
     此步骤注册编辑器工厂和编辑器文件扩展名。  
  
3. 取消注册编辑器工厂。  
  
     处理 VSPackage 时，编辑器工厂会自动取消注册。 如果编辑器工厂对象实现 <xref:System.IDisposable> 接口，则在取消 `Dispose` 注册工厂后，将调用其方法 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。  
  
## <a name="registration-using-a-registry-script"></a>使用注册表脚本注册  
 在本机中注册编辑器工厂和文件类型 [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] 使用注册表脚本写入 windows 注册表，如下所示。  
  
#### <a name="to-register-editor-file-types-using-a-registry-script"></a>使用注册表脚本注册编辑器文件类型  
  
1. 在注册表脚本中，定义编辑器工厂和编辑器工厂 GUID 字符串，如 `GUID_BscEditorFactory` 以下注册表脚本的部分所示。 此外，还可以定义扩展插件和编辑器扩展的优先级：  
  
    ```  
  
          NoRemove Editors     {         %GUID_BscEditorFactory% = s 'RTF Editor'         {             val Package = s '%CLSID_Package%'             val DisplayName = s 'An RTF Editor'             val ExcludeDefTextEditor = d 1             val AcceptBinaryFiles = d 0  
  
            LogicalViews  
            {  
                val %LOGVIEWID_TextView% = s ''  
            }  
  
            OpenWithEntries  
            {  
            }  
  
            Extensions            {                val rtf = d 50            }  
        }  
    }  
    ```  
  
     此示例中的编辑器文件扩展名被标识为 ".rtf"，其优先级为 "50"。 GUID 字符串在 BscEdit 示例项目的 Resource .h 文件中定义。  
  
2. 注册 VSPackage。  
  
3. 注册编辑器工厂。  
  
     编辑器工厂在实现中注册 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A> 。  
  
    ```  
    // create editor factory.  
    if (m_srpEdFact == NULL)   
    {  
        CComObject<CBscEditorFactory> *pEdFact = new CComObject<CBscEditorFactory>;  
        if (NULL == pEdFact)  
          return E_OUTOFMEMORY;  
  
        if (!pEdFact->FInit(this))  
          return E_UNEXPECTED;  
  
        m_srpEdFact = (IVsEditorFactory *) pEdFact;    // Note: assignment to a smart pointer does an AddRef()  
    }  
    // Query service for IVsRegisterEditors, register the editor factory  
    CComPtr<IVsRegisterEditors> srpRegEd;  
    if ((SUCCEEDED(m_srpPkgSiteSP->QueryService(SID_SVsRegisterEditors, IID_IVsRegisterEditors,(void **)&srpRegEd ))) && (srpRegEd != NULL))  
      {  
        ATLTRACE(TEXT(">> CVsPackage, registering editor factory.\n"));  
          if (FAILED(srpRegEd->RegisterEditor(GUID_BscEditorFactory,  
                      m_srpEdFact, &m_dwEditorCookie)))   
          {  
             ATLTRACE(TEXT(">> CVsPackage, RegisterEditor() failed.\n"));  
            return E_FAIL;  
          }  
      }  
        return S_OK;  
    }  
    ```  
  
     GUID 字符串在 BscEdit 项目的 Resource .h 文件中定义。
