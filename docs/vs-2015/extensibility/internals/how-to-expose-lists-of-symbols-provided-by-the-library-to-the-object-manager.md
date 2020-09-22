---
title: 如何：将库提供的符号列表公开到对象管理器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- IVsSimpleLibrary2 interface, lists of symbols
- IVsLibrary2 interface, lists of symbols
- symbols, call browser
- lists, symbols for the object manager
- symbols, exposing lists to the object manager
ms.assetid: 19757068-bdaa-4e7e-85d6-f8ce5026a859
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 888ffbf255816fb04d84cb72219df2cfeae73f45
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840619"
---
# <a name="how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager"></a>如何：向对象管理器公开库提供的符号列表
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

符号浏览工具、 **类视图**、 **对象浏览器**、 **调用浏览器** 和 **查找符号结果**会将新数据的请求传递给 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 对象管理器。 对象管理器查找适当的库，并请求新的符号列表。 这些库通过接口向对象管理器提供请求的数据来做出响应 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> 。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]对象管理器调用接口中的方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> 来获取数据，并使用它来填充或更新符号浏览工具的视图。  
  
 在调用工具、展开节点或刷新视图时，库可能会获取数据请求。 第一次调用符号浏览工具时，对象管理器会请求库提供顶级列表。 当用户展开列表节点时，库将提供该节点下的子节点列表。 每个对象管理器查询都包含相关项的索引。 若要显示新列表，对象管理器必须确定列表中有多少项、项目的类型、名称、辅助功能和其他属性。  
  
> [!NOTE]
> 下面的托管代码示例演示如何通过实现接口来提供符号列表 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> 。 对象管理器调用此接口中的方法，并使用获取的数据填充或更新符号浏览工具。  
>   
> 对于本机代码符号提供程序实现，请使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectList2> 接口。  
  
## <a name="providing-lists-of-symbols-to-the-object-manager"></a>向对象管理器提供符号列表  
  
#### <a name="to-provide-lists-of-symbols-to-the-object-manager"></a>向对象管理器提供符号列表  
  
1. 通过实现方法来获取符号列表中的项数 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetItemCount%2A> 。 下面的示例演示对象管理器如何获取列表中项的数量信息。  
  
    ```vb  
    Protected m_Methods As System.Collections.Generic.SortedList(Of String, Method) = New System.Collections.Generic.SortedList(Of String, Method)()  
  
    Public Function GetItemCount(ByRef pCount As UInteger) As Integer  
        pCount = CUInt(m_Methods.Count)  
        Return Microsoft.VisualStudio.VSConstants.S_OK  
    End Function  
    ```  
  
    ```csharp  
    protected System.Collections.Generic.SortedList<string, Method> m_Methods = new System.Collections.Generic.SortedList<string, Method>();  
  
    public int GetItemCount(out uint pCount)  
    {  
        pCount = (uint)m_Methods.Count;  
        return Microsoft.VisualStudio.VSConstants.S_OK;  
    }  
  
    ```  
  
