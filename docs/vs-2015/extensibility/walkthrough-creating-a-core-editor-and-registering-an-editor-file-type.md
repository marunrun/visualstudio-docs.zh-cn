---
title: 演练：创建核心编辑器和注册编辑器文件类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - walkthrough
ms.assetid: 24d2bffd-a35c-46db-8515-fd60b884b7fb
caps.latest.revision: 30
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 14296aa335ba6710d4d9eac8e5338af7463c0aac
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687638"
---
# <a name="walkthrough-creating-a-core-editor-and-registering-an-editor-file-type"></a>演练：创建核心编辑器和注册编辑器文件类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练演示如何创建启动 VSPackage[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]核心编辑器具有.myext 文件扩展名的文件时已加载。  
  
## <a name="prerequisites"></a>系统必备  
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。  
  
## <a name="locations-for-the-visual-studio-package-project-template"></a>在 Visual Studio 包项目模板位置  
 可在“新建项目”  对话框中的三个不同位置找到 Visual Studio 包项目模板：  
  
1. 在“Visual Basic 扩展性”之下。 项目的默认语言为 Visual Basic。  
  
2. 在“C# 扩展性”之下。 项目的默认语言为 C#。  
  
3. 在“其他项目类型扩展性”之下。 项目的默认语言为 C++。  
  
### <a name="to-create-the-vspackage"></a>若要创建 VSPackage  
  
