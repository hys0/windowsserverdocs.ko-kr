---
ms.assetid: 460792e4-9f1d-4e7b-b6b2-53e057f839df
title: "광고 FS 배포 토폴로지 고려 사항"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 46692653ba10558a9236bd321127591bc7c8a275
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="using-ad-ds-claims-with-ad-fs"></a>ADFS AD DS 클레임 사용
  
>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
  
연결 된 응용 프로그램에 대 한 액세스 제어 풍부한 Active Directory 도메인 서비스 \(AD DS\)\-issued 사용자와 디바이스 클레임 Active Directory Federation Services \(AD FS\) 함께 사용 하 여 사용할 수 있습니다.  
  
## <a name="about-dynamic-access-control"></a>동적 액세스 제어에 대해  
Windows Server에서® 2012 동적 액세스 제어 기능 수 있도록 사용자 클레임에 따라 파일에 대 한 액세스 권한을 부여 \ (있는 의해 발생 사용자 계정 attributes\) 및 장치 클레임 \ (있는 의해 발생 컴퓨터 계정 attributes\) Active Directory 도메인 서비스 \(AD DS\) 발급 한 합니다. AD DS 클레임 발급 한 통합된 인증 Kerberos 인증 프로토콜을 통해 Windows에 통합 됩니다.  
  
