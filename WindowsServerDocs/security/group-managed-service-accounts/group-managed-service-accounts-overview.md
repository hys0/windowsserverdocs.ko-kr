---
title: Group Managed Service Accounts Overview
description: Windows Server 보안
ms.prod: windows-server
ms.technology: security-gmsa
ms.topic: article
ms.assetid: cef0693c-f861-48a7-a1c0-8d1bc06143ce
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 87739b503a5978173d67be90408c22339cae0df9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856976"
---
# <a name="group-managed-service-accounts-overview"></a>Group Managed Service Accounts Overview

>적용 대상: Windows Server(반기 채널), Windows Server 2016

IT 전문가를 위한이 항목에서는 실제 응용 프로그램, Microsoft의 구현 변경 내용, 하드웨어 및 소프트웨어 요구 사항에 대해 설명 하 여 그룹 관리 서비스 계정을 소개 합니다.


## <a name="feature-description"></a><a name="BKMK_OVER"></a>기능 설명
SMSA (독립 실행형 관리 서비스 계정)는 자동 암호 관리, 간소화 된 SPN (서비스 사용자 이름) 관리 및 다른 관리자에 게 관리를 위임 하는 기능을 제공 하는 관리 되는 도메인 계정입니다. 이 유형의 MSA (관리 서비스 계정)는 Windows Server 2008 R2 및 Windows 7에서 도입 되었습니다.

GMSA (그룹 관리 서비스 계정)는 도메인 내에서 동일한 기능을 제공 하지만 여러 서버에서 해당 기능을 확장 합니다. 네트워크 부하 분산 된 솔루션과 같이 서버 팜에서 호스트 되는 서비스에 연결 하는 경우 상호 인증을 지 원하는 인증 프로토콜을 사용 하려면 서비스의 모든 인스턴스가 동일한 보안 주체를 사용 해야 합니다. 서비스 주체로 gMSA를 사용 하는 경우 Windows 운영 체제는 관리자를 사용 하 여 암호를 관리 하는 대신 계정에 대 한 암호를 관리 합니다.

Microsoft 키 배포 서비스 \(kdssvc.dll\)는 Active Directory 계정의 키 식별자를 사용 하 여 최신 키 또는 특정 키를 안전 하 게 가져오는 메커니즘을 제공 합니다. 키 배포 서비스는 계정용 키를 만드는 데 사용되는 암호를 공유합니다. 이러한 키는 정기적으로 변경됩니다. GMSA 도메인 컨트롤러는 gMSA의 다른 특성 외에도 키 배포 서비스에서 제공 하는 키의 암호를 계산 합니다.  구성원 호스트는 도메인 컨트롤러에 연결 하 여 현재 및 이전 암호 값을 가져올 수 있습니다.

## <a name="practical-applications"></a><a name="BKMK_APP"></a>실용적인 응용 프로그램
gMSAs는 서버 팜에서 실행 되는 서비스에 대해 단일 id 솔루션을 제공 하거나 네트워크 Load Balancer 뒤에 있는 시스템에 대해 단일 id 솔루션을 제공 합니다. GMSA 솔루션을 제공 하 여 새 gMSA 주 서버에 대 한 서비스를 구성 하 고 암호 관리를 Windows에서 처리할 수 있습니다.

GMSA 서비스 또는 서비스 관리자를 사용 하는 경우 서비스 인스턴스 간의 암호 동기화를 관리할 필요가 없습니다. GMSA는 오랜 시간 동안 오프 라인 상태로 유지 되는 호스트 및 모든 서비스 인스턴스에 대 한 구성원 호스트의 관리를 지원 합니다. 즉, 기존 클라이언트 컴퓨터가 현재 연결 중인 서비스 인스턴스를 몰라도 인증할 수 있는 단일 ID를 지원하는 서버 팜을 배포할 수 있습니다.

장애 조치(failover) 클러스터는 gMSA를 지원하지 않습니다. 그러나 클러스터 서비스를 기반으로 실행되는 서비스가 Windows 서비스, 응용 프로그램 풀 또는 예약된 작업이거나 기본적으로 gMSA 또는 sMSA를 지원하는 경우에는 gMSA 또는 sMSA를 사용할 수 있습니다.

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>소프트웨어 요구 사항

GMSAs를 관리 하는 데 사용 되는 Windows PowerShell 명령을 실행 하려면 64\-비트 아키텍처가 필요 합니다.

관리 서비스 계정은 Kerberos 지원 암호화 유형에 종속됩니다. 클라이언트 컴퓨터가 서버에 대해 인증할 때 Kerberos를 사용하는 경우 DC는 DC와 서버에 모두 지원되는 암호화를 사용하여 보호된 Kerberos 서비스 티켓을 만듭니다. DC는 계정의의 msds-primary-computer\-Supported Types 특성을 사용 하 여 서버에서 지 원하는 암호화를 결정 하 고, 특성이 없는 경우 클라이언트 컴퓨터에서 더 강력한 암호화 유형을 지원 하지 않는다고 가정 합니다. 호스트가 RC4를 지원 하지 않도록 구성 된 경우 인증은 항상 실패 합니다. 이 때문에 AES는 항상 MSA에 대해 명시적으로 구성되어 있어야 합니다.

> [!NOTE]
> Windows Server 2008 R2부터는 DES가 기본적으로 사용하지 않도록 설정되어 있습니다. 지원되는 암호화 유형에 대한 자세한 내용은 [Kerberos 인증의 변경 내용](https://technet.microsoft.com/library/dd560670(WS.10).aspx)을 참조하세요.

gMSAs는 Windows Server 2012 이전의 Windows 운영 체제에는 적용 되지 않습니다.

## <a name="server-manager-information"></a>서버 관리자 정보
서버 관리자 또는 Install\-Add-windowsfeature cmdlet을 사용 하 여 MSA 및 gMSA를 구현 하는 데 필요한 구성 단계는 없습니다.

## <a name="see-also"></a><a name="BKMK_LINKS"></a>참고 항목
다음 표에서는 관리 서비스 계정 및 그룹 관리 서비스 계정 관련 추가 리소스의 링크를 제공합니다.

|콘텐츠 유형|참조|
|--------|-------|
|**제품 평가**|[관리 서비스 계정의 새로운 기능](what-s-new-for-managed-service-accounts.md)<p>[Windows 7 및 Windows Server 2008 r 2 용 관리 서비스 계정 설명서](https://technet.microsoft.com/library/ff641731(v=ws.10).aspx)<p>[서비스 계정 단계\-\-단계별 가이드](https://technet.microsoft.com/library/dd548356(v=ws.10).aspx)|
|**계획**|아직 사용할 수 없음|
|**배포**|아직 사용할 수 없음|
|**작업**|[Active Directory의 관리 서비스 계정](https://technet.microsoft.com/library/dd378925(v=ws.10).aspx)|
|**문제 해결**|아직 사용할 수 없음|
|**조건**|[그룹 관리 서비스 계정 시작](getting-started-with-group-managed-service-accounts.md)|
|**도구 및 설정**|[Active Directory Domain Services의 관리 서비스 계정](https://technet.microsoft.com/library/dd378925(v=WS.10).aspx)|
|**커뮤니티 리소스**|[관리 서비스 계정: 이해, 구현, 모범 사례 및 문제 해결](https://blogs.technet.com/b/askds/archive/2009/09/10/managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting.aspx)|
|**관련 기술**|[Active Directory Domain Services 개요](active-directory-domain-services-overview.md)|


