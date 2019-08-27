---
title: 本地化 VSIX 包 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- localize package
- localize extension
- localized deployment
ms.assetid: 10e80b13-b39e-466c-a7c8-774a862355af
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6143b21884bc92ac79ae0fd7292a11780fec4478
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63439762"
---
# <a name="localizing-vsix-packages"></a>本地化 VSIX 包
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过创建的每种目标语言 Extension.vsixlangpack 文件，然后将它们放在正确的文件夹，可以将本地化 VSIX 包。 安装本地化的包时，扩展插件的本地化的名称显示以及的本地化说明。 如果你提供本地化的许可证文件或指向的本地化信息的 URL，则它们也会显示。  
  
 如果内容 VSIX 包中包含 VSPackage 添加的菜单命令或其他 UI，请参阅[本地化菜单命令](../extensibility/localizing-menu-commands.md)有关本地化的新 UI 元素的信息。  
  
## <a name="directory-structure"></a>目录结构  
 当用户安装扩展**扩展和更新**检查其名称与目标计算机的 Visual Studio 区域设置相匹配的文件夹的 VSIX 包的最高级别。 如果**扩展和更新**找到了.vsixlangpack 文件文件夹中，它将替换为该文件以供的.vsixmanifest 文件中的相应值中的本地化的值。 在安装该扩展时，会显示这些值。 下面的示例显示了已本地化为西班牙语 (ES-ES) 和法语 (FR-FR) 的 VSIX 包的目录结构。  
  
 MyExtension.dll  
  
 Extension.vsixmanifest  
  
 [Content_Types].xml  
  
 es-ES  
  
 Extension.vsixlangpack  
  
 fr-FR  
  
 Extension.vsixlangpack  
  
> [!NOTE]
> 中的 VSIX 支持的项目模板[!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)]生成 VSIX 清单并将其命名 source.extension.vsixmanifest。 当 Visual Studio 生成项目时，它将复制该文件的内容到 Extension.VsixManifest VSIX 包中。  
  
## <a name="the-extensionvsixlangpack-file"></a>Extension.vsixlangpack 文件  
 Extension.vsixlangpack 文件遵循[VSIX 语言包架构](../extensibility/vsx-language-pack-schema-reference.md)。 此架构具有[VSIXLanguagePack](../extensibility/vsixlanguagepack-element-vsix-language-pack-schema.md)根元素，而且这些四个子元素：[LocalizedName](../extensibility/localizedname-element-vsix-language-pack-schema.md)， [LocalizedDescription](../extensibility/localizeddescription-element-vsix-language-pack-schema.md)， [MoreInfoURL](../extensibility/moreinfourl-element-vsix-language-pack-schema.md)，并且[许可证](../extensibility/license-element-vsix-language-pack-schema.md)。 这些子元素对应于`Name`， `Description`， `MoreInfoURL`，和`License`的子元素`Identifier`Extension.vsixmanifest 文件的元素。  
  
 在创建 vsixlangpack 文件时，必须设置`Include in Vsix`属性设置为`true`。 否则，将忽略的本地化的安装文本。  
  
#### <a name="to-set-the-include-in-vsix-property"></a>若要设置包括在 Vsix 属性  
  
1. 在中**解决方案资源管理器**，右键单击 Extension.vsixlangpack 文件，然后单击**属性**。  
  
2. 在属性网格中，单击**包含在 Vsix**，并将其值设置为`true`。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 下面的示例演示 Extension.vsixmanifest 文件，以及西班牙语的相应 Extension.vsixlangpack 文件的相关部分。 如果目标计算机的 Visual Studio 区域设置设置为西班牙语，语言包中的值替换在清单中的值。  
  
### <a name="code"></a>代码  
 [Extension.vsixmanifest]  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<VSIX ...>  
  <Identifier ...>  
    <Name>Family Tree</Name>  
    <Description>This extension places a custom treeview control in the toolbox that is optimized for handling family tree information.</Description>  
    <License>EULA.rtf</License>  
    <MoreInfoURL>http://www.contoso.com/products/FamilyTree.htm</MoreInfoURL>  
    ...  
  </Identifier>  
  <References .../>  
  <Content .../>  
</VSIX>  
```  
  
 [Extension.vsixlangpack]  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<VsixLanguagePack Version="1.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema-lp/2010">  
  <LocalizedName>Arbol de Familia</LocalizedName>  
  <LocalizedDescription> Esta extensión pone control personalizado en la caja de herramientas por manejar información de familia.</LocalizedDescription>  
  <License>es\Eula.rtf</License>  
  <MoreInfoUrl> http://www.contoso.com/products/es/ArbolDeFamilia.htm</MoreInfoUrl>  
</VsixLanguagePack>  
```  
  
## <a name="see-also"></a>请参阅  
 [VSIX LanguagePack 元素](../extensibility/vsixlanguagepack-element-vsix-language-pack-schema.md)   
 [VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)   
 [VSIX 项目模板](../extensibility/vsix-project-template.md)
