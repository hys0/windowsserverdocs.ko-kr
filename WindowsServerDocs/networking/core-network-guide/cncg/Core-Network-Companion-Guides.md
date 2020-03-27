---
title: 핵심 네트워크 부록 가이드
description: 이 항목에서는 Windows Server 2016 핵심 네트워크 가이드의 부록 가이드 개요를 제공 합니다.
manager: brianlic
ms.technology: networking
ms.prod: windows-server
ms.topic: article
ms.assetid: d57af0bd-9301-4f62-9888-f528cd10451d
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 5f3ae4f9c22e61a8428a257d9324fe164eeaa04b
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319101"
---
# <a name="core-network-companion-guidance"></a>핵심 네트워크 부록 지침

>적용 대상: Windows Server(반기 채널), Windows Server 2016

Windows Server 2016 동안 [핵심 네트워크 가이드](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide) 새로운 Active Directory를 배포 하는 방법에 대해 설명&reg; 포리스트는 새 루트 도메인 및 부록 가이드 지원 네트워킹 인프라와 네트워크에 기능을 추가 하는 기능 제공 합니다.

각 부록 가이드를 통해 핵심 내트워크를 배포한 후 구체적인 목표를 달성할 수 있습니다. 부록 가이드가 여러 개 있고 이 가이드를 올바른 순서로 함께 배포한 경우 신중하고 비용 효율적이며 이성적인 방법으로 매우 복잡한 목표를 달성할 수 있는 경우도 있습니다.

핵심 네트워크 가이드를 미처 참고하기 전에 Active Directory 도메인 및 핵심 네트워크를 배포한 경우에도 부록 가이드를 사용하여 네트워크에 기능을 추가할 수 있습니다. 필수 구성 요소 목록으로 핵심 네트워크 가이드를 사용하고 부록 가이드로 추가 기능을 배포한다는 사실을 알기만 하면 됩니다. 물론 사용자 네트워크가 핵심 네트워크 가이드에서 제공하는 필수 구성 요소를 충족해야 합니다.

## <a name="core-network-companion-guide-deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>802.1 X 유선 및 무선 배포에 대 한 서버 인증서를 배포 하는 핵심 네트워크 부록 가이드: 

이 부록 가이드에서는 네트워크 정책 서버를 실행 중인 컴퓨터에 대 한 서버 인증서를 배포 하 여 핵심 네트워크에 작성 하는 방법에 설명 \(NPS\), 원격 액세스 서비스 \(RAS\), 또는 둘 다.

확장할 수 있는 인증 프로토콜 인증서 기반 인증 방법을 배포 하는 경우 서버 인증서가 필요한 \(EAP\) 및 보호 된 EAP \(PEAP\) 네트워크 액세스 인증 합니다. Active Directory 인증서 서비스를 사용 하 여 서버 인증서 배포 \(AD CS\) EAP 및 PEAP 인증서 기반 인증에 대 한 메서드는 다음과 같은 이점을 제공 합니다.

- NPS 또는 RAS 서버의 ID를 프라이빗 키에 바인딩
- 도메인 구성원 NPS 및 RAS 서버에 인증서를 자동으로 등록 하기 위한 비용 효율적이 고 안전한 메서드
- 인증서와 인증 기관을 관리하는 효율적인 방법
- 인증서 기반 인증으로 보안 유지
- 다른 용도를 위해 인증서의 사용 확장 가능
  
서버 인증서를 배포 하는 방법에 대 한 지침을 참조 하십시오. [802.1 X 유선 및 무선 배포에 대 한 서버 인증서 배포](server-certs/Deploy-Server-Certificates-for-802.1X-Wired-and-Wireless-Deployments.md)합니다.  
## <a name="core-network-companion-guide-deploy-password-based-8021x-authenticated-wireless-access"></a>핵심 네트워크 부록 가이드: 암호 기반 802.1 X 인증된 무선 액세스 배포

