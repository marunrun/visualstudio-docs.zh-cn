---
title: 如何：取消文件更改通知 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - suppress file change notification
ms.assetid: 891c1eb4-f6d0-4073-8df0-2859dbd417ca
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3f045175eae165b75a887ada2716b19f34fc228b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204083"
---
# <a name="how-to-suppress-file-change-notifications"></a>如何：禁止显示文件更改通知
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果更改了表示文本缓冲区的物理文件，则会显示一个对话框，其中显示一条消息，提示 **你是否要保存对以下各项的更改？** 这称为 "文件更改通知"。 如果对文件进行了许多更改，则此对话框会反复显示，因而很快就会变得恼人。  
  
 您可以使用以下过程以编程方式禁止显示此对话框。 通过执行此操作，可以立即重新加载文件，而无需每次都提示用户保存更改。  
  
### <a name="to-suppress-file-change-notification"></a>禁止显示文件更改通知  
  
1. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> 方法以确定哪个文本缓冲区对象与打开的文件相关联。  
  
2. 定向 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 到内存中的对象，以忽略监视文件更改，方法是 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl> 从 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> (文档数据) 对象获取接口，然后通过 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl.IgnoreFileChanges%2A> `fIgnore` 将参数设置为来实现方法 `true` 。  
  
3. 调用上的方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> 和，并 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> 使用文件更改来更新内存中 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 对象 (例如，将字段添加到组件) 。  
  
4. 使用更改更新磁盘上的文件，而不考虑用户可能正在进行的任何挂起的编辑。  
  
     这样，当你指示 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 对象继续监视文件更改通知时，内存中的文本缓冲区会反映生成的更改以及所有其他挂起的编辑。 磁盘上的文件反映了你所生成的最新代码，以及用户在用户编辑代码中所做的任何以前保存的更改。  
  
5. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl.IgnoreFileChanges%2A> 方法， <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 通过将参数设置为，通知对象继续监视文件更改通知 `fIgnore` `false` 。  
  
6. 如果你计划对文件进行一些更改（如源代码管理 (SCC) 的情况），则必须告知全局文件更改服务暂时挂起文件更改通知。  
  
     例如，如果重写文件，然后更改时间戳，则必须挂起文件更改通知，因为每个操作都作为一个单独的文件更改事件进行计数。 若要启用全局文件更改通知，应改为调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx.IgnoreFile%2A> 方法。  
  
## <a name="example"></a>示例  
 下面演示了如何禁止显示文件更改通知。  
  
```cpp#  
//Misc. helper classes  
  
CSuspendFileChanges::CSuspendFileChanges(  
    /* [in] */ const CString& strMkDocument,   
    /* [in] */ BOOL fSuspendNow /* = TRUE */)   
:  
    m_strMkDocument(strMkDocument),  
    m_fFileChangeSuspended(FALSE)  
{  
    if(fSuspendNow)  
        Suspend();  
}  
CSuspendFileChanges::~CSuspendFileChanges()  
{  
    Resume();  
}  
void CSuspendFileChanges::Suspend()  
{  
    USES_CONVERSION;  
  
    // Prevent suspend from suspending more than once.  
    if(m_fFileChangeSuspended)  
        return;  
  
    IVsRunningDocumentTable* pRDT =   
      _VxModule.GetIVsRunningDocumentTable();  
    ASSERT(pRDT);  
    if (!pRDT)  
        return;  
  
    CComPtr<IUnknown> srpDocData;  
    VSCOOKIE vscookie = VSCOOKIE_NIL;  
    pRDT->FindAndLockDocument(RDT_NoLock, T2COLE(m_strMkDocument),    
      NULL, NULL, &srpDocData, &vscookie);  
    if ( (vscookie == VSCOOKIE_NIL) || !srpDocData)  
        return;  
    CComPtr<IVsFileChangeEx> srpIVsFileChangeEx;  
    HRESULT hr = _VxModule.QueryService(SID_SVsFileChangeEx,   
      IID_IVsFileChangeEx, (void **)&srpIVsFileChangeEx);  
    if (SUCCEEDED(hr) && srpIVsFileChangeEx)  
    {  
        m_fFileChangeSuspended = TRUE;  
        srpIVsFileChangeEx->IgnoreFile(NULL, m_strMkDocument, TRUE);   
        srpDocData->QueryInterface(IID_IVsDocDataFileChangeControl,   
          (void**)&m_srpIVsDocDataFileChangeControl);  
        if(m_srpIVsDocDataFileChangeControl)  
            m_srpIVsDocDataFileChangeControl->IgnoreFileChanges(TRUE);  
    }  
}  
void CSuspendFileChanges::Resume()  
{  
    if(!m_fFileChangeSuspended)  
        return;  
  
    CComPtr<IVsFileChangeEx> srpIVsFileChangeEx;  
    HRESULT hr = _VxModule.QueryService(SID_SVsFileChangeEx,   
      IID_IVsFileChangeEx, (void **)&srpIVsFileChangeEx);  
    if (SUCCEEDED(hr) && srpIVsFileChangeEx)  
  
    srpIVsFileChangeEx->IgnoreFile(NULL, m_strMkDocument, FALSE);   
    if(m_srpIVsDocDataFileChangeControl)  
        m_srpIVsDocDataFileChangeControl->IgnoreFileChanges(FALSE);  
    m_fFileChangeSuspended = FALSE;  
    m_srpIVsDocDataFileChangeControl.Release();  
}  
// Misc. helper classes  
```  
  
## <a name="robust-programming"></a>可靠编程  
 如果你的情况涉及对文件进行多次更改（如 SCC），则必须先恢复全局文件更改通知，然后才能提醒文档数据恢复对文件更改的监视。
