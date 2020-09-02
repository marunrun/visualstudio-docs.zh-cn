---
title: 如何：为 ClickOnce 应用程序创建文件关联 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- file associations, ClickOnce applications
- ClickOnce deployment, file associations
ms.assetid: 835230c8-3177-440f-85e3-e40f1d8b4f9d
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 82ffecdc719dad2f38208de00dc95438b3ff36ef
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697704"
---
# <a name="how-to-create-file-associations-for-a-clickonce-application"></a>如何：为 ClickOnce 应用程序创建文件关联
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序可以与一个或多个文件扩展名相关联，这样当用户打开这些类型的文件时，应用程序将自动启动。 向应用程序添加文件扩展名支持 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 非常简单。  
  
### <a name="to-create-file-associations-for-a-clickonce-application"></a>为 ClickOnce 应用程序创建文件关联  
  
1. 以正常方式创建 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序，或使用现有的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序。  
  
2. 使用文本编辑器或 XML 编辑器（如记事本）打开应用程序清单。  
  
3. 查找 `assembly` 元素。 有关详细信息，请参阅 [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)。  
  
4. 添加元素作为元素的子元素 `assembly` `fileAssociation` 。 `fileAssociation`元素具有四个属性：  
  
   - `extension`：要与应用程序关联的文件扩展名。  
  
   - `description`：将显示在 Windows shell 中的文件类型的说明。  
  
   - `progid`：唯一标识文件类型的字符串，用于在注册表中标记。  
  
   - `defaultIcon`：用于此文件类型的图标。 此图标必须作为文件资源添加到应用程序清单中。 有关详细信息，请参阅[如何：将数据文件添加到 ClickOnce 应用程序中](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md)。  
  
     有关和元素的示例 `file` `fileAssociation` ，请参阅[ \<fileAssociation> 元素](../deployment/fileassociation-element-clickonce-application.md)。  
  
5. 如果要将多个文件类型与应用程序关联，请添加其他 `fileAssociation` 元素。 请注意， `progid` 每个属性的属性应不同。  
  
6. 使用完应用程序清单后，对清单重新签名。 可以通过使用 Mage.exe 从命令行执行此操作。  
  
    `mage -Sign WindowsFormsApp1.exe.manifest -CertFile mycert.pfx`  
  
    有关详细信息，请参阅 [Mage.exe (清单生成和编辑工具) ](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)  
  
## <a name="see-also"></a>另请参阅  
 [\<fileAssociation> Element](../deployment/fileassociation-element-clickonce-application.md)   
 [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)   
 [Mage.exe（清单生成和编辑工具）](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)
