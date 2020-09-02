---
title: 关于文件扩展名 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- file extensions
- file name extensions
ms.assetid: 99f4f9ff-fb84-4258-9787-6890f308a57f
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 866a30279ca2c79f4a490a040f76bc3a86c6a6e1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148034"
---
# <a name="about-file-name-extensions"></a>关于文件扩展名
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

注册 VSPackage 的文件扩展名时，可以将其与的版本相关联 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。 如果在计算机上安装了多个版本的，则这一点非常重要 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。  
  
 Vspackage 的文件扩展名在 HKEY_CLASSES_ROOT 键下注册，其默认值指向关联的编程标识符 (ProgID) 。  
  
 下面是 vcproj 文件扩展名的注册信息的示例：  
  
```  
HKEY_CLASSES_ROOT\  
   .vcproj\  
      (default)=" VisualStudio.vcproj.8.0"   
```  
  
 与关联的文件 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 必须具有一个版本控制的 ProgID，如 `VisualStudio.vcproj.8.0` ，以允许并行安装产品以维护产品版本之间的文件扩展名关联。 使用版本特定的 ProgID，还可以使用标准谓词（如 "打开"、"编辑" 等），而无需考虑覆盖或被其他应用程序或版本覆盖的问题 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。  
  
 在某些情况下，不应更改与文件扩展名关联的 ProgID。 例如，.htm 文件扩展名 (progid = htmlfile) 的 ProgID 在操作系统的多个位置进行硬编码，并且在与 .htm 和 .html 文件的关联中是众所周知和使用的。  
  
## <a name="see-also"></a>另请参阅  
 [为并行部署注册文件扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)   
 [指定文件扩展名的文件处理程序](../extensibility/specifying-file-handlers-for-file-name-extensions.md)
