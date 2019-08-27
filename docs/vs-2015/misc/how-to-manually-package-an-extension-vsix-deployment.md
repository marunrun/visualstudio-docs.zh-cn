---
title: 如何：手动将扩展打包 （VSIX 部署） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
ms.assetid: d25990e0-e782-4a79-9d9a-1caf3c56c6a2
caps.latest.revision: 10
manager: jillfra
ms.openlocfilehash: e4d721fca8d429fe81de30306a8823e3d7fd9cab
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65681682"
---
# <a name="how-to-manually-package-an-extension-vsix-deployment"></a>如何：手动将扩展打包 （VSIX 部署）
可以创建 VSIX 包来包装 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展，以便进行部署。 创建包的方式有三种：  
  
- 使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] SDK 中包含的可扩展性模板之一创建 VSIX 包项目。 在大多数情况下，这是最简单的选项。  
  
- 将扩展项目的输出包装在一个空 [VSIX 项目](../extensibility/vsix-project-template.md)中。 对于模板、不受支持的程序集和自定义类型，建议使用此选项。  
  
- 手动创建 VSIX 包。 仅当其他两个选项不可用时，才建议使用此选项。  
  
  本文档介绍第三个选项。  
  
## <a name="creating-a-vsix-package"></a>创建 VSIX 包  
 若要手动对扩展打包，请向扩展项目中添加 extension.manifest 文件和 [Content_Types].xml 文件，将其与生成输出一起放在压缩文件中，并对压缩文件重命名，使其具有 .vsix 文件扩展名。 要打包的扩展必须是 [VSIX 架构](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)支持的类型。  
  
> [!NOTE]
> 在 VSIX 包中的文件的名称不能包含空格，也不保留在统一资源标识符 (URI)，作为字符定义下[ \[RFC2396\]](http://go.microsoft.com/fwlink/?LinkId=90339)。  
  
#### <a name="to-manually-create-a-vsix-package"></a>手动创建 VSIX 包  
  
1. 创建一个 Visual Studio 扩展，其类型受 VSIX 架构支持。  
  
2. 创建一个 XML 文件，将其命名为 `extension.vsixmanifest`。  
  
3. 根据 VSIX 架构填写 extension.vsixmanifest 文件。 有关示例清单，请参阅 [PackageManifest 元素（根元素，VSX 架构）](https://msdn.microsoft.com/f8ae42ba-775a-4d2b-976a-f556e147f187)。  
  
4. 再创建一个 XML 文件，将其命名为 `[Content_Types].xml`。  
  
5. 填写 [Content_Types].xml 文件中的规定[的结构 Content_types\].xml 文件](../extensibility/the-structure-of-the-content-types-dot-xml-file.md)。  
  
6. 将这两个 XML 文件与要部署的扩展一起放在某个目录。  
  
     如果是项目模板或项模板，则将包含该模板的 .zip 文件放在 XML 文件所在的文件夹中。 不要将 XML 文件放在 .zip 文件中。  
  
     在其他所有情况下，将 XML 文件放在生成输出所在的目录中。  
  
7. 在 Windows 资源管理器中，右键单击包含扩展内容和这两个 XML 文件的文件夹，单击“发送到” ，然后单击“压缩(zipped)文件夹” 。  
  
8. 将生成的 .zip 文件重命名为 *Filename*.vsix，其中 *Filename* 是用于安装包的可再发行文件的名称。  
  
## <a name="see-also"></a>请参阅  
 [传送 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)   
 [VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)   
 [PackageManifest 元素 （根元素，VSX 架构）](https://msdn.microsoft.com/f8ae42ba-775a-4d2b-976a-f556e147f187)