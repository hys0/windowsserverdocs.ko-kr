---
title: "액세스 권한을된 보안"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5dec0c2-06fe-4c91-9bdc-67cc6a3ede60
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: eb83903204b00ef6c1eb116554ec54bc2211a399
ms.sourcegitcommit: 7b01b54032ec56432116626e08fbd92508c3a7d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="securing-privileged-access"></a>액세스 권한을된 보안

>Windows Server 2016 적용 됩니다.

액세스 최신 조직의 보안 보장 비즈니스 자산 설정 하는 중요 한 첫 번째 단계는 권한 보호 합니다. 조직에서 대부분의 또는 모든 비즈니스 자산의 보안을 운영 하 고 관리 IT 시스템 권한 있는 계정 무결성에 따라 다릅니다. 이러한 계정 및 다른 요소 같은 도난 공격 자격 증명을 사용 하 여 시스템 대상으로 지정 된 데이터를 액세스를 신속 하 게 액세스 권한을된의 사이버 공격자 대상으로 하는 [Pass-the-해시 및 티켓을 통과](https://www.microsoft.com/pth)합니다.

보호에 대해 관리자 액세스 확인 악성 위험에서 이러한 시스템을 분리 하 완벽 하 고 진심으 감사 접근 방식을 취합니다 해야 했습니다. 다음이 그림은 분리 하 고이 안내에서 관리 보호에 대 한 추천을 제공 하는 세 단계 설명 합니다.

![분리 하 고이 안내에서 관리 보호에 대 한 추천을 제공 하는 세 단계 다이어그램](../media/securing-privileged-access/PAW_LP_Fig1.JPG)

목표 로드맵:

-   **2-4 주 계획**: 신속 하 게 사용 하는 가장 자주 공격 기술 줄이기

-   **1-3 개월 계획**: 가시성 빌드 관리자 활동 제어

-   **6 월 계획**: 방어 더 사전 보안 상황을 계속

이 로드맵 결정된 악성에 대 한 액세스 권한을된 보호를 위해 수행 하는 것이 좋습니다. 이 로드맵 기존 기능 및 프로그램 조직에서 특정 요구에 맞게 조정할 수 있습니다.

> [!NOTE]
> 액세스 권한 보호 요소를 처리 하기 위해 변경을 뿐만 아니라 기술 구성 요소 (호스트 방어, 계정 보호, id 관리 등)를 포함 하 여 및 관리 방법 및 기술의 광범위 한를 해야 합니다.

## <a name="why-is-securing-privileged-access-important"></a>액세스 권한을 보호할 중요 한 이유는?
대부분의 조직에서 대부분의 또는 모든 비즈니스 자산의 보안을 운영 하 고 관리 IT 시스템 권한 있는 계정 무결성에 따라 다릅니다. 사이버 공격자 대상이 지정 된 데이터에는 조직의 모든 액세스를 신속 하 게 Active Directory와 같은 시스템에 대 한 액세스 권한을된에 집중 합니다.

기존 보안 방식을 조직의 네트워크 수신 및 송신 포인트를 사용 하 여 기본 보안 주변으로 중점적 하지만 두 추세 하 여 네트워크 보안 효과 크게 감소 되었습니다.

-   조직 호스트 데이터 및 리소스 기존 네트워크 경계 모바일 엔터프라이즈 Pc의 외부, 휴대폰 및 태블릿, 클라우드 서비스는 디바이스 및 BYOD 장치

-   물론은 워크스테이션 피싱 및 기타 웹 및 메일 공격 통해 네트워크 경계 내에 액세스할 수 있는 일관 되 고 지속적인 기능을 주었습니다.

자연 복잡 한 최신 엔터프라이즈 네트워크 보안 주변의 대신 조직의 신원 층의 인증과 컨트롤입니다. 관리자 권한이 있는 계정의이 새 "보안 주변" 제어 하는 효과적으로 중요 한 액세스 권한을된 보호 하기 위해 다음과 같습니다.

![조직의 신원을 계층을 보여 주는 다이어그램](../media/securing-privileged-access/PAW_LP_Fig2.JPG)

관리자 계정을 제어할 수 있는 악의적인 사용자 해당 권한을 아래와 같이 게인을 대상 조직의 소모를 사용할 수 있습니다.

![관리자 계정을 제어할 수 있는 악의적인 사용자 해당 권한의 사용 하 여 대상 조직의 소모 게인을 추진는 방법을 보여 주는 다이어그램](../media/securing-privileged-access/PAW_LP_Fig3.JPG)

일반적으로 관리자 계정 제어에서 공격자 이어질 공격의 유형에 대 한 자세한 내용은 참조 하세요는 [The 해시 전달 웹 사이트](https://www.microsoft.com/pth) 표현 흰색 문서, 동영상 등을 합니다.

다음이 그림은 액세스 권한을된 작업 웹 검색 및 메일에 액세스 하는 등의 높은 위험 표준 사용자 작업에서 분리 하 고 로드맵 설정 관리에 대 한 별도 "채널을" 보여 줍니다.

![액세스 권한을된 작업 웹 검색 및 메일에 액세스 하는 등의 높은 위험 표준 사용자 작업에서 분리 하 설정 하는 방법 관리에 대 한 별도 "채널" 보여 주는 다이어그램](../media/securing-privileged-access/PAW_LP_Fig4.JPG)

악의적인 사용자는 여러 가지 방법 액세스 권한을된 제어할 수 있는 하기 때문에이 로드맵에 설명 된 대로 전체론적인 하 고 자세한 기술 접근이 필요이 위험을 완화 합니다. 로드맵 격리할 되며이 그림 defense 열 각 영역에 완화 구축 하 여 액세스 권한을된를 사용할 수 있는 환경에서 요소 강화 다음과 같습니다.

![테이블 열 공격 및 defense 표시](../media/securing-privileged-access/PAW_LP_Fig5.JPG)

## <a name="security-privileged-access-roadmap"></a>보안 특권 액세스 로드맵
로드맵은 이미 수 있는 기술을 사용 하 여 최대화할 되도록 설계 되었으므로 보안 키 같은 기술을 활용을 통합 하 이미 배포 했을 수 제 3 자 보안 도구를 배포 합니다.

3 단계 권장 로드맵이 나뉩니다.

-   신속 하 게 사용 하는 가장 자주 공격 기술 완화-2-4 주 계획

-   1-3 개월 계획-빌드합니다 유형과 관리자 활동 제어

-   6 월 계획-방어 더 사전 보안 상태를 구축 Continue

각 단계는 로드맵의 비용 및 경쟁 하 여 온-프레미스에 대 한 액세스 권한을된 공격 및 자산 클라우드에 대 한 문제를 발생 하도록 설계 되었습니다. 로드맵은 가장 효과적인 및 먼저 이러한 공격와 솔루션 구현 한 경험에 따라 가장 빠른 구현 일정을 우선 순위를 지정 합니다.

> [!NOTE]
> 방법에 대 한 타임 라인 대략적인 되며 구현 고객에 대 한 경험을 기반으로 합니다. 기간 환경과 변경 관리 프로세스의 조직의 복잡 한에 따라 달라 집니다.

### <a name="security-privileged-access-roadmap-stage-1"></a>1 단계 보안 특권 액세스 로드맵:
1 단계는 로드맵은 신속 하 게 사용 하는 가장 자주 공격 기술을 자격 증명 도용의 및 남용 완화에 집중. 1 단계는 약 4 2 주 동안에서 구현 하도록 설계 되었으며이 다이어그램에 표시 됩니다.

![1 단계 그림 약 4 2 주 동안에서 구현 하도록](../media/securing-privileged-access/PAW_LP_Fig6.JPG)

이러한 구성 요소를 포함 하는 보안 액세스 권한을 로드맵 1 단계:

**1. 작업 관리자의 관리자 계정이 별도**

인터넷 위험 별도 위해 (피싱 공격 웹 검색) 관리자 권한이에서 관리자 권한으로 모든 담당자 전용된 계정을 만듭니다. 이에 대 한 추가 지침 게시 발 지침에 포함 된 [여기](http://Aka.ms/CyberPAW)합니다.

**2. 특권된 액세스 워크스테이션 (발) 1 단계: Active Directory 관리자**

인터넷 위험 별도 위해 (피싱 공격 웹 검색) 도메인 관리자 권한이에서 광고 관리자 권한으로 담당자 전용된 액세스 권한을된 워크스테이션 (발)을 만듭니다. 이 발 프로그램의 첫 번째 단계 이며 게시 가이드 1 단계 [여기](http://Aka.ms/CyberPAW)합니다.

**3. 고유한 로컬 관리자 암호를 워크스테이션**

**4. 서버에 대 한 현지 관리자 고유한 암호**

다른 컴퓨터를 공격 로컬 관리자 계정 암호 해시 로컬 삼로 데이터베이스를 도용 하 고 것 아무나 악의적 사용자의 위험을 완화 하 각 워크스테이션과 서버에서 임의의 고유한 암호를 구성 하 고 해당 암호 Active Directory에 등록 랩 도구를 사용 해야 합니다. 워크스테이션과 서버에서 사용할 수 있도록 로컬 관리자 암호 솔루션을 받을 수 있는 [여기](http://Aka.ms/LAPS)합니다.

운영 랩 및 발 환경에 대 한 추가 지침을 확인할 수 있습니다 [여기](http://aka.ms/securitystandards)합니다.

### <a name="security-privileged-access-roadmap-stage-2"></a>2 단계 보안 특권 액세스 로드맵:
2 단계는 완화 1 단계에서에서 빌드하고 약 1-3 개월 이내에 구현 하도록 설계 됩니다. 이 단계 단계가 다이어그램에서 표시 됩니다.

![2 단계 단계를 보여 주는 다이어그램](../media/securing-privileged-access/PAW_LP_Fig7.JPG)

**1. 발 단계 2, 3: 관리자 및 추가 강화 모든**

인터넷 위험 모든 권한 관리 계정 구분을 위해 1 단계에서 시작 발 계속 진행 하 고에 대 한 액세스 권한을된 사용 하 여 모든 직원 전용된 워크스테이션 구현 합니다. 2 단계를 안내의 3이이 지도 게시 [여기](http://Aka.ms/CyberPAW)합니다.

**2. 시간 범위 권한을 (영구 관리자 없음)**

권한 노출을 시간을 줄이고의 사용에 대 한 가시성, 아래 등 적절 한 솔루션을 사용 하 여 시간 (JIT)에 권한을 제공 합니다.

-   Microsoft 신원을 관리자 (MIM)의 사용에 대 한 Active Directory (AD DS 도메인 서비스)를 [액세스 권한 관리자 (PAM)](https://technet.microsoft.com/en-us/library/mt150258.aspx) 기능이 있습니다.

-   Azure Active Directory를 사용 하 여 [Azure AD 권한 있는 신원을 관리 PIM ()](http://aka.ms/AzurePIM) 기능이 있습니다.

**3입니다. 다단계 시간 범위 상승에 대 한**

보증 수준의 관리자 인증을 늘리려면 권한을 부여 하기 전에 다단계 인증을 해야 합니다.
Azure 다단계 인증 MFA ()를 사용 하 여 Azure AD PIM MIM PAM와이 수행할 수 있습니다.

**4. DC 유지 관리에 대 한 충분 한 바로 관리자 (JEA)**

계정 관리 권한이 도메인와 관련 된 위험에 노출 수량을 줄이기 위해 도메인 컨트롤러에서 일반적인 유지 관리 작업을 수행 powershell에서 바로 충분히 관리 (JEA) 기능을 사용 합니다. JEA 기술을 특정 사용자를 (도메인 컨트롤러)와 같은 서버에서 관리자 권한으로 제공 하지 않고 특정 관리 작업을 수행할 수 있습니다. 이 가이드를 다운로드 [TechNet](http://aka.ms/JEA)합니다.

**5. 아래 공격 도메인 및 Dc**

숲을 제어 하는 악성에 대 한 기회를 줄이기 위해 공격자 도메인 컨트롤러의에서 또는 개체 도메인의 제어를 제어할 수 수행할 수 있는 경로 줄입니다 해야 합니다. 이러한 위험 게시 줄이기 위해 지침에 따라 [여기](http://aka.ms/HardenAD)합니다.

**6. 공격 검색**

활성 자격 증명 도용 및 id로 표시 여부를 공격 신속 하 게 이벤트에 응답 하 고 손상, 포함 될 수 있도록 구축 하 고 구성 [Microsoft Advanced 위협 분석 (ATA)](https://www.microsoft.com/ata)합니다.

ATA를 설치 하기 전에 프로세스 ATA를 감지 하는 주요 보안 문제를 처리 하는 장소에 있는 확인 해야 합니다.

-   에 대 한 자세한 내용은 문제 대응 프로세스를 설정, [IT 보안 문제에 대 한 응답](https://aka.ms/irr) 하 고 "의심 스러운 활동에 응답" 및 "위반에서 복구" 섹션의 [완화 Pass-the-해시 및 기타 자격 증명 도용의](https://www.microsoft.com/pth), 버전 2.

-   대 한 자세한 내용은 IR 프로세스 준비 ATA 이벤트 및 배포 ATA 생성 하기 위해 지원 하기 위해 Microsoft 서비스 참여를 액세스 하 여 Microsoft 담당자에 게 문의 [이 페이지](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx)합니다.

-   액세스 [이 페이지](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx) 참여를 조사 하 고 인시던트에서 복구 지원 하기 위해 Microsoft 서비스에 대 한 자세한 내용은

-   구현 ATA를 사용할 수 있는 배포 가이드에 따라 [여기](http://aka.ms/ata)합니다.

### <a name="security-privileged-access-roadmap-stage-3"></a>3 단계 보안 특권 액세스 로드맵:
강화을 한편 전체 완화 추가 단계 1과 2에서의 완화에서 빌드를 로드맵 3 단계 합니다. 3 단계가 다이어그램에서 시각적으로 표시 됩니다.

![3 단계를 보여 주는 다이어그램](../media/securing-privileged-access/PAW_LP_Fig8.JPG)

이러한 기능은 이전 단계에서 완화 하 고 여 방어 사전 더 많은 상황을으로 이동 합니다.

**1. 역할 및 위임 모델 현대화**

보안 위험이 줄이기 위해 역할 및를 계층 모델 규칙을 준수, 클라우드 서비스 관리 역할 관리자 유용성 키 원칙은으로 통합 위임 모델의 모든 측면에 다시 디자인 해야 합니다. 이 모델은 기능을 활용 JIT 및 JEA 작업 자동화 기술을 뿐만 아니라 단계로 이전에 배포이 목표를 달성 하도록 합니다.

**2. 스마트 카드 또는 모든 관리자에 대 한 Passport 인증**

보증 수준 및 관리자 인증 유용성 향상, 호스트 Azure Active Directory에 및 Windows Server Active Directory (클라우드 서비스에 연결 된 계정 포함)에서 모든 관리자 계정에 강력한 인증을 해야 합니다.

**3. 관리자 숲 Active Directory 관리자**

Active Directory 관리자에 대 한 가장 강력한 보호를 제공 하는 보안 종속성 프로덕션 Active Directory에 있는 모든 공격 하지만, 생산 환경에서 가장 신뢰할 수 있는 시스템 분리 됩니다 환경을 설정 합니다. 에 대 한 자세한 내용은 ESAE 아키텍처 방문 [이 페이지](http://aka.ms/esae)합니다.

**4. Dc (Server 2016)에 대 한 코드 무결성 정책**

악의적인 사용자 공격 작동 및 관리 오류 실수로에서 도메인 컨트롤러의 무단된 프로그램 위험을 제한 하려면 커널 (드라이버 포함) 및 사용자 (응용 프로그램)는 컴퓨터에서 실행 하도록 허가 된 실행만 사용할 수 있도록 모드에 대 한 Windows Server 2016 코드 무결성을 구성 합니다.

**5. 차폐 Vm 가상 dc (Server 2016 Hyper-v 패브릭)**

를 보호 하기 위해 가상화 도메인 컨트롤러에서 공격 가상 컴퓨터의 고유한 물리적 보안 손실을 이용 하는 기능을 사용 하면이 새 서버 2016 Hyper-v 가상 Dc 로부터 Active Directory 비밀 도난 것을 방지할 합니다. 이 해결 방법에 대해 검사, 도난 및 저장소 및 네트워크 관리자가 변조 VM 데이터를 보호 하 고 VM Hyper-v 호스트 관리자 공격에 대 한 액세스 강화 생성 2 Vm 암호화할 수 있습니다.

## <a name="am-i-done"></a>@ 하셨나요?
이 로드맵 완료 현재는 알려진 하 고 사용할 수 있는 악성 오늘 공격에 대 한 강력한 액세스 권한을된 보호 얻게 됩니다. 보안 위협은 지속적으로 발전 및 shift, 좋습니다 비용 시키고 귀하의 환경 표적화 악성 성공 속도 줄이기에 집중 하는 지속적인 프로세스도 보안을 볼 수 있도록 합니다.

액세스 권한 보호 최신 조직의 보안 보장 비즈니스 자산 설정 하는 중요 한 첫 번째 단계는 하지만 제공 필요한 보안 보장 정책, 작업, 보안 정보, 서버, 응용 프로그램, Pc, 디바이스, 클라우드 패브릭 및 기타 구성 요소 같은 요소를 포함 하는 완벽 한 보안 프로그램의 일부만 않습니다.

대 한 자세한 내용은 완벽 한 보안 로드맵 빌드를 사용할 수 있는 엔터프라이즈 설계자 문서에 대 한 Microsoft 클라우드 보안 "고객 책임 및 로드맵" 섹션을 참조 [여기](http://aka.ms/securecustomer)합니다.

나 이러한 항목 중 하나를 지원 하기 위해 Microsoft 서비스에 대 한 자세한 내용은 Microsoft 담당자에 게 문의 또는 방문 [이 페이지](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx)합니다.

### <a name="related-topics"></a>관련된 항목
[프리미어 이스트: the 해시 Pass 및 기타 형태의 도난 자격 증명을 완화 하는 방법](https://channel9.msdn.com/Blogs/Taste-of-Premier/Taste-of-Premier-How-to-Mitigate-Pass-the-Hash-and-Other-Forms-of-Credential-Theft)

[Microsoft Advanced 위협 Analytics](http://aka.ms/ata)

[Credential Guard와 파생된 도메인 자격 증명을 보호](https://technet.microsoft.com/en-us/library/mt483740%28v=vs.85%29.aspx)

[장치 가드 개요](https://technet.microsoft.com/en-us/library/dn986865(v=vs.85).aspx)

[우선 순위가 높은 자산 안전한 관리자 워크스테이션와 보호](https://msdn.microsoft.com/en-us/library/mt186538.aspx)

[격리 된 사용자 모드 Dave Probert (9 채널)을 통해 Windows 10에서](https://channel9.msdn.com/Blogs/Seth-Juarez/Isolated-User-Mode-in-Windows-10-with-Dave-Probert)

[사용자 모드 프로세스와 위하여를 통해 Windows 10의에서 기능 격리 가브리엘 (채널 9)](http://channel9.msdn.com/Blogs/Seth-Juarez/Isolated-User-Mode-Processes-and-Features-in-Windows-10-with-Logan-Gabriel)

[더 많은 프로세스와 Dave Probert (채널 9)와 격리 된 사용자 모드 Windows 10의 기능](https://channel9.msdn.com/Blogs/Seth-Juarez/More-on-Processes-and-Features-in-Windows-10-Isolated-User-Mode-with-Dave-Probert)

[Windows 10 격리 된 사용자 모드 (Channel 9)를 사용 하 여 자격 증명 도용의 완화](https://channel9.msdn.com/Blogs/Seth-Juarez/Mitigating-Credential-Theft-using-the-Windows-10-Isolated-User-Mode)

[Windows Kerberos에 무과실 KDC 유효성 검사를 사용 하도록 설정](https://www.microsoft.com/en-us/download/details.aspx?id=6382)

[Windows Server 2012 용 Kerberos 인증의 새로운 기능](https://technet.microsoft.com/library/hh831747.aspx)

[Windows Server 2008 R2 단계별로에서 AD ds 인증 메커니즘 보증](https://technet.microsoft.com/library/dd378897(v=ws.10).aspx)

[신뢰할 수 있는 플랫폼 모듈](https://docs.microsoft.com/en-us/windows/device-security/tpm/trusted-platform-module-overview)
