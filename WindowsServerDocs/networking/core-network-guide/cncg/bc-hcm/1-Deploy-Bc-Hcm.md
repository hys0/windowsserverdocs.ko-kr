---
title: BranchCache 호스트 캐시 모드 배포
description: 이 가이드에서는 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache를 배포 하는 방법 지침을 제공
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: 4235231c-4732-4ea9-9330-2a8c8a616d39
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 49e74132dba2909b7e5b639c95ef50064cf23e8c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356383"
---
# <a name="deploy-branchcache-hosted-cache-mode"></a>BranchCache 호스트 캐시 모드 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

계획 및 배포를 완벽 하 게 작동 하는 네트워크 및 새로운 Active Directory에 필요한 핵심 구성 요소에 대 한 지침을 제공 하는 Windows Server 2016 핵심 네트워크 가이드&reg; 새 포리스트에 있는 도메인입니다.

이 가이드에서는 읽기와 하나 이상의 지점에서 호스트 캐시 모드로 BranchCache를 배포 하기 위한 지침을 제공 하 여 핵심 네트워크에 구축 하는 방법에 설명\-클라이언트 컴퓨터가 Windows를 실행 하는 도메인 컨트롤러만&reg; Windows 8.1 또는 Windows 8, 10, 도메인에 가입 되어 있습니다.

>[!IMPORTANT]
>배포 하거나 이미 Windows Server 2008 r 2를 실행 하는 BranchCache 호스트 캐시 서버를 배포 하려는 경우에이 가이드를 사용 하지 마십시오. 이 가이드에서는 Windows Server를 실행 하는 호스트 캐시 서버와 호스트 캐시 모드를 배포 하기 위한 지침을 제공&reg; 2016 년까지 Windows Server 2012 R2 또는 Windows Server 2012.

이 가이드에는 다음 섹션이 수록되어 있습니다.

