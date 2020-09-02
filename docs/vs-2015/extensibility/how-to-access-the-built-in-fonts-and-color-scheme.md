---
title: 如何：访问内置字体和配色方案 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- fonts, accessing built-in
- font and color control [Visual Studio SDK], categories
- colors, accessing built-in schemes
ms.assetid: 6905845e-e88e-4805-adcf-21da39108ec7
caps.latest.revision: 24
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a43fb3a22ecb2d04542eacf07bf883590868b75b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65685310"
---
# <a name="how-to-access-the-built-in-fonts-and-color-scheme"></a>如何：访问内置字体和配色方案
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 集成开发环境 (IDE) 具有与编辑器窗口关联的字体和颜色方案。 可以通过接口访问此方案 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 。  
  
 若要使用内置的字体和颜色方案，VSPackage 必须：  
  
- 定义要用于默认字体和颜色服务的类别。  
  
- 向默认的字体和颜色服务器注册类别。  
  
- 通过使用和接口，通知 IDE 特定窗口使用内置的显示项和类别 `T:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer` `T:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer` 。  
  
  IDE 使用生成的类别作为窗口的句柄。 类别的名称显示在 "**字体和颜色**" 属性页的 "**显示其设置：** " 下拉框中。  
  
### <a name="to-define-a-category-using-built-in-fonts-and-colors"></a>使用内置字体和颜色定义类别  
  
1. 创建一个任意 GUID。  
  
    此 GUID 用于唯一标识类别<strong>。</strong> 此类别重用 IDE 的默认字体和颜色规范。  
  
   > [!NOTE]
   > 当使用或其他接口检索字体和颜色数据时 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents> ，vspackage 将使用此 GUID 来引用内置信息。  
  
2. 必须将类别的名称添加到 VSPackage 的资源 () 文件中，以便可以在 IDE 中显示时根据需要对其进行本地化。  
  
    有关详细信息，请参阅 [添加或删除字符串](https://msdn.microsoft.com/library/077077b4-0f4b-4633-92d6-60b321164cab)。  
  
### <a name="to-register-a-category-using-built-in-fonts-and-colors"></a>使用内置字体和颜色注册类别  
  
1. 在以下位置构造一种特殊类型的类别注册表项：  
  
     [HKLM\SOFTWARE\Microsoft \Visual Studio \\ *\<Visual Studio version>* \FontAndColors \\ *\<Category>* ]  
  
     *\<Category>* 是类别的非本地化名称。  
  
2. 填充注册表以使用带有四个值的常用字体和配色方案：  
  
    |名称|类型|数据|说明|  
    |----------|----------|----------|-----------------|  
    |类别|REG_SZ|GUID|标识包含常用字体和配色方案的类别的任意 GUID。|  
    |包|REG_SZ|GUID|F5E7E71D-1401-11D1-883B-0000F87579D2<br /><br /> 此 GUID 由使用默认字体和颜色配置的所有 Vspackage 使用。|  
    |NameID|REG_DWORD|ID|VSPackage 中可本地化类别名称的资源 ID。|  
    |ToolWindowPackage|REG_SZ|GUID|实现接口的 VSPackage 的 GUID <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 。|  
  
3. 
  
### <a name="to-initiate-the-use-of-system-provided-fonts-and-colors"></a>启动系统提供的字体和颜色的使用  
  
1. 在 `T:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer` 窗口的实现和初始化过程中创建接口的实例。  
  
2. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer.GetPropertyCategory%2A> 方法以获取 `T:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer` 与当前实例相对应的接口实例 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 。  
  
3. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer.SetProperty%2A>两次调用。  
  
   - 作为参数调用一次 `VSEDITPROPID_ViewGeneral_ColorCategory` 。  
  
   - 作为参数调用一次 `VSEDITPROPID_ViewGeneral_FontCategory` 。  
  
     这会将默认字体和颜色服务作为窗口的属性进行设置和公开。  
  
## <a name="example"></a>示例  
 下面的示例启动了内置字体和颜色的使用。  
  
```  
CComVariant vt;  
CComQIPtr<IVsTextEditorPropertyCategoryContainer> spPropCatContainer(m_spView);  
if (spPropCatContainer != NULL){  
    CComPtr<IVsTextEditorPropertyContainer> spPropContainer;  
    if (SUCCEEDED(spPropCatContainer->GetPropertyCategory(GUID_EditPropCategory_View_MasterSettings,   
                                                          &spPropContainer))){  
        CComVariant vt;CComVariant VariantGUID(bstrGuidText);  
        spPropContainer->SetProperty(VSEDITPROPID_ViewGeneral_FontCategory, VariantGUID);  
        spPropContainer->SetProperty(VSEDITPROPID_ViewGeneral_ColorCategory, VariantGUID);  
    }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用字体和颜色](../extensibility/using-fonts-and-colors.md)   
 [获取文本着色的字体和颜色信息](../extensibility/getting-font-and-color-information-for-text-colorization.md)   
 [访问存储的字体和颜色设置](../extensibility/accessing-stored-font-and-color-settings.md)   
 [字体和颜色概述](../extensibility/font-and-color-overview.md)
