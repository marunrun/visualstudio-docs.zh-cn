---
title: 错误： 依赖项&#39;文件&#39;项目中&#39;项目&#39;不能将复制到运行目录，因为它将与依赖关系冲突&#39;文件&#39;|Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
f1_keywords:
- vs.tasklisterror.copy_version_conflict
ms.assetid: cd7de1eb-7d58-4e2c-9811-a7201f7817be
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7726d615c3495845ffdf73d69ffc7d8fae155272
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65688280"
---
# <a name="error-the-dependency-39file39-in-project-39project39-cannot-be-copied-to-the-run-directory-because-it-would-conflict-with-dependency-39file39"></a>错误： 依赖项&#39;文件&#39;项目中&#39;项目&#39;不能将复制到运行目录，因为它将与依赖关系冲突&#39;文件&#39;
引用之间存在冲突；为使应用程序运行，将多个具有相同文件名的不同的依赖项复制到 bin 目录中。 由于没有任何依赖项是主引用，因此运行目录无法解决此冲突。  
  
 此错误将导致生成失败。  
  
 双击此“任务列表”项将跳转到在其中发生冲突的项目的引用节点。  
  
 **若要更正此错误**  
  
- 将某个程序集设为你项目的直接引用。 此方法可能存在的缺点是，不保证你所选择的程序集适用于需要引用程序集的某一其他版本的程序集。  
  
     \- 或 -  
  
- 请确保程序集的这两个副本具有强名称且在全局程序集缓存中。 这样就无需将程序集复制到 bin 目录中。  
  
## <a name="see-also"></a>请参阅  
 [管理项目中的引用](../ide/managing-references-in-a-project.md)   
 [全局程序集缓存](https://msdn.microsoft.com/library/cf5eacd0-d3ec-4879-b6da-5fd5e4372202)   
 [具有强名称的程序集](https://msdn.microsoft.com/library/d4a80263-f3e0-4d81-9b61-f0cbeae3797b)   
 [程序集版本控制](https://msdn.microsoft.com/library/775ad4fb-914f-453c-98ef-ce1089b6f903)   
 [如何：创建和删除项目依赖项](../ide/how-to-create-and-remove-project-dependencies.md)