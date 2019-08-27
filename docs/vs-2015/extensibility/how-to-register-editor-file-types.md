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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204122"
---
# <a name="how-to-register-editor-file-types"></a>如何：注册编辑器文件类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要注册编辑器文件类型的最简单方法是使用作为的一部分提供的注册属性[!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)]托管包框架 (MPF) 类。 如果要在本机实现您的软件包[!INCLUDE[vcprvc](../includes/vcprvc-md.md)]，还可以编写注册表脚本注册你的编辑器和关联的扩展。  
  
## <a name="registration-using-mpf-classes"></a>注册使用 MPF 类  
  
#### <a name="to-register-editor-file-types-using-mpf-classes"></a>若要注册使用 MPF 类编辑器文件类型  
  
1. 提供<xref:Microsoft.VisualStudio.Shell.ProvideEditorExtensionAttribute>类编辑器在你的 VSPackage 的类中的相应参数。  
  
    ```  
    [Microsoft.VisualStudio.Shell.ProvideEditorExtensionAttribute(typeof(EditorFactory), ".Sample", 32,   
         ProjectGuid = "{A2FE74E1-B743-11d0-AE1A-00A0C90FFFC3}",   
         TemplateDir = "..\\..\\Templates",   
         NameResourceID = 106)]  
    ```  
  
     其中"。示例"是为此编辑器中，注册的扩展，"32"是其优先级别。  
  
     `projectGuid`中定义的其他文件类型的 guid <xref:Microsoft.VisualStudio.VSConstants.CLSID.MiscellaneousFilesProject_guid>。 杂项文件类型，以便生成的文件不会为生成过程的一部分提供。  
  
     `TemplateDir` 表示包含所托管的基本编辑器示例附带的模板文件的文件夹。  
  
     `NameResourceID` BasicEditorUI 项目 Resources.h 文件中定义并标识为"My 编辑器"编辑器。  
  
2. 重写 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 方法。  
  
     中的实现<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>方法中，调用<xref:Microsoft.VisualStudio.Shell.Package.RegisterEditorFactory%2A>方法并传递下面所示为编辑器工厂的实例。  
  
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
  
     此步骤中注册编辑器工厂和编辑器文件扩展名。  
  
3. 取消注册编辑器工厂。  
  
     当释放 VSPackage 时，编辑器工厂会自动注销。 如果编辑器工厂对象实现<xref:System.IDisposable>接口，其`Dispose`后工厂已被注销与调用方法[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。  
  
## <a name="registration-using-a-registry-script"></a>注册使用注册表脚本  
 在本机注册编辑器工厂和文件类型[!INCLUDE[vcprvc](../includes/vcprvc-md.md)]完成使用注册表脚本将写入 windows 注册表中，如以下所示。  
  
#### <a name="to-register-editor-file-types-using-a-registry-script"></a>若要注册使用注册表脚本编辑器的文件类型  
  
1. 在注册表脚本中，定义编辑器工厂和编辑器工厂的 GUID 字符串中所示`GUID_BscEditorFactory`部分中的以下注册表脚本。 此外，定义扩展插件和编辑器扩展的优先级：  
  
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
  
     在此示例中的编辑器文件扩展名标识为".rtf"并且其优先级为"50"。 Resource.h 文件的 BscEdit 示例项目中定义的 GUID 字符串。  
  
2. 将 VSPackage 注册。  
  
3. 注册编辑器工厂。  
  
     注册时使用的编辑器工厂<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A>实现。  
  
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
  
     在 Resource.h BscEdit 项目文件中定义的 GUID 字符串。
