---
title: 添加和删除属性页 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- property pages, adding
- property pages, project subtypes
- property pages, removing
ms.assetid: 34853412-ab8a-4caa-9601-7d0727b2985d
caps.latest.revision: 30
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 98838f09df3094e16d5f1a18263ffdad603ded0b
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440142"
---
# <a name="adding-and-removing-property-pages"></a>添加和删除属性页
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

项目设计器提供了用于管理项目属性、 设置和中的资源的集中的位置[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 它显示为中的单个窗口[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]集成开发环境 (IDE)，并包含可通过在左侧选项卡来访问在右侧窗格的数目。 在项目设计器中 （通常称为属性页） 的窗格因项目类型和语言而异。 可以通过访问项目设计器**属性**命令**项目**菜单。  
  
 项目子类型常常需要在项目设计器中显示附加属性页。 同样，某些项目子类型可能需要删除的内置属性页。 若要执行，项目子类型必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>接口并重写<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>方法。 通过重写此方法并使用`propId`参数，其中包含的值之一<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>枚举，可以筛选、 添加或删除项目属性。 例如，您可能需要将页面添加到依赖于配置的属性页。 若要执行此操作，需要筛选依赖于配置的属性页，然后将新页面添加到现有列表。  
  
## <a name="adding-and-removing-property-pages-in-project-designer"></a>添加和删除项目设计器中的属性页  
  
#### <a name="to-remove-a-property-page-in-project-designer"></a>若要在项目设计器中删除属性页  
  
1. 重写`GetProperty(uint itemId, int propId, out object property)`方法筛选属性页并获取`clsids`列表。  
  
    ```vb  
    Protected Overrides int GetProperty(uint itemId, int propId, out object property)  
    Protected Overrides Function GetProperty(ByVal itemId As UInteger, ByVal propId As Integer, ByRef [property] As Object) As Integer  
        'Use propId to filter configuration-independent property pages.  
        Select Case propId  
            ....   
            Case CInt(Fix(__VSHPROPID2.VSHPROPID_PropertyPagesCLSIDList))  
                'Get a semicolon-delimited list of clsids of the configuration-independent property pages  
                ErrorHandler.ThrowOnFailure(MyBase.GetProperty(itemId, propId, [property]))  
                   Dim propertyPagesList As String = ((String)[property]).ToUpper(CultureInfo.InvariantCulture)  
                'Remove the property page here  
                   ....  
            ....  
        End Select  
            ....   
        Return MyBase.GetProperty(itemId, propId, [property])  
    End Function  
  
    ```  
  
    ```csharp  
    protected override int GetProperty(uint itemId, int propId, out object property)  
    {  
        //Use propId to filter configuration-independent property pages.  
        switch (propId)  
        {  
            . . . .  
  
            case (int)__VSHPROPID2.VSHPROPID_PropertyPagesCLSIDList:  
                {  
                    //Get a semicolon-delimited list of clsids of the configuration-independent property pages  
                    ErrorHandler.ThrowOnFailure(base.GetProperty(itemId, propId, out property));  
                    string propertyPagesList = ((string)property).ToUpper(CultureInfo.InvariantCulture);  
                    //Remove the property page here  
                    . . . .  
                }  
             . . . .  
         }  
            . . . .  
        return base.GetProperty(itemId, propId, out property);  
    }  
    ```  
  
2. 删除**生成事件**页上从获取`clsids`列表。  
  
    ```vb  
    Private buildEventsPageGuid As String = "{1E78F8DB-6C07-4D61-A18F-7514010ABD56}"  
    Private index As Integer = propertyPagesList.IndexOf(buildEventsPageGuid)  
    If index <> -1 Then  
        ' GUIDs are separated by ';' so if you remove the last GUID, also remove the last ';'  
        Dim index2 As Integer = index + buildEventsPageGuid.Length + 1  
        If index2 >= propertyPagesList.Length Then  
            propertyPagesList = propertyPagesList.Substring(0, index).TrimEnd(";"c)  
        Else  
            propertyPagesList = propertyPagesList.Substring(0, index) + propertyPagesList.Substring(index2)  
        End If  
    End If  
    'New property value  
    property = propertyPagesList  
    ```  
  
    ```csharp  
    string buildEventsPageGuid = "{1E78F8DB-6C07-4D61-A18F-7514010ABD56}";  
    int index = propertyPagesList.IndexOf(buildEventsPageGuid);  
    if (index != -1)  
    {  
        // GUIDs are separated by ';' so if you remove the last GUID, also remove the last ';'  
        int index2 = index + buildEventsPageGuid.Length + 1;  
        if (index2 >= propertyPagesList.Length)  
            propertyPagesList = propertyPagesList.Substring(0, index).TrimEnd(';');  
        else  
            propertyPagesList = propertyPagesList.Substring(0, index) + propertyPagesList.Substring(index2);  
    }  
    //New property value  
    property = propertyPagesList;  
    ```  
  
#### <a name="to-add-a-property-page-in-project-designer"></a>若要在项目设计器中添加属性页  
  
1. 创建你想要添加的属性页。  
  
    ```vb  
    Class DeployPropertyPage  
            Inherits Form  
            Implements Microsoft.VisualStudio.OLE.Interop.IPropertyPage  
        'Summary: Return a stucture describing your property page.  
        ....   
        Public Sub GetPageInfo(ByVal pPageInfo As Microsoft.VisualStudio.OLE.Interop.PROPPAGEINFO())  
            Dim info As PROPPAGEINFO = New PROPPAGEINFO()  
            info.cb = CUInt(Marshal.SizeOf(GetType(PROPPAGEINFO)))  
            info.dwHelpContext = 0  
            info.pszDocString = Nothing  
            info.pszHelpFile = Nothing  
            info.pszTitle = "Deployment" 'Assign tab name  
            info.SIZE.cx = Me.Size.Width  
            info.SIZE.cy = Me.Size.Height  
            If Not pPageInfo Is Nothing AndAlso pPageInfo.Length > 0 Then  
                pPageInfo(0) = info  
            End If  
        End Sub  
    End Class  
    ```  
  
    ```csharp  
    class DeployPropertyPage : Form, Microsoft.VisualStudio.OLE.Interop.IPropertyPage  
    {  
        . . . .   
        //Summary: Return a stucture describing your property page.  
        public void GetPageInfo(Microsoft.VisualStudio.OLE.Interop.PROPPAGEINFO[] pPageInfo)  
        {  
            PROPPAGEINFO info = new PROPPAGEINFO();  
            info.cb = (uint)Marshal.SizeOf(typeof(PROPPAGEINFO));  
            info.dwHelpContext = 0;  
            info.pszDocString = null;  
            info.pszHelpFile = null;  
            info.pszTitle = "Deployment";  //Assign tab name  
            info.SIZE.cx = this.Size.Width;  
            info.SIZE.cy = this.Size.Height;  
            if (pPageInfo != null && pPageInfo.Length > 0)  
                pPageInfo[0] = info;  
        }  
    }  
    ```  
  
2. 注册新的属性页。  
  
    ```vb  
    <MSVSIP.ProvideObject(GetType(DeployPropertyPage), RegisterUsing = RegistrationMethod.CodeBase)>  
    ```  
  
    ```csharp  
    [MSVSIP.ProvideObject(typeof(DeployPropertyPage), RegisterUsing = RegistrationMethod.CodeBase)]  
    ```  
  
3. 重写`GetProperty(uint itemId, int propId, out object property)`方法来筛选器属性页中，获取`clsids`列出，添加新的属性页。  
  
    ```vb  
    Protected Overrides Function GetProperty(ByVal itemId As UInteger, ByVal propId As Integer, ByRef [property] As Object) As Integer  
        'Use propId to filter configuration-dependent property pages.  
        Select Case propId  
            ....   
            case CInt(Fix(__VSHPROPID2.VSHPROPID_CfgPropertyPagesCLSIDList)):  
                'Get a semicolon-delimited list of clsids of the configuration-dependent property pages.  
                ErrorHandler.ThrowOnFailure(MyBase.GetProperty(itemId, propId, [property]))  
                'Add the Deployment property page.  
                [property] &= ";"c + GetType(DeployPropertyPage).GUID.ToString("B")  
        End Select  
            ....   
            Return MyBase.GetProperty(itemId, propId, [property])  
    End Function  
    ```  
  
    ```csharp  
    protected override int GetProperty(uint itemId, int propId, out object property)  
    {  
        //Use propId to filter configuration-dependent property pages.  
        switch (propId)  
        {  
            . . . .  
            case (int)__VSHPROPID2.VSHPROPID_CfgPropertyPagesCLSIDList:  
                {  
                    //Get a semicolon-delimited list of clsids of the configuration-dependent property pages.  
                    ErrorHandler.ThrowOnFailure(base.GetProperty(itemId, propId, out property));  
                    //Add the Deployment property page.  
                    property += ';' + typeof(DeployPropertyPage).GUID.ToString("B");  
                }  
         }  
            . . . .  
        return base.GetProperty(itemId, propId, out property);  
    }  
    ```  
  
> [!NOTE]
> 本主题中提供的所有代码示例都是一个更大示例的组成部分[VSSDK 示例](../misc/vssdk-samples.md)。  
  
## <a name="see-also"></a>请参阅  
 [项目子类型](../extensibility/internals/project-subtypes.md)