- 启动[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]并创建[!INCLUDE[csprcs](../includes/csprcs-md.md)]名为 VSPackage `MyPackage`，如中所述[演练：创建菜单命令 VSPackage](https://msdn.microsoft.com/d699c149-5d1e-47ff-94c7-e1222af02c32)。  
  
### <a name="to-add-the-editor-factory"></a>若要添加编辑器工厂  
  
1. 右键单击**MyPackage**项目，指向**添加**，然后单击**类**。  
  
2. 在中**添加新项**对话框框中，请确保**类**选择模板，则类型`EditorFactory.cs`作为名称，然后单击**添加**将类添加到你的项目。  
  
     应会自动打开 EditorFactory.cs 文件。  
  
3. 在代码中引用以下程序集。  
  
    ```vb  
    Imports System.Runtime.InteropServices  
    Imports Microsoft.VisualStudio  
    Imports Microsoft.VisualStudio.Shell  
    Imports Microsoft.VisualStudio.Shell.Interop  
    Imports Microsoft.VisualStudio.OLE.Interop  
    Imports Microsoft.VisualStudio.TextManager.Interop  
    Imports IOleServiceProvider = Microsoft.VisualStudio.OLE.Interop.IServiceProvider  
    ```  
  
    ```csharp  
    using System.Runtime.InteropServices;  
    using Microsoft.VisualStudio;  
    using Microsoft.VisualStudio.Shell;  
    using Microsoft.VisualStudio.Shell.Interop;  
    using Microsoft.VisualStudio.OLE.Interop;  
    using Microsoft.VisualStudio.TextManager.Interop;  
    using IOleServiceProvider = Microsoft.VisualStudio.OLE.Interop.IServiceProvider;  
  
    ```  
  
4. 添加将 GUID 传递给`EditorFactory`类添加`Guid`立即在类声明的属性。  
  
     您可以使用 guidgen.exe 随时生成新的 GUID[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]的命令提示符，或通过单击**创建 GUID**上**工具**菜单。 此处使用的 GUID 是仅为示例;不要在项目中使用它。  
  
    ```vb  
    <Guid("0eea3187-c5fa-48d4-aa72-b5eecd3b17b1")> _  
    ```  
  
    ```csharp  
    [Guid("0eea3187-c5fa-48d4-aa72-b5eecd3b17b1")]   
    ```  
  
5. 在类定义中，添加两个私有变量来包含父包和服务提供程序。  
  
    ```vb  
    Class EditorFactory  
        Private parentPackage As Package  
        Private serviceProvider As IOleServiceProvider  
    ```  
  
    ```csharp  
    class EditorFactory  
    {  
        private Package parentPackage;  
        private IOleServiceProvider serviceProvider;  
    }  
  
    ```  
  
6. 添加接受一个参数的类型的公共类构造函数<xref:Microsoft.VisualStudio.Shell.Package>:  
  
    ```vb  
    Public Sub New(ByVal parentPackage As Package)  
        Me.parentPackage = parentPackage  
    End Sub  
    ```  
  
    ```csharp  
    public EditorFactory(Package parentPackage)  
    {  
        this.parentPackage = parentPackage;  
    }  
    ```  
  
7. 修改`EditorFactory`类声明为派生<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>接口。  
  
    ```vb  
    Class EditorFactory Implements IVsEditorFacto  
    ```  
  
    ```csharp  
    class EditorFactory : IVsEditorFactory  
  
    ```  
  
8. 右键单击<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>，单击**实现接口**，然后单击**显式实现接口**。  
  
     这会添加必须实现中的四种方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>接口。  
  
9. 将 `IVsEditorFactory.Close` 方法的内容替换为以下代码。  
  
    ```vb  
    Return VSConstants.S_OK  
    ```  
  
    ```csharp  
    return VSConstants.S_OK;  
    ```  
  
10. 内容替换为`IVsEditorFactory.SetSite`用下面的代码。  
  
    ```vb  
    Me.serviceProvider = psp  
    Return VSConstants.S_OK  
    ```  
  
    ```csharp  
    this.serviceProvider = psp;  
    return VSConstants.S_OK;  
    ```  
  
11. 将 `IVsEditorFactory.MapLogicalView` 方法的内容替换为以下代码。  
  
    ```vb  
    Dim retval As Integer = VSConstants.E_NOTIMPL  
    pbstrPhysicalView = Nothing ' We support only one view.  
    If rguidLogicalView.Equals(VSConstants.LOGVIEWID_Designer)OrElse _  
    rguidLogicalView.Equals(VSConstants.LOGVIEWID_Primary) Then  
        retval = VSConstants.S_OK  
    End If  
    Return retval  
    ```  
  
    ```csharp  
    int retval = VSConstants.E_NOTIMPL;  
    pbstrPhysicalView = null;   // We support only one view.  
    if (rguidLogicalView.Equals(VSConstants.LOGVIEWID_Designer) ||  
    rguidLogicalView.Equals(VSConstants.LOGVIEWID_Primary))  
    {  
        retval = VSConstants.S_OK;  
    }  
    return retval;  
    ```  
  
12. 将 `IVsEditorFactory.CreateEditorInstance` 方法的内容替换为以下代码。  
  
    ```vb  
    Dim retval As Integer = VSConstants.E_FAIL          
  
    ' Initialize these to empty to start with   
    ppunkDocView = IntPtr.Zero  
    ppunkDocData = IntPtr.Zero  
    pbstrEditorCaption = ""  
    pguidCmdUI = Guid.Empty  
    pgrfCDW = 0  
  
    If (grfCreateDoc And (VSConstants.CEF_OPENFILE Or _  
    VSConstants.CEF_SILENT)) = 0 Then  
        Throw New ArgumentException("Only Open or Silent is valid")  
    End If  
    If punkDocDataExisting <> IntPtr.Zero Then  
        Return VSConstants.VS_E_INCOMPATIBLEDOCDATA  
    End If  
  
    ' Instantiate a text buffer of type VsTextBuffer.   
    ' Note: we only need an IUnknown (object) interface for   
    ' this invocation.   
    Dim clsidTextBuffer As Guid = GetType(VsTextBufferClass).GUID  
    Dim iidTextBuffer As Guid = VSConstants.IID_IUnknown  
    Dim pTextBuffer As Object = pTextBuffer = _  
    parentPackage.CreateInstance(clsidTextBuffer, iidTextBuffer, _  
    GetType(Object))  
  
    If Not pTextBuffer Is Nothing Then  
        ' "Site" the text buffer with the service provider we were   
        ' provided.   
        Dim textBufferSite As IObjectWithSite = TryCast(pTextBuffer, _  
        IObjectWithSite)  
        If Not textBufferSite Is Nothing Then  
            textBufferSite.SetSite(Me.serviceProvider)  
        End If  
  
        ' Instantiate a code window of type IVsCodeWindow.   
        Dim clsidCodeWindow As Guid = GetType(VsCodeWindowClass).GUID  
        Dim iidCodeWindow As Guid = GetType(IVsCodeWindow).GUID  
        Dim pCodeWindow As IVsCodeWindow = _  
        CType(Me.parentPackage.CreateInstance(clsidCodeWindow, _  
        iidCodeWindow, GetType(IVsCodeWindow)), IVsCodeWindow)  
        If Not pCodeWindow Is Nothing Then  
            ' Give the text buffer to the code window.   
            ' We are giving up ownership of the text buffer!   
            pCodeWindow.SetBuffer(CType(pTextBuffer, IVsTextLines))  
  
            ' Now tell the caller about all this new stuff   
            ' that has been created.   
            ppunkDocView = Marshal.GetIUnknownForObject(pCodeWindow)  
            ppunkDocData = Marshal.GetIUnknownForObject(pTextBuffer)  
  
            ' Specify the command UI to use so keypresses are   
            ' automatically dealt with.   
            pguidCmdUI = VSConstants.GUID_TextEditorFactory  
  
            ' This caption is appended to the filename and   
            ' lets us know our invocation of the core editor   
            ' is up and running.   
            pbstrEditorCaption = " [MyPackage]"  
  
            retval = VSConstants.S_OK  
        End If  
    End If  
    Return retval  
    ```  
  
    ```csharp  
    int retval = VSConstants.E_FAIL;  
  
    // Initialize these to empty to start with  
    ppunkDocView       = IntPtr.Zero;  
    ppunkDocData       = IntPtr.Zero;  
    pbstrEditorCaption = "";  
    pguidCmdUI         = Guid.Empty;   
    pgrfCDW            = 0;  
  
    if ((grfCreateDoc & (VSConstants.CEF_OPENFILE |   
          VSConstants.CEF_SILENT)) == 0)  
    {   
        throw new ArgumentException("Only Open or Silent is valid");  
    }  
    if (punkDocDataExisting != IntPtr.Zero)  
    {  
        return VSConstants.VS_E_INCOMPATIBLEDOCDATA;  
    }  
  
    // Instantiate a text buffer of type VsTextBuffer.  
    // Note: we only need an IUnknown (object) interface for   
    // this invocation.  
    Guid clsidTextBuffer = typeof(VsTextBufferClass).GUID;  
    Guid iidTextBuffer   = VSConstants.IID_IUnknown;  
    object pTextBuffer   = pTextBuffer = parentPackage.CreateInstance(  
          ref clsidTextBuffer,  
          ref iidTextBuffer,  
          typeof(object));  
  
    if (pTextBuffer != null)  
    {  
        // "Site" the text buffer with the service provider we were  
        // provided.  
        IObjectWithSite textBufferSite = pTextBuffer as IObjectWithSite;  
        if (textBufferSite != null)  
        {  
            textBufferSite.SetSite(this.serviceProvider);  
        }  
  
        // Instantiate a code window of type IVsCodeWindow.  
        Guid clsidCodeWindow = typeof(VsCodeWindowClass).GUID;  
        Guid iidCodeWindow   = typeof(IVsCodeWindow).GUID;  
        IVsCodeWindow pCodeWindow =  
        (IVsCodeWindow)this.parentPackage.CreateInstance(   
              ref clsidCodeWindow,  
              ref iidCodeWindow,  
              typeof(IVsCodeWindow));  
        if (pCodeWindow != null)  
        {  
            // Give the text buffer to the code window.  
            // We are giving up ownership of the text buffer!  
            pCodeWindow.SetBuffer((IVsTextLines)pTextBuffer);  
  
            // Now tell the caller about all this new stuff   
            // that has been created.  
            ppunkDocView = Marshal.GetIUnknownForObject(pCodeWindow);  
            ppunkDocData = Marshal.GetIUnknownForObject(pTextBuffer);  
  
            // Specify the command UI to use so keypresses are   
            // automatically dealt with.  
            pguidCmdUI = VSConstants.GUID_TextEditorFactory;  
  
            // This caption is appended to the filename and  
            // lets us know our invocation of the core editor   
            // is up and running.  
            pbstrEditorCaption = " [MyPackage]";  
  
            retval = VSConstants.S_OK;  
        }   
    }   
    return retval;   
    ```  
  
13. 编译该项目，并确保没有任何错误。  
  
### <a name="to-register-the-editor-factory"></a>若要注册编辑器工厂  
  
1. 在**解决方案资源管理器**，双击要打开到字符串表，该表中的 Resources.resx 文件条目**String1 为**选定。  
  
2. 更改名称的标识符`IDS_EDITORNAME`和文本到**MyPackage 编辑器。** 此字符串将显示为您的编辑器的名称。  
  
3. 打开 VSPackage.resx 文件并添加一个新字符串，将名称设置为**101**到`IDS_EDITORNAME`。 这样，包使用的资源 ID 访问刚刚创建的字符串。  
  
    > [!NOTE]
    > 如果 VSPackage.resx 文件包含另一个字符串`name`属性设置为**101**，替换另一个唯一的数字值，在此处以及以下步骤中。  
  
4. 在中**解决方案资源管理器**，打开 MyPackagePackage.cs 文件。  
  
     这是主要包文件。  
  
5. 之前添加以下用户属性`Guid`属性。  
  
    ```vb  
    <ProvideEditorFactoryAttribute(GetType(EditorFactory), 101)> _  
    <ProvideEditorExtensionAttribute(GetType(EditorFactory), _  
          ".myext", 32, NameResourceID:=101 )> _  
    ```  
  
    ```csharp  
    [ProvideEditorFactory(typeof(EditorFactory), 101)]  
    [ProvideEditorExtension(typeof(EditorFactory),   
          ".myext", 32, NameResourceID = 101)]   
    ```  
  
     <xref:Microsoft.VisualStudio.Shell.ProvideEditorExtensionAttribute>属性将相关联的.myext 文件扩展名与编辑器工厂，以便任何时候，只要具有加载扩展插件、 调用编辑器工厂的文件。  
  
6. 添加到一个私有变量`MyPackage`类，构造函数中之前，并为其提供类型`EditorFactory`。  
  
    ```vb  
    Private editorFactory As EditorFactory  
    ```  
  
    ```csharp  
    private EditorFactory editorFactory;  
    ```  
  
7. 查找`Initialize`方法 (可能需要打开`Package Members`隐藏的区域)，并在调用后添加以下代码`base.Initialize()`。  
  
    ```vb  
    'Create our editor factory and register it.   
    Me.editorFactory = New EditorFactory(Me)  
    MyBase.RegisterEditorFactory(Me.editorFactory)  
    ```  
  
    ```csharp  
    // Create our editor factory and register it.  
    this.editorFactory = new EditorFactory(this);  
    base.RegisterEditorFactory(this.editorFactory);  
  
    ```  
  
8. 编译此程序，并确保没有任何错误。  
  
     此步骤在实验注册表配置单元注册编辑器工厂[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 如果系统提示重写 resource.h 文件，请单击**确定**。  
  
9. 创建一个名为 TextFile1.myext 的示例文件。  
  
10. 按**F5**若要打开的实验实例[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。  
  
11. 在实验性[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，然后在**文件**菜单中，依次指向**打开**，然后单击**文件**。  
  
12. 查找 TextFile1.myext，然后单击**打开**。  
  
     现在应加载的文件。  
  
## <a name="robust-programming"></a>可靠编程  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]核心编辑器处理各种基于文本的文件类型和语言服务，以提供一套丰富的功能，如语法突出显示，大括号匹配和 IntelliSense 文字自动完成和成员完成列表与紧密协作。 如果您正在使用基于文本的文件，您可以使用以及自定义语言服务支持特定的文件类型的核心编辑器。  
  
 VSPackage 可以调用[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]核心编辑器通过提供一个编辑器工厂。 加载与之相关联的文件时，即使用此编辑器工厂。 如果文件是项目的一部分，核心编辑器自动被调用除非你的 VSPackage 被重写。 但是，如果在项目外部加载文件，然后核心编辑器必须显式由调用你的 VSPackage。  
  
 有关核心编辑器的详细信息，请参阅[内核心编辑器](../extensibility/inside-the-core-editor.md)。  
  
## <a name="see-also"></a>请参阅  
 [在核心编辑器](../extensibility/inside-the-core-editor.md)   
 [使用旧 API 实例化核心编辑器](../extensibility/instantiating-the-core-editor-by-using-the-legacy-api.md)