이 부록 가이드 Institute of Electrical and Electronics Engineers를 배포 하는 방법에 대 한 지침을 제공 하 여 핵심 네트워크에 작성 하는 방법에 설명 \(IEEE\) 802.1 X\-인증 보호 확장할 수 있는 인증 프로토콜 \ – Microsoft Challenge Handshake 인증 프로토콜 버전 2를 사용 하 여 IEEE 802.11 무선 액세스 \(PEAP\-MS\-CHAP v2\)합니다.

인증 방법 PEAP\-MS\-CHAP v 2를 사용 하려면 네트워크 정책\) \(서버를 실행 하는 인증 서버에서 클라이언트에 NPS id를 증명 하기 위해 서버 인증서를 사용 하 여 무선 클라이언트를 제공 해야 하지만 인증서를 사용 하 여 사용자 인증이 수행 되지 않습니다. 대신 사용자가 도메인 사용자 이름과 암호를 제공 합니다.

때문에 PEAP\-MS\-CHAP v2 필요는 사용자가 인증 프로세스 중 인증서가 아니라 암호 기반 자격 증명 제공, 일반적으로 더 쉽고 저렴 하 게 EAP 보다 배포\-TLS 또는 PEAP\-TLS 합니다.

이 가이드를 사용 하는 PEAP와 함께 무선 액세스를 배포 하기 전에\-MS\-CHAP v2 인증 방법으로 다음을 수행 해야 합니다.

1. 핵심 네트워크 인프라를 배포 하는 핵심 네트워크 가이드의 지침에 따라 또는 이미 있는 기술 가이드에서 제공 해당 네트워크에 배포 합니다.
2. 802.1 X 유선 및 무선 배포를 위한 핵심 네트워크 부록 가이드 배포 서버 인증서의 지침에 따라 또는 이미 있는 기술 가이드에서 제공 해당 네트워크에 배포 합니다.

무선 액세스 시 PEAP와 함께 배포 하는 방법에 대 한 지침은\-MS\-v2 CHAP, 참조 [배포 암호 기반 802.1 X 인증 무선 액세스](wireless/a-deploy-8021X-wireless-access.md)합니다.

## <a name="core-network-companion-guide-deploy-branchcache-hosted-cache-mode"></a>핵심 네트워크 부록 가이드: BranchCache 호스트 캐시 모드 배포

이 부록 가이드에는 하나 이상의 지점에 호스트 된 캐시 모드에서 BranchCache를 배포 하는 방법을 설명 합니다.

BranchCache는 이전 버전의 Windows 및 Windows Server 및 Windows Server 2016 및 Windows 10 운영 체제의 일부 버전에 포함 되어 있는 광역 네트워크 (WAN) 대역폭 최적화 기술입니다.

호스트된 캐시 모드로 BranchCache를 배포하는 경우 지점의 콘텐츠 캐시는 하나 이상의 서버 컴퓨터(호스트 캐시 서버)에서 호스팅됩니다. 호스트 캐시 서버는 지사에서 여러 가지 용도에 서버를 사용할 수 있는 캐시를 호스트 하는 것 외에도 작업을 실행할 수 있습니다.

BranchCache 호스트 캐시 모드는 원래 요청 하 고 데이터를 캐시 하는 클라이언트를 오프 라인 상태인 경우에 콘텐츠를 사용할 수 있으므로 캐시 효율성이 높아집니다. 호스트 캐시 서버는 항상 사용할 수 있기 때문에 더 많은 콘텐츠가 캐시되고 WAN 대역폭을 보다 많이 절약할 수 있으며 BranchCache 효율성이 향상됩니다.

호스트 캐시 모드를 배포할 때 다중 서브넷 지점에 있는 모든 클라이언트는 클라이언트가 서로 다른 서브넷에 있는 경우에 호스트 캐시 서버에 저장 된 단일 캐시에 액세스할 수 있습니다.

호스트 캐시 모드로 BranchCache를 배포 하는 방법에 대 한 자세한 내용은 참조 하십시오. [배포할 BranchCache 호스트 캐시 모드](bc-hcm/1-Deploy-Bc-Hcm.md)합니다.