- [이 가이드를 사용 하기 위한 필수 조건](#bkmk_pre)

- [이 가이드 정보](#bkmk_about)

- [이 가이드에서 설명하지 않는 정보](#bkmk_not)

- [기술 개요](#bkmk_tech)

- [BranchCache 호스트 캐시 모드 배포 개요](2-Bc-Hcm-Deploy-Overview.md)

- [BranchCache 호스트 캐시 모드 배포 계획](3-Bc-Hcm-Plan.md)

- [BranchCache 호스트 캐시 모드 배포](4-Bc-Hcm-Deployment.md)

- [추가 리소스](11-Bc-Hcm-additional-resources.md)

## <a name="bkmk_pre"></a>이 가이드를 사용 하기 위한 필수 조건

Windows Server 2016 핵심 네트워크 가이드에 부록 가이드입니다. 이 가이드를 사용하여 호스트 캐시 모드로 BranchCache를 배포하려면 먼저 다음을 수행해야 합니다.

- 핵심 네트워크 가이드를 사용하여 본사에 핵심 네트워크를 배포하거나, 핵심 네트워크 가이드에 제공된 기술이 네트워크에 이미 설치되고 정상적으로 작동하게 합니다. 이러한 기술에는 TCP 포함\/IP v4, DHCP, Active Directory 도메인 서비스 \(AD DS\), 및 DNS입니다.

    > [!NOTE]
    > Windows Server 2016 [핵심 네트워크 가이드](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide) 는 Windows Server 2016 기술 라이브러리에서 사용할 수 있습니다.  

- 본사에서 또는 클라우드 데이터 센터에서 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 BranchCache 콘텐츠 서버를 배포 합니다. BranchCache 콘텐츠 서버를 배포 하는 방법에 대 한 자세한 내용은 참조 [추가 리소스](11-Bc-Hcm-additional-resources.md)합니다.

- 광역 네트워크를 설정 \(WAN\) 지점 사무실, 본사 간의 연결 및 해당되는 경우 가상 사설망을 사용하여 클라우드 리소스를 \(VPN\), DirectAccess, 또는 기타 연결 방법을 합니다.

- BITS Background Intelligent Transfer Service (), 하이퍼 텍스트 전송 프로토콜 (HTTP) 및 서버 메시지 블록 (SMB)를 지 원하는 BranchCache를 제공 하는 다음 운영 체제 중 하나를 실행 하는 지점의 클라이언트 컴퓨터를 배포 합니다.
    - Windows 10 Enterprise
    - Windows 10 Education
    - Windows 8.1 Enterprise
    - Windows 8 Enterprise

> [!NOTE]
> 다음 운영 체제에서 BranchCache HTTP와 SMB 기능을 지원 하지 않지만 비트 BranchCache 기능을 지원 합니다.
>     - Windows 10 Pro 비트만 지원
>     - Windows 8.1 Pro 비트만 지원
>     - Windows 8 Pro 비트만 지원

## <a name="bkmk_about"></a>이 가이드 정보

이 가이드는 Windows Server 2016 핵심 네트워크 가이드 또는 Windows Server 2012 핵심 네트워크 가이드의 지침에 따라 핵심 네트워크를 배포 하는 네트워크 및 시스템 관리자를 위한 것으로, 이전에 배포 된 핵심 네트워크 가이드에 포함 된 기술에는 Active Directory Domain Services \(AD DS @ no__t-1, 도메인 이름 서비스 \(DNS @ no__t-3, 동적 호스트 구성 프로토콜 \(DHCP @ no__t-5, TCP @ no__t-6IP v4가 포함 됩니다.

이 배포 시나리오에서 사용되는 각 기술에 대한 디자인 및 배포 가이드를 검토하는 것이 좋습니다. 이들 가이드를 통해 이 배포 시나리오가 조직 네트워크에 필요한 서비스 및 구성을 제공하는지 확인할 수 있습니다.

## <a name="bkmk_not"></a>이 가이드에서 제공 하지 않는 내용

이 가이드에서는 BranchCache 모드 및 기능에 대한 정보를 포함하여 BranchCache에 대한 개념 정보를 제공하지 않습니다.  

이 가이드에서는 WAN 연결이나 DHCP, RODC 또는 VPN 서버와 같은 기타 기술을 지사에 배포하는 방법에 대한 정보를 제공하지 않습니다.

또한 이 가이드에서는 호스트 캐시 서버를 배포할 때 사용해야 하는 하드웨어에 대한 지침을 제공하지 않습니다. 호스트 캐시 서버에서 다른 서비스 및 응용 프로그램을 실행할 수 있지만 워크로드, 하드웨어 용량 및 지사 규모, 특정 컴퓨터에 BranchCache 호스트 캐시 서버를 설치할지 여부 및 캐시에 할당할 디스크 공간 크기에 따라 결정해야 합니다.  
이 가이드는 Windows 7을 실행 중인 컴퓨터를 구성 하기 위한 지침을 제공 하지 않습니다. 하도록 구성 해야 지점에 이미 Windows 7을 실행 하는 클라이언트 컴퓨터를 설정한 경우 Windows 10, Windows 8.1 및 Windows 8을 실행 중인 클라이언트 컴퓨터에 대 한이 가이드에 제공 된 것과 다른 프로시저를 사용 합니다.
  
또한 Windows 7을 실행 하는 컴퓨터의 경우 호스트 캐시 서버 클라이언트 컴퓨터를 신뢰 하는 인증 기관에서 발급 하는 서버 인증서로 구성 해야 합니다. @no__t 모든 클라이언트 컴퓨터에서 Windows 10, Windows 8.1 또는 Windows 8을 실행 하는 경우 서버 인증서를 사용 하 여 호스트 캐시 서버를 구성할 필요가 없습니다. \) 
> [!IMPORTANT]
> Windows Server 2008 r 2를 사용 하 여 호스트 캐시 서버는 Windows Server 2008 r 2를 실행 하는 경우 [BranchCache 배포 가이드](https://technet.microsoft.com/library/ee649232(v=ws.10).aspx) 이 가이드를 호스트 캐시 모드로 BranchCache를 배포 하는 대신 합니다. Windows 10에 Windows 7에서의 Windows 버전을 실행 중인 모든 BranchCache 클라이언트에이 설명서에서 설명 하는 그룹 정책 설정을 적용 합니다. 이 가이드의 단계를 사용 하 여 Windows Server 2008 r 2를 실행 중인 컴퓨터를 구성할 수 없습니다.

## <a name="bkmk_tech"></a>기술 개요

이 부록 가이드에서 설치 및 구성하는 데 필요한 기술은 BranchCache뿐입니다. 웹 및 파일 서버와 같은 콘텐츠 서버에서 Windows PowerShell BranchCache 명령을 실행해야 하지만 어떤 방식으로든 콘텐츠 서버를 변경하거나 다시 구성할 필요가 없습니다. 또한 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012에서 AD DS를 실행 중인 도메인 컨트롤러에서 그룹 정책을 사용 하 여 클라이언트 컴퓨터를 구성 해야 합니다.

### <a name="branchcache"></a>BranchCache

BranchCache는 일부 버전의 Windows Server 2016 및 Windows 10 운영 체제와 Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2 및 Windows 7의 일부 버전에 포함 되어 있는 광역 네트워크 (WAN) 대역폭 최적화 기술입니다.

파일을 사용자가 원격 서버의 콘텐츠에 액세스할 때 WAN 대역폭을 최적화 하려면 BranchCache 본사에서 클라이언트가 요청한 콘텐츠를 다운로드 또는 호스트 된 클라우드 콘텐츠 서버와 wan이 아닌 로컬 동일한 콘텐츠를 액세스 하는 지점에서 다른 클라이언트 컴퓨터 수 있도록 지점 사무실 위치에서 콘텐츠를 캐시 합니다.

호스트 캐시 모드로 BranchCache를 배포하는 경우 지사에서 클라이언트 컴퓨터를 호스트 캐시 모드 클라이언트로 구성한 다음 지사에 호스트 캐시 서버를 배포해야 합니다. 이 가이드에서는 웹 및 파일 서버에서 prehashed 및 미리 로드 된 콘텐츠를 사용 하 여 호스트 캐시 서버를 배포 하는 방법을 보여 줍니다.\-콘텐츠 서버를 기반으로 합니다.

### <a name="group-policy"></a>그룹 정책

Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012의 그룹 정책에 제공 하 고 대상된 사용자 및 컴퓨터는 Active Directory 환경 내에서 집합에 하나 이상의 원하는 구성 이나 정책 설정을 적용 하는 데 인프라입니다. 

이 인프라는 그룹 정책 엔진 및 여러 클라이언트의 구성 됩니다\-확장명 \(Cse\) 하는 대상 클라이언트 컴퓨터에서 정책 설정을 읽는 역할을 합니다.

그룹 정책은 이 시나리오에서 BranchCache 호스트 캐시 모드로 도메인 구성원 클라이언트 컴퓨터를 구성하는 데 사용됩니다.

이 가이드를 계속 하려면 참조 [BranchCache 호스트 캐시 모드 배포 개요](2-Bc-Hcm-Deploy-Overview.md)합니다.
