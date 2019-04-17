---
title: 배포 BranchCache 호스트 캐시 모드
description: 이 가이드 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache 배포에 대해 설명
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 4235231c-4732-4ea9-9330-2a8c8a616d39
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 326a1f1edfe6cb763a33ebfc8fd5abdd5b6aab3a
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-branchcache-hosted-cache-mode"></a>배포 BranchCache 호스트 캐시 모드

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows Server 2016 Core 네트워크 가이드 계획 및 배포 새로운 Active Directory를 완벽 하 게 작동 네트워크에 필요한 핵심 구성 요소에 대 한 지침을 제공&reg; 새 숲 속의 도메인.

이 가이드에서는 Read\-Only 도메인 컨트롤러 클라이언트 컴퓨터 Windows를 실행 하는 하나 이상의 지사에서 호스트 캐시 모드로 BranchCache 배포 하기 위한 지침을 제공 하 여 핵심 네트워크에서 작성 하는 방법을 설명&reg; 10, Windows 8.1 또는 Windows 8 도메인에 가입 하 고 있습니다.

>[!IMPORTANT]
>이 가이드 배포 또는 Windows Server 2008 R2 실행 되는 호스트 BranchCache 캐시 서버를 이미 배포를 계획 하는 경우에 사용 하지 마십시오. 이 가이드에서는 Windows Server 실행 되는 호스트 캐시 서버를 사용 하 여 호스팅된 캐시 모드 배포 하기 위한 지침&reg; 2016, Windows Server 2012 R2 또는 Windows Server 2012 합니다.

이 가이드 다음 섹션에 포함 되어 있습니다.

