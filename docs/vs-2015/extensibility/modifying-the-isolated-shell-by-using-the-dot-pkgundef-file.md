---
title: 使用修改独立 Shell。.Pkgundef 文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, isolated mode%2C .pkgundef file
ms.assetid: 9cee2a20-f8ac-4d9d-aef9-068fcd9f27a4
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: eab02fe900e96ba37c63faae535974788f99ba78
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62538380"
---
# <a name="modifying-the-isolated-shell-by-using-the-pkgundef-file"></a>通过使用 .Pkgundef 文件修改独立 Shell
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以修改 .pkgundef 文件以从独立 shell 应用程序中排除指定的注册表项。 通常，在计算机上首次启动应用程序时，Visual Studio shell 会将现有的 Visual Studio 注册表项复制到应用程序的根注册表项。 这包括对当前已安装的 Vspackage 的所有引用。  
  
 若要从独立 shell 应用程序中排除特定的注册表项，请将添加到 .pkgundef 文件中的包密钥后跟条目。 键和项的表示形式与 .pkgdef 文件中的相同;也就是说，如 [$RootKey $] 或 [$RootKey $ \\ *子项*] 和 "*entry*" =*value*，其中*子项*是要进行影响的子项， *entry*是要删除的项，*值*为 `""` 或 `dword:00000000` 。  
  
 若要从注册表项中排除多个项，只需列出一次键，然后列出要排除的每个条目对应的一行。  
  
 若要从独立 shell 应用程序中排除整个注册表项，请将该项添加到 .pkgundef 文件，但不要为该项指定任何注册表项。  
  
 可以将注释添加到 .pkgundef 文件。 单行注释必须有两个斜杠作为前两个字符。  
  
 例如，若要删除 " **连接到数据库** " 并 **连接到** " **工具** " 菜单上的 "服务"，可以取消注释行：  
  
```  
[$RootKey$\Packages\{8D8529D3-625D-4496-8354-3DAD630ECC1B}]  
```  
  
 并添加行：  
  
```  
[$RootKey$\Packages\{198E76C1-34C0-424D-9957-B3EBD80265FB}]  
```  
  
 应用程序的 .pkgundef 文件。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 功能的包 Guid](../extensibility/package-guids-of-visual-studio-features.md)   
 [自定义独立 Shell](../extensibility/customizing-the-isolated-shell.md)
