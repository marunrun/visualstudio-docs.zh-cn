---
title: ClickOnce 非托管 API 参考 |Microsoft Docs
ms.date: 11/04/2016
api_name:
- CleanOnlineAppCache
- GetDeploymentDataFromManifest
- LaunchApplication
api_location:
- dfshim.dll
api_type:
- COM
topic_type:
- apiref
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- LaunchApplication [ClickOnce unmanaged]
- ClickOnce, unmanaged APIs
- CleanOnlineAppCache [ClickOnce unmanaged]
- CleanOnlineAppCacheW interface [ClickOnce unmanaged]
- GetDeploymentDataFromManifest [ClickOnce unmanaged]
ms.assetid: ec002138-4054-456d-bcc1-79ac2f4a4fd7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 3b536a17df4f54158aa6f157a0d9795cf359ddc0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62900264"
---
# <a name="clickonce-unmanaged-api-reference"></a>ClickOnce 非托管 API 参考
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] dfshim.dll 中的非托管公共 Api。

## <a name="cleanonlineappcache"></a>CleanOnlineAppCache
 从应用程序缓存中清除或卸载所有联机应用程序 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。

### <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回表示失败的 HRESULT。 如果发生托管异常，则返回 0x80020009 (DISP_E_EXCEPTION) 。

### <a name="remarks"></a>备注
 如果调用 CleanOnlineAppCache，将启动该 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 服务（如果尚未运行）。

## <a name="getdeploymentdatafrommanifest"></a>GetDeploymentDataFromManifest
 检索清单和激活 URL 中的部署信息。

### <a name="parameters"></a>参数

|参数|说明|类型|
|---------------|-----------------|----------|
|`pcwzActivationUrl`|指向 `ActivationURL` 的指针。|LPCWSTR|
|`pcwzPathToDeploymentManifest`|指向 `PathToDeploymentManifest` 的指针。|LPCWSTR|
|`pwzApplicationIdentity`|指向缓冲区的指针，该缓冲区用于接收以 NULL 结尾的字符串，该字符串指定了返回的完整应用程序标识。|LPWSTR|
|`pdwIdentityBufferLength`|一个指向 DWORD 长度 `pwzApplicationIdentity` （在 WCHARs 中）的 DWORD 值的指针。 这包括 NULL 终止字符的空间。|LPDWORD|
|`pwzProcessorArchitecture`|指向缓冲区的指针，该缓冲区用于接收以 NULL 结尾的字符串，该字符串指定清单中的应用程序部署的处理器体系结构。|LPWSTR|
|`pdwArchitectureBufferLength`|一个指向 DWORD 长度 `pwzProcessorArchitecture` （在 WCHARs 中）的 DWORD 值的指针。|LPDWORD|
|`pwzApplicationManifestCodebase`|指向缓冲区的指针，该缓冲区用于接收以 NULL 结尾的字符串，该字符串指定清单中的应用程序清单的基本代码。|LPWSTR|
|`pdwCodebaseBufferLength`|一个指向 DWORD 长度 `pwzApplicationManifestCodebase` （在 WCHARs 中）的 DWORD 值的指针。|LPDWORD|
|`pwzDeploymentProvider`|指向缓冲区的指针，该缓冲区用于接收以 NULL 结尾的字符串，该字符串指定清单中的部署提供程序（如果存在）。 否则，将返回空字符串。|LPWSTR|
|`pdwProviderBufferLength`|一个指向 DWORD 的指针，它是的长度 `pwzProviderBufferLength` 。|LPDWORD|

### <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回表示失败的 HRESULT。 如果缓冲区太小，则返回 HRESULTFROMWIN32 (ERROR_INSUFFICIENT_BUFFER) 。

### <a name="remarks"></a>备注
 指针不能为 null。 `pcwzActivationUrl` 和 `pcwzPathToDeploymentManifest` 不得为空。

 调用方负责清理激活 URL。 例如，在需要时添加转义符或删除查询字符串。

 调用方负责限制输入长度。 例如，最大 URL 长度为2KB。

## <a name="launchapplication"></a>LaunchApplication
 使用部署 URL 启动或安装应用程序。

### <a name="parameters"></a>参数

|参数|说明|类型|
|---------------|-----------------|----------|
|`deploymentUrl`|指向以 NULL 结尾的字符串的指针，该字符串包含部署清单的 URL。|LPCWSTR|
|`data`|留待将来使用。 必须为 NULL。|LPVOID|
|`flags`|留待将来使用。 必须为 0。|DWORD|

### <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回表示失败的 HRESULT。 如果发生托管异常，则返回 0x80020009 (DISP_E_EXCEPTION) 。

## <a name="see-also"></a>另请参阅
- <xref:System.Deployment.Application.DeploymentServiceCom.CleanOnlineAppCache%2A>