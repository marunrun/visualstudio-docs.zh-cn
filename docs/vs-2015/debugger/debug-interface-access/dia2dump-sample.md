---
title: Dia2dump 示例 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- sample applications [DIA SDK]
- Dia2dump sample [DIA SDK]
ms.assetid: 492c0893-7043-452f-a020-890a47230d20
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a817720c1ad73b666e0c9a586bb583120a2533c1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68197598"
---
# <a name="dia2dump-sample"></a>Dia2dump 示例
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Dia2dump 示例随 Visual Studio 安装，并包含 Dia2dump.cpp 源文件。 已编译可执行文件从命令行运行，并显示整个程序数据库 (.pdb) 文件的内容。  
  
### <a name="to-install-the-sample"></a>若要安装示例  
  
1. 验证您的系统满足所有 Visual Studio 安装程序起始页中所述的安装程序要求。  
  
2. 安装 Visual Studio，并按照包括的示例的所有设置和安装说明进行都操作。  
  
#### <a name="to-build-the-sample"></a>生成示例  
  
1. 在 Visual Studio 中打开 Dia2dump.sln 文件。 (如有必要，Visual Studio 将首先帮助您升级 Dia2dump 项目。）  
  
2. 在项目属性页中**C /C++**  &#124; **常规** &#124; **附加包含目录**属性，指定`..\DIA SDK\include`目录。 这可确保编译器可以找到 dia2.h 文件。  
  
3. 在“生成”菜单上，单击“重新生成解决方案”   。  
  
4. 关闭 Visual Studio。  
  
#### <a name="to-run-the-sample"></a>运行示例  
  
1. 打开命令提示符并键入以下命令：  
  
    ```  
    dia2dump filename  
    ```  
  
## <a name="see-also"></a>请参阅  
 [Dia2dump.cpp 源文件](../../debugger/debug-interface-access/dia2dump-cpp-source-file.md)   
 [如何：升级 Visual Studio 项目失败疑难解答](../../porting/how-to-troubleshoot-unsuccessful-visual-studio-project-upgrades.md)