2. 通过实现方法获取有关给定列表项的类别和特性的信息 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetCategoryField2%2A> 。 项类别是在枚举中指定的 <xref:Microsoft.VisualStudio.Shell.Interop.LIB_CATEGORY> 。 下面的示例演示对象管理器如何获取给定类别的项的特性。  
  
    ```vb  
    Public Function GetCategoryField2(ByVal index As UInteger, ByVal Category As Integer, ByRef pfCatField As UInteger) As Integer  
        pfCatField = 0  
  
        Select Case CType(Category, LIB_CATEGORY)  
            Case LIB_CATEGORY.LC_MEMBERTYPE  
                pfCatField = CUInt(_LIBCAT_MEMBERTYPE.LCMT_METHOD)  
  
            Case LIB_CATEGORY.LC_MEMBERACCESS  
                Dim method As Method = m_Methods.Values(CInt(Fix(index)))  
  
                If method.IsPublic Then  
                    pfCatField = CUInt(_LIBCAT_MEMBERACCESS.LCMA_PUBLIC)  
                ElseIf method.IsPrivate Then  
                    pfCatField = CUInt(_LIBCAT_MEMBERACCESS.LCMA_PRIVATE)  
                ElseIf method.IsFamily Then  
                    pfCatField = CUInt(_LIBCAT_MEMBERACCESS.LCMA_PROTECTED)  
                ElseIf method.IsFamilyOrAssembly Then  
                    pfCatField = CUInt(_LIBCAT_MEMBERACCESS.LCMA_PROTECTED) Or CUInt(_LIBCAT_MEMBERACCESS.LCMA_PACKAGE)  
                Else  
                    ' Show everything else as internal.  
                    pfCatField = CUInt(_LIBCAT_MEMBERACCESS.LCMA_PACKAGE)  
                End If  
  
            Case LIB_CATEGORY.LC_VISIBILITY  
                pfCatField = CUInt(_LIBCAT_VISIBILITY.LCV_VISIBLE)  
  
            Case LIB_CATEGORY.LC_LISTTYPE  
                pfCatField = CUInt(_LIB_LISTTYPE.LLT_MEMBERS)  
  
            Case Else  
                Return Microsoft.VisualStudio.VSConstants.S_FALSE  
        End Select  
        Return Microsoft.VisualStudio.VSConstants.S_OK  
    End Function  
    ```  
  
    ```csharp  
    public int GetCategoryField2(uint index, int Category, out uint pfCatField)  
    {  
        pfCatField = 0;  
  
        switch ((LIB_CATEGORY)Category)  
        {  
            case LIB_CATEGORY.LC_MEMBERTYPE:  
                pfCatField = (uint)_LIBCAT_MEMBERTYPE.LCMT_METHOD;  
                break;  
  
            case LIB_CATEGORY.LC_MEMBERACCESS:  
                {  
                    Method method = m_Methods.Values[(int)index];  
  
                    if (method.IsPublic)  
                    {  
                        pfCatField = (uint)_LIBCAT_MEMBERACCESS.LCMA_PUBLIC;  
                    }  
                    else if (method.IsPrivate)  
                    {  
                        pfCatField = (uint)_LIBCAT_MEMBERACCESS.LCMA_PRIVATE;  
                    }  
                    else if (method.IsFamily)  
                    {  
                        pfCatField = (uint)_LIBCAT_MEMBERACCESS.LCMA_PROTECTED;  
                    }  
                    else if (method.IsFamilyOrAssembly)  
                    {  
                        pfCatField = (uint)_LIBCAT_MEMBERACCESS.LCMA_PROTECTED |  
                                     (uint)_LIBCAT_MEMBERACCESS.LCMA_PACKAGE;  
                    }  
                    else  
                    {  
                        // Show everything else as internal.  
                        pfCatField = (uint)_LIBCAT_MEMBERACCESS.LCMA_PACKAGE;  
                    }  
                }  
                break;  
  
            case LIB_CATEGORY.LC_VISIBILITY:  
                pfCatField = (uint)_LIBCAT_VISIBILITY.LCV_VISIBLE;  
                break;  
  
            case LIB_CATEGORY.LC_LISTTYPE:  
                pfCatField = (uint)_LIB_LISTTYPE.LLT_MEMBERS;  
                break;  
  
            default:  
                return Microsoft.VisualStudio.VSConstants.S_FALSE;  
        }  
        return Microsoft.VisualStudio.VSConstants.S_OK;  
    }  
  
    ```  
  
3. 通过实现方法来获取给定列表项的文本表示形式 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetTextWithOwnership%2A> 。 下面的示例演示如何获取给定项的完整名称。  
  
    ```vb  
    Public Function GetTextWithOwnership(<System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.OLE.Interop.ULONG")> ByVal index As UInteger, <System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.Shell.Interop.VSTREETEXTOPTIONS")> ByVal tto As Microsoft.VisualStudio.Shell.Interop.VSTREETEXTOPTIONS, <System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.OLE.Interop.WCHAR")> ByRef ppszText As String) As Integer  
        ppszText = m_Methods.Values(CInt(Fix(index))).FullName  
        Return Microsoft.VisualStudio.VSConstants.S_OK  
    End Function  
    ```  
  
    ```csharp  
    public int GetTextWithOwnership([System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.OLE.Interop.ULONG")] uint index, [System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.Shell.Interop.VSTREETEXTOPTIONS")] Microsoft.VisualStudio.Shell.Interop.VSTREETEXTOPTIONS tto, [System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.OLE.Interop.WCHAR")] out string ppszText)  
    {  
        ppszText = m_Methods.Values[(int)index].FullName;  
        return Microsoft.VisualStudio.VSConstants.S_OK;  
    }  
  
    ```  
  
