---
title: VSIX 颜色编译器 |Microsoft Docs
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 99395da7-ec34-491d-9baa-0590d23283ce
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c92fb2ad45bc0fb09c7e9bd8e87db38c13a99736
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546739"
---
# <a name="vsix-color-compiler"></a>VSIX 颜色编译器
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio Extension Color 编译器工具是一个控制台应用程序，它使用表示现有 Visual Studio 主题的颜色的 .xml 文件并将其将到 .pkgdef 文件，以便可以在 Visual Studio 中使用这些颜色。 由于比较 .xml 文件之间的差异很简单，因此此工具可用于管理源代码管理中的自定义颜色。 它还可以与生成环境挂钩，使生成的输出为有效的 .pkgdef 文件。  
  
 **主题 XML 架构**  
  
 完整的主题 .xml 文件如下所示：  
  
```xml  
<Themes>  
      <!—one or Theme elements -->  
      <Theme>  
        <!-- one or more Category elements -->  
        <Category>  
          <!-- one or more Color elements -->  
          <Color>  
            <!-- zero or one Background element -->  
            <Background />  
            <!-- zero or one Foreground element -->  
            <Foreground />  
          </Color>  
        </Category>  
      </Theme>  
</Themes>  
```  
  
 **主题**  
  
 \<Theme>元素定义整个主题。 主题必须包含至少一个 \<Category> 元素。 主题元素定义如下：  
  
```xml  
<Theme Name="name" GUID="guid">  
      <!-- one or more Category elements -->  
</Theme>  
```  
  
|**特性**|**定义**|  
|-|-|  
|名称|请求主题的名称|  
|GUID|请求主题的 GUID （必须匹配 GUID 格式）|  
  
 为 Visual Studio 创建自定义颜色时，需要为以下主题定义这些颜色。 如果特定主题没有任何颜色，Visual Studio 会尝试从浅色主题中加载缺少的颜色。  
  
|**主题名称**|**主题 GUID**|  
|-|-|  
|亮|{de3dbbcd-f642-433c-8353-8f1df4370aba}|  
|暗|{1ded0138-47ce-435e-84ef-9ec1f439b749}|  
|蓝色|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|  
|高对比度|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|  
  
 **类别**  
  
 \<Category>元素定义主题中的颜色的集合。 类别名称提供逻辑分组，并且应尽可能将其定义为最窄。 类别必须至少包含一个 \<Color> 元素。 类别元素定义如下：  
  
```xml  
<Category Name="name" GUID="guid">  
      <!-- one or more Color elements -->  
 </Category>  
```  
    
|**特性**|**定义**|  
|-|-|  
|名称|请求类别名称|  
|GUID|请求类别的 GUID （必须匹配 GUID 格式）|  
  
 **颜色**  
  
 \<Color>元素为 UI 的组件或状态定义颜色。 颜色的首选命名方案为 [UI 类型] [状态]。 不要使用 "color" 一词，因为它是多余的。 颜色应当清楚地指示元素类型以及将应用颜色的条件或 "状态"。 颜色不得为空，并且必须包含和元素中的一个或两个 \<Background> \<Foreground> 。 定义颜色元素的方式如下：  
  
```xml  
<Color Name="name">  
        <Background /> <!-- zero or one Background element -->  
        <Foreground /> <!-- zero or one Foreground element -->  
 </Color>  
```  
  
|**特性**|**定义**|  
|-|-|  
|名称|请求颜色的名称|  
  
 **背景和/或前台**  
  
 \<Background>和 \<Foreground> 元素定义颜色的值，并为 UI 元素的背景或前景类型定义类型。 这些元素没有任何子级。  
  
```xml  
<Background Type="type" Source="int" />  
<Foreground Type="type" Source="int" />  
```  
  
|**特性**|**定义**|  
|-|-|  
|类型|请求颜色的类型。 该参数可以是下列值之一：<br /><br /> *CT_INVALID：* 颜色无效或未设置。<br /><br /> *CT_RAW：* 原始 ARGB 值。<br /><br /> *CT_COLORINDEX：* 请勿使用。<br /><br /> *CT_SYSCOLOR：* SysColor 中的 Windows 系统颜色。<br /><br /> *CT_VSCOLOR：*__VSSYSCOLOREX 中的 Visual Studio 颜色。<br /><br /> *CT_AUTOMATIC：* 自动颜色。<br /><br /> *CT_TRACK_FOREGROUND：* 请勿使用。<br /><br /> *CT_TRACK_BACKGROUND：* 请勿使用。|  
|源|请求用十六进制表示的颜色的值|  
  
 Type 属性中的架构支持 __VSCOLORTYPE 枚举支持的所有值。 但是，我们建议你仅使用 CT_RAW 和 CT_SYSCOLOR。  
  
 **全部结合**  
  
 这是有效的主题 .xml 文件的一个简单示例：  
  
```xml  
<Themes>  
  <Theme Name="Light" GUID="{de3dbbcd-f642-433c-8353-8f1df4370aba}">  
    <Category Name="MyCategory" GUID="{0A96238B-70CE-4479-9170-EECEAA3FCD58}">  
      <Color Name="MyActiveBorder">  
        <Background Type="CT_RAW" Source="FFCCCEDB" />  
      </Color>  
    </Category>  
  </Theme>  
</Themes>  
```  
  
## <a name="how-to-use-the-tool"></a>如何使用该工具  
 **语法**  
  
 VsixColorCompiler \<XML file> \<PkgDef file>\<Optional Args>  
  
 **参数**  
  
|**交换机名称**|**说明**|**必需或可选**|  
|-|-|-|  
|未命名（.xml 文件）|这是第一个未命名的参数，是要转换的 XML 文件的路径。|必选|  
|未命名（.pkgdef 文件）|这是第二个未命名的参数，是生成的 .pkgdef 文件的输出路径。<br /><br /> 默认值： \<XML Filename> . .pkgdef|可选|  
|/noLogo|设置此标志将停止打印产品和版权信息。|可选|  
|/?|打印出帮助信息。|可选|  
|/help|打印出帮助信息。|可选|  
  
 **示例**  
  
- VsixColorCompiler D:\xml\colors.xml D:\pkgdef\colors.pkgdef  
  
- VsixColorCompiler D:\xml\colors.xml/noLogo  
  
## <a name="notes"></a>注意  
  
- 此工具需要安装最新版本的 VC + + 运行时。  
  
- 仅支持单个文件。 不支持通过文件夹路径进行的大容量转换。  
  
## <a name="sample-output"></a>示例输出  
 该工具生成的 .pkgdef 文件将类似于以下项：  
  
```  
[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\Environment]  
"Data"=hex:3a,00,00,00,0b,00,00,00,01,00,00,00,c3,d9,4e,62,fd,bd,fa,41,96,c3,7c,82,4e,a3,2e,3d,01,00,00,00,0c,00,00,00,41,63,74,69,76,65,42,6f,72,64,65,72,01,cc,ce,db,ff,01,33,31,24,ff  
  
[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\TreeView]  
"Data"=hex:38,00,00,00,0b,00,00,00,01,00,00,00,8e,f0,ec,92,13,8b,f4,4c,99,e9,ae,26,92,38,21,85,01,00,00,00,0a,00,00,00,42,61,63,6b,67,72,6f,75,6e,64,01,f5,f5,f5,ff,01,1e,1e,1e,ff  
```
