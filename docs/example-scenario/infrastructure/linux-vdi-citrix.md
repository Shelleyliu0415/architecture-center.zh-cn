---
title: 将 Citrix 用于 Linux 虚拟桌面
description: 在 Azure 上使用 Citrix 为 Linux 桌面构建 VDI 环境。
author: miguelangelopereira
ms.date: 09/12/2018
ms.openlocfilehash: 374d59f7a528bd89870baa601a49a30ea00a08f1
ms.sourcegitcommit: b2a4eb132857afa70201e28d662f18458865a48e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2018
ms.locfileid: "48819136"
---
# <a name="linux-virtual-desktops-with-citrix"></a><span data-ttu-id="9792a-103">将 Citrix 用于 Linux 虚拟桌面</span><span class="sxs-lookup"><span data-stu-id="9792a-103">Linux Virtual Desktops with Citrix</span></span>

<span data-ttu-id="9792a-104">本示例方案适用于任何需要用于 Linux 桌面的虚拟桌面基础结构 (VDI) 的行业。</span><span class="sxs-lookup"><span data-stu-id="9792a-104">This example scenario is applicable to any industry that needs a Virtual Desktop Infrastructure (VDI) for Linux Desktops.</span></span> <span data-ttu-id="9792a-105">VDI 是指在数据中心服务器上的虚拟机中运行用户桌面的过程。</span><span class="sxs-lookup"><span data-stu-id="9792a-105">VDI refers to the process of running a user desktop inside a virtual machine that lives on a server in the datacenter.</span></span> <span data-ttu-id="9792a-106">本方案中的客户选择使用基于 Citrix 的解决方案来满足其 VDI 需求。</span><span class="sxs-lookup"><span data-stu-id="9792a-106">The customer in this scenario chose to use a Citrix-based solution for their VDI needs.</span></span>

<span data-ttu-id="9792a-107">组织通常采用异构环境，其中包含员工使用的多个设备和操作系统。</span><span class="sxs-lookup"><span data-stu-id="9792a-107">Organizations often have heterogeneous environments with multiple devices and operating systems being used by employees.</span></span> <span data-ttu-id="9792a-108">要在维护安全环境的同时提供一致的应用程序访问方式，可能存在一定的难度。</span><span class="sxs-lookup"><span data-stu-id="9792a-108">It can be challenging to provide consistent access to applications while maintaining a secure environment.</span></span> <span data-ttu-id="9792a-109">借助用于 Linux 桌面的 VDI 解决方案，不管最终用户使用哪种设备或 OS，组织都能提供访问。</span><span class="sxs-lookup"><span data-stu-id="9792a-109">A VDI solution for Linux desktops will allow your organization to provide access irrespective of the device or OS used by the end user.</span></span>

<span data-ttu-id="9792a-110">本示例解决方案的部分优势包括：</span><span class="sxs-lookup"><span data-stu-id="9792a-110">Some benefits for this sample solution include the following:</span></span>
* <span data-ttu-id="9792a-111">让更多的用户访问同一个基础结构，通过共享的 Linux 虚拟桌面来提高投资回报。</span><span class="sxs-lookup"><span data-stu-id="9792a-111">Return on investment will be higher with shared Linux virtual desktops by giving more users access to the same infrastructure.</span></span> <span data-ttu-id="9792a-112">在集中式 VDI 环境中整合资源，不需要配置强大的最终用户设备。</span><span class="sxs-lookup"><span data-stu-id="9792a-112">By consolidating resources on a centralized VDI environment, the end user devices don't need to be as powerful.</span></span>
* <span data-ttu-id="9792a-113">不管最终用户设备的配置如何，都能保持一致的性能。</span><span class="sxs-lookup"><span data-stu-id="9792a-113">Performance will be consistent regardless of the end user device.</span></span>
* <span data-ttu-id="9792a-114">用户可从任何设备（包括非 Linux 设备）访问 Linux 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9792a-114">Users can access Linux applications from any device (including non-Linux devices).</span></span>
* <span data-ttu-id="9792a-115">可在 Azure 数据中心保护各地员工的敏感数据。</span><span class="sxs-lookup"><span data-stu-id="9792a-115">Sensitive data can be secured in the Azure data center for all distributed employees.</span></span>

