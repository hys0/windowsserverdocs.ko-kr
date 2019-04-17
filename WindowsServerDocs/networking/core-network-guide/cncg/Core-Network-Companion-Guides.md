---
title: 핵심 네트워크 도우미 가이드
description: 이 항목에서는 Windows Server 2016 Core 네트워크 가이드 도우미 가이드를 소개
manager: brianlic
ms.technology: networking
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: d57af0bd-9301-4f62-9888-f528cd10451d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3c272c51cc69017b75e50e79e58186c0ea7c6391
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="core-network-companion-guides"></a>핵심 네트워크 도우미 가이드

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Windows Server 2016 동안 [Core 네트워크 가이드](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide) 새로운 Active Directory를 배포 하는 방법에 대해 설명&reg; 새 루트 도메인와 지원 네트워킹 인프라 도우미 가이드 숲 속 네트워크 기능을 추가 하는 기능 제공 합니다.

각 도우미 가이드 핵심 네트워크를 배포한 후 특정 목표를 달성 수 있습니다. 어떤 경우에 함께 하 고 올바른 순서로 배포할 때 여러 도우미 안내 하는 수 있는 적절 한 비용 효과적인 측정된 방식으로 복잡 한 목표를 달성 하기.

핵심 네트워크 가이드 발생 하기 전에 Active Directory 도메인, core 네트워크를 배포 하는 경우 네트워크에 기능 추가 도우미 가이드를 사용할 수 있습니다. 간단 하 게 필수를 목록으로 핵심 네트워크 가이드를 사용 하 여 의견을 있는 도우미 가이드 추가 기능을 배포 네트워크 충족 해야 핵심 네트워크 가이드도 제공 되는 필수.

## <a name="core-network-companion-guide-deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>802.1 X 유무선 배포에 대 한 서버 인증서를 배포 하는 네트워크 도우미 가이드 핵심: 

이 제공 된 설명서 네트워크 정책 서버 \(NPS\) 원격 액세스 서비스 \(RAS\) 이상을 실행 하는 컴퓨터에 대 한 서버 인증서를 배포 하 여 핵심 네트워크 시 빌드하는 방법에 설명 합니다.

네트워크 액세스를 인증에 대 한 확장 인증 프로토콜 \(EAP\)와 보호 EAP \(PEAP\) 인증서 기반 인증 방법을 배포할 때 서버 인증서가 필요 합니다. 서버 인증서 Active Directory 인증서 서비스와 배포 \ (AD CS \) 방법 EAP 및 PEAP 인증서 기반 인증을 위해 다음과 같은 이점을 제공 합니다.

- 개인 키 NPS 또는 RAS 서버의 id 구속력
- 자동으로 도메인 회원 NPS 및 RAS 서버의 인증서를 등록 하기 위한 비용 효율적이 고 안전한 방법
- 인증서 및 인증 기관 관리 하는 데 효과적인 방법
- 인증서 기반 인증을 통해 제공 되는 보안
- 확장 추가 목적을 위해 인증서를 사용 하는 기능
  
서버 인증서를 배포 하는 방법에 관한 참조 [802.1 X 유선 및 무선 배포에 대 한 서버 인증서 배포](server-certs/Deploy-Server-Certificates-for-802.1X-Wired-and-Wireless-Deployments.md)합니다.  
## <a name="core-network-companion-guide-deploy-password-based-8021x-authenticated-wireless-access"></a>핵심 네트워크 도우미 가이드: 배포 암호 기반 802.1 X 인증된 무선 액세스

이 제공 된 설명서 전기 연구소 및 전자 제품 엔지니어 \(IEEE\) 802.1X\ 배포 하는 방법에 대 한 지침을 제공 하 여 핵심 네트워크 시 빌드하는 방법에 설명-인증 보호 Extensible 인증 Protocol\-Microsoft Challenge Handshake 인증 프로토콜 버전 2 사용 하 여 무선 액세스 IEEE 802.11 \ (PEAP\ 기능 MS\ 기능을 제공 v2\).

하지만 PEAP\ 기능 MS\ 기능을 제공 v2 인증 방법에는 네트워크 정책 서버 \(NPS\) 존재 무선 클라이언트 서버 인증서 NPS 서버 id 클라이언트를 증명을 사용 하 여 실행 하는 서버 인증을 사용자 인증 인증서를 사용 하 여 수행 되지 않습니다-도메인 사용자 이름 및 암호 사용자가 제공 하는 대신 필요 합니다.

사용자는 인증서 보다는 자격 증명 암호 기반 인증 과정 제공는 PEAP\ 기능 MS\ 기능을 제공 v2 하므로 일반적으로 쉽고 저렴 EAP\ TLS 또는 PEAP\ TLS 보다 배포 하는 합니다.

이 가이드를 사용 하 여 무선 액세스 PEAP\ 기능 MS\ 기능을 제공 v2 인증 방법을 배포 하기 전에 다음을 수행 해야 합니다.

1. 이미 있는 기술 가이드에서 제공 해당 네트워크에 배포 또는 핵심 네트워크 가이드의 핵심 네트워크 인프라를 배포 하는 지침을 따릅니다.
2. 이미 있는 기술 가이드에서 제공 해당 네트워크에 배포 또는 802.1 X 유선 및 무선 배포에 대 한 핵심 네트워크 도우미 가이드 배포 서버 인증서의 지침을 따릅니다.

무선 액세스 PEAP\ 기능 MS\ 기능을 제공 v 2 배포 하는 방법에 대 한 지침을 참조 하세요. [암호 배포 기반 802.1 X 인증 무선 액세스](wireless/a-deploy-8021X-wireless-access.md)합니다.

## <a name="core-network-companion-guide-deploy-branchcache-hosted-cache-mode"></a>핵심 네트워크 도우미 가이드: 배포 BranchCache 호스트 캐시 모드

이 제공 된 설명서 BranchCache 모드로 호스트 캐시 하나 이상의 지사에서 배포 하는 방법에 설명 합니다.

BranchCache은 이전 버전의 Windows 및 Windows Server 뿐만 아니라 Windows Server 2016 및 Windows 10 운영 체제의 일부 버전에 포함 되어 있는 다양 한 영역 네트워크 (WAN) 대역폭 최적화 기술 합니다.

호스트 캐시 모드로 BranchCache 배포 하는 경우 콘텐츠 캐시를 지점은 하나 또는 라고 하는 많은 서버 컴퓨터 호스팅 캐시 서버 합니다. 호스트 캐시 서버 지사에서 여러 가지 목적 서버를 사용할 수 있는 캐시 호스트 하는 것 외에도 작업을 실행할 수 있습니다.

캐시 된 데이터를 원래 요청 하는 클라이언트 오프 라인 상태인 경우에 콘텐츠를 사용할 수 있으므로 호스트 BranchCache 캐시 모드 캐시 효율성을 높여 줍니다. 호스트 캐시 서버를 사용할 수 있는 항상 때문에 더 많은 콘텐츠 캐시 된 큰 WAN 대역폭 절약 제공 하 고 BranchCache 효율성을 개선 합니다.

호스트 캐시 모드 배포 하는 경우 모든 클라이언트 여러 서브넷 지점에 클라이언트 다른에 있는 경우에 호스트 캐시 서버에 저장 되는 단일 캐시를 액세스할 수 있습니다.

캐시 호스트 모드로 BranchCache 배포 하는 방법에 관한 참조 [캐시 모드를 호스트 BranchCache 배포](bc-hcm/1-Deploy-Bc-Hcm.md)합니다.
