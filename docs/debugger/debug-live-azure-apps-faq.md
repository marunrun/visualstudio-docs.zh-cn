---
title: 快照调试的常见问题解答 | Microsoft Docs
ms.date: 11/07/2017
ms.topic: reference
helpviewer_keywords:
- debugger
ms.assetid: 944f1eb0-a74b-4d28-ae2b-a370cd869add
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 813f06f55b6ae8f03a8d5a8e452ca05c4fe2054c
ms.sourcegitcommit: 32144a09ed46e7223ef7dcab647a9f73afa2dd55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2019
ms.locfileid: "67586844"
---
# <a name="frequently-asked-questions-for-snapshot-debugging-in-visual-studio"></a>在 Visual Studio 中进行快照调试的常见问答解答

下面列出了在使用 Snapshot Debugger 调试实时 Azure 应用程序时可能出现的问题。

#### <a name="what-is-the-performance-cost-of-taking-a-snapshot"></a>获取快照的性能成本是什么？

当 Snapshot Debugger 捕获应用快照时，它会创建应用进程的分支并挂起分支的副本。 调试快照时，将针对进程的分支副本进行调试。 此过程只需 10-20 毫秒，但不会复制应用的完整堆。 而是仅复制页表并将页设置为写入时复制。 如果堆上的某些应用对象发生更改，则会复制其相应页。 这就是每个快照具有较小的内存中成本的原因（对于大多数应用，大约具有数百千字节）。

#### <a name="what-happens-if-i-have-a-scaled-out-azure-app-service-multiple-instances-of-my-app"></a>如果我有一个横向扩展的 Azure 应用服务（多个应用实例），会发生什么情况？

具有多个应用实例时，快照点会应用于每个实例。 只有符合指定条件的第一个快照点才会创建快照。 如果你有多个快照点，则后续快照将来自创建了第一个快照的同一个实例。 发送到输出窗口的记录点将仅显示来自一个实例的消息，而发送到应用程序日志的记录点将发送来自所有实例的消息。

#### <a name="how-does-the-snapshot-debugger-load-symbols"></a>Snapshot Debugger 如何加载符号？

若要使用 Snapshot Debugger，本地应用程序或部署到 Azure 应用服务的应用程序必须具有匹配的符号。 （目前不支持嵌入的 PDB。）Snapshot Debugger 将自动从 Azure 应用服务下载符号。 自 Visual Studio 2017 版本 15.2 起，部署到 Azure 应用服务时，也会同时部署应用的符号。

#### <a name="does-the-snapshot-debugger-work-against-release-builds-of-my-application"></a>Snapshot Debugger 是否适用于我的应用程序的发布版本？

是 - Snapshot Debugger 适用于发布版本。 当快照点置于某个函数中时，该函数被重新编译回调试版本，使其可调试。 停止 Snapshot Debugger 会将函数返回到发布版本的版本。

#### <a name="can-logpoints-cause-side-effects-in-my-production-application"></a>记录点是否可能在我的生产应用程序中产生副作用？

否 - 添加到应用的任何日志消息都会进行虚拟评估。 它们不会对你的应用程序产生任何副作用。 但是，可能无法使用记录点访问某些本机属性。

#### <a name="does-the-snapshot-debugger-work-if-my-server-is-under-load"></a>如果我的服务器处于负载中，Snapshot Debugger 是否会运行？

是，快照调试可用于处于负载中的服务器。 当服务器上的可用内存量较少时，Snapshot Debugger 会进行限制，并且不会捕获快照。

#### <a name="how-do-i-uninstall-the-snapshot-debugger"></a>如何卸载快照调试器？

可以通过执行以下步骤来卸载应用服务上的 Snapshot Debugger 站点扩展：

1. 关闭你的应用服务通过在 Visual Studio 中的云资源管理器或 Azure 门户。
1. 导航到应用服务的 Kudu 站点（即，yourappservice.scm  .azurewebsites.net）并导航到“站点扩展”  。
1. 单击 Snapshot Debugger 站点扩展上的 X 以将其删除。

