---
title: 如何：访问内置的字体和配色方案 |Microsoft Docs
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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65685310"
---
# <a name="how-to-access-the-built-in-fonts-and-color-scheme"></a>如何：访问内置的字体和配色方案
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 集成的开发环境 (IDE) 具有一种与编辑器窗口相关联的字体和颜色的方案。 您可以访问通过此方案<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>接口。  
  
 若要使用内置的字体和颜色方案，VSPackage 必须：  
  
- 定义要用于默认字体和颜色服务的类别。  
  
- 向默认字体和颜色服务器注册的类别。  
  
- 建议 IDE 特定窗口通过使用内置的显示项和类别`T:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer`和`T:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer`接口。  
  
  IDE 窗口的句柄作为使用生成的类别。 该类别的名称显示在**显示其设置：** 下拉列表框中的**字体和颜色**属性页。  
  
### <a name="to-define-a-category-using-built-in-fonts-and-colors"></a>若要定义使用内置的字体和颜色的类别  
  
1. 创建任意的 GUID。  
  
    使用此 GUID 来唯一地标识一个类别<strong>。</strong> IDE 的默认字体和颜色规范，将重新使用此类别。  
  
   > [!NOTE]
   > 检索使用字体和颜色数据时<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents>或其他接口的 Vspackage 使用此 GUID 来引用内置的信息。  
  
2. 该类别的名称必须添加到 VSPackage 的资源 (.rc) 文件内的字符串表中，以便可以根据需要在 IDE 中显示时进行本地化。  
  
    有关详细信息，请参阅[添加或删除字符串](https://msdn.microsoft.com/library/077077b4-0f4b-4633-92d6-60b321164cab)。  
  
### <a name="to-register-a-category-using-built-in-fonts-and-colors"></a>若要注册使用内置的字体和颜色的类别  
  
1. 构造一个特殊类型的类别中的以下位置的注册表条目：  
  
     [HKLM\SOFTWARE\Microsoft \Visual Studio\\*\<Visual Studio version>* \FontAndColors\\*\<Category>*]  
  
     *\<类别 >* 类别的非本地化名称。  
  
2. 填充注册表来使用的常用字体和配色方案包含四个值：  
  
    |名称|类型|数据|描述|  
    |----------|----------|----------|-----------------|  
    |类别|REG_SZ|GUID|标识包含股票的字体和配色方案的类别的任意 GUID。|  
    |package|REG_SZ|GUID|{F5E7E71D-1401-11D1-883B-0000F87579D2}<br /><br /> 此 GUID 可供所有使用默认的字体和颜色配置的 Vspackage。|  
    |NameID|REG_DWORD|Id|在 VSPackage 中的可本地化的类别名称的资源 ID。|  
    |ToolWindowPackage|REG_SZ|GUID|VSPackage 实现的 GUID<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>接口。|  
  
3. 
  
### <a name="to-initiate-the-use-of-system-provided-fonts-and-colors"></a>若要启动使用系统提供的字体和颜色  
  
1. 创建的实例`T:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer`接口作为窗口的实现和初始化的一部分。  
  
2. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer.GetPropertyCategory%2A>方法来获取的实例`T:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer`接口对应于当前<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>实例。  
  
3. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer.SetProperty%2A>两次。  
  
   - 使用一次调用`VSEDITPROPID_ViewGeneral_ColorCategory`作为自变量。  
  
   - 使用一次调用`VSEDITPROPID_ViewGeneral_FontCategory`作为自变量。  
  
     此设置，并将默认字体和颜色服务公开为窗口的属性。  
  
## <a name="example"></a>示例  
 下面的示例启动内置的字体和颜色的使用。  
  
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
  
## <a name="see-also"></a>请参阅  
 [使用字体和颜色](../extensibility/using-fonts-and-colors.md)   
 [获取字体和颜色信息对文本着色](../extensibility/getting-font-and-color-information-for-text-colorization.md)   
 [访问存储的字体和颜色设置](../extensibility/accessing-stored-font-and-color-settings.md)   
 [字体和颜色概述](../extensibility/font-and-color-overview.md)
