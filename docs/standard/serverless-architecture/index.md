---
title: 无服务器应用：体系结构、模式和 Azure 实现
description: 无服务器体系结构指南。 了解何时、为何以及如何为企业应用程序实现无服务器体系结构（相对于服务架构 [IaaS] 或平台即服务 [PaaS]）。
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 6/26/2018
ms.openlocfilehash: 89e5f387e218703a2f6311ef848b3d613a9279f7
ms.sourcegitcommit: 4c158beee818c408d45a9609bfc06f209a523e22
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37404805"
---
![](./media/Cover.jpg)

# <a name="serverless-apps-architecture-patterns-and-azure-implementation"></a><span data-ttu-id="fa12e-104">无服务器应用：体系结构、模式和 Azure 实现</span><span class="sxs-lookup"><span data-stu-id="fa12e-104">Serverless apps: Architecture, patterns, and Azure implementation</span></span>

> <span data-ttu-id="fa12e-105">下载地址：<https://aka.ms/serverless-ebook></span><span class="sxs-lookup"><span data-stu-id="fa12e-105">DOWNLOAD available at: <https://aka.ms/serverless-ebook></span></span>

<span data-ttu-id="fa12e-106">发布者</span><span class="sxs-lookup"><span data-stu-id="fa12e-106">PUBLISHED BY</span></span>

<span data-ttu-id="fa12e-107">Microsoft 开发人员部门、.NET 和 Visual Studio 产品团队</span><span class="sxs-lookup"><span data-stu-id="fa12e-107">Microsoft Developer Division, .NET, and Visual Studio product teams</span></span>

<span data-ttu-id="fa12e-108">Microsoft Corporation 的一个部门</span><span class="sxs-lookup"><span data-stu-id="fa12e-108">A division of Microsoft Corporation</span></span>

<span data-ttu-id="fa12e-109">One Microsoft Way</span><span class="sxs-lookup"><span data-stu-id="fa12e-109">One Microsoft Way</span></span>

<span data-ttu-id="fa12e-110">Redmond, Washington 98052-6399</span><span class="sxs-lookup"><span data-stu-id="fa12e-110">Redmond, Washington 98052-6399</span></span>

<span data-ttu-id="fa12e-111">版权所有 © 2018 Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="fa12e-111">Copyright © 2018 by Microsoft Corporation</span></span>

<span data-ttu-id="fa12e-112">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="fa12e-112">All rights reserved.</span></span> <span data-ttu-id="fa12e-113">未经发布者书面许可，不得以任何形式或任何方式复制或传播本书中的任何内容。</span><span class="sxs-lookup"><span data-stu-id="fa12e-113">No part of the contents of this book may be reproduced or transmitted in any form or by any means without the written permission of the publisher.</span></span>

<span data-ttu-id="fa12e-114">本书“按原样”提供，表达作者的观点和看法。</span><span class="sxs-lookup"><span data-stu-id="fa12e-114">This book is provided "as-is" and expresses the author's views and opinions.</span></span> <span data-ttu-id="fa12e-115">本书中表达的观点、看法和信息（包括 URL 和其他 Internet 网站引用）如有更改，恕不另行通知。</span><span class="sxs-lookup"><span data-stu-id="fa12e-115">The views, opinions and information expressed in this book, including URL and other Internet website references, may change without notice.</span></span>

<span data-ttu-id="fa12e-116">本书中提及的一些示例仅用于说明，纯属虚构。</span><span class="sxs-lookup"><span data-stu-id="fa12e-116">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="fa12e-117">不存在任何实际关联或联系，请勿妄加推断。</span><span class="sxs-lookup"><span data-stu-id="fa12e-117">No real association or connection is intended or should be inferred.</span></span>

<span data-ttu-id="fa12e-118">Microsoft 和 <https://www.microsoft.com> 上“商标”网页列出的商标是 Microsoft 集团公司的商标。</span><span class="sxs-lookup"><span data-stu-id="fa12e-118">Microsoft and the trademarks listed at <https://www.microsoft.com> on the "Trademarks" webpage are trademarks of the Microsoft group of companies.</span></span>