- [이 가이드를 사용 하 여 사항](#bkmk_pre)

- [이 가이드 정보](#bkmk_about)

- [이 가이드 제공 하지 않는 항목](#bkmk_not)

- [기술 개요](#bkmk_tech)

- [BranchCache 호스트 캐시 모드 배포 개요](2-Bc-Hcm-Deploy-Overview.md)

- [BranchCache 캐시 모드 호스트 배포 계획](3-Bc-Hcm-Plan.md)

- [BranchCache 캐시 모드 배포 호스트](4-Bc-Hcm-Deployment.md)

- [추가 리소스](11-Bc-Hcm-additional-resources.md)

## <a name="bkmk_pre"></a>이 가이드를 사용 하 여 사항

Windows Server 2016 Core 네트워크 가이드에 대 한 도우미 지침입니다. 이 가이드를 사용 하 여 호스팅된 캐시 모드에 BranchCache을 배포 하려면 사용자 먼저 다음을 수행 해야 합니다.

- 핵심 네트워크 가이드를 사용 하 여 기본 사무실에 핵심 네트워크를 배포 하거나 이미 기술에에서 제공한 핵심 네트워크 가이드 설치 되어 있고 네트워크에서 제대로 작동 합니다. 이러한 기술을 TCP\/IP v4, DHCP, Active Directory 도메인 서비스 \(AD DS\) 및 DNS 포함 됩니다.

    > [!NOTE]
    > Windows Server 2016 [Core 네트워크 가이드](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide) Windows Server 2016 기술 라이브러리에서 사용할 수 있습니다.  

- 주 사무실에 또는 클라우드 데이터 센터에 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 BranchCache 콘텐츠 서버를 배포 합니다. BranchCache 콘텐츠 서버를 배포 하는 방법에 대 한 참고 [추가 리소스](11-Bc-Hcm-additional-resources.md)합니다.

- 연결할 다양 한 영역 네트워크 \(WAN\) 분기 사무실, 주 office 및, 해당 되는 경우 클라우드 리소스를 가상 개인을 사용 하 여 네트워크 \(VPN\), DirectAccess, 또는 다른 연결 방법을 합니다.

- 분기 사무실에 BranchCache 배경 지능형 서비스 BITS (전송), Hyper 텍스트 전송 (HTTP 프로토콜)를 및 블록 SMB (서버 메시지)에 대 한 지원을 제공 하는 다음 운영 체제 중 하나를 실행 하는 클라이언트 컴퓨터를 배포 합니다.
    - Windows 10 Enterprise
    - Windows 10 Education
    - Windows 8.1 Enterprise
    - Windows 8 Enterprise

>[!NOTE]
>다음 운영 체제 BranchCache HTTP 및 SMB 기능을 지원 하지 않는 하지만 BranchCache 비트 기능을 지원 합니다.
>     - Windows 10 Pro로 비트만 지원
>     - Windows 8.1 Pro 비트만 지원
>     - Windows 8 Pro 비트만 지원

## <a name="bkmk_about"></a>이 가이드 정보

이 가이드는 네트워크 및 시스템 관리자에 게 핵심 네트워크를 배포 하는 Windows Server 2016 Core 네트워크 설명서 또는 Windows Server 2012 Core 네트워크 가이드의 지침에 따라 하거나 이전에 Active Directory 도메인 서비스 \(AD DS\), 도메인 이름 서비스 \(DNS\), Dynamic Host Configuration 프로토콜 \(DHCP\) Core 네트워크 가이드에 포함 된 기술 배포한 사람들을 위해 설계 TCP\/IP v4 합니다.

각이 배포 시나리오에서 사용 되는 기술에 대 한 디자인 및 배포 설명서를 검토 하는 것이 좋습니다. 이 가이드가 배포 시나리오 조직의 네트워크에 필요한 구성과 서비스 제공 하는지 여부를 결정할 수 있습니다.

## <a name="bkmk_not"></a>이 가이드 제공 하지 않는 항목

이 가이드 BranchCache, BranchCache 모드 및 기능에 대 한 정보를 포함 하는 방법에 대해를 제공 하지 않습니다.  

이 가이드 WAN 연결 또는 다른 기술에 VPN 서버의 RODC, DHCP 등 사용자 지점 배포 하는 방법에 대 한 정보를 제공 하지 않습니다.

또한,이 가이드 호스트 캐시 서버 배포할 때 사용 하는 하드웨어에서 지침을 제공 하지 않습니다. 하지만 여 호스팅된 캐시 서버, 작업과 하드웨어 기능별로 분기 office 크기에 따라 결정을 확인 해야, 특정 컴퓨터에서 호스트 BranchCache 캐시 서버 설치할지 여부를 및 디스크 공간에 대 한 캐시를 할당에서 다른 서비스와 응용 프로그램을 실행할 수는 있습니다.  
이 가이드 구성 Windows 7을 실행 하는 컴퓨터에 대 한 지침을 제공 하지 않습니다. 이러한 구성 해야 지점에서 Windows 7을 실행 하는 클라이언트 컴퓨터를 사용 하는 경우 Windows 10, Windows 8.1 및 Windows 8을 실행 하는 클라이언트 컴퓨터에 대 한 가이드이 제공 된 것과 다른 절차를 사용 하 여 합니다.
  
또한 Windows 7을 실행 하는 컴퓨터를 사용 하는 클라이언트 컴퓨터 신뢰 하는 인증 기관에서 발급 한 서버의 인증서 사용 하 여 호스팅된 캐시 서버를 구성 해야 합니다. \ (서버의 인증서 사용 하 여 호스팅된 캐시 서버 구성 필요한 경우 Windows 10, Windows 8.1 또는 Windows 8을 실행 하는 클라이언트 컴퓨터의 모든 없습니다. \) 
> [!IMPORTANT]
> Windows Server 2008 r 2를 사용 하 여 호스팅된 캐시 서버 Windows Server 2008 r 2를 실행 하는 경우 [BranchCache 배포 가이드](https://technet.microsoft.com/library/ee649232(v=ws.10).aspx) 이 가이드 호스트 캐시 모드로 BranchCache 배포 하는 대신 합니다. Windows 10에 Windows 7에서의 Windows 버전을 실행 중인 모든 BranchCache 클라이언트 해당 가이드에서 설명 하는 그룹 정책 설정을 적용 됩니다. 이 가이드 단계를 사용 하 여 실행 하는 컴퓨터 Windows Server 2008 r 2를 구성할 수 없습니다.

## <a name="bkmk_tech"></a>기술 개요

이 제공 된 설명서를 BranchCache는 설치 하 고 구성 해야 하는 유일한 기술 합니다. 그러나 웹 같은 콘텐츠 서버 및 프로그램 파일 서버에 Windows PowerShell BranchCache 명령을 실행 필요가 없습니다 변경 또는 다른 방법으로 콘텐츠 서버를 다시 구성 하 해야 합니다. 또한 광고 DS Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012에서 실행 되는 도메인 컨트롤러에서 그룹 정책을 사용 하 여 컴퓨터를 구성 해야 합니다.

### <a name="branchcache"></a>BranchCache

BranchCache 일부 버전의 Windows Server 2016 및 Windows 10 운영 체제 및 Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2 및 Windows 7의 일부 버전에 포함 되어 있는 다양 한 영역 네트워크 (WAN) 대역폭 최적화 기술을입니다.

WAN 대역폭 사용자가 원격 서버에 콘텐츠에 액세스 하는 때를 최적화 하려면 BranchCache 콘텐츠 요청 했습니다. 주로 office를 다운로드 하거나 클라우드 콘텐츠 서버 호스트 고 캐시 office 지점 콘텐츠 wan가 대신 로컬 동일한 콘텐츠에 액세스할 수 지점에서 다른 컴퓨터를 허용 합니다.

호스트 캐시 모드로 BranchCache 배포 하는 경우 호스트 캐시 모드 클라이언트로 지점에 컴퓨터를 구성 해야 하 고 지점에 호스트 캐시 서버에 배포 해야 합니다. 이 가이드 prehashed 및 미리 로드 된 콘텐츠를 웹에서 사용 하 여 호스팅된 캐시 서버 배포 및 파일 콘텐츠 서버 server\ 기반으로 하는 방법을 보여 줍니다.

### <a name="group-policy"></a>그룹 정책

Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012에서 그룹 정책을 제공 하며, 원하는 구성 또는 정책 설정을 집합에만 적용 대상으로 사용자와 Active Directory 환경 내에서 컴퓨터의 하는 데 사용 된 인프라입니다. 

이 인프라 그룹 정책 엔진 및 읽기 대상 클라이언트 컴퓨터에서 정책 설정을 담당 하는 여러 client\ 확장 \(CSEs\) 이루어져 있습니다.

호스트 BranchCache 캐시 모드로 도메인 구성원 클라이언트 컴퓨터 구성 하려면이 시나리오에서 그룹 정책을 사용 됩니다.

이 가이드를 계속 참조 [BranchCache 호스트 캐시 모드 배포 개요](2-Bc-Hcm-Deploy-Overview.md)합니다.
