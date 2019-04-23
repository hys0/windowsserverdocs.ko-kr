---
title: Group Managed Service Accounts Overview
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-gmsa
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cef0693c-f861-48a7-a1c0-8d1bc06143ce
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 24e3e3c15544de2f3bed4a7ef177b659e8095385
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836974"
---
# <a name="group-managed-service-accounts-overview"></a>Group Managed Service Accounts Overview

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 유용한 팁을 설명 하 여 관리 서비스 계정 그룹을 소개 하는 IT 전문가 대 한 Microsoft의 구현에 하드웨어 및 소프트웨어 요구 사항을 변경 합니다.


## <a name="BKMK_OVER"></a>기능 설명
독립 실행형 관리 서비스 계정 (sMSA)에 자동 암호 관리, 간소화 된 서비스 사용자 이름 (SPN) 관리 및 다른 관리자에 게 관리를 위임 하는 기능을 제공 하는 관리 되는 도메인 계정입니다. 이 유형의 관리 되는 서비스 계정 (MSA)는 Windows Server 2008 R2 및 Windows 7에서 도입 되었습니다.

그룹 관리 서비스 계정 (gMSA) 도메인 내에서 동일한 기능을 제공 하지만 해당 기능을 여러 서버로 확장 합니다. 네트워크 부하 분산 솔루션과 같은 서버 팜에서 호스트 되는 서비스에 연결 하는 경우 상호 인증을 지 원하는 인증 프로토콜 서비스의 모든 인스턴스는 동일한 보안 주체를 사용 해야 합니다. GMSA로 서비스 주체를 사용 하면 Windows 운영 체제는 암호를 관리 하려면 관리자에 의존 하지 않고 계정의 암호를 관리 합니다.

Microsoft 키 배포 서비스 \(kdssvc.dll\) 안전 하 게 Active Directory 계정에 대 한 키 식별자를 사용 하 여 특정 키 또는 최신 키를 가져올 수 메커니즘을 제공 합니다. 키 배포 서비스는 계정용 키를 만드는 데 사용되는 암호를 공유합니다. 이러한 키는 정기적으로 변경됩니다. GMSA를 도메인 컨트롤러는 gMSA의 다른 특성 외에도 키 배포 서비스에서 제공 하는 키의 암호를 계산 합니다.  구성원 호스트 도메인 컨트롤러에 연결 하 여 현재 및 이전 암호 값을 가져올 수 있습니다.

## <a name="BKMK_APP"></a>실제 응용 프로그램
Gmsa 서버 팜에서 또는 네트워크 부하 분산 장치 뒤에서 시스템에서 실행 중인 서비스에 대 한 단일 id 솔루션을 제공 합니다. GMSA 솔루션을 제공 함으로써 새 gMSA 계정에 대 한 서비스를 구성할 수 있습니다 및 암호 관리는 Windows에서 처리 합니다.

GMSA를 사용 하 여, 서비스 또는 서비스 관리자가 필요가 없습니다 서비스 인스턴스 간의 암호 동기화를 관리 합니다. GMSA를 오랫동안 및 관리 서비스의 모든 인스턴스에 대 한 구성원 호스트를 오프 라인 유지 되는 호스트를 지원 합니다. 즉, 기존 클라이언트 컴퓨터가 현재 연결 중인 서비스 인스턴스를 몰라도 인증할 수 있는 단일 ID를 지원하는 서버 팜을 배포할 수 있습니다.

장애 조치(failover) 클러스터는 gMSA를 지원하지 않습니다. 그러나 클러스터 서비스를 기반으로 실행되는 서비스가 Windows 서비스, 응용 프로그램 풀 또는 예약된 작업이거나 기본적으로 gMSA 또는 sMSA를 지원하는 경우에는 gMSA 또는 sMSA를 사용할 수 있습니다.

## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항

64\-비트 아키텍처는 Gmsa를 관리 하는 데 사용 되는 Windows PowerShell 명령을 실행 해야 합니다.

관리 서비스 계정은 Kerberos 지원 암호화 유형에 종속됩니다. 클라이언트 컴퓨터가 서버에 대해 인증할 때 Kerberos를 사용하는 경우 DC는 DC와 서버에 모두 지원되는 암호화를 사용하여 보호된 Kerberos 서비스 티켓을 만듭니다. DC는이 계정의 msDS\-SupportedEncryptionTypes 특성 결정을 서버 암호화를 지원 하며, 특성이 없는 경우 클라이언트 컴퓨터는 보다 강력한 암호화 종류를 지원 하지 않습니다 가정 합니다. 호스트가 RC4를 지원 하지 않도록 구성 되어, 경우 인증은 항상 실패 합니다. 이 때문에 AES는 항상 MSA에 대해 명시적으로 구성되어 있어야 합니다.

> [!NOTE]
> Windows Server 2008 R2부터는 DES가 기본적으로 사용하지 않도록 설정되어 있습니다. 지원되는 암호화 유형에 대한 자세한 내용은 [Kerberos 인증의 변경 내용](https://technet.microsoft.com/library/dd560670(WS.10).aspx)을 참조하세요.

Gmsa를 Windows Server 2012 이전의 Windows 운영 체제에 적용 되지 않습니다.

## <a name="server-manager-information"></a>서버 관리자 정보
MSA 및 서버 관리자 또는 설치를 사용 하 여 gMSA를 구현 하는 데 필요한 구성 단계가 없는\-WindowsFeature cmdlet.

## <a name="BKMK_LINKS"></a>참고 항목
다음 표에서는 관리 서비스 계정 및 그룹 관리 서비스 계정 관련 추가 리소스의 링크를 제공합니다.

|콘텐츠 형식|참조|
|--------|-------|
|**제품 평가**|[관리 서비스 계정에 대 한 새로운 기능](what-s-new-for-managed-service-accounts.md)<br /><br />[관리 서비스 계정 Windows 7 및 Windows Server 2008 R2에 대 한 설명서](https://technet.microsoft.com/library/ff641731(v=ws.10).aspx)<br /><br />[서비스 계정 단계\-여\-가이드](https://technet.microsoft.com/library/dd548356(v=ws.10).aspx)|
|**계획**|아직 사용할 수 없음|
|**배포**|아직 사용할 수 없음|
|**작업**|[Active Directory의 관리 서비스 계정](https://technet.microsoft.com/library/dd378925(v=ws.10).aspx)|
|**문제 해결**|아직 사용할 수 없음|
|**평가**|[관리 서비스 계정 그룹을 사용 하 여 시작](getting-started-with-group-managed-service-accounts.md)|
|**도구 및 설정**|[Active Directory Domain Services의 관리 서비스 계정](https://technet.microsoft.com/library/dd378925(v=WS.10).aspx)|
|**커뮤니티 리소스**|[관리 서비스 계정: 이해, 구현, 모범 사례 및 문제 해결](http://blogs.technet.com/b/askds/archive/2009/09/10/managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting.aspx)|
|**관련 기술**|[Active Directory Domain Services 개요](active-directory-domain-services-overview.md)|