<span data-ttu-id="fa12e-119">Mac 和 macOS 是 Apple Inc. 的商标</span><span class="sxs-lookup"><span data-stu-id="fa12e-119">Mac and macOS are trademarks of Apple Inc.</span></span>

<span data-ttu-id="fa12e-120">所有其他标记和徽标均为其各自所有者的财产。</span><span class="sxs-lookup"><span data-stu-id="fa12e-120">All other marks and logos are property of their respective owners.</span></span>

<span data-ttu-id="fa12e-121">作者:</span><span class="sxs-lookup"><span data-stu-id="fa12e-121">Author:</span></span>

> <span data-ttu-id="fa12e-122">[Jeremy Likness](https://twitter.com/jeremylikness)，Microsoft Corp. APEX 高级云开发大使</span><span class="sxs-lookup"><span data-stu-id="fa12e-122">**[Jeremy Likness](https://twitter.com/jeremylikness)**, Sr. Cloud Developer Advocate, APEX, Microsoft Corp.</span></span>

<span data-ttu-id="fa12e-123">参与者：</span><span class="sxs-lookup"><span data-stu-id="fa12e-123">Contributor:</span></span>

> <span data-ttu-id="fa12e-124">[Cecil Phillip](https://twitter.com/cecilphillip)，Microsoft Corp. APEX 二级云开发大使</span><span class="sxs-lookup"><span data-stu-id="fa12e-124">**[Cecil Phillip](https://twitter.com/cecilphillip)**, Cloud Developer Advocate II, APEX, Microsoft Corp.</span></span>

<span data-ttu-id="fa12e-125">编辑：</span><span class="sxs-lookup"><span data-stu-id="fa12e-125">Editors:</span></span>

> <span data-ttu-id="fa12e-126">[Bill Wagner](https://twitter.com/billwagner)，Microsoft Corp. APEX 高级内容开发者</span><span class="sxs-lookup"><span data-stu-id="fa12e-126">**[Bill Wagner](https://twitter.com/billwagner)**, Senior Content Developer, APEX, Microsoft Corp.</span></span>

> <span data-ttu-id="fa12e-127">[Maira Wenzel](https://twitter.com/mairacw)，Microsoft Corp. APEX 高级内容开发者</span><span class="sxs-lookup"><span data-stu-id="fa12e-127">**[Maira Wenzel](https://twitter.com/mairacw)**, Senior Content Developer, APEX, Microsoft Corp.</span></span>

<span data-ttu-id="fa12e-128">参与者和审阅者：</span><span class="sxs-lookup"><span data-stu-id="fa12e-128">Participants and reviewers:</span></span>

> <span data-ttu-id="fa12e-129">[Steve Smith](https://twitter.com/ardalis)，Ardalis Services 所有者。</span><span class="sxs-lookup"><span data-stu-id="fa12e-129">**[Steve Smith](https://twitter.com/ardalis)**, Owner, Ardalis Services.</span></span>

## <a name="introduction"></a><span data-ttu-id="fa12e-130">介绍</span><span class="sxs-lookup"><span data-stu-id="fa12e-130">Introduction</span></span>

<span data-ttu-id="fa12e-131">无服务器是云平台向纯云本机代码方向的进化。</span><span class="sxs-lookup"><span data-stu-id="fa12e-131">Serverless is the evolution of cloud platforms in the direction of pure cloud native code.</span></span> <span data-ttu-id="fa12e-132">通过无服务器，开发者更接近业务逻辑，避免基础结构问题。</span><span class="sxs-lookup"><span data-stu-id="fa12e-132">Serverless brings developers closer to business logic while insulating them from infrastructure concerns.</span></span> <span data-ttu-id="fa12e-133">这种模式并不意味着“没有服务器”，而是“更少的服务器”。</span><span class="sxs-lookup"><span data-stu-id="fa12e-133">It's a pattern that doesn't imply "no server" but rather, "less server."</span></span> <span data-ttu-id="fa12e-134">无服务器代码是事件驱动的。</span><span class="sxs-lookup"><span data-stu-id="fa12e-134">Serverless code is event-driven.</span></span> <span data-ttu-id="fa12e-135">无论是传统的 HTTP Web 请求，还是计时器或上传文件的结果都可以触发代码。</span><span class="sxs-lookup"><span data-stu-id="fa12e-135">Code may be triggered by anything from a traditional HTTP web request to a timer or the result of uploading a file.</span></span> <span data-ttu-id="fa12e-136">无服务器背后的基础结构可实现即时缩放以满足弹性需求，并提供微计费以真正“为所使用的量付费”。</span><span class="sxs-lookup"><span data-stu-id="fa12e-136">The infrastructure behind serverless allows for instant scale to meet elastic demands and offers micro-billing to truly "pay for what you use."</span></span> <span data-ttu-id="fa12e-137">无服务器需要一种新的生成应用程序的思维和方法，它并不是解决每个问题的正确解决方案。</span><span class="sxs-lookup"><span data-stu-id="fa12e-137">Serverless requires a new way of thinking and approach to building applications and isn't the right solution for every problem.</span></span> <span data-ttu-id="fa12e-138">作为开发者，必须确定：</span><span class="sxs-lookup"><span data-stu-id="fa12e-138">As a developer, you must decide:</span></span>

* <span data-ttu-id="fa12e-139">无服务器的优点和缺点是什么？</span><span class="sxs-lookup"><span data-stu-id="fa12e-139">What are the pros and cons of serverless?</span></span>
* <span data-ttu-id="fa12e-140">为什么要考虑为自己的应用程序使用无服务器？</span><span class="sxs-lookup"><span data-stu-id="fa12e-140">Why should you consider serverless for your own applications?</span></span>
* <span data-ttu-id="fa12e-141">如何生成、测试、部署和维护无服务器代码？</span><span class="sxs-lookup"><span data-stu-id="fa12e-141">How can you build, test, deploy, and maintain your serverless code?</span></span>
* <span data-ttu-id="fa12e-142">在现有应用程序中将代码迁移到无服务器有什么意义？完成此转换的最佳方法是什么？</span><span class="sxs-lookup"><span data-stu-id="fa12e-142">Where does it make sense to migrate code to serverless in existing applications, and what is the best way to accomplish this transformation?</span></span>

## <a name="about-this-guide"></a><span data-ttu-id="fa12e-143">关于本指南</span><span class="sxs-lookup"><span data-stu-id="fa12e-143">About this guide</span></span>

<span data-ttu-id="fa12e-144">本指南重点介绍使用无服务器的应用程序的云本机开发。</span><span class="sxs-lookup"><span data-stu-id="fa12e-144">This guide focuses on cloud native development of applications that use serverless.</span></span> <span data-ttu-id="fa12e-145">本书重点介绍了这些优点并揭示了开发无服务器应用的潜在缺点，并提供了对无服务器体系结构的调查。</span><span class="sxs-lookup"><span data-stu-id="fa12e-145">The book highlights the benefits and exposes the potential drawbacks of developing serverless apps and provides a survey of serverless architectures.</span></span> <span data-ttu-id="fa12e-146">介绍了有关使用无服务器的许多示例以及各种无服务器设计模式。</span><span class="sxs-lookup"><span data-stu-id="fa12e-146">Many examples of how serverless can be used are illustrated along with various serverless design patterns.</span></span>

<span data-ttu-id="fa12e-147">本指南介绍了 Azure 无服务器平台的组件，并重点介绍了如何使用 [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview) 实现无服务器。</span><span class="sxs-lookup"><span data-stu-id="fa12e-147">This guide explains the components of the Azure serverless platform and focuses specifically on implementation of serverless using [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview).</span></span> <span data-ttu-id="fa12e-148">你将了解触发器和绑定以及如何使用 Durable Functions 实现依赖于状态的无服务器应用。</span><span class="sxs-lookup"><span data-stu-id="fa12e-148">You'll learn about triggers and bindings as well as how to implement serverless apps that rely on state using durable functions.</span></span> <span data-ttu-id="fa12e-149">最后，业务示例和案例研究将有助于提供用于确定无服务器是否是项目正确方法的上下文和参考框架。</span><span class="sxs-lookup"><span data-stu-id="fa12e-149">Finally, business examples and case studies will help provide context and a frame of reference to determine whether serverless is the right approach for your projects.</span></span>

## <a name="evolution-of-cloud-platforms"></a><span data-ttu-id="fa12e-150">云平台的演变</span><span class="sxs-lookup"><span data-stu-id="fa12e-150">Evolution of cloud platforms</span></span>

<span data-ttu-id="fa12e-151">无服务器是云平台多次迭代的巅峰。</span><span class="sxs-lookup"><span data-stu-id="fa12e-151">Serverless is the culmination of several iterations of cloud platforms.</span></span> <span data-ttu-id="fa12e-152">这种演变始于数据中心的物理计算机，然后经历了服务架构 (IaaS) 和平台即服务 (PaaS) 的发展阶段。</span><span class="sxs-lookup"><span data-stu-id="fa12e-152">The evolution began with physical metal in the data center and progressed through Infrastructure as a Service (IaaS) and Platform as a Service (PaaS).</span></span>

![从本地到无服务器的演变](./media/serverless-evolution-iaas-paas.png)

<span data-ttu-id="fa12e-154">在云之前，开发和运营之间存在明显的界限。</span><span class="sxs-lookup"><span data-stu-id="fa12e-154">Before the cloud, a discernible boundary existed between development and operations.</span></span> <span data-ttu-id="fa12e-155">部署应用程序需要回答无数问题，例如：</span><span class="sxs-lookup"><span data-stu-id="fa12e-155">Deploying an application meant answering myriad questions like:</span></span>

* <span data-ttu-id="fa12e-156">应该安装什么硬件？</span><span class="sxs-lookup"><span data-stu-id="fa12e-156">What hardware should be installed?</span></span>
* <span data-ttu-id="fa12e-157">如何保护对计算机的物理访问？</span><span class="sxs-lookup"><span data-stu-id="fa12e-157">How is physical access to the machine secured?</span></span>
* <span data-ttu-id="fa12e-158">数据中心是否需要不间断电源 (UPS)？</span><span class="sxs-lookup"><span data-stu-id="fa12e-158">Does the data center require an Uninterruptible Power Supply (UPS)?</span></span>
* <span data-ttu-id="fa12e-159">存储备份发送到何处？</span><span class="sxs-lookup"><span data-stu-id="fa12e-159">Where are storage backups sent?</span></span>
* <span data-ttu-id="fa12e-160">应该有冗余电源吗？</span><span class="sxs-lookup"><span data-stu-id="fa12e-160">Should there be redundant power?</span></span>

<span data-ttu-id="fa12e-161">此类问题不胜枚举，相关开销巨大。</span><span class="sxs-lookup"><span data-stu-id="fa12e-161">The list goes on and the overhead was enormous.</span></span> <span data-ttu-id="fa12e-162">在许多情况下，IT 部门不得不处理大量浪费。</span><span class="sxs-lookup"><span data-stu-id="fa12e-162">In many situations, IT departments were forced to deal with incredible waste.</span></span> <span data-ttu-id="fa12e-163">浪费是由服务器过度分配导致的，例如用于灾难恢复的备份计算机以及用于横向扩展的备用服务器。幸运的是，随着虚拟化技术（如 [Hyper-V](/virtualization/hyper-v-on-windows/about/)）和虚拟机 (VM) 的引入，产生了服务架构 (IaaS)。</span><span class="sxs-lookup"><span data-stu-id="fa12e-163">The waste was due to over-allocation of servers as backup machines for disaster recovery and standby servers to enable scale-out. Fortunately, the introduction of virtualization technology (like [Hyper-V](/virtualization/hyper-v-on-windows/about/)) with Virtual Machines (VMs) gave rise to Infrastructure as a Service (IaaS).</span></span> <span data-ttu-id="fa12e-164">虚拟化基础结构允许运营将一组标准服务器设置为主干网，从而形成一个灵活的环境，能够“按需”预配唯一服务器。</span><span class="sxs-lookup"><span data-stu-id="fa12e-164">Virtualized infrastructure allowed operations to set up a standard set of servers as the backbone, leading to a flexible environment capable of provisioning unique servers "on demand."</span></span> <span data-ttu-id="fa12e-165">更重要的是，虚拟化为使用云提供虚拟机“即服务”奠定了基础。</span><span class="sxs-lookup"><span data-stu-id="fa12e-165">More important, virtualization set the stage for using the cloud to provide virtual machines "as a service."</span></span> <span data-ttu-id="fa12e-166">公司不必担心冗余电源或物理计算机的问题。</span><span class="sxs-lookup"><span data-stu-id="fa12e-166">Companies could easily get out of the business of worrying about redundant power or physical machines.</span></span> <span data-ttu-id="fa12e-167">他们可专注于虚拟环境。</span><span class="sxs-lookup"><span data-stu-id="fa12e-167">Instead, they focused on the virtual environment.</span></span>

<span data-ttu-id="fa12e-168">IaaS 仍然需要大量开销，因为运营仍然负责执行各种任务。</span><span class="sxs-lookup"><span data-stu-id="fa12e-168">IaaS still requires heavy overhead because operations is still responsible for various tasks.</span></span> <span data-ttu-id="fa12e-169">这些任务包括：</span><span class="sxs-lookup"><span data-stu-id="fa12e-169">These tasks include:</span></span>

* <span data-ttu-id="fa12e-170">修补和备份服务器。</span><span class="sxs-lookup"><span data-stu-id="fa12e-170">Patching and backing up servers.</span></span>
* <span data-ttu-id="fa12e-171">安装包。</span><span class="sxs-lookup"><span data-stu-id="fa12e-171">Installing packages.</span></span>
* <span data-ttu-id="fa12e-172">使操作系统保持最新状态。</span><span class="sxs-lookup"><span data-stu-id="fa12e-172">Keeping the operating system up-to-date.</span></span>
* <span data-ttu-id="fa12e-173">监控应用程序。</span><span class="sxs-lookup"><span data-stu-id="fa12e-173">Monitoring the application.</span></span>

<span data-ttu-id="fa12e-174">新的发展通过平台即服务 (PaaS) 减少了开销。</span><span class="sxs-lookup"><span data-stu-id="fa12e-174">The next evolution reduced the overhead by providing Platform as a Service (PaaS).</span></span> <span data-ttu-id="fa12e-175">借助 PaaS，云提供程序可处理操作系统、安全修补程序和支持特定平台所需的包。</span><span class="sxs-lookup"><span data-stu-id="fa12e-175">With PaaS, the cloud provider handles operating systems, security patches, and even the required packages to support a specific platform.</span></span> <span data-ttu-id="fa12e-176">开发者只需选择“平台目标”（如“Web 应用程序”或“API 终结点”）并直接部署代码，而不用生成 VM，然后配置 .NET Framework 并启用 Internet Information Services (IIS) 服务器。</span><span class="sxs-lookup"><span data-stu-id="fa12e-176">Instead of building a VM then configuring the .NET Framework and standing up Internet Information Services (IIS) servers, developers simply choose a "platform target" such as "web application" or "API endpoint" and deploy code directly.</span></span> <span data-ttu-id="fa12e-177">基础结构问题减少到：</span><span class="sxs-lookup"><span data-stu-id="fa12e-177">The infrastructure questions are reduced to:</span></span>

* <span data-ttu-id="fa12e-178">需要什么大小的服务？</span><span class="sxs-lookup"><span data-stu-id="fa12e-178">What size services are needed?</span></span>
* <span data-ttu-id="fa12e-179">如何横向扩展服务（添加更多服务器或节点）？</span><span class="sxs-lookup"><span data-stu-id="fa12e-179">How do the services scale out (add more servers or nodes)?</span></span>
* <span data-ttu-id="fa12e-180">如何纵向扩展服务（增加托管服务器或节点的容量）？</span><span class="sxs-lookup"><span data-stu-id="fa12e-180">How do the services scale up (increase the capacity of hosting servers or nodes)?</span></span>

<span data-ttu-id="fa12e-181">无服务器通过专注于事件驱动代码进一步抽象化服务器。</span><span class="sxs-lookup"><span data-stu-id="fa12e-181">Serverless further abstracts servers by focusing on event-driven code.</span></span> <span data-ttu-id="fa12e-182">开发者可关注执行一项操作的微服务，而非平台。</span><span class="sxs-lookup"><span data-stu-id="fa12e-182">Instead of a platform, developers can focus on a microservice that does one thing.</span></span> <span data-ttu-id="fa12e-183">生成无服务器代码的两个关键问题是：</span><span class="sxs-lookup"><span data-stu-id="fa12e-183">The two key questions for building the serverless code are:</span></span>

* <span data-ttu-id="fa12e-184">什么触发代码？</span><span class="sxs-lookup"><span data-stu-id="fa12e-184">What triggers the code?</span></span>
* <span data-ttu-id="fa12e-185">代码会执行哪些操作？</span><span class="sxs-lookup"><span data-stu-id="fa12e-185">What does the code do?</span></span>

<span data-ttu-id="fa12e-186">通过无服务器，抽象化基础结构。</span><span class="sxs-lookup"><span data-stu-id="fa12e-186">With serverless, infrastructure is abstracted.</span></span> <span data-ttu-id="fa12e-187">在某些情况下，开发者不再担心主机。</span><span class="sxs-lookup"><span data-stu-id="fa12e-187">In some cases, the developer no longer worries about the host at all.</span></span> <span data-ttu-id="fa12e-188">无论是运行 IIS、Kestrel、Apache 还是其他 Web 服务器的实例来管理 Web 请求，开发者都会关注 HTTP 触发器。</span><span class="sxs-lookup"><span data-stu-id="fa12e-188">Whether or not an instance of IIS, Kestrel, Apache, or some other web server is running to manage web requests, the developer focuses on an HTTP trigger.</span></span> <span data-ttu-id="fa12e-189">触发器为请求提供标准的跨平台有效负载。</span><span class="sxs-lookup"><span data-stu-id="fa12e-189">The trigger provides the standard, cross-platform payload for the request.</span></span> <span data-ttu-id="fa12e-190">有效负载不仅简化了开发过程，而且便于测试，在某些情况下，使代码可跨平台轻松移植。</span><span class="sxs-lookup"><span data-stu-id="fa12e-190">The payload not only simplifies the development process, but facilitates testing and in some cases, makes the code easily portable across platforms.</span></span>

<span data-ttu-id="fa12e-191">无服务器的另一个功能是微计费。</span><span class="sxs-lookup"><span data-stu-id="fa12e-191">Another feature of serverless is micro-billing.</span></span> <span data-ttu-id="fa12e-192">Web 应用通常托管 Web API 终结点。</span><span class="sxs-lookup"><span data-stu-id="fa12e-192">It's common for web applications to host Web API endpoints.</span></span> <span data-ttu-id="fa12e-193">在传统的裸机、IaaS 和 PaaS 实现中，托管 API 的资源是连续付费的。</span><span class="sxs-lookup"><span data-stu-id="fa12e-193">In traditional bare metal, IaaS and even PaaS implementations, the resources to host the APIs are paid for continuously.</span></span> <span data-ttu-id="fa12e-194">这意味着即使没有访问终结点，也需要付费来托管终结点。</span><span class="sxs-lookup"><span data-stu-id="fa12e-194">That means you pay to host the endpoints even when they aren't being accessed.</span></span> <span data-ttu-id="fa12e-195">通常会发现调用某个 API 比调用其他 API 的次数更多，因此整个系统基于支持热门终结点进行缩放。</span><span class="sxs-lookup"><span data-stu-id="fa12e-195">Often you'll find one API is called more than others, so the entire system is scaled based on supporting the popular endpoints.</span></span> <span data-ttu-id="fa12e-196">借助无服务器，可独立缩放每个终结点并支付使用费用，因此在不调用 API 时不会产生任何成本。</span><span class="sxs-lookup"><span data-stu-id="fa12e-196">Serverless enables you to scale each endpoint independently and pay for usage, so no costs are incurred when the APIs aren't being called.</span></span> <span data-ttu-id="fa12e-197">在许多情况下，迁移可以大大降低用于支持终结点的持续成本。</span><span class="sxs-lookup"><span data-stu-id="fa12e-197">Migration may in many circumstances dramatically reduce the ongoing cost to support the endpoints.</span></span>

## <a name="what-this-guide-doesnt-cover"></a><span data-ttu-id="fa12e-198">本指南未涵盖的内容</span><span class="sxs-lookup"><span data-stu-id="fa12e-198">What this guide doesn't cover</span></span>

<span data-ttu-id="fa12e-199">本指南特别强调了体系结构方法和设计模式，并未深入探讨 Azure Functions、[逻辑应用](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps)或其他无服务器平台的实现细节。</span><span class="sxs-lookup"><span data-stu-id="fa12e-199">This guide specifically emphasizes architecture approaches and design patterns and isn't a deep dive into the implementation details of Azure Functions, [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps), or other serverless platforms.</span></span> <span data-ttu-id="fa12e-200">本指南不包括逻辑应用的高级工作流或 Azure Functions 的功能等，如配置跨源资源共享(CORS)、应用自定义域或上传 SSL 证书。</span><span class="sxs-lookup"><span data-stu-id="fa12e-200">This guide doesn't cover, for example, advanced workflows with Logic Apps or features of Azure Functions such as configuring Cross-Origin Resource Sharing (CORS), applying custom domains, or uploading SSL certificates.</span></span> <span data-ttu-id="fa12e-201">可以通过联机 [Azure Functions 文档](https://docs.microsoft.com/azure/azure-functions/functions-reference)获得这些详细信息。</span><span class="sxs-lookup"><span data-stu-id="fa12e-201">These details are available through the online [Azure Functions documentation](https://docs.microsoft.com/azure/azure-functions/functions-reference).</span></span>

### <a name="additional-resources"></a><span data-ttu-id="fa12e-202">其他资源</span><span class="sxs-lookup"><span data-stu-id="fa12e-202">Additional resources</span></span>

* [<span data-ttu-id="fa12e-203">Azure 体系结构中心</span><span class="sxs-lookup"><span data-stu-id="fa12e-203">Azure Architecture center</span></span>](https://docs.microsoft.com/azure/architecture/)
* [<span data-ttu-id="fa12e-204">云应用程序的最佳做法</span><span class="sxs-lookup"><span data-stu-id="fa12e-204">Best practices for cloud applications</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/api-design)

## <a name="who-should-use-the-guide"></a><span data-ttu-id="fa12e-205">本指南的目标读者</span><span class="sxs-lookup"><span data-stu-id="fa12e-205">Who should use the guide</span></span>

<span data-ttu-id="fa12e-206">本指南面向具有以下需求的开发者和解决方案架构师：需要使用 .NET 生成企业应用程序（这些应用程序可能使用本地或云端的无服务器组件）。</span><span class="sxs-lookup"><span data-stu-id="fa12e-206">This guide was written for developers and solution architects who want to build enterprise applications with .NET that may use serverless components either on premises or in the cloud.</span></span> <span data-ttu-id="fa12e-207">可为具有以下需求的开发者、架构师和技术决策制定者提供帮助：</span><span class="sxs-lookup"><span data-stu-id="fa12e-207">It's useful to developers, architects, and technical decision makers interested in:</span></span>

* <span data-ttu-id="fa12e-208">了解无服务器开发的优点和缺点</span><span class="sxs-lookup"><span data-stu-id="fa12e-208">Understanding the pros and cons of serverless development</span></span>
* <span data-ttu-id="fa12e-209">学习如何处理无服务器体系结构</span><span class="sxs-lookup"><span data-stu-id="fa12e-209">Learning how to approach serverless architecture</span></span>
* <span data-ttu-id="fa12e-210">无服务器应用实现的示例</span><span class="sxs-lookup"><span data-stu-id="fa12e-210">Example implementations of serverless apps</span></span>

## <a name="how-to-use-the-guide"></a><span data-ttu-id="fa12e-211">如何使用本指南</span><span class="sxs-lookup"><span data-stu-id="fa12e-211">How to use the guide</span></span>

<span data-ttu-id="fa12e-212">本指南的第一部分通过比较几种不同的体系结构方法来探讨无服务器的可行性。</span><span class="sxs-lookup"><span data-stu-id="fa12e-212">The first part of this guide examines why serverless is a viable option by comparing several different architecture approaches.</span></span> <span data-ttu-id="fa12e-213">本指南分析了技术和开发生命周期，因为软件开发的所有方面都受到体系结构决策的影响。</span><span class="sxs-lookup"><span data-stu-id="fa12e-213">It examines both the technology and development lifecycle, because all aspects of software development are impacted by architecture decisions.</span></span> <span data-ttu-id="fa12e-214">然后，本指南介绍了用例和设计模式，并说明了使用 Azure Functions 的参考实现。</span><span class="sxs-lookup"><span data-stu-id="fa12e-214">The guide then examines use cases and design patterns and includes reference implementations using Azure Functions.</span></span> <span data-ttu-id="fa12e-215">每个部分都包含介绍特定方面的其他资源。</span><span class="sxs-lookup"><span data-stu-id="fa12e-215">Each section contains additional resources to learn more about a particular area.</span></span> <span data-ttu-id="fa12e-216">该指南最后提供了有关无服务器实现的演练和实践探索的资源。</span><span class="sxs-lookup"><span data-stu-id="fa12e-216">The guide concludes with resources for walkthroughs and hands-on exploration of serverless implementation.</span></span>

## <a name="send-your-feedback"></a><span data-ttu-id="fa12e-217">提供你的反馈</span><span class="sxs-lookup"><span data-stu-id="fa12e-217">Send your feedback</span></span>

<span data-ttu-id="fa12e-218">我们正在不断完善指南和相关示例，欢迎你提供反馈！</span><span class="sxs-lookup"><span data-stu-id="fa12e-218">The guide and related samples are constantly evolving, so your feedback is welcomed!</span></span> <span data-ttu-id="fa12e-219">如果对如何改进本指南有任何建议，请使用 [GitHub 问题](https://github.com/dotnet/docs/issues)上任何页面底部的反馈部分进行反馈。</span><span class="sxs-lookup"><span data-stu-id="fa12e-219">If you have comments about how this guide can be improved, use the feedback section at the bottom of any page built on [GitHub issues](https://github.com/dotnet/docs/issues).</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="fa12e-220">下一篇</span><span class="sxs-lookup"><span data-stu-id="fa12e-220">Next</span></span>](architecture-approaches.md)