---
title: 그룹 관리 서비스 계정 개요
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
ms.openlocfilehash: 4912ae273e603b4a3362c4984da710f780c3e8b3
ms.sourcegitcommit: f26d2668f57624a3865ca4ffd36a698eea7b503e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2018
---
# <a name="group-managed-service-accounts-overview"></a>그룹 관리 서비스 계정 개요

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 IT 전문가 실제 응용 프로그램을 설명 하 여 해당 그룹 관리 서비스 계정 소개에 대 한 Microsoft의 구현 및 하드웨어 및 소프트웨어 요구 사항을 변경 됩니다.


## <a name="BKMK_OVER"></a>기능 설명
독립 실행형 관리 서비스 계정, Windows Server 2008 R2 및 Windows 7에서 소개 된, 관리 되는 도메인 계정 암호 자동 관리 및 등의 다른 관리자 관리 위임 간단한 SPN 관리를 제공 하는 됩니다.

그룹 관리 서비스 계정 도메인 내 같은 기능을 제공 되지만 여러 서버 해당 기능을 확장 합니다. 네트워크 부하 분산 등 팜에서 호스트 되는 서비스에 연결할 때 서비스의 모든 경우 동일한 주 사용 하 여 상호 인증을 지원 인증 프로토콜 필요 합니다. 그룹 관리 서비스 계정 서비스 정책으로를 사용 하는 Windows 운영 체제 관리자가 암호를 관리할 수에 의존 하지 않고 계정에 대 한 암호를 관리 합니다.

Microsoft 키 배포 서비스 \(kdssvc.dll\)를 안전 하 게 최신 키 또는 키 식별자를 사용 하 여 Active Directory 계정에 대 한 특정 키를 가져오는 방법을 제공 합니다. 키 배포 서비스 계정의 키를 만드는 데 사용 되는 비밀 정보를 공유 합니다. 이러한 키는 정기적으로 변경 됩니다. 그룹 관리 서비스 계정에 대 한 도메인 컨트롤러 계산 뿐만 아니라 다른 특성 그룹 관리 서비스 계정 키 배포 서비스에서 제공 하는 키의 암호를 합니다.  구성원 호스트 도메인 컨트롤러에 문의 하 여 현재 및 이전 암호 값을 얻을 수 있습니다.

## <a name="BKMK_APP"></a>실용적인 응용 프로그램
그룹 관리 서비스 계정 또는 네트워크 부하 분산 뒤 시스템 서버 그룹에서 실행 되는 서비스에 대 한 단일 id 솔루션을 제공 합니다. 그룹 MSA 솔루션을 제공 하 여 새 그룹 주 MSA에 대해 서비스 구성할 수 있으며 암호 관리 Windows에 의해 처리 됩니다.

그룹을 사용 하 여 관리 서비스 계정, 서비스 또는 서비스 관리자 필요가 없습니다 인스턴스 서비스 간의 암호 동기화를 관리 합니다. 그룹 관리 서비스 계정 오랜된 기간 및 서비스의 모든 인스턴스 구성원 호스트 관리 오프 라인으로 유지 호스트를 지원 합니다. 즉, 연결 된 서비스의 인스턴스 모르는 기존 클라이언트 컴퓨터 인증할 수 있는 단일 id를 지 원하는 서버 팜 배포할 수 있습니다.

클러스터 장애 조치 gMSAs 지원 하지 않습니다. 그러나 Windows 서비스, 앱 풀, 예약된 된 작업 인지 gMSA 또는 sMSA 기본적으로 지원 경우는 gMSA 또는 sMSA 위에 클러스터 서비스가 실행 되는 서비스 사용할 수 있습니다.

## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항

64\ 비트 아키텍처 그룹 관리 서비스 계정 관리 하는 데 사용 되는 Windows PowerShell 명령을 실행 해야 합니다.

관리 서비스 계정 Kerberos 지원 암호화 종류에 따라 달라 집니다. 클라이언트 컴퓨터 Kerberos DC 만들고 사용 하 여 서버에 인증 Kerberos 서비스 티켓 DC 및 서버 지원 암호화도 보호 합니다. DC 작업을 결정 하는 계정 msDS\ SupportedEncryptionTypes 특성을 사용 하 여 서버 암호화를 지원 하 고 없는 특성 인 것으로 간주 클라이언트 컴퓨터는 강력한 암호화 형식을 지원 하지 않습니다. 호스트 r c 4를 지원 하지 않을 하도록 구성, 인증 되지 항상 것입니다. 이러한 이유로 AES 항상 명시적으로 구성 해야 Msa에 대해 합니다.

> [!NOTE]
> Windows Server 2008 R2 부터는 DES 기본적으로 불가능 합니다. 지원 되는 암호화 형식에 대 한 자세한 내용은 참조 [Kerberos 인증에서 변경 사항](https://technet.microsoft.com/library/dd560670(WS.10).aspx)합니다.

그룹 관리 서비스 계정 Windows Server 2012 전에 Windows 운영 체제에 적용 되지 않습니다.

## <a name="server-manager-information"></a>서버 관리자 정보
구성 단계가 MSA를 구현 하 고 서버 관리자 또는 Install\ WindowsFeature cmdlet 사용 하 여 MSA 그룹화 하는 데 필요한 합니다.

## <a name="BKMK_LINKS"></a>참조 하십시오
다음 표에서 관리 서비스 계정 및 그룹 관리 서비스 계정 관련 된 추가 리소스에 대 한 링크를 제공 합니다.

|콘텐츠 종류|참조|
|--------|-------|
|**제품 평가**|[관리 서비스 계정에 대 한 새로운 기능](what-s-new-for-managed-service-accounts.md)<br /><br />[관리 서비스 계정 Windows 7 및 Windows Server 2008 r 2에 대 한 설명서](https://technet.microsoft.com/library/ff641731(v=ws.10).aspx)<br /><br />[계정 Step\ by\ 단계 가이드 서비스](https://technet.microsoft.com/library/dd548356(v=ws.10).aspx)|
|**계획**|아직 사용할 수 없음|
|**배포**|아직 사용할 수 없음|
|**작업**|[관리 서비스 계정 Active Directory에](https://technet.microsoft.com/library/dd378925(v=ws.10).aspx)|
|**문제 해결**|아직 사용할 수 없음|
|**평가판**|[관리 서비스 계정 하는 그룹 시작](getting-started-with-group-managed-service-accounts.md)|
|**도구 및 설정**|[관리 서비스 계정 Active Directory 도메인 서비스에서](https://technet.microsoft.com/library/dd378925(v=WS.10).aspx)|
|**커뮤니티 리소스**|[이해: 관리 서비스 계정, 구현 모범 사례 및 문제 해결](http://blogs.technet.com/b/askds/archive/2009/09/10/managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting.aspx)|
|**관련된 기술이**|[Active Directory Domain Services 개요](active-directory-domain-services-overview.md)|


