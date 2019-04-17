---
ms.assetid: 6a852428-c1ec-4703-b3b3-a4bfdf8cbb9d
title: "작업 & #39,의 Active Directory 도메인 서비스에서 Windows Server 2016의 새로운 기능"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1fdd012af6f025d58340f63f98da0d8dc11df0e0
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="what39s-new-in-active-directory-domain-services-for-windows-server-2016"></a>작업 & #39,의 Active Directory 도메인 서비스에 대 한 Windows Server 2016의 새로운 기능

>Windows Server 2016 적용 됩니다.

Active Directory (AD DS 도메인 서비스)에 다음과 같은 새로운 기능 Active Directory 환경의 보안을 유지 하 여 클라우드 전용 배포도 클라우드에서 일부 응용 프로그램 및 서비스 호스트는 온-프레미스 호스트 다른 장소와 하이브리드 배포 하는 데 도움이 조직에 대 한 기능을 개선 합니다. 향상 된 기능 다음과 같습니다.  
  
-   [액세스 권한을된 관리](https://technet.microsoft.com/library/mt150258.aspx   
)  
  
- [Azure Active Directory 가입을 통해 Windows 10 장치에 확장 클라우드 기능](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-overview/)   
  
- [Windows 10에 대 한 Azure AD에 도메인 가입 장치를 연결 환경을](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-devices-group-policy/)   
  
- [조직에서 Microsoft Passport 작업에 대 한 사용](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-passport-deployment/)    
  
-  [파일 FRS (복제 서비스) 및 Windows Server 2003 기능 수준의 사용 중단](ad-ds/active-directory-functional-levels.md)  
  
  
## <a name="BKMK_PAM"></a>액세스 권한을된 관리  
권한 관리 액세스 (PAM) 보안을 줄일 수 문제로 인해 발생 하는 Active Directory 환경에 대 한 이러한 해시를 통과, 창 피싱 및 유사 유형의 공격 도난 기술을 자격 증명 합니다. Microsoft 신원을 관리자 (MIM)를 사용 하 여 구성 된 새로운 관리 액세스 솔루션을 제공 합니다. PAM 가지가 도입 되었습니다.  
  
-   새로운 방호 MIM으로 제공 되는 Active Directory 숲입니다. 방호 숲 기존 숲 된 특별 한 PAM 신뢰를 있습니다. 악의적인 활동 및 권한이 있는 계정의 사용에 대 한 기존 숲에서 격리 무료 것으로 알려져 하는 새로운 Active Directory 환경을 제공 합니다.  
  
-   MIM 승인의 요청에 따라 새로운 워크플로 함께 관리자 권한 요청에 새 프로세스입니다.  
  
-   새 그림자 보안 사용자 (그룹) 방호 숲 속의 관리자 권한 요청에 응답 MIM으로 제공 됩니다. 섀도 보안 사용자는 기존 숲 속의 관리 그룹 SID 참조 하는 특성 합니다. 따라서 모든 액세스를 제어 (Acl 목록)을 변경 하지 않고 그림자 그룹을 기존 숲 속의 리소스에 액세스할 수 있습니다.  
  
-   만료 된 그림자 그룹의 시간 바인딩된 멤버십 수 있는 기능을 연결 합니다. 사용자는 관리 작업을 수행 하는 데 필요한만 충분 한 시간에 대 한 그룹에 추가할 수 있습니다. 시간 범위 멤버십 Kerberos 티켓 수명 전파 되는 라이브 시간 (TTL) 값으로 표시 됩니다.  
  
    > [!NOTE]  
    > 만료 링크는 연결 된 모든 특성에서 사용할 수 있습니다. 하지만 회원/구성원 연결 된 특성 사용자 및 그룹 간의 관계는 유일한 예 만료 연결 기능을 사용 하는 완벽 한 솔루션 등 PAM 미리 구성 합니다.  
  
-   KDC 향상 된 기능에 기본 제공 Active Directory 도메인 컨트롤러 Kerberos 티켓 수명 최저 가능한 라이브 시간 (TTL) 값 경우 사용자가 여러 번 바인딩된 멤버십 관리 그룹에를 제한 합니다. 예를 들어 Kerberos 허용 (TGT) 티켓이 수명은 시간이 로그온 할 때 시간 범위 그룹 A에 추가 되 면 있는 그룹 대답:에 남아 있는 또한 다른 시간 범위 B 그룹 A 보다 낮은 TTL 있는 그룹 구성원 다음 TGT 수명이 경우 B. 그룹에서 남은 시간이  
  
-   수 있도록 쉽게 모니터링 새로운 기능 액세스 요청 누가, 액세스 권한을 부여 된 및 어떤 작업이 수행 된 식별 합니다.  
  
**요구 사항**  
  
-   Microsoft Id 관리자  
  
-   Active Directory 포리스트 Windows Server 2012 r 2의 이상 기능 수준이 있습니다.  
  
## <a name="BKMK_AzureADJoin"></a>Azure AD 가입  
Azure Active Directory 참여 기업 및 개인 장치에 대 한 향상 된 기능에 대 한 엔터프라이즈, 비즈니스 및 EDU 고객-신원을 경험 향상 됩니다.  
  
한 혜택:  
  