4. 通过实现方法获取给定列表项的图标信息 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetDisplayData%2A> 。 图标表示类型 (类、方法等) 以及列表项)  (private、public 等辅助功能。 下面的示例演示如何根据给定的项特性获取图标信息。  
  
    ```vb  
    Public Overridable Function GetDisplayData(ByVal index As UInteger, ByVal pData As Microsoft.VisualStudio.Shell.Interop.VSTREEDISPLAYDATA()) As Integer  
        If pData Is Nothing Then  
            Return Microsoft.VisualStudio.VSConstants.E_INVALIDARG  
        End If  
  
        Dim method As Method = m_Methods.Values(CInt(Fix(index)))  
  
        Dim iImage As Integer = 12 * 6 ' See env\inc\OMGlyphs.h.  
  
        Const OM_GLYPH_ACC_PUBLIC As Integer = 0  
        Const OM_GLYPH_ACC_INTERNAL As Integer = 1  
        Const OM_GLYPH_ACC_PROTECTED As Integer = 3  
        Const OM_GLYPH_ACC_PRIVATE As Integer = 4  
  
        If method.IsPublic Then  
            iImage += OM_GLYPH_ACC_PUBLIC  
        ElseIf method.IsPrivate Then  
            iImage += OM_GLYPH_ACC_PRIVATE  
        ElseIf method.IsFamily Then  
            iImage += OM_GLYPH_ACC_PROTECTED  
        ElseIf method.IsFamilyOrAssembly Then  
            iImage += OM_GLYPH_ACC_PROTECTED  
        Else  
            iImage += OM_GLYPH_ACC_INTERNAL  
        End If  
  
        pData(0).Image = CUShort(iImage)  
        pData(0).SelectedImage = CUShort(iImage)  
  
        Return Microsoft.VisualStudio.VSConstants.S_OK  
    End Function  
    ```  
  
    ```csharp  
    public virtual int GetDisplayData(uint index, Microsoft.VisualStudio.Shell.Interop.VSTREEDISPLAYDATA[] pData)  
    {  
        if (pData == null)  
        {  
            return Microsoft.VisualStudio.VSConstants.E_INVALIDARG;  
        }  
  
        Method method = m_Methods.Values[(int)index];  
  
        int iImage = 12 * 6;    // See env\inc\OMGlyphs.h.  
  
        const int OM_GLYPH_ACC_PUBLIC = 0;  
        const int OM_GLYPH_ACC_INTERNAL = 1;  
        const int OM_GLYPH_ACC_PROTECTED = 3;  
        const int OM_GLYPH_ACC_PRIVATE = 4;  
  
        if (method.IsPublic)  
        {  
            iImage += OM_GLYPH_ACC_PUBLIC;  
        }  
        else if (method.IsPrivate)  
        {  
            iImage += OM_GLYPH_ACC_PRIVATE;  
        }  
        else if (method.IsFamily)  
        {  
            iImage += OM_GLYPH_ACC_PROTECTED;  
        }  
        else if (method.IsFamilyOrAssembly)  
        {  
            iImage += OM_GLYPH_ACC_PROTECTED;  
        }  
        else  
        {  
            iImage += OM_GLYPH_ACC_INTERNAL;  
        }  
  
        pData[0].Image = (ushort)iImage;  
        pData[0].SelectedImage = (ushort)iImage;  
  
        return Microsoft.VisualStudio.VSConstants.S_OK;  
    }  
  
    ```  
  
5. 获取有关给定列表项是否可通过实现方法进行扩展的信息 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetExpandable3%2A> 。 下面的示例演示如何获取有关是否可以展开给定项的信息。  
  
    ```vb  
    Public Function GetExpandable(ByVal index As UInteger, ByRef pfExpandable As Integer) As Integer  
        pfExpandable = Microsoft.VisualStudio.VSIP.Samples.CallBrowser.Constants.TRUE  
        Return Microsoft.VisualStudio.VSConstants.S_OK  
    End Function  
  
    Public Function GetExpandable3(ByVal index As UInteger, ByVal ListTypeExcluded As UInteger, ByRef pfExpandable As Integer) As Integer  
        Return GetExpandable(index, pfExpandable)  
    End Function  
    ```  
  
    ```csharp  
    public int GetExpandable(uint index, out int pfExpandable)  
    {  
        pfExpandable = Microsoft.VisualStudio.VSIP.Samples.CallBrowser.Constants.TRUE;  
        return Microsoft.VisualStudio.VSConstants.S_OK;  
    }  
  
    public int GetExpandable3(uint index, uint ListTypeExcluded, out int pfExpandable)  
    {  
        return GetExpandable(index, out pfExpandable);  
    }  
  
    ```  
  
6. 通过实现方法获取给定列表项的子符号的子列表 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetList2%2A> 。 下面的示例演示如何获取 **调用** 或 **调用方** 关系图的给定项的子符号列表。  
  
    ```vb  
    ' Call graph list.  
    Public Class CallsList  
        Inherits ResultsList  
        Implements Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2  
        Public Sub New(ByVal library As Library)  
            MyBase.New(library)  
        End Sub  
  
        Public Function GetList2(ByVal index As UInteger, ByVal ListType As UInteger, ByVal flags As UInteger, ByVal pobSrch As Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2(), ByRef ppList As Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2) As Integer  
            Return MyBase.GetCallsList(index, ppList)  
        End Function  
    End Class  
  
    ' Callers graph list.  
    Public Class CallersList  
        Inherits ResultsList  
        Implements Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2  
        Public Sub New(ByVal library As Library)  
            MyBase.New(library)  
        End Sub  
  
        Public Function GetList2(ByVal index As UInteger, ByVal ListType As UInteger, ByVal flags As UInteger, ByVal pobSrch As Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2(), ByRef ppList As Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2) As Integer  
            Return MyBase.GetCallersList(index, ppList)  
        End Function  
    End Class  
  
    ' Call graph list.  
    Public Function GetCallsList(ByVal index As UInteger, ByRef ppList As Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2) As Integer  
        ppList = Nothing  
        Dim callsList As ResultsList = New CallsList(m_Library)  
  
        Dim method As Method = m_Methods.Values(CInt(Fix(index)))  
        Dim strMethod As String = method.m_strPrototype  
  
        Dim Calls As System.Collections.Generic.List(Of CallInstance) = m_Library.CallGraph.GetCallGraph(method)  
  
        For i As Integer = 0 To Calls.Count - 1  
            Dim caller As Method = Calls(i).m_Target  
            callsList.AddMethod(caller)  
        Next i  
  
        ppList = CType(callsList, Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2)  
        Return Microsoft.VisualStudio.VSConstants.S_OK  
    End Function  
  
    ' Callers graph list.  
    Public Function GetCallersList(ByVal index As UInteger, ByRef ppList As Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2) As Integer  
        ppList = Nothing  
        Dim callersList As ResultsList = New CallersList(m_Library)  
  
        Dim method As Method = m_Methods.Values(CInt(Fix(index)))  
        Dim strMethod As String = method.m_strPrototype  
  
        Dim Callers As System.Collections.Generic.List(Of CallInstance) = m_Library.CallGraph.GetCallersGraph(method)  
  
        For i As Integer = 0 To Callers.Count - 1  
            Dim caller As Method = Callers(i).m_Source  
            callersList.AddMethod(caller)  
        Next i  
  
        ppList = CType(callersList, Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2)  
        Return Microsoft.VisualStudio.VSConstants.S_OK  
    End Function  
  
    ' Get a child list of symbols for a given list item.  
    Public Function GetList2(ByVal index As UInteger, ByVal ListType As UInteger, ByVal flags As UInteger, ByVal pobSrch As Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2(), ByRef ppList As Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2) As Integer  
        ppList = Nothing  
  
        Dim method As Method = m_Methods.Values(CInt(Fix(index)))  
        Dim strMethod As String = method.m_strPrototype  
  
        ' Determine if the list belongs to Call or Callers graphs.  
        If CUInt(m_nFlags And CUInt(Microsoft.VisualStudio.Shell.Interop._VSOBSEARCHOPTIONS2.VSOBSO_CALLSFROM)) > 0 Then  
            ' Build the list for the Call graph.  
            Return MyBase.GetCallsList(index, ppList)  
        ElseIf CUInt(m_nFlags And CUInt(Microsoft.VisualStudio.Shell.Interop._VSOBSEARCHOPTIONS2.VSOBSO_CALLSTO)) > 0 Then  
            ' Build the list for the Callers graph.  
            Return MyBase.GetCallersList(index, ppList)  
        End If  
  
        Return Microsoft.VisualStudio.VSConstants.E_FAIL  
    End Function  
    ```  
  
    ```csharp  
    // Call graph list.  
    public class CallsList :  
        ResultsList,  
        Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2  
    {  
        public CallsList(Library library) :  
            base(library)  
        {  
        }  
  
        public int GetList2(uint index, uint ListType, uint flags, Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2[] pobSrch, out Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2 ppList)  
        {  
            return base.GetCallsList(index, out ppList);  
        }  
    }  
  
    // Callers graph list.  
    public class CallersList :  
        ResultsList,  
        Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2  
    {  
        public CallersList(Library library) :  
            base(library)  
        {  
        }  
  
        public int GetList2(uint index, uint ListType, uint flags, Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2[] pobSrch, out Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2 ppList)  
        {  
            return base.GetCallersList(index, out ppList);  
        }  
    }  
  
    // Call graph list.  
    public int GetCallsList(uint index, out Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2 ppList)  
    {  
        ppList = null;  
        ResultsList callsList = new CallsList(m_Library);  
  
        Method method = m_Methods.Values[(int)index];  
        string strMethod = method.m_strPrototype;  
  
        System.Collections.Generic.List<CallInstance> Calls = m_Library.CallGraph.GetCallGraph(method);  
  
        for (int i = 0; i < Calls.Count; i++)  
        {  
            Method caller = Calls[i].m_Target;  
            callsList.AddMethod(caller);  
        }  
  
        ppList = (Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2)(callsList);  
        return Microsoft.VisualStudio.VSConstants.S_OK;  
    }  
  
    // Callers graph list.  
    public int GetCallersList(uint index, out Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2 ppList)  
    {  
        ppList = null;  
        ResultsList callersList = new CallersList(m_Library);  
  
        Method method = m_Methods.Values[(int)index];  
        string strMethod = method.m_strPrototype;  
  
        System.Collections.Generic.List<CallInstance> Callers = m_Library.CallGraph.GetCallersGraph(method);  
  
        for (int i = 0; i < Callers.Count; i++)  
        {  
            Method caller = Callers[i].m_Source;  
            callersList.AddMethod(caller);  
        }  
  
        ppList = (Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2)(callersList);  
        return Microsoft.VisualStudio.VSConstants.S_OK;  
    }  
  
    // Get a child list of symbols for a given list item.  
    public int GetList2(uint index, uint ListType, uint flags, Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2[] pobSrch, out Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2 ppList)  
    {  
        ppList = null;  
  
        Method method = m_Methods.Values[(int)index];  
        string strMethod = method.m_strPrototype;  
  
        // Determine if the list belongs to Call or Callers graphs.  
        if ((uint)(m_nFlags & (uint)Microsoft.VisualStudio.Shell.Interop._VSOBSEARCHOPTIONS2.VSOBSO_CALLSFROM) > 0)  
        {  
            // Build the list for the Call graph.  
            return base.GetCallsList(index, out ppList);  
        }  
        else if ((uint)(m_nFlags & (uint)Microsoft.VisualStudio.Shell.Interop._VSOBSEARCHOPTIONS2.VSOBSO_CALLSTO) > 0)  
        {  
            // Build the list for the Callers graph.  
            return base.GetCallersList(index, out ppList);  
        }  
  
        return Microsoft.VisualStudio.VSConstants.E_FAIL;  
    }  
  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)   
 [如何：向对象管理器注册库](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)   
 [如何：标识库中的符号](../../extensibility/internals/how-to-identify-symbols-in-a-library.md)   
 [旧版语言服务扩展性](../../extensibility/internals/legacy-language-service-extensibility.md)
