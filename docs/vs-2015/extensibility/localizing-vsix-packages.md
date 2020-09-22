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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840453"
---
# <a name="localizing-vsix-packages"></a>本地化 VSIX 包
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过为每个目标语言创建 vsixlangpack 文件，然后将其放在正确的文件夹中，来本地化 VSIX 包。 当安装本地化的包时，将显示该扩展的本地化名称以及本地化说明。 如果提供本地化的许可证文件或指向本地化信息的 URL，则它们也会显示。  
  
 如果内容你的 VSIX 包包含添加菜单命令或其他 UI 的 VSPackage，请参阅 [本地化菜单命令](../extensibility/localizing-menu-commands.md) 以获取有关本地化新 UI 元素的信息。  
  
## <a name="directory-structure"></a>目录结构  
 当用户安装扩展时， **扩展和更新** 将检查其名称与目标计算机的 Visual Studio 区域设置匹配的文件夹的 VSIX 包顶级。 如果 **扩展和更新** 在文件夹中找到 vsixlangpack 文件，则会将该文件中的本地化值替换为 source.extension.vsixmanifest 文件中的相应值。 安装扩展时，将显示这些值。 下面的示例演示了本地化为西班牙语 (es) 和法语 (fr-fr) 的 VSIX 包的目录结构。  
  
 MyExtension.dll  
  
 扩展名 source.extension.vsixmanifest  
  
 [Content_Types] .xml  
  
 es-ES  
  
 扩展名 vsixlangpack  
  
 fr-FR  
  
 扩展名 vsixlangpack  
  
> [!NOTE]
> [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)]生成 vsix 清单并将其命名为 source.extension.vsixmanifest 的支持 vsix 的项目模板。 当 Visual Studio 生成项目时，它会将该文件的内容复制到 VSIX 包的 Source.extension.vsixmanifest 中。  
  
## <a name="the-extensionvsixlangpack-file"></a>Vsixlangpack 文件  
 Vsixlangpack 文件遵循 [VSIX 语言包架构](../extensibility/vsx-language-pack-schema-reference.md)。 此架构具有一个 [VSIXLanguagePack](../extensibility/vsixlanguagepack-element-vsix-language-pack-schema.md) 根元素和以下四个子元素： [LocalizedName](../extensibility/localizedname-element-vsix-language-pack-schema.md)、 [LocalizedDescription](../extensibility/localizeddescription-element-vsix-language-pack-schema.md)、 [其他](../extensibility/moreinfourl-element-vsix-language-pack-schema.md)和 [License](../extensibility/license-element-vsix-language-pack-schema.md)。 这些子元素对应于 `Name` source.extension.vsixmanifest 文件的元素的、、 `Description` `MoreInfoURL` 和 `License` 子元素 `Identifier` 。  
  
 创建 vsixlangpack 文件时，必须将 `Include in Vsix` 属性设置为 `true` 。 否则，将忽略本地化安装文本。  
  
#### <a name="to-set-the-include-in-vsix-property"></a>设置 Include in Vsix 属性  
  
1. 在 **解决方案资源管理器**中，右键单击 vsixlangpack 文件，然后单击 " **属性**"。  
  
2. 在 "属性" 网格中，单击 " **在 Vsix 中包含**"，并将其值设置为 `true` 。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>说明  
 下面的示例显示 source.extension.vsixmanifest 文件的相关部分以及用于西班牙语的相应 vsixlangpack 文件。 如果目标计算机的 Visual Studio 区域设置为西班牙语，则语言包中的值将替换清单中的值。  
  
### <a name="code"></a>代码  
 [Source.extension.vsixmanifest]  
  
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
  
 [Vsixlangpack]  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<VsixLanguagePack Version="1.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema-lp/2010">  
  <LocalizedName>Arbol de Familia</LocalizedName>  
  <LocalizedDescription> Esta extensión pone control personalizado en la caja de herramientas por manejar información de familia.</LocalizedDescription>  
  <License>es\Eula.rtf</License>  
  <MoreInfoUrl> http://www.contoso.com/products/es/ArbolDeFamilia.htm</MoreInfoUrl>  
</VsixLanguagePack>  
```  
  
## <a name="see-also"></a>另请参阅  
 [VSIX LanguagePack 元素](../extensibility/vsixlanguagepack-element-vsix-language-pack-schema.md)   
 [VSIX 包的解析](../extensibility/anatomy-of-a-vsix-package.md)   
 [VSIX 项目模板](../extensibility/vsix-project-template.md)