-   **최신 설정을 사용 가능 여부** corp 소유 하 고 Windows 디바이스에서 합니다. 산소 서비스 개인 Microsoft 계정에 더 이상 필요: 사용자의 기존 회사 계정을 준수 끄기 이제 실행 합니다. 산소 서비스는 온-프레미스 Windows 도메인에 가입 하는 Pc 및 Pc와 Azure AD 테 ("클라우드 domain")에 "연결"는 장치에서 작동 합니다. 이러한 설정은 다음과 같습니다.  
  
    -   로밍 또는 개인 설정, 내게 필요한 옵션 설정 및 자격 증명  
  
    -   백업 및 복원  
  
    -   회사 계정 사용 하 여 Microsoft 스토어에 대 한 액세스  
  
    -   라이브 타일 및 알림  
  
-   **조직 리소스에 액세스** corp 소유 하 고는 Windows 도메인에 가입 수 없는 모바일 장치 (휴대폰, 패) 또는 BYOD  
  
-   **단일 로그인에** Office 365 및 기타 조직 앱, 웹 사이트 및 리소스에 있습니다.  
  
-   **BYOD 디바이스에서**개인적으로 소유 하 고 디바이스에 회사 계정을 온-프레미스 도메인 또는 Azure AD) (에서 추가 하 고 즐길 수 있게 조건 계정을 제어 및 장치 건강 대와 같은 새로운 기능을 준수 하는 방식에서 리소스를 통해 앱 및 웹에서 작동 하도록 SSO 합니다.  
  
-   **MDM 통합** 자동 등록 장치에 MDM (Intune 또는 제 3 자)를 사용 하면  
  
-   **"키오스크" 모드를 설정 하 고 디바이스를 공유** 여러 사용자 조직에 대 한  
  
-   **개발자 환경** enterprise 및 공유 프로그래밍 스택 개인 컨텍스트를 제공 하는 앱을 빌드할 수 있습니다.  
  
-   **이미징** 옵션을 사용 하면 장치를 구성 corp 소유 하 고 첫 실행 경험 하는 동안 직접 이미징 및 사용자가 허용 중에서 선택할 수 있습니다.  
  
자세한 내용은 참조 [회사에 대 한 Windows 10: 작업에 대 한 디바이스를 사용 하는 방법](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-windows10-devices-overview/?rnd=1)합니다.  
  
## <a name="BKMK_IDLocker"></a>Microsoft Passport  
Microsoft Passport은 새 키 기반 인증 조직과 범위를 벗어나는 암호 소비자 접근 합니다. 이러한 형식의 인증 위반, 도난 및 phish 안전한 자격 증명에 의존합니다.  
  
사용자는 인증서 나 비대칭 주요 페어링에 연결 된 정보에는 PIN 또는 생체 인식 로그도, 디바이스에 로그온 합니다. Id 공급자 (IDPs) IDLocker로 사용자의 공개 키를 매핑하여 사용자를 확인 하 고 로그에 한 번 암호 (OTP), Phonefactor 또는 다른 알림 메커니즘을 통해 정보를 제공 합니다.  
  
자세한 내용은 참조 [암호 Microsoft Passport를 않고도 id를 인증](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-passport/)  
  
## <a name="BKMK_FRSDeprecation"></a>파일 FRS (복제 서비스) 및 Windows Server 2003 기능 수준의 사용 중단  
하지만 복제 서비스 (FRS 파일) 및 Windows Server 2003 기능 수준 이전 버전의 Windows Server에서 더 이상 사용 되지, Windows Server 2003 운영 체제가 더 이상 지원 되지 반복에 합니다. 결과적으로, Windows Server 2003을 실행 하는 도메인 컨트롤러에서 도메인 제거 해야 합니다. 도메인 및 숲 기능 수준을 기울여야 최소한의 환경에 추가 되지 이전 버전의 Windows Server를 실행 하는 도메인 컨트롤러를 방지 하기 위해 Windows Server 2008 합니다.  
  
Windows Server 2008 및 높은 도메인 기능 수준에서 배포 서비스 (DFS 파일) 복제 SYSVOL 폴더 내용 도메인 컨트롤러 간에 복제 하는 데 사용 됩니다. Windows Server 2008 도메인 기능 수준을 이상 새 도메인 만들면 DFS 복제 SYSVOL 복제할 자동으로 사용 됩니다. 낮은 기능 수준 도메인을 만든 경우 FRS DFS 복제 sysvol를 사용 하 여 마이그레이션을 해야 합니다. 마이그레이션 단계에 따라 중 하나 수 있습니다는 [technet 절차](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx) 하거나를 참조할 수는 [저장소 팀 생겼습니다 블로그에서 단계 효율성을 높였습니다](http://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx)합니다.  
  
Windows Server 2003 도메인 및 숲 기능 수준 계속 지원 될 수 있지만 조직 기능 수준을 (또는 이상 가능한 경우) Windows Server 2008를 발생 시켜 SYSVOL 복제 호환 되도록 하는 앞으로 지원 합니다. 또한, 그 외 여러 혜택와 기능 사용할 수 있는 방법이 클수록 높은 기능 수준에서 합니다. 다음 리소스에 대 한 자세한 내용 보려면  
  
-   [이해 기능 수준 Active Directory Domain Services (AD DS)](ad-ds/active-directory-functional-levels.md)  
  
-   [도메인 기능 수준을](https://technet.microsoft.com/library/cc753104.aspx)  
  
-   [숲 기능 수준 높이기](https://technet.microsoft.com/library/cc730985.aspx)  
  