## <a name="relevant-use-cases"></a><span data-ttu-id="9792a-116">相关用例</span><span class="sxs-lookup"><span data-stu-id="9792a-116">Relevant use cases</span></span>

<span data-ttu-id="9792a-117">以下用例可以考虑本方案：</span><span class="sxs-lookup"><span data-stu-id="9792a-117">Consider this scenario for the following use case:</span></span>

* <span data-ttu-id="9792a-118">从 Linux 或非 Linux 设备安全访问任务关键型的专用 Linux VDI 桌面</span><span class="sxs-lookup"><span data-stu-id="9792a-118">Providing secure access to mission-critical, specialized Linux VDI desktops from Linux or non-Linux devices</span></span>

## <a name="architecture"></a><span data-ttu-id="9792a-119">体系结构</span><span class="sxs-lookup"><span data-stu-id="9792a-119">Architecture</span></span>

<span data-ttu-id="9792a-120">[![](./media/azure-citrix-sample-diagram.png "体系结构示意图")](./media/azure-citrix-sample-diagram.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="9792a-120">[![](./media/azure-citrix-sample-diagram.png "Architecture Diagram")](./media/azure-citrix-sample-diagram.png#lightbox)</span></span>

<span data-ttu-id="9792a-121">本示例方案演示如何从企业网络访问 Linux 虚拟桌面：</span><span class="sxs-lookup"><span data-stu-id="9792a-121">This example scenario demonstrates allowing the corporate network to access the Linux Virtual Desktops:</span></span>

* <span data-ttu-id="9792a-122">在本地环境与 Azure 之间建立 ExpressRoute，以便快速可靠地连接到云。</span><span class="sxs-lookup"><span data-stu-id="9792a-122">An ExpressRoute is established between the on-premises environment and Azure, for fast and reliable connectivity to the cloud.</span></span>
* <span data-ttu-id="9792a-123">为 VDI 部署 Citrix XenDeskop 解决方案。</span><span class="sxs-lookup"><span data-stu-id="9792a-123">Citrix XenDeskop solution deployed for VDI.</span></span>
* <span data-ttu-id="9792a-124">CitrixVDA 在 Ubuntu（或其他支持的分发版）上运行。</span><span class="sxs-lookup"><span data-stu-id="9792a-124">The CitrixVDA run on Ubuntu (or another supported distro).</span></span>
* <span data-ttu-id="9792a-125">Azure 网络安全组应用正确的网络 ACL。</span><span class="sxs-lookup"><span data-stu-id="9792a-125">Azure Network Security Groups will apply the correct network ACLs.</span></span>
* <span data-ttu-id="9792a-126">Citrix ADC (NetScaler) 发布所有 Citrix 服务并对其进行负载均衡。</span><span class="sxs-lookup"><span data-stu-id="9792a-126">Citrix ADC (NetScaler) will publish and load balance all the Citrix services.</span></span>
* <span data-ttu-id="9792a-127">Active Directory 域服务用于将 Citrix 服务器加入域。</span><span class="sxs-lookup"><span data-stu-id="9792a-127">Active Directory Domain Services will be used to domain join the Citrix servers.</span></span> <span data-ttu-id="9792a-128">VDA 服务器不会加入域。</span><span class="sxs-lookup"><span data-stu-id="9792a-128">VDA servers will not be domain joined.</span></span>
* <span data-ttu-id="9792a-129">Azure 混合文件同步在整个解决方案中启用共享存储。</span><span class="sxs-lookup"><span data-stu-id="9792a-129">Azure Hybrid File Sync will enable shared storage across the solution.</span></span> <span data-ttu-id="9792a-130">例如，可以在远程/家庭解决方案中使用它。</span><span class="sxs-lookup"><span data-stu-id="9792a-130">For example, it can be used in remote/home solutions.</span></span>

<span data-ttu-id="9792a-131">本方案使用以下 SKU：</span><span class="sxs-lookup"><span data-stu-id="9792a-131">For this scenario, the following SKUs are used:</span></span>

- <span data-ttu-id="9792a-132">Citrix ADC (NetScaler)：2 个包含 [NetScaler 12.0 VPX Standard Edition 200 MBPS PAYG 映像](https://azuremarketplace.microsoft.com/pt-br/marketplace/apps/citrix.netscalervpx-120?tab=PlansAndPrice)的 D4sv3</span><span class="sxs-lookup"><span data-stu-id="9792a-132">Citrix ADC (NetScaler): 2 x D4sv3 with [NetScaler 12.0 VPX Standard Edition 200 MBPS PAYG image](https://azuremarketplace.microsoft.com/pt-br/marketplace/apps/citrix.netscalervpx-120?tab=PlansAndPrice)</span></span>
- <span data-ttu-id="9792a-133">Citrix 许可证服务器：1 个 D2s v3</span><span class="sxs-lookup"><span data-stu-id="9792a-133">Citrix License Server: 1 x D2s v3</span></span>
- <span data-ttu-id="9792a-134">Citrix VDA：4 个 D8s v3</span><span class="sxs-lookup"><span data-stu-id="9792a-134">Citrix VDA: 4 x D8s v3</span></span>
- <span data-ttu-id="9792a-135">Citrix Storefront：2 个 D2s v3</span><span class="sxs-lookup"><span data-stu-id="9792a-135">Citrix Storefront: 2 x D2s v3</span></span>
- <span data-ttu-id="9792a-136">Citrix 传送控制器：2 个 D2s v3</span><span class="sxs-lookup"><span data-stu-id="9792a-136">Citrix Delivery Controller: 2 x D2s v3</span></span>
- <span data-ttu-id="9792a-137">域控制器：2 个 D2sv3</span><span class="sxs-lookup"><span data-stu-id="9792a-137">Domain Controllers: 2 x D2sv3</span></span>
- <span data-ttu-id="9792a-138">Azure 文件服务器：2 个 D2sv3</span><span class="sxs-lookup"><span data-stu-id="9792a-138">Azure File Servers: 2 x D2sv3</span></span>

> [!NOTE]
> <span data-ttu-id="9792a-139">所有许可证（NetScaler 除外）都是自带许可证 (BYOL)</span><span class="sxs-lookup"><span data-stu-id="9792a-139">All the licenses (other than NetScaler) are bring-your-own-license (BYOL)</span></span>

### <a name="components"></a><span data-ttu-id="9792a-140">组件</span><span class="sxs-lookup"><span data-stu-id="9792a-140">Components</span></span>

- <span data-ttu-id="9792a-141">[Azure 虚拟网络](/azure/virtual-network/virtual-networks-overview)允许 VM 之类的资源以安全方式彼此通信、与 Internet 通信，以及与本地网络通信。</span><span class="sxs-lookup"><span data-stu-id="9792a-141">[Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) allows resources such as VMs to securely communicate with each other, the internet, and on-premises networks.</span></span> <span data-ttu-id="9792a-142">虚拟网络提供隔离和细分，可以筛选和路由流量，并且允许在不同位置之间进行连接。</span><span class="sxs-lookup"><span data-stu-id="9792a-142">Virtual networks provide isolation and segmentation, filter and route traffic, and allow connection between locations.</span></span> <span data-ttu-id="9792a-143">在本方案中，所有资源将使用一个虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="9792a-143">One virtual network will be used for all resources in this scenario.</span></span>
- <span data-ttu-id="9792a-144">[Azure 网络安全组](/azure/virtual-network/security-overview)包含一个安全规则列表，这些规则可根据源或目标 IP 地址、端口和协议允许或拒绝入站或出站网络流量。</span><span class="sxs-lookup"><span data-stu-id="9792a-144">[Azure network security groups](/azure/virtual-network/security-overview) contain a list of security rules that allow or deny inbound or outbound network traffic based on source or destination IP address, port, and protocol.</span></span> <span data-ttu-id="9792a-145">本方案中的虚拟网络受网络安全组规则的保护，这些规则可以限制应用程序组件之间的流量。</span><span class="sxs-lookup"><span data-stu-id="9792a-145">The virtual networks in this scenario are secured with network security group rules that restrict the flow of traffic between the application components.</span></span>
- <span data-ttu-id="9792a-146">[Azure 负载均衡器](/azure/application-gateway/overview)根据规则和运行状况探测来分配入站流量。</span><span class="sxs-lookup"><span data-stu-id="9792a-146">[Azure load balancer](/azure/application-gateway/overview) distributes inbound traffic according to rules and health probes.</span></span> <span data-ttu-id="9792a-147">负载均衡器提供低延迟和高吞吐量，以及为所有 TCP 和 UDP 应用程序纵向扩展到数以百万计的流。</span><span class="sxs-lookup"><span data-stu-id="9792a-147">A load balancer provides low latency and high throughput, and scales up to millions of flows for all TCP and UDP applications.</span></span> <span data-ttu-id="9792a-148">本方案使用内部负载均衡器在 Citrix NetScaler 上分配流量。</span><span class="sxs-lookup"><span data-stu-id="9792a-148">An internal load balancer is used in this scenario to distribute traffic on the Citrix NetScaler.</span></span>
- <span data-ttu-id="9792a-149">[Azure 混合文件同步](https://github.com/MicrosoftDocs/azure-docs/edit/master/articles/storage/files/storage-sync-files-planning.md)用于所有共享存储。</span><span class="sxs-lookup"><span data-stu-id="9792a-149">[Azure Hybrid File Sync](https://github.com/MicrosoftDocs/azure-docs/edit/master/articles/storage/files/storage-sync-files-planning.md) will be used for all shared storage.</span></span> <span data-ttu-id="9792a-150">存储将使用混合文件同步复制到两个文件服务器。</span><span class="sxs-lookup"><span data-stu-id="9792a-150">The storage will replicate to two file servers using Hybrid File Sync.</span></span>
- <span data-ttu-id="9792a-151">[Azure SQL 数据库](/azure/sql-database/sql-database-technical-overview)是基于最新稳定版 Microsoft SQL Server 数据库引擎的关系数据库即服务 (DBaaS)。</span><span class="sxs-lookup"><span data-stu-id="9792a-151">[Azure SQL Database](/azure/sql-database/sql-database-technical-overview) is a relational database-as-a-service (DBaaS) based on the latest stable version of Microsoft SQL Server Database Engine.</span></span> <span data-ttu-id="9792a-152">它用于托管 Citrix 数据库。</span><span class="sxs-lookup"><span data-stu-id="9792a-152">It will be used for hosting Citrix databases.</span></span>
- <span data-ttu-id="9792a-153">使用 [ExpressRoute](/azure/expressroute/expressroute-introduction) 可通过连接服务提供商所提供的专用连接，将本地网络扩展到 Microsoft 云。</span><span class="sxs-lookup"><span data-stu-id="9792a-153">[ExpressRoute](/azure/expressroute/expressroute-introduction) lets you extend your on-premises networks into the Microsoft cloud over a private connection facilitated by a connectivity provider.</span></span> 
- <span data-ttu-id="9792a-154">[Active Directory 域服务用于目录服务和用户身份验证</span><span class="sxs-lookup"><span data-stu-id="9792a-154">[Active Directory Domain Services is used for Directory Services and user authentication</span></span>
- <span data-ttu-id="9792a-155">[Azure 可用性集](/azure/virtual-machines/windows/tutorial-availability-sets)确保在 Azure 上部署的 VM 能够跨群集中多个隔离的硬件节点分布。</span><span class="sxs-lookup"><span data-stu-id="9792a-155">[Azure Availabilty Sets](/azure/virtual-machines/windows/tutorial-availability-sets) will ensure that the VMs you deploy on Azure are distributed across multiple isolated hardware nodes in a cluster.</span></span> <span data-ttu-id="9792a-156">这样，就可以确保当 Azure 中发生硬件或软件故障时，只有一部分 VM 会受到影响，整体解决方案仍可使用和操作。</span><span class="sxs-lookup"><span data-stu-id="9792a-156">Doing this ensures that if a hardware or software failure within Azure happens, only a subset of your VMs are impacted and that your overall solution remains available and operational.</span></span> 
- <span data-ttu-id="9792a-157">[Citrix ADC (NetScaler)](https://www.citrix.com/products/citrix-adc) 是应用程序传送控制器，执行特定于应用程序的流量分析，以智能分配、优化和保护 Web 应用程序的第 4 层到第 7 层 (L4-L7) 网络流量。</span><span class="sxs-lookup"><span data-stu-id="9792a-157">[Citrix ADC (NetScaler)](https://www.citrix.com/products/citrix-adc) is an application delivery controller that performs application-specific traffic analysis to intelligently distribute, optimize, and secure Layer 4-Layer 7 (L4–L7) network traffic for web applications.</span></span> 
- <span data-ttu-id="9792a-158">[Citrix Storefront](https://www.citrix.com/products/citrix-virtual-apps-and-desktops/citrix-storefront.html) 是企业应用存储，可以改善安全性并简化部署，针对任何平台上的 Citrix 接收器提供无可比拟的、接近本机速度的新式用户体验。</span><span class="sxs-lookup"><span data-stu-id="9792a-158">[Citrix Storefront](https://www.citrix.com/products/citrix-virtual-apps-and-desktops/citrix-storefront.html) is an enterprise app store that improves security and simplifies deployments, delivering a modern, unmatched near-native user experience across Citrix Receiver on any platform.</span></span> <span data-ttu-id="9792a-159">使用 StoreFront 能够轻松管理多站点和多版本 Citrix 虚拟应用与桌面环境。</span><span class="sxs-lookup"><span data-stu-id="9792a-159">StoreFront makes it easy to manage multi-site and multi-version Citrix Virtual Apps and Desktops environments.</span></span> 
- <span data-ttu-id="9792a-160">[Citrix 许可证服务器](https://www.citrix.com/buy/licensing/overview.html)管理 Citrix 产品的许可证。</span><span class="sxs-lookup"><span data-stu-id="9792a-160">[Citrix License Server](https://www.citrix.com/buy/licensing/overview.html) will manage the licenses for Citrix products.</span></span>
- <span data-ttu-id="9792a-161">[Citrix XenDesktops VDA](https://docs.citrix.com/en-us/citrix-virtual-apps-desktops-service) 用于与应用程序和桌面建立连接。</span><span class="sxs-lookup"><span data-stu-id="9792a-161">[Citrix XenDesktops VDA](https://docs.citrix.com/en-us/citrix-virtual-apps-desktops-service) enables connections to applications and desktops.</span></span> <span data-ttu-id="9792a-162">VDA 安装在运行用户应用程序或虚拟桌面的计算机上。</span><span class="sxs-lookup"><span data-stu-id="9792a-162">The VDA is installed on the machine that runs the applications or virtual desktops for the user.</span></span> <span data-ttu-id="9792a-163">VDA 使计算机能够注册到传送控制器，并可以管理用户设备的高清用户体验 (HDX) 连接。</span><span class="sxs-lookup"><span data-stu-id="9792a-163">It enables the machines to register with Delivery Controllers and manage the High Definition eXperience (HDX) connection to a user device.</span></span>
- <span data-ttu-id="9792a-164">[Citrix 传送控制器](https://docs.citrix.com/en-us/xenapp-and-xendesktop/7-15-ltsr/manage-deployment/delivery-controllers)是负责管理用户访问以及中转和优化连接的服务器端组件。</span><span class="sxs-lookup"><span data-stu-id="9792a-164">[Citrix Delivery Controller](https://docs.citrix.com/en-us/xenapp-and-xendesktop/7-15-ltsr/manage-deployment/delivery-controllers) is the server-side component responsible for managing user access, plus brokering and optimizing connections.</span></span> <span data-ttu-id="9792a-165">控制器还提供用于创建桌面和服务器映像的计算机创建服务。</span><span class="sxs-lookup"><span data-stu-id="9792a-165">Controllers also provide the Machine Creation Services that create desktop and server images.</span></span>

### <a name="alternatives"></a><span data-ttu-id="9792a-166">备选项</span><span class="sxs-lookup"><span data-stu-id="9792a-166">Alternatives</span></span>

- <span data-ttu-id="9792a-167">Azure 支持 VDI 解决方案的多个合作伙伴，例如 VMware、Workspot，等等。</span><span class="sxs-lookup"><span data-stu-id="9792a-167">There are multiple partners with VDI solutions that supported in Azure such as VMware, Workspot, and others.</span></span> <span data-ttu-id="9792a-168">本特定示例体系结构基于使用 Citrix 的已部署项目。</span><span class="sxs-lookup"><span data-stu-id="9792a-168">This specific sample architecture is based on a deployed project that used Citrix.</span></span>
- <span data-ttu-id="9792a-169">Citrix 提供的某个云服务可以抽象化此体系结构的一部分。</span><span class="sxs-lookup"><span data-stu-id="9792a-169">Citrix provides a cloud service that abstracts part of this architecture.</span></span> <span data-ttu-id="9792a-170">此服务可能是本解决方案的替代方案。</span><span class="sxs-lookup"><span data-stu-id="9792a-170">It could be an alternative for this solution.</span></span> <span data-ttu-id="9792a-171">有关详细信息，请参阅 [Citrix Cloud](https://www.citrix.com/products/citrix-cloud)。</span><span class="sxs-lookup"><span data-stu-id="9792a-171">For more information, see [Citrix Cloud](https://www.citrix.com/products/citrix-cloud).</span></span>

## <a name="considerations"></a><span data-ttu-id="9792a-172">注意事项</span><span class="sxs-lookup"><span data-stu-id="9792a-172">Considerations</span></span>

- <span data-ttu-id="9792a-173">检查 [Citrix Linux 要求](https://docs.citrix.com/en-us/linux-virtual-delivery-agent/current-release/system-requirements)。</span><span class="sxs-lookup"><span data-stu-id="9792a-173">Check the [Citrix Linux Requirements](https://docs.citrix.com/en-us/linux-virtual-delivery-agent/current-release/system-requirements).</span></span>
- <span data-ttu-id="9792a-174">延迟可能会对整体解决方案产生影响。</span><span class="sxs-lookup"><span data-stu-id="9792a-174">Latency can have impact on the overall solution.</span></span> <span data-ttu-id="9792a-175">对于生产环境，请相应地进行测试。</span><span class="sxs-lookup"><span data-stu-id="9792a-175">For a production environment, test accordingly.</span></span>
- <span data-ttu-id="9792a-176">根据具体的方案，本解决方案可能需要配备用于 VDA 的 GPU 的 VM。</span><span class="sxs-lookup"><span data-stu-id="9792a-176">Depending on the scenario, the solution may need VMs with GPUs for VDA.</span></span> <span data-ttu-id="9792a-177">本解决方案假设不要求使用 GPU。</span><span class="sxs-lookup"><span data-stu-id="9792a-177">For this solution, it is assumed that GPU is not a requirement.</span></span>

### <a name="availability-scalability-and-security"></a><span data-ttu-id="9792a-178">可用性、可伸缩性和安全性</span><span class="sxs-lookup"><span data-stu-id="9792a-178">Availability, Scalability, and Security</span></span>

- <span data-ttu-id="9792a-179">本示例解决方案是为了实现所有角色（许可服务器除外）的高可用性而设计的。</span><span class="sxs-lookup"><span data-stu-id="9792a-179">This sample solution is designed for high availability for all roles other than the licensing server.</span></span> <span data-ttu-id="9792a-180">由于在许可证服务器脱机的情况下，环境将在 30 天宽限期内继续运行，因此，不需要在该服务器上配置额外的冗余。</span><span class="sxs-lookup"><span data-stu-id="9792a-180">Because the environment continues to function during a 30-day grace period if the license server is offline, no additional redundancy is required on that server.</span></span>
- <span data-ttu-id="9792a-181">提供类似角色的所有服务器应部署在[可用性集](/azure/virtual-machines/windows/manage-availability#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy)中。</span><span class="sxs-lookup"><span data-stu-id="9792a-181">All servers providing similar roles should be deployed in [Availability Sets](/azure/virtual-machines/windows/manage-availability#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy).</span></span>
- <span data-ttu-id="9792a-182">本示例解决方案不包括灾难恢复功能。</span><span class="sxs-lookup"><span data-stu-id="9792a-182">This sample solution does not include Disaster Recovery capabilities.</span></span> <span data-ttu-id="9792a-183">[Azure Site Recovery](/azure/site-recovery/site-recovery-overview) 可能是这种设计的适当加载项。</span><span class="sxs-lookup"><span data-stu-id="9792a-183">[Azure Site Recovery](/azure/site-recovery/site-recovery-overview) could be a good add-on to this design.</span></span>
- <span data-ttu-id="9792a-184">对于生产部署，应实施[备份](/azure/backup/backup-introduction-to-azure-backup)、[监视](/azure/monitoring-and-diagnostics/monitoring-overview)和[更新管理](/azure/automation/automation-update-management)等管理解决方案。</span><span class="sxs-lookup"><span data-stu-id="9792a-184">For a production deployment management solution should be implemented such as [backup](/azure/backup/backup-introduction-to-azure-backup), [monitoring](/azure/monitoring-and-diagnostics/monitoring-overview) and [update management](/azure/automation/automation-update-management).</span></span>
- <span data-ttu-id="9792a-185">本示例解决方案应适用于采用混合技术的大约 250 个并发用户（每台 VDA 服务器大约有 50-60 个用户）。</span><span class="sxs-lookup"><span data-stu-id="9792a-185">This sample solution should work for about 250 concurrent (about 50-60 per VDA server) users with a mixed usage.</span></span> <span data-ttu-id="9792a-186">但是，具体的用户数在很大程度上取决于所用应用程序的类型。</span><span class="sxs-lookup"><span data-stu-id="9792a-186">But that will greatly depended on the type of applications being used.</span></span> <span data-ttu-id="9792a-187">对于生产用途，应执行严格的负载测试。</span><span class="sxs-lookup"><span data-stu-id="9792a-187">For production use, rigorous load testing should be performed.</span></span>

## <a name="deploy-this-scenario"></a><span data-ttu-id="9792a-188">部署此方案</span><span class="sxs-lookup"><span data-stu-id="9792a-188">Deploy this scenario</span></span>

<span data-ttu-id="9792a-189">有关部署信息，请参阅官方 [Citrix 文档](https://docs.citrix.com/en-us/citrix-virtual-apps-desktops/install-configure.html)。</span><span class="sxs-lookup"><span data-stu-id="9792a-189">For deployment information see the official [Citrix documentation](https://docs.citrix.com/en-us/citrix-virtual-apps-desktops/install-configure.html).</span></span>

## <a name="pricing"></a><span data-ttu-id="9792a-190">定价</span><span class="sxs-lookup"><span data-stu-id="9792a-190">Pricing</span></span>

- <span data-ttu-id="9792a-191">Azure 服务费用不包括 Citrix XenDestop 许可证。</span><span class="sxs-lookup"><span data-stu-id="9792a-191">The Citrix XenDestop licenses are not included in Azure service charges.</span></span>
- <span data-ttu-id="9792a-192">Citrix NetScaler 许可费用包含在即用即付模型中。</span><span class="sxs-lookup"><span data-stu-id="9792a-192">The Citrix NetScaler license is included in a pay-as-you-go model.</span></span>
- <span data-ttu-id="9792a-193">使用预留实例可大大降低解决方案的计算费用。</span><span class="sxs-lookup"><span data-stu-id="9792a-193">Using reserved instances will greatly reduce the compute cost for the solution.</span></span>
- <span data-ttu-id="9792a-194">不包括 ExpressRoute 费用。</span><span class="sxs-lookup"><span data-stu-id="9792a-194">The ExpressRoute cost is not included.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9792a-195">后续步骤</span><span class="sxs-lookup"><span data-stu-id="9792a-195">Next Steps</span></span>

- <span data-ttu-id="9792a-196">在[此处](https://docs.citrix.com/en-us/citrix-virtual-apps-desktops/install-configure)查看有关规划和部署的 Citrix 文档。</span><span class="sxs-lookup"><span data-stu-id="9792a-196">Check Citrix documentation for planning and deployment [here](https://docs.citrix.com/en-us/citrix-virtual-apps-desktops/install-configure).</span></span>
- <span data-ttu-id="9792a-197">若要在 Azure 中部署 Citrix ADC (NetScaler)，请在[此处](https://github.com/citrix/netscaler-azure-templates)查看 Citrix 提供的资源管理器模板。</span><span class="sxs-lookup"><span data-stu-id="9792a-197">To deploy Citrix ADC (NetScaler) in Azure, review the Resource Manager templates provided by Citrix [here](https://github.com/citrix/netscaler-azure-templates).</span></span>