#### <a name="why-are-ports-opened-during-a-snapshot-debugger-session"></a>为什么在 Snapshot Debugger 会话期间打开端口？

Snapshot Debugger 必须打开一组端口才能调试在 Azure 中获取的快照，这些端口与远程调试所需的端口相同。 [可以在此处找到端口列表](../debugger/remote-debugger-port-assignments.md)。

#### <a name="how-do-i-disable-the-remote-debugger-extension"></a>如何禁用远程调试器扩展？

对于应用服务：
1. 禁用远程调试器扩展通过 Azure 门户为应用服务。
2. Azure 门户 > 应用程序服务资源边栏选项卡 >*应用程序设置*
3. 导航到*调试*部分，然后单击*Off*按钮*远程调试*。

适用于 AKS:
1. 更新 Dockerfile 来删除相应部分[Docker 映像上的 Visual Studio 快照调试器](https://github.com/Microsoft/vssnapshotdebugger-docker)。
2. 重新生成并重新部署已修改的 Docker 映像。

对于虚拟机/虚拟机规模集，如下所示删除远程调试器扩展，证书，key Vault 和入站 NAT 池：

1. 删除远程调试器扩展

   有几种方法，若要禁用远程调试器的虚拟机和虚拟机规模集：

      - 禁用通过云资源管理器的远程调试器

         - 云资源管理器 > 虚拟机资源 > 禁用调试 （禁用调试不存在的虚拟机规模集上云资源管理器）。

      - 禁用远程调试器使用 PowerShell 脚本/Cmdlet

         为虚拟机：

         ```powershell
         Remove-AzVMExtension -ResourceGroupName $rgName -VMName $vmName -Name Microsoft.VisualStudio.Azure.RemoteDebug.VSRemoteDebugger
         ```

         虚拟机规模集：

         ```powershell
         $vmss = Get-AzVmss -ResourceGroupName $rgName -VMScaleSetName $vmssName
         $extension = $vmss.VirtualMachineProfile.ExtensionProfile.Extensions | Where {$_.Name.StartsWith('VsDebuggerService')} | Select -ExpandProperty Name
         Remove-AzVmssExtension -VirtualMachineScaleSet $vmss -Name $extension
         ```

      - 禁用远程调试器通过 Azure 门户
         - Azure 门户 > 你的虚拟机/虚拟机规模集资源边栏选项卡 > 扩展
         - 卸载 Microsoft.VisualStudio.Azure.RemoteDebug.VSRemoteDebugger 扩展

         > [!NOTE]
         > 虚拟机规模集-在门户不允许删除 DebuggerListener 端口。 你将需要使用 Azure PowerShell。 有关详细信息，请参见以下内容。

2. 删除证书和 Azure 密钥保管库

   在安装适用于虚拟机或虚拟机规模集的远程调试器扩展时，会创建客户端和服务器证书以与客户端身份验证与 Azure 虚拟机/虚拟机规模集资源。

   - 客户端证书

      此证书是自签名的证书位于 Cert: / CurrentUser/My /

      ```
      Thumbprint                                Subject
      ----------                                -------

      1234123412341234123412341234123412341234  CN=ResourceName
      ```

      若要从计算机中删除此证书的一种方法是通过 PowerShell

      ```powershell
      $ResourceName = 'ResourceName' # from above
      Get-ChildItem -Path Cert:\CurrentUser\My | Where-Object {$_.Subject -match $ResourceName} | Remove-Item
      ```

   - 服务器证书
      - 为到 Azure 密钥保管库机密部署相应的服务器证书指纹。 VS 将尝试查找或前缀 MSVSAZ * 中对应于虚拟机的区域来创建密钥保管库或虚拟机规模集资源。 所有虚拟机或虚拟机都规模集部署到该区域的资源因此将共享同一密钥保管库。
      - 若要删除的服务器证书指纹机密，请转到 Azure 门户和承载所需的资源的同一区域中查找 MSVSAZ * 密钥保管库。 删除机密应标为 `remotedebugcert<<ResourceName>>`
      - 此外需要从通过 PowerShell 所需的资源中删除服务器机密。

      对于虚拟机：

      ```powershell
      $vm.OSProfile.Secrets[0].VaultCertificates.Clear()
      Update-AzVM -ResourceGroupName $rgName -VM $vm
      ```

      虚拟机规模集：

      ```powershell
      $vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Clear()
      Update-AzVmss -ResourceGroupName $rgName -VMScaleSetName $vmssName -VirtualMachineScaleSet $vmss
      ```

3. 请删除所有 DebuggerListener 入站 NAT 池 （虚拟机规模集仅）

   远程调试器引入了 DebuggerListener 应用于规模集的负载均衡器入站 NAT 池。

   ```powershell
   $inboundNatPools = $vmss.VirtualMachineProfile.NetworkProfile.NetworkInterfaceConfigurations.IpConfigurations.LoadBalancerInboundNatPools
   $inboundNatPools.RemoveAll({ param($pool) $pool.Id.Contains('inboundNatPools/DebuggerListenerNatPool-') }) | Out-Null

   if ($LoadBalancerName)
   {
      $lb = Get-AzLoadBalancer -ResourceGroupName $ResourceGroup -name $LoadBalancerName
      $lb.FrontendIpConfigurations[0].InboundNatPools.RemoveAll({ param($pool) $pool.Id.Contains('inboundNatPools/DebuggerListenerNatPool-') }) | Out-Null
      Set-AzLoadBalancer -LoadBalancer $lb
   }
   ```

#### <a name="how-do-i-disable-snapshot-debugger"></a>如何禁用快照调试程序？

为应用服务：
1. 为应用服务通过 Azure 门户中禁用快照调试程序。
2. Azure 门户 > 应用程序服务资源边栏选项卡 >*应用程序设置*
3. 删除在 Azure 门户中的以下应用设置并保存所做的更改。
   - INSTRUMENTATIONENGINE_EXTENSION_VERSION
   - SNAPSHOTDEBUGGER_EXTENSION_VERSION

   > [!WARNING]
   > 对应用程序设置的任何更改将应用程序重新启动。 有关应用程序设置的详细信息，请参阅[Azure 门户中配置应用服务应用](/azure/app-service/web-sites-configure)。

适用于 AKS:
1. 更新 Dockerfile 来删除相应部分[Docker 映像上的 Visual Studio 快照调试器](https://github.com/Microsoft/vssnapshotdebugger-docker)。
2. 重新生成并重新部署已修改的 Docker 映像。

虚拟机/虚拟机规模集：

有几种方法，若要禁用快照调试程序：
- 云资源管理器 > 虚拟机/虚拟机规模集资源 > 禁用诊断

- Azure 门户 > 虚拟机/虚拟机规模集资源边栏选项卡 > 扩展 > 卸载 microsoft.insights.vmdiagnosticssettings 后扩展

- 中的 PowerShell Cmdlet [Az PowerShell](https://docs.microsoft.com/powershell/azure/overview)

   虚拟机：

   ```powershell
      Remove-AzVMExtension -ResourceGroupName $rgName -VMName $vmName -Name Microsoft.Insights.VMDiagnosticsSettings
   ```

   虚拟机规模集：

   ```powershell
      $vmss = Get-AzVmss -ResourceGroupName $rgName -VMScaleSetName $vmssName
      Remove-AzVmssExtension -VirtualMachineScaleSet $vmss -Name Microsoft.Insights.VMDiagnosticsSettings
   ```

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中进行调试](../debugger/index.md)
- [使用快照调试器调试实时 ASP.NET 应用](../debugger/debug-live-azure-applications.md)
- [调试实时 ASP.NET Azure 虚拟 Machines\Virtual 机规模集使用快照调试程序](../debugger/debug-live-azure-virtual-machines.md)
- [调试实时 ASP.NET Azure Kubernetes，使用快照调试程序](../debugger/debug-live-azure-kubernetes.md)
- [快照调试疑难解答和已知问题](../debugger/debug-live-azure-apps-troubleshooting.md)
