---
title: Windows Admin Center란?
description: Windows Admin Center란(Project Honolulu)?
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 06/07/2019
ms.openlocfilehash: cb4e3ab2bf98a0c2d51483642fe5388e468dbbb4
ms.sourcegitcommit: 20d07170c7f3094c2fb4455f54b13ec4b102f2d7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/13/2020
ms.locfileid: "81269270"
---
# <a name="what-is-windows-admin-center"></a>Windows Admin Center란?

> 적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center는 Azure 또는 클라우드 종속성 없이 Windows Server를 관리할 수 있는 로컬로 배포하는 브라우저 기반의 새로운 관리 도구 집합입니다. Windows Admin Center는 서버 인프라의 모든 측면에 대한 완전한 제어를 부여하며 인터넷에 연결되지 않은 개인 네트워크에서의 서버 관리에 특히 유용합니다.

Windows Admin Center는 서버 관리자 및 MMC와 같은 "기본 제공" 관리 도구의 진화된 모델입니다. System Center를 보완하며 해당 기능을 대신하지는 않습니다.

![](../media/wac-complements.png)

## <a name="how-does-windows-admin-center-work"></a>Windows Admin Center는 어떻게 작동합니까?

Windows Admin Center는 웹 브라우저에서 실행되며 Windows Server 또는 도메인 조인 Windows 10에 설치된 **Windows Admin Center 게이트웨이**를 통해 Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows 10 등을 관리합니다. 게이트웨이는 WinRM을 통해 원격 PowerShell 및 WMI를 사용하여 서버를 관리합니다. 게이트웨이는 [다운로드](https://aka.ms/windowsadmincenter)할 수 있는 단일 경량 .msi 패키지에서 Windows Admin Center에 포함됩니다.

DNS에 게시되고 해당 회사 방화벽을 통해 액세스할 수 있을 때 Windows Admin Center 게이트웨이를 통해 어디서든 Microsoft Edge 또는 Google Chrome으로 안전하게 서버에 연결하고 관리할 수 있습니다.

![](../media/architecture.png)

## <a name="learn-how-windows-admin-center-improves-your-management-environment"></a>Windows Admin Center가 관리 환경을 개선하는 방법을 설명합니다.

### <a name="familiar-functionality"></a>**친숙한 기능**

Windows Admin Center는 MMC(Microsoft Management Console)와 같이 처음부터 시스템이 빌드 및 관리되는 방식을 위해 고안된 오늘날 잘 알려진 오랜 관리 플랫폼의 혁명입니다. Windows Admin Center는 현재 Windows Server 및 클라이언트를 관리하는 데 사용하는 다양한 친숙한 도구를 포함합니다.

### <a name="easy-to-install-and-use"></a>**설치 및 사용이 용이**

Windows 10 컴퓨터에 [설치](../deploy/install.md)하고 몇 분만에 관리를 시작하고 또는 게이트웨이 역할을 하는 Windows 2016 서버에 설치하여 조직 전체가 웹 브라우저에서 컴퓨터를 관리하도록 합니다.

### <a name="complements-existing-solutions"></a>**기존 솔루션 보완**

Windows Admin Center는 System Center, Azure 관리 및 보안과 같은 솔루션과 함께 작동하며 세부적인 단일 컴퓨터 관리 작업을 수행하는 기능을 추가합니다.

### <a name="manage-from-anywhere"></a>**어디에서든지 관리**

공용 인터넷에 Windows Admin Center 게이트웨이 서버를 게시한 다음 모두 안전한 방식으로 어디에서든지 서버에 연결하여 서버를 관리할 수 있습니다.

### <a name="enhanced-security-for-your-management-platform"></a>**관리 플랫폼에 대한 향상된 보안**

Windows Admin Center에는의 사용자 관리 플랫폼의 [보안을 강화](../plan/user-access-options.md)하는 많은 기능이 있습니다. 역할 기반 액세스 제어를 사용하면 관리 기능에 액세스할 수 있는 관리자를 미세 조정할 수 있습니다. 게이트웨이 인증 옵션에는 로컬 그룹, 로컬 도메인 기반 Active Directory 및 클라우드 기반 Azure Active Directory가 포함됩니다.  또한, 환경에서 수행되는 관리 작업에 대한 [정보를 얻을 수](../use/logging.md) 있습니다.

### <a name="azure-integration"></a>**Azure 통합**

Windows Admin Center에는 Azure Active Directory, Azure Backup, Azure Site Recovery 등을 비롯한 [Azure 서비스와 통합](../plan/azure-integration-options.md)할 수 있는 많은 지점이 있습니다.

### <a name="manage-hyper-converged-clusters"></a>**하이퍼 컨버지드 클러스터 관리**

Windows Admin Center는 가상화된 컴퓨팅, 스토리지 및 네트워킹 구성 요소를 포함하여 [하이퍼 컨버지드 클러스터 관리](../use/manage-hyper-converged.md)를 위한 최상의 환경을 제공합니다.

### <a name="extensibility"></a>**확장성**

Windows Admin Center는 Microsoft 및 타사 개발자를 위한 기능과 함께 처음부터 현재 제품을 능가하는 도구 및 솔루션을 구축하는 것을 염두에 두고 만들어졌습니다. Microsoft는 개발자가 Windows Admin Center에 대한 자신의 도구를 만들 수 있도록 하는 [SDK](../extend/extensibility-overview.md)를 제공합니다.

> [!Tip]
> Windows Admin Center를 설치할 준비가 되셨습니까? [지금 다운로드](https://aka.ms/windowsadmincenter)