동적 액세스 제어에 대 한 자세한 내용은 참조 [동적 액세스 제어 콘텐츠 로드맵](../../solution-guides/Dynamic-Access-Control--Scenario-Overview.md#BKMK_APP)합니다.  
  
### <a name="whats-new-in-ad-fs"></a>Adfs의 새로운 무엇 인가요?  
동적 액세스 제어 시나리오에 대 한 확장, Windows Server 2012에서 ADFS 이제 수 있습니다.  
  
-   컴퓨터 계정 특성 AD DS 내에서 사용자 계정 특성 외에 액세스 합니다. Adfs의 이전 버전에서는 Federation 서비스 액세스 하지 못했습니다 컴퓨터 계정 특성 전혀 AD DS에서.  
  
-   AD Kerberos 인증 티켓에 있는 디바이스 또는 사용자 클레임 발급 DS 사용 합니다. Adfs의 이전 버전에서는 클레임 엔진 사용자를 읽을 수 했으며 Kerberos에서 그룹 보안 Id \(SIDs\) 하지만 하지 못했습니다 모든 읽을 Kerberos 티켓에 포함 된 정보를 요구 합니다.  
  
-   사용자 또는 디바이스 클레임 SAML 토큰 응용 프로그램 풍부한 액세스 제어 하는 데 사용할 수 있는에 발행 DS AD 변환 됩니다.  
  
## <a name="benefits-of-using-ad-ds-claims-with-ad-fs"></a>AD DS 사용할 때의 이점 Adfs와 클레임  
이러한 AD DS 클레임 발급 Kerberos 인증 티켓에 삽입 하 고 다음 혜택을 제공 하기 위해 ADFS 함께 사용 수 있습니다.  
  
-   풍부 액세스 제어 정책이 필요한 조직 AD DS AD DS 특정된 사용자 또는 컴퓨터 계정에에서 저장 한 특성 값에 따라 클레임 실행을 사용 하 여 claims\ 기반 응용 프로그램 및 리소스에 액세스할 수 있게 합니다. 이를 작성 하 고 관리와 관련 된 추가 오버 줄이는 관리자가 수행할 수 있습니다.  
  
    -   응용 프로그램 및 Windows 통합 인증을 통해 액세스할 수 있는 리소스에 대 한 액세스를 제어 하는 데 사용 되는 광고 DS 보안 그룹입니다.  
  
    -   신뢰 Business\ to\ 비즈니스 \(B2B\)에 대 한 액세스를 제어 하는 데 사용 되는 포리스트 \ / 리소스와 인터넷에 액세스할 수 있는 응용 프로그램입니다.  
  
-   조직 수 이제 무단된 액세스를 방지 네트워크 리소스에 특정 컴퓨터 계정을 특성 AD DS에 저장 된 값 있는지 여부에 따라 클라이언트에서에서 \ (예:는 컴퓨터의 DNS name\)에서 리소스에 액세스 제어 정책 일치 \ (예: ACLd claims\ 사용 되는 파일 서버) 또는 신뢰 파티 정책 \ (claims\ 인식 웹 application\ 예를 들어, 함). 이 리소스 또는 응용 프로그램은 미세한 액세스 제어 정책 설정 하려면 관리자 수행할 수 있습니다.  
  
    -   Windows 통합 인증을 통해 액세스할 수 있습니다.  
  
    -   인터넷 ADFS 인증 메커니즘을 통해 액세스할 수 있습니다. ADFS 장치 클레임에 액세스할 수 있는 인터넷 리소스 또는 신뢰 파티 응용 프로그램에서 사용할 수 있는 SAML 토큰 캡슐화 할 ADFS 클레임에 발행 AD DS 변환 데 사용할 수 있습니다.  
  
## <a name="differences-between-ad-ds-and-ad-fs-issued-claims"></a>광고 DS와 ADFS 간의 차이점 발급 클레임  
클레임 DS 비교 ADFS AD에서 발급 한에 대해 이해 하는 두 가지 구분 요인 가지가 있습니다. 이러한 차이점 다음과 같습니다.  
  
-   AD DS 티켓 Kerberos SAML 토큰 하지에 클레임만 발급 수 있습니다. AD DS 문제 클레임 방법에 대 한 자세한 내용은 참조 [동적 액세스 제어 콘텐츠 로드맵](../../solution-guides/Dynamic-Access-Control--Scenario-Overview.md#BKMK_APP)합니다.  
  
-   ADFS 토큰 SAML Kerberos 티켓 하지에 클레임만 발급 수 있습니다. ADFS 클레임 문제 하는 방법에 대 한 자세한 내용은 참조 [클레임 엔진 The 역할](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)합니다.  
  
## <a name="how-ad-ds-issued-claims-work-with-ad-fs"></a>AD DS ADFS 클레임 작업 발급 방법  
AD DS 클레임 발급 한 사용자의 인증 상황에 맞는 하지 않고 Active Directory에 대 한 별도 LDAP 호출에서 직접 사용자와 디바이스가 클레임에 액세스 하 Adfs로 사용할 수 있습니다. 다음 그림와 해당 단계 자세히 동적 액세스 제어 시나리오에 대 한 액세스 claims\ 기반 제어를 사용 하도록 설정 하려면이 프로세스의 작동 방식에 대해 설명 합니다.  
  
![클레임을 사용 하 여](media/UsingADDSClaimswithADFS.gif)  
  
1.  AD DS 관리자 AD DS 스키마에서 Active Directory 관리 센터 콘솔 또는 PowerShell cmdlet 사용 하면 특정 클레임 유형 개체를 사용합니다.  
  
2.  ADFS 관리자 AD FS Management console을 만들고 클레임 공급자와 당사자 구성를 사용 하 여 사용 하 여 신뢰 pass\ 쓰루 변환 주장 규칙 또는 합니다.  
  
3.  Windows 클라이언트 네트워크에 액세스 하려고 했습니다. Kerberos 인증 과정의 일환으로, 클라이언트 해당 사용자를 표시 하지 않는 \(TGT\) 티켓 아직 모든 클레임 도메인 컨트롤러에 포함 컴퓨터 ticket\ 부여 합니다. 도메인 컨트롤러 다음 DS 광고에 사용된 클레임 형식에 대 한 비추고 결과 클레임 반환된 Kerberos 티켓에 포함 되어 있습니다.  
  
4.  User\/클라이언트를 ACLd 클레임 요구 하는 파일 리소스에 액세스 하려고 Kerberos에서 표시 된 복합 ID 이러한 클레임 있어 리소스에 액세스할 수 있습니다.  
  
5.  동일한 클라이언트가 ADFS 인증에 대해 구성 하는 웹 사이트나 웹 응용 프로그램에 액세스할 때 사용자가 Windows 통합된 인증에 대 한 구성 된 ADFS federation 서버에 리디렉션됩니다. 클라이언트는 Kerberos 사용 하는 도메인 컨트롤러에 요청을 보냅니다. 도메인 컨트롤러 Kerberos 클라이언트 다음 federation 서버에 제공할 수 있는 요청한 클레임 포함 된 티켓을 발행 합니다.  
  
6.  클레임 규칙 클레임 공급자에서 구성 된 방식에 따라 및 필요로 하 파티 신뢰를 구성 이전에 관리자 ADFS 클레임에서 Kerberos 티켓 읽고 클라이언트에 대해 발급 SAML 토큰에 포함 됩니다.  
  
7.  클라이언트가 올바른 클레임 포함 된 SAML 토큰 받으며는 해당 웹 사이트로 이동 합니다.  
  
AD DS 발급 한 주장 ADFS 작업할에 필요한 클레임 규칙을 만드는 방법에 대 한 자세한 내용은 참조 [들어오는 주장 변환할 규칙](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
