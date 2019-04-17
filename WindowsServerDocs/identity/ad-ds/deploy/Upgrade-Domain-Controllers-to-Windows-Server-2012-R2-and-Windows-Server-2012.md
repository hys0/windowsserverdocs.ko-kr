---
ms.assetid: e4c31187-f15f-410b-bb79-8d63e2f2b421
title: "Windows Server 2012와 Windows Server 2012 R2 도메인 컨트롤러 업그레이드"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e317c5a939d417bac844c4080223d7b5e0eec149
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="upgrade-domain-controllers-to-windows-server-2012-r2-and-windows-server-2012"></a>Windows Server 2012와 Windows Server 2012 R2 도메인 컨트롤러 업그레이드

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목 Windows Server 2012 R2 및 Windows Server 2012에서 Active Directory 도메인 서비스에 대 한 배경 정보를 제공 하 고 Windows Server 2008 또는 Windows Server 2008 R2 도메인 컨트롤러 업그레이드 프로세스에 설명 합니다.  
  
-   [업그레이드 단계 도메인 컨트롤러](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_UpgradeWorkflow)  
  
-   [Windows Server 2012에서 새로운 무엇 인가요?](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_WhatsNewEight)  
  
-   [Windows Server 2012 r 2에서 AD DS 새로운 무엇 인가요?](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_NewWS2012R2)  
  
-   [Windows Server 2012에서 광고 DS의 새로운 무엇 인가요?](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_WhatsNewAD)  
  
-   [AD DS 서버 역할 설치 변경](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_InstallationChanges)  
  
-   [사용 하지 않는 기능 및 Windows Server 2012에서 광고 DS 관련 동작 변경](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_DeprecatedFeatures)  
  
-   [운영 체제 요구 사항](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_SysReqs)  
  
-   [지원 되는 업그레이드 경로 위치에서](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_UpgradePaths)  
  
-   [수준 기능 및 요구 사항](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_FunctionalLevels)  
  
-   [광고 DS 상호 운용성 다른 서버 역할와 Windows 운영 체제](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_ServerRoles)  
  
-   [마스터 역할 작업](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_OpsMasters)  
  
-   [Windows Server 2012를 실행 하는 도메인 컨트롤러 가상화](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_Virtual)  
  
-   [Windows Server 2012 서버 관리](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_Admin)  
  
-   [응용 프로그램 호환성](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_AppCompat)  
  
-   [알려진된 문제](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_KnownIssues)  
  
## <a name="BKMK_UpgradeWorkflow"></a>업그레이드 단계 도메인 컨트롤러  
최신 버전의 Windows Server를 실행 하 고 필요에 따라 이전 도메인 컨트롤러 내리기 하는 도메인 컨트롤러를 도메인 업그레이드 하는 권장된 방법은입니다. 이 방법은 기존 도메인 컨트롤러의 운영 체제를 업그레이드 하는 것이 좋습니다. 이 목록은 일반 단계에 따라 Windows Server의 최신 버전을 실행 하는 도메인 컨트롤러 홍보 하기 전에 다룹니다.  
  
1.  Verify the target server meets [system requirements](https://technet.microsoft.com/library/dn303418.aspx).  
  
2.  확인 [응용 프로그램 호환성](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_AppCompat)합니다.  
  
3.  보안 설정을 확인 합니다. For more information, see [Deprecated features and behavior changes related to AD DS in Windows Server 2012](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_DeprecatedFeatures) and [Secure default settings in Windows Server 2008 and Windows Server 2008 R2](https://technet.microsoft.com/library/upgrade-domain-controllers-to-windows-server-2008-r2(WS.10).aspx#BKMK_SecureDefault).  
  
4.  설치를 실행 하려면 컴퓨터에서 대상 서버에 연결을 확인 합니다.  
  
5.  필요한 작업이 마스터 역할의 사용 가능 여부를 확인 합니다.  
  
    -   기존 도메인 및 숲 Windows Server 2012를 실행 하는 첫 번째 DC를 설치 하려면 설치 실행 되는 시스템 adprep /forestprep 실행 하는 데 스키마 마스터와 adprep /domainprep 실행 하는 데 infrastructure 마스터에 대 한 연결이 필요 합니다.  
  
    -   첫 번째 DC 숲 스키마 이미 확장 된 도메인의를 설치 하려면 하기만 하면 infrastructure 마스터에 연결 됩니다.  
  
    -   을 설치 하거나 기존 숲 속의 도메인 제거 하려면 마스터 명명 도메인에 연결을 해야 합니다.  
  
    -   도메인 컨트롤러 설치 된 경우에 RID 마스터에 대 한 연결을 해야 합니다.  
  
    -   기존 숲 속의 첫 번째 읽기 전용 도메인 컨트롤러를 설치 하는 경우 각 응용 디렉터리 파티션, 라고도 비 도메인 이름 상황에 맞는 또는 NDNC 인프라 마스터에 대 한 연결이 필요 합니다.  
  
6.  광고 DS 설치 프로그램을 실행 하는 데 필요한 자격 증명을 제공 해야 합니다.  
  
    |설치 알림|자격 증명 요구 사항|  
    |-----------------------|---------------------------|  
    |새 숲 설치|로컬 관리자 대상 서버에서|  
    |기존 숲 속의 새 도메인 설치|엔터프라이즈 관리|  
    |기존 도메인에 추가 DC 설치|도메인 관리|  
    |Adprep /forestprep 실행|스키마 관리, Enterprise 관리자 및 도메인 관리자|  
    |Adprep /domainprep 실행|도메인 관리|  
    |Adprep 하십시오를 실행합니다|도메인 관리|  
    |Adprep /rodcprep 실행|엔터프라이즈 관리|  
  
    AD DS 설치할 수 있는 권한이 위임 수 있습니다. For more information, see [Installation Management Tasks](https://technet.microsoft.com/library/cc773327(WS.10).aspx).  
  
다음 링크에서 새 및 Windows Server 2012 복제 도메인 컨트롤러 Windows PowerShell cmdlet 및 서버 관리자를 사용 하 여 홍보 단계 단계별 지침을 확인할 수 있습니다.  
  
-   [Active Directory Domain Services (수준을 100) 설치](https://technet.microsoft.com/library/hh472162.aspx)  
  
-   [새로운 Windows Server 2012 Active Directory 숲 (수준을 200) 설치](https://technet.microsoft.com/library/jj574166.aspx)  
  
-   [기존 도메인 (200 수준)의 복제 Windows Server 2012 도메인 컨트롤러 설치](https://technet.microsoft.com/library/jj574134.aspx)  
  
-   [새로운 Windows Server 2012 Active Directory 자녀 또는 밤나무 도메인 (수준을 200) 설치](https://technet.microsoft.com/library/jj574105.aspx)  
  
-   [Windows Server 2012 Active Directory 설치 Read-Only RODC (도메인 컨트롤러) (200 수준)](https://technet.microsoft.com/library/jj574152.aspx)  
  
-   [설정을를 Windows Server 2012 도메인 컨트롤러 (영어 (미국))에 대 한 단계별 가이드](https://social.technet.microsoft.com/wiki/contents/articles/12370.step-by-step-guide-for-setting-up-windows-server-2012-domain-controller-en-us.aspx)  
  
## <a name="BKMK_WhatsNewEight"></a>Windows Server 2012에서 새로운 무엇 인가요?  
서버 역할으로 나열 된 새로운 기능 및 기술 영역은 다음과에서 같습니다. For more whitepapers, video demonstrations, and presentations about other features in Windows Server 2012, see [Server and Cloud Platform](https://www.microsoft.com/server-cloud/default.aspx).  
  
||||  
|-|-|-|  
|[Active Directory 인증서 서비스 (AD CS)](https://technet.microsoft.com/library/hh831373.aspx)|[Active Directory 권한 관리 서비스 (AD RMS)](https://technet.microsoft.com/library/hh831554.aspx)|[BitLocker 드라이브 암호화](https://technet.microsoft.com/library/hh831412.aspx)|  
|[BranchCache](https://technet.microsoft.com/library/jj127252.aspx)|[Dynamic Host Configuration protocol DHCP)](https://technet.microsoft.com/library/jj200226.aspx)|[Domain Name System DNS)](https://technet.microsoft.com/library/jj200224.aspx)|  
|[장애 조치 클러스터링](https://technet.microsoft.com/library/hh831414.aspx)|[파일 서버 리소스 관리자](https://technet.microsoft.com/library/hh831746.aspx)|[그룹 정책](https://technet.microsoft.com/library/jj574108.aspx)|  
|[Hyper-v](https://technet.microsoft.com/library/hh831410.aspx)|[IP 주소 관리 (IPAM)](https://technet.microsoft.com/library/jj200214.aspx)|[Kerberos 인증](https://technet.microsoft.com/library/hh831747.aspx)|  
|[관리 서비스 계정](https://technet.microsoft.com/library/hh831451.aspx)|[네트워킹](https://technet.microsoft.com/library/jj200215.aspx)|[원격 데스크톱 서비스](https://technet.microsoft.com/library/hh831527.aspx)|  
|[보안 감사](https://technet.microsoft.com/library/hh849638.aspx)|[서버 관리자](https://blogs.technet.com/b/servermanager/archive/2012/06/27/server-manager-power-of-many-simplicity-of-one.aspx)|[스마트 카드](https://technet.microsoft.com/library/hh849637.aspx)|  
|[TLS/SSL (Schannel SSP)](https://technet.microsoft.com/library/hh831771.aspx)|[Windows 배포 서비스](https://technet.microsoft.com/library/hh974416.aspx)|[PowerShell Windows 3.0](https://technet.microsoft.com/library/hh857339)|  
  
### <a name="automatic-maintenance-and-changes-to-restart-behavior-after-updates-are-applied-by-windows-update"></a>자동 유지 관리 및 변경 사항을 Windows 업데이트에서 업데이트를 적용 한 후 동작을 다시 시작  
이전에 Windows 8, Windows 업데이트에서 업데이트 확인 다운로드 하 고 설치 하는 자체 내부 일정을 관리 합니다. 이 Windows 업데이트 에이전트는 항상 백그라운드에서 실행, 메모리 및 기타 시스템 리소스 사용 필요 합니다.  
  
Windows 8 and Windows Server 2012 introduce a new feature called [Automatic Maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037(v=vs.85).aspx). 자동 유지 관리 각각 자체 일정을 관리 하는 데 사용 하 고 실행 논리 다양 한 기능을 통합 되어 있습니다. This consolidation allows for all these components to use far less system resources, work consistently, respect the new [Connected Standby](https://msdn.microsoft.com/library/windows/hardware/jj248729.aspx) state for new device types, and consume less battery on portable devices.  
  
Windows 업데이트 자동 유지 관리 Windows 8 및 Windows Server 2012에서의 일부 이기 때문에 날짜와 시간 업데이트를 설치 하도록 설정 하는 데 내부 일정은 더 이상 효과적인. To help ensure consistent and predictable restart behavior for all devices and computers in your enterprise, including those that run Windows 8 and Windows Server 2012, see Microsoft KB article [2885694](https://support.microsoft.com/kb/2885694) (or see October 2013 cumulative rollup [2883201](https://support.microsoft.com/kb/2883201)), then configure policy settings described in the WSUS blog post [Enabling a more predictable Windows Update experience for Windows 8 and Windows Server 2012 (KB 2885694)](http://blogs.technet.com/b/wsus/archive/2013/10/08/enabling-a-more-predictable-windows-update-experience-for-windows-8-and-windows-server-2012-kb-2885694.aspx).  
  

## <a name="BKMK_NewWS2012R2"></a>Windows Server 2012 r 2에서 AD DS 새로운 무엇 인가요?  
다음 표에서 가능한 경우 자세한 정보 링크와 Windows Server 2012 r 2의 광고 DS에 대 한 새로운 기능 요약 되어 있습니다. For a more detailed explanation of some features, including their requirements, see [What's New in Active Directory in Windows Server 2012 R2](https://technet.microsoft.com/library/dn268294.aspx).  
  
|기능|설명|  
|-----------|---------------|  
|[Workplace Join](https://technet.microsoft.com/library/dn280945.aspx)|정보 작업자를 회사 리소스 및 서비스에 액세스 하려면 해당 회사와 개인 디바이스를 연결할 수 있습니다.|  
|[웹 응용 프로그램 프록시](https://technet.microsoft.com/library/dn280942.aspx)|새 원격 액세스 역할 서비스를 사용 하 여 웹 응용 프로그램에 대 한 액세스를 제공 합니다.|  
|[Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx)|ADFS 간단한 배포 및 사용자가 개인 장치에서 리소스에 액세스 하 고 IT 부서 액세스 제어 관리할 수 있도록 개선 했습니다.|  
|[SPN 및 UPN 고유](https://technet.microsoft.com/library/dn535779.aspx)|사용자 계정 이름을 (Upn)을 실행 중인 Windows Server 2012 R2 도메인 컨트롤러 차단 중복 서비스 Spn 사용자 이름 () 생성 합니다.|  
|[Winlogon 자동 다시 시작 Sign-on (ARSO)](https://technet.microsoft.com/library/dn535772.aspx)|수 있도록 잠금 화면 응용 프로그램을 다시 시작 된 Windows 8.1 디바이스에서 사용할 수 있습니다.|  
|[TPM 키 대](https://technet.microsoft.com/library/dn581921.aspx)|암호화 인증서 요청 자가 개인 키도를 신뢰할 수 있는 TPM (플랫폼 모듈) 보호 실제로 발급된 된 인증서에 증명 CAs 수 있습니다.|  
|[자격 증명 보호 및 관리](https://technet.microsoft.com/library/dn408190.aspx)|새 자격 증명 보호 및 도메인 인증 컨트롤 도난 자격 증명을 줄일 수 있습니다.|  
|[파일 FRS (복제 서비스)의 사용 중단](https://technet.microsoft.com/library/dn535775.aspx)|Windows Server 2003 도메인 기능 수준은 기능 수준 FRS SYSVOL 복제 하는 데 사용 하기 때문에 사용 되지 않습니다. 있다는 의미 Windows Server 2012 r 2를 실행 하는 서버에 새 도메인을 만들 때, 도메인 기능 수준이 있어야 Windows Server 2008 또는 최신 합니다. Windows Server 2012 R2 도메인 기능 Windows Server 2003 수준이; 기존 도메인에 실행 하는 도메인 컨트롤러를 추가할 수 있습니다. 방금 수준에서 새 도메인을 만들 수 없습니다.|  
|[새 도메인 및 숲 기능 수준](../active-directory-functional-levels.md)|Windows Server 2012 r 2에 대 한 새로운 기능 수준 가지가 있습니다. Windows Server 2012 r 2 DFL에서 사용할 수 있는 새로운 기능입니다.|  
|[LDAP 쿼리 최적화 프로그램 변경](https://technet.microsoft.com/library/dn535775.aspx)|LDAP 검색 효율성 및 LDAP 검색 쿼리 복잡 한 시간에 성능이 개선 되었습니다.|  
|[1644 이벤트 개선 사항](https://technet.microsoft.com/library/dn535775.aspx)|이벤트 ID 1644 문제 해결을 지원 LDAP 검색 결과 통계 추가 되었습니다.|  
|[Active Directory 복제 처리량 개선](https://technet.microsoft.com/library/dn535775.aspx)|M b 정도 600 p s 40Mbps 로부터 최대 AD 복제 처리량 조정|  
  
## <a name="BKMK_WhatsNewAD"></a>Windows Server 2012에서 광고 DS의 새로운 무엇 인가요?  
다음 표에서 가능한 경우 자세한 정보 링크와 Windows Server 2012에서 광고 DS에 대 한 새로운 기능 요약 되어 있습니다. For a more detailed explanation of some features, including their requirements, see [What's New in Active Directory Domain Services (AD DS)](https://technet.microsoft.com/library/hh831477.aspx).  
  
|기능|설명|  
|-----------|---------------|  
|Active Directory-Based Activation (AD BA) see [Volume Activation Overview](https://technet.microsoft.com/library/hh831612.aspx)|메일 및 볼륨 소프트웨어 라이선스의 관리 구성 간단 하 게 됩니다.|  
|[Active Directory Federation Services ADFS)](https://technet.microsoft.com/library/hh831502.aspx)|역할 설치 추가 보안 설정, 자동 신뢰 관리, SAML 프로토콜 지원 등 서버 관리자 통해 간체 합니다.|  
|플러시 이벤트 active Directory 손실된 페이지|-1119 jet 오류로 NTDS ISAM 이벤트 530 손실된 페이지 플러시 이벤트 Active Directory 데이터베이스를 검색 기록 됩니다.|  
|[Active Directory 휴지통 Bin 사용자 인터페이스](https://technet.microsoft.com/library/hh831702.aspx#ad_recycle_bin_mgmt)|Active Directory 관리 센터 (ADAC) Windows Server 2008 r 2에 도입 원래 휴지통 bin 기능의 GUI 관리를 추가 합니다.|  
|[Active Directory 복제 및 토폴로지 Windows PowerShell cmdlet](https://technet.microsoft.com/library/hh831757.aspx)|만들고 관리할 Active Directory 사이트, 사이트 링크, 연결 개체를 지 원하는 더 많은 Windows PowerShell 사용 하 여 합니다.|  
|[동적 액세스 제어](https://technet.microsoft.com/library/hh831717.aspx)|레거시 액세스 제어 모델 향상 시키는 새로운 승인 클레임 기반 플랫폼입니다.|  
|[정교한 암호 정책 사용자 인터페이스](https://technet.microsoft.com/library/hh831702.aspx#fine_grained_pswd_policy_mgmt)|ADAC 만들, 편집 및 Windows Server 2008에서 추가 원래 Pso 할당 GUI 지원을 추가 합니다.|  
|[그룹 관리 서비스 계정 (gMSA)](https://technet.microsoft.com/library/hh831782.aspx)|새로운 보안 주 형식은 gMSA 이라고 합니다. 여러 호스트에서 실행 되는 서비스 동일한 gMSA 계정에서 실행할 수 있습니다.|  
|[DirectAccess 오프 라인 도메인 가입](https://technet.microsoft.com/library/jj574150.aspx)|오프 라인 도메인 가입 DirectAccess 필수를 포함 하 여 확장 합니다.|  
|[가상 도메인 컨트롤러 (DC) 복제을 통해 신속 하 게 배포](https://technet.microsoft.com/library/hh831734.aspx#virtualized_dc_cloning)|Dc 가상화 기존 가상 도메인 컨트롤러를 사용 하 여 Windows PowerShell cmdlet 복제 하 여 신속 하 게 배포할 수 있습니다.|  
|[풀 변경 내용을 제거합니다](https://technet.microsoft.com/library/jj574229.aspx)|새 모니터링 이벤트 및 할당량 글로벌 RID 풀 과도 하 게 소모 로부터 보호 하기 위해 추가 합니다. 기존 풀 소모 되는 경우 필요에 따라 글로벌 RID 풀의 크기를은.|  
|보안 시간 서비스|네트워크에서 비밀 정보를 제거 m d 5 해시 기능을 제거 하 고 서버 인증 Windows 8 시간 클라이언트 하는 데 필요한 여 W32tm에 대 한 보안을 강화|  
|[Dc 가상화 USN 롤백 보호](https://technet.microsoft.com/library/hh831734.aspx#safe_virt_dc)|실수로 복원 스냅숏을 가상화 dc 더 이상 USN 롤백을 하면 됩니다.|  
|[Windows PowerShell 기록 뷰어](https://technet.microsoft.com/library/hh831702.aspx#windows_powershell_history_viewer)|관리자가 ADAC 사용할 때 실행 되는 Windows PowerShell 명령 볼 수 있도록 합니다.|  
  
### <a name="BKMK_"></a>자동 유지 관리 및 변경 사항을 Windows 업데이트에서 업데이트를 적용 한 후 동작을 다시 시작  
이전에 Windows 8, Windows 업데이트에서 업데이트 확인 다운로드 하 고 설치 하는 자체 내부 일정을 관리 합니다. 이 Windows 업데이트 에이전트는 항상 백그라운드에서 실행, 메모리 및 기타 시스템 리소스 사용 필요 합니다.  
  
Windows 8 and Windows Server 2012 introduce a new feature called [Automatic Maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037(v=vs.85).aspx). 자동 유지 관리 각각 자체 일정을 관리 하는 데 사용 하 고 실행 논리 다양 한 기능을 통합 되어 있습니다. This consolidation allows for all these components to use far less system resources, work consistently, respect the new [Connected Standby](https://msdn.microsoft.com/library/windows/hardware/jj248729.aspx) state for new device types, and consume less battery on portable devices.  
  
Windows 업데이트 자동 유지 관리 Windows 8 및 Windows Server 2012에서의 일부 이기 때문에 날짜와 시간 업데이트를 설치 하도록 설정 하는 데 내부 일정은 더 이상 효과적인. 모든 디바이스 및 사용자 enterprise, Windows 8 및 Windows Server 2012를 실행 하는 등의 컴퓨터에 대해 일관 되 고 예측 가능한 다시 시작 동작 보장 하기 위해 다음 그룹 정책 설정을 구성할 수 있습니다.  
  
-   **컴퓨터 구성 | 정책 | 관리 템플릿 | Windows 구성 요소 | Windows 업데이트 | 자동 업데이트를 구성**  
  
-   **컴퓨터 구성 | 정책 | 관리 템플릿 | Windows 구성 요소 | Windows 업데이트 | 로그인된 한 사용자와 자동 다시 시작**  
  
-   **컴퓨터 구성 | 정책 | 관리 템플릿 | Windows 구성 요소 | 유지 관리 스케줄러 | 임의 지연 유지 관리**  
  
다음 표에서 동작을 원하는 다시 제공 하도록 이러한 설정을 구성 하는 방법 몇 가지 예입니다.  
  
|||  
|-|-|  
|**시나리오**|**권장된 구성**|  
|**WSUS 관리**<br /><br />-매주 한 업데이트를 설치 합니다.<br />-오후 11 금요일 재부팅|자동으로 설치를 원하는 시간까지 자동 다시 부팅을 방지 하는 컴퓨터 설정<br /><br />**정책**: 자동 업데이트 (사용 가능)을 구성 합니다.<br /><br />자동 업데이트를 구성: 4 자동으로 다운로드 및 설치를 예약<br /><br />**정책**: 로그온 사용자 (사용 안 함)와 자동 다시 시작<br /><br />**WSUS 마감**: 오후 11 금요일으로 설정|  
|**WSUS 관리**<br /><br />-전체 서로 다른 시간/일 지그재그 설치|함께 업데이트 해야 하는 다양 한 그룹에 대 한 대상 그룹 설정<br /><br />위의 단계 이전 시나리오에 대 한 사용<br /><br />다른 대상 그룹에 대 한 다른 마감 설정|  
|**지원 되지 마감 관리 되지 않는 WSUS-**<br /><br />-서로 다른 시간에 지그재그 설치|**정책**: 자동 업데이트 (사용 가능)을 구성 합니다.<br /><br />자동 업데이트를 구성: 4 자동으로 다운로드 및 설치를 예약<br /><br />**Registry key:** Enable the registry key discussed in Microsoft KB article [2835627](https://support.microsoft.com/kb/2835627)<br /><br />**정책:** 자동 유지 관리 임의 지연 (사용 가능)<br /><br />설정 **정기적으로 유지 관리 임의 지연** PT6H 임의 지연 6 시간에 대 한 다음 동작을 제공 하려면:<br /><br />업데이트 설치 될 예정 구성 된 유지 관리 시간이 이용 임의 지연에<br /><br />번 다시 시작 각 컴퓨터 열리는 정확 하 게 3 일 후에 대 한<br /><br />각 디바이스 그룹에 대 한 다른 유지 관리 시간이 또는 설정|  
  
Windows 엔지니어링 팀의 구현 이러한 변경 내용은 이유에 대 한 자세한 내용은 참조 하십시오 [최소화 한 후 Windows 업데이트에서에서 자동 업데이트를 다시 시작](http://blogs.msdn.com/b/b8/archive/2011/11/14/minimizing-restarts-after-automatic-updating-in-windows-update.aspx)합니다.  
  
## <a name="BKMK_InstallationChanges"></a>AD DS 서버 역할 설치 변경  
X86는 또는 X64 실행 Windows Server 2008 r 2를 통해 Windows Server 2003, 버전의 Active Directory 설치 마법사, Dcpromo.exe, 및 Dcpromo.exe 실행 하기 전에 Adprep.exe 명령줄 도구 선택적 변형은 미디어에서 또는 설치 자리를 비운 사이에 설치 해야 합니다.  
  
Windows Server 2012에서 시작 명령줄 설치를 Windows PowerShell 모듈 ADDSDeployment을 사용 하 여 수행 합니다. 프로 모션 GUI 기반 사용 하 여 완전히 새로운 광고 DS 구성 마법사 서버 관리자에서 수행 됩니다. 설치 과정을 간소화 하기 위해 ADPREP AD DS 설치에 통합 되었으며 하 고 필요에 따라 자동으로 실행 합니다. 자동으로 Windows PowerShell 기반 광고 DS 구성 마법사 Dc 추가 하는 다음 원격으로 관련 도메인 컨트롤러에 필요한 ADPREP 명령을 실행 되는 도메인의 스키마 및 infrastructure 마스터 역할 대상으로 합니다.  
  
설치를 시작 하기 전에 필수 검사 광고 DS 설치 마법사에서 오류를 식별 합니다. 모든 업그레이드를 완료 부분적으로에서 관심사를 제거 하기 위해 오류 조건이 수정할 수 있습니다. 또한 마법사 그래픽 설치 중에 지정 된 모든 옵션이 포함 된 Windows PowerShell 스크립트를 내보냅니다.  
  
전체적으로, 광고 DS 설치 변경을 DC 역할 설치 과정을 간소화 하 고 전 세계 지역 및 도메인 여러 도메인 컨트롤러를 배포 하는 경우에 특히 관리 오류 가능성 줄일 합니다.  
More detailed information on GUI and Windows PowerShell-based installations, including command line syntax and step-by-step wizard instructions, see [Install Active Directory Domain Services](https://technet.microsoft.com/library/hh472162.aspx). 제어 스키마 변경 사항 기존 숲 속의 Windows Server 2012 Dc 설치 독립적인 Active Directory 숲 속의 소개 하고자 하는 관리자에 대 한 Adprep.exe 명령은 관리자 권한 명령 프롬프트 실행할 수 있습니다.  
  
## <a name="BKMK_DeprecatedFeatures"></a>사용 하지 않는 기능 및 Windows Server 2012에서 광고 DS 관련 동작 변경  
AD DS 관련 된 몇 가지 변경 내용을 가지가 있습니다.  
  
-   **Adprep32.exe의 사용 중단**  
  
    한 버전의 Adprep.exe 이며 이상을 실행 Windows Server 2008 64 비트 서버의 필요에 따라 실행 될 수 있습니다. 원격으로 실행할 수 있으며 32 비트 운영 체제 또는 Windows Server 2003에 대 한 마스터 역할 호스트 작업을 대상으로 지정 하는 경우 원격으로 실행 해야 합니다.  
  
-   **Dcpromo.exe의 사용 중단**  
  
    Windows Server 2012에서만 것도 실행할 수 있지만 응답 파일 또는 조직이 기존 자동화 새로운 Windows PowerShell 설치 옵션을 전환 하는 시간을 주려면 명령줄 매개 Dcpromo 사용 되지 않습니다.  
  
-   **사용자 계정에 LMHash 사용 안 함**  
  
    Windows Server 2008, Windows Server 2008 R2 및 Windows Server 2012에서 템플릿을 사용이 Windows 2000와 Windows Server 2003 도메인 컨트롤러의 보안 템플릿 NoLMHash 정책 보안 기본값 보안을 설정 합니다. Disable the NoLMHash policy for LMHash-dependent clients as required, using the steps in KB article [946405](https://support.microsoft.com/kb/946405).  
  
도메인 컨트롤러부터 Windows Server 2008, Windows 2000 또는 Windows Server 2003을 실행 하는 도메인 컨트롤러에 비해 많음 다음 보안 기본 설정을 한도 있습니다.  
  
|||||  
|-|-|-|-|  
|암호화 형식이 나 정책|Windows Server 2008 기본|기본 Windows Server 2012와 Windows Server 2008 R2|메모|  
|AllowNT4Crypto|사용 안 함|사용 안 함|제 3 자 블록 SMB (서버 메시지) 클라이언트 도메인 컨트롤러에 보안 기본 설정으로 호환 되지 않을 수 있습니다. 모든 경우에 이러한 설정은 상호 운용성, 보안 소모만 수 있도록 완화 될 수 있습니다. For more information, see [article 942564](https://go.microsoft.com/fwlink/?LinkId=164558) in the Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=164558).|  
|DES|사용 하도록 설정|사용 안 함|[Article 977321](https://go.microsoft.com/fwlink/?LinkId=177717) in the Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=177717)|  
|통합된 인증에 대 한 CBT/추가 보호|해당 없음|사용 하도록 설정|See [Microsoft Security Advisory (937811)](https://go.microsoft.com/fwlink/?LinkId=164559) (https://go.microsoft.com/fwlink/?LinkId=164559) and [article 976918](https://go.microsoft.com/fwlink/?LinkId=178251) in the Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=178251).<br /><br />Review and install the hotfix in [article 977073](https://go.microsoft.com/fwlink/?LinkId=186394) (https://go.microsoft.com/fwlink/?LinkId=186394) in the Microsoft Knowledge Base as required.|  
|LMv2|사용 하도록 설정|사용 안 함|[Article 976918](https://go.microsoft.com/fwlink/?LinkId=178251) in the Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=178251)|  
  
## <a name="BKMK_SysReqs"></a>운영 체제 요구 사항  
다음 표에서 Windows Server 2012에 대 한 최소 시스템 요구 사항은 같습니다. For more information about system requirements and pre-installation information, see [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx). 새 Active Directory 숲을 설치 하지 추가 시스템 요구 사항 있지만 도메인 컨트롤러, LDAP 클라이언트 요청 및 사용 Active Directory 응용 프로그램에 대 한 성능을 개선 하기 위해 Active Directory 데이터베이스의 콘텐츠를 캐시에 충분 한 메모리를 추가 해야 합니다. 기존 도메인 컨트롤러 업그레이드 하거나 새 도메인 컨트롤러 기존 숲에 추가 하는 경우 다음 섹션 서버 디스크 공간 요구 사항을 만족을 검토 합니다.  
  
|||  
|-|-|  
|프로세서|1.4 g h z 64 비트 프로세서|  
|RAM|512MB|  
|여유 디스크 공간 요구 사항|32GB|  
|화면 해상도|800 x 600 이상|  
|기타|DVD 드라이브, 키보드, 인터넷 액세스|  
  
### <a name="BKMK_DiskSpaceDCWin8"></a>도메인 컨트롤러 업그레이드 디스크 공간 요구 사항  
이 섹션에서 Windows Server 2008 또는 Windows Server 2008 R2 도메인 컨트롤러 업그레이드에 대해서만 디스크 공간 요구 사항에 설명 합니다. For more information about disk space requirements for upgrading domain controllers to earlier versions of Windows Server, see [Disk space requirements for upgrading to Windows Server 2008](https://technet.microsoft.com/library/cc754463(WS.10).aspx#BKMK_2008) or [Disk space requirements for upgrading to Windows Server 2008 R2](https://technet.microsoft.com/library/cc754463(WS.10).aspx#BKMK_2008R2).  
  
Active Directory 데이터베이스와 로그 파일 및 사용자 지정 응용 프로그램 구동 스키마 확장, 응용 프로그램 및 관리자 시작한 인덱스와 개체와 특성은 사용자에 추가 되며 디렉터리 배포 수명 도메인 컨트롤러 (일반적으로 5-8 년)를 위한 공간을 지원 하기 위해 섬에는 디스크 크기 조정 합니다. 배포 시에 바로 크기 조정 배포 후 디스크 저장소를 확장 하는 데 필요한 큰 터치 비용에 비해 많음 좋은 투자가 일반적으로입니다. For more information, see [Capacity Planning for Active Directory Domain Services](https://social.technet.microsoft.com/wiki/contents/articles/14355.capacity-planning-for-active-directory-domain-services.aspx).  
  
여러분의 계획을 업그레이드 하는 도메인 컨트롤러에서 Active Directory를 (NTDS 데이터베이스는 있는지 확인. DIT) 확보십시오 20% 이상의 여유 디스크 공간이 합니다. 운영 체제를 업그레이드를 시작 하기 전에 파일을 DIT. 볼륨의 디스크 공간이 부족 경우 업그레이드가 실패 하 고 업그레이드 호환성 보고서 반환 디스크 공간이 부족 나타내는 오류 합니다.  
  
이 경우 공간을 다시 캡처하려 Active Directory 데이터베이스 오프 라인는 조각 모음을 시도 하 고 업그레이드 후 다시 수 있습니다. For more information, see [Compact the Directory Database File (Offline Defragmentation)](https://technet.microsoft.com/library/cc794920(v=WS.10).aspx).  
  
### <a name="available-skus"></a>사용 가능한 Sku  
4 버전의 Windows Server는: Foundation, Essentials, 표준 및 Datacenter 합니다.   
AD DS 역할을 지 원하는 버전에서는 두 가지는 표준 및 Datacenter 있습니다.  
  
이전 버전의 Windows Server 버전 서버 역할, 프로세서 개수 및 대용량 메모리 지원 지원에 다릅니다. 두 개의 가상 인스턴스 Standard edition에 사용할 수 표준 및 Datacenter edition Windows Server의 일부 기능 및 기본 하드웨어를 지원 하지만 자녀가 virtualization 권한-에 따라 다양 한 하 고 무제한 가상 인스턴스 Datacenter edition에 대 한 수 있습니다.  
  
### <a name="windows-client-and-windows-server-operating-systems-that-are-supported-to-join-windows-server-domains"></a>Windows 클라이언트와 Windows Server 도메인에 참가할 지원 되는 Windows Server 운영 체제  
다음 Windows는 클라이언트와 Windows Server 운영 체제 이상을 Windows Server 2012를 실행 하는 도메인 컨트롤러 관련 구성원 컴퓨터가 도메인에 대 한 지원는 다음과 같습니다.  
  
-   클라이언트 운영 체제: Windows 8.1, Windows 8, Windows 7, Windows Vista 
  
    Windows 8.1 또는 Windows 8을 실행 하는 컴퓨터가 도메인 컨트롤러 실행된는 이전 버전의 Windows Server, Windows Server 2003 포함 이상 있는 도메인 가입 수도 있습니다. 하지만이 경우, 일부 Windows 8 기능 추가 구성 해야 할 수 있습니다 또는 제공 되지 않을 수 있습니다. For more information about those features and other recommendations for managing Windows 8 clients in downlevel domains, see [Running Windows 8 member computers in Windows Server 2003 domains](https://social.technet.microsoft.com/wiki/contents/articles/17361.running-windows-8-member-computers-in-windows-server-2003-domains.aspx).  
  
-   서버 운영 체제: Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2, Windows Server 2003  
  
## <a name="BKMK_UpgradePaths"></a>지원 되는 업그레이드 경로 위치에서  
Windows Server 2012를 Windows Server 2008 또는 Windows Server 2008 R2 64 비트 버전을 실행 하는 도메인 컨트롤러 업그레이드할 수 있습니다. 32 비트 버전의 Windows Server 2008 또는 Windows Server 2003을 실행 하는 도메인 컨트롤러 업그레이드할 수 없습니다. 대신 하기 도메인에 있는 Windows Server의 최신 버전을 실행 하는 도메인 컨트롤러를 설치 하 고는 Windows Server 2003 도메인 컨트롤러를 제거 합니다.  
  
|이러한 버전을 실행 하는 경우|이러한 버전으로 업그레이드할 수 있습니다.|  
|-------------------------------------|-------------------------------------|  
|Windows Server 2008 표준 s p 2<br /><br />또는<br /><br />Windows Server 2008 Enterprise s p 2|Windows Server 2012 표준<br /><br />또는<br /><br />Windows Server 2012 데이터 센터|  
|Windows Server 2008 Datacenter s p 2|Windows Server 2012 데이터 센터|  
|Windows는 Server 2008 웹|Windows Server 2012 표준|  
|S p 1과 Windows Server 2008 R2 표준<br /><br />또는<br /><br />S p 1과 Windows Server 2008 R2 Enterprise|Windows Server 2012 표준<br /><br />또는<br /><br />Windows Server 2012 데이터 센터|  
|S p 1과 Windows Server 2008 R2 Datacenter|Windows Server 2012 데이터 센터|  
|Windows는 Server 2008 R2 웹|Windows Server 2012 표준|  
  
For more information about supported upgrade paths, see [Evaluation Versions and Upgrade Options for Windows Server 2012](https://go.microsoft.com/fwlink/?LinkId=260917). Note 일반 정품 버전에 직접 평가 버전의 Windows Server 2012를 실행 하는 도메인 컨트롤러를 변환할 수 없습니다. 대신, 일반 정품 버전을 실행 하는 서버에 추가 도메인 컨트롤러를 설치 하 고 평가 버전에서 실행 되는 도메인 컨트롤러에서 광고 DS 제거 합니다.  
  
알려진된 문제 때문에 Windows Server 2012를 설치 하는 서버 Core Windows Server 2008 r 2를 설치 하는 서버 Core를 실행 하는 도메인 컨트롤러를 업그레이드할 수 없습니다. 업그레이드는 업그레이드 프로세스에 늦게 단색 검은 화면이 중단 됩니다. 이러한 Dc 재부팅 하면 이전 운영 체제 버전으로 롤백할 boot.ini에서 옵션을 제공 합니다. 재부팅 자동 롤백이 이전 운영 체제 버전을 시작 합니다. 해결 방법이 있으면 될 때까지 제자리에 Windows Server 2008 r 2를 설치 하는 서버 Core 자동으로 실행 하는 기존 도메인 컨트롤러 업그레이드 대신 Windows Server 2012 서버 Core 설치를 실행 중인 새 도메인 컨트롤러를 설치 하는 것이 좋습니다. For more information, see KB article [2734222](https://support.microsoft.com/kb/2734222).  
  
## <a name="BKMK_FunctionalLevels"></a>수준 기능 및 요구 사항  
 Windows Server 2012를 Windows Server 2003 숲 기능 수준이 필요합니다. 즉, 기존 Active Directory 숲을 Windows Server 2012를 실행 하는 도메인 컨트롤러를 추가 하기 전에 숲 기능 수준 Windows Server 2003 이상 이어야 합니다. 이 즉, Windows Server 2008 R2, Windows Server 2008 또는 Windows Server 2003을 실행 하는 도메인 컨트롤러 동일한 숲 속의 작동 하지만 Windows 2000 Server 실행 하는 도메인 컨트롤러 되지 않은 지원 및 Windows Server 2012를 실행 하는 도메인 컨트롤러의 설치를 차단 합니다. 숲 Windows Server 2003을 실행 하는 도메인 컨트롤러에 포함 된 경우 이상 기능 숲 있지만 수준은 Windows 2000 여전히, 설치도 차단 합니다.  
  
Windows Server 2012 도메인 컨트롤러에 숲에 추가 하기 전에 Windows 2000 도메인 컨트롤러를 제거 해야 합니다. 이 경우 다음 워크플로 고려 합니다.  
  
1.  Windows Server 2003 이상을 실행 하는 도메인 컨트롤러를 설치 합니다. 이러한 도메인 컨트롤러의 Windows Server 평가판에 배포할 수 있습니다. This step also requires [running adprep.exe](https://technet.microsoft.com/library/dd464018(WS.10).aspx) for that operating system release as a prerequisite.  
  
2.  Windows 2000 도메인 컨트롤러를 제거 합니다. 특히, 정상적으로 내리기 또는 강제로 Windows 2000 Server 도메인 컨트롤러 도메인 하 고 사용 하는 Active Directory 사용자와 모든 제거 도메인 컨트롤러 도메인 컨트롤러 계정을 제거 하려면 컴퓨터에서 제거 합니다.  
  
3.  Windows Server 2003 이상 숲 기능 수준을 발생 합니다.  
  
4.  Windows Server 2012를 실행 하는 도메인 컨트롤러를 설치 합니다.  
  
5.  이전 버전의 Windows Server를 실행 하는 도메인 컨트롤러를 제거 합니다.  
  
새로운 Windows Server 2012 도메인 기능 수준 통해 새로운 기능이 하나:는 **KDC 클레임, 복합 인증 및 Kerberos armoring에 대 한 지원** KDC 관리 템플릿 정책에는 두 가지 설정이 (**클레임을 항상 제공** 및 **무방비 인증 요청이 실패**) Windows Server 2012 도메인 기능 수준 해야 하는 합니다.  
  
Windows Server 2012 숲 기능 수준 새로운 기능을 제공 하지는 않지만 보장 숲에서 만든 새 도메인 Windows Server 2012 도메인 기능 수준에서 자동으로 작동 합니다. Windows Server 2012 도메인 기능 수준 클레임, 복합 인증 및 Kerberos armoring에 대 한 다른 새로운 기능 KDC 지원 이상 제공 하지 않습니다. 하지만 도메인에 있는 도메인 컨트롤러 Windows Server 2012를 실행 하면 됩니다. 다른 기능 수준에서 사용할 수 있는 다른 기능에 대 한 자세한 내용은 참조 [이해 Active Directory 도메인 서비스 (AD DS) 기능 수준](../active-directory-functional-levels.md)합니다.  
  
숲 기능 수준 특정 값을 설정한 후 롤백할 수 없거나 구성원과 숲 기능 수준 낮추기: Windows Server 2012 숲 기능 수준 올린, 다음 Windows Server 2008 r 2를 줄일 수 있습니다. Active Directory 휴지통을 설정 하지 않은 경우에 Windows Server 2008 R2 또는 Windows Server 2008 R2 또는 Windows Server 2008 Windows Server 2012에서 기능 수준 다시 Windows Server 2008 숲을 줄일 수 있습니다. 숲 기능 수준 Windows Server 2008 r 2를 설정 된 경우 것 수 없는 롤백할 예를 들어, Windows Server 2003 합니다.  
  
도메인 기능 수준 특정 값을 설정한 후 롤백할 수 없거나는 다음과 같은 차이점이 도메인 기능 수준 낮추기: Windows Server 2008 R2 또는 Windows Server 2012 도메인 기능 수준을 발생 하 고 있는 Windows Server 2008 또는 아래 숲 기능 수준을 경우 Windows Server 2008 또는 Windows Server 2008 R2 도메인 기능 수준을 배포 하는 옵션이 백업 합니다. Windows Server 2008를 Windows Server 2008 R2 또는 Windows Server 2012를 Windows Server 2008 R2 또는 Windows Server 2008 에서만 도메인 기능 수준의 줄일 수 있습니다. 도메인 기능 수준 Windows Server 2008 r 2를 설정 된 경우 것 수 없는 롤백할 예를 들어, Windows Server 2003 합니다.  
  
기능 하위 수준에서 사용할 수 있는 기능에 대 한 자세한 내용은 참조 [이해 Active Directory 도메인 서비스 (AD DS) 기능 수준](../active-directory-functional-levels.md)합니다.  
  
기능 수준 이외 Windows Server 2012를 실행 하는 도메인 컨트롤러에서 이전 버전의 Windows Server를 실행 하는 도메인 컨트롤러에서 사용할 수 있는 추가 기능을 제공 합니다. 예를 들어, Windows Server 2012를 실행 하는 도메인 컨트롤러 이전 버전의 Windows Server를 실행 하는 도메인 컨트롤러 수 있지만 가상 도메인 컨트롤러 복제할 사용할 수 있습니다. 하지만 가상 도메인 컨트롤러 복제와 Windows Server 2012에서 가상 도메인 컨트롤러 되는지 궁금할 없는 수준 요구 사항이 제대로 작동 합니다.  
  
> [!NOTE]  
> Microsoft Exchange Server 2013 숲 기능 수준 Windows server 2003 이상이 필요합니다.  
  
## <a name="BKMK_ServerRoles"></a>광고 DS 상호 운용성 다른 서버 역할와 Windows 운영 체제  
AD DS 다음 Windows 운영 체제에 사용할 수 없습니다.  
  
-   Windows 다중 서버  
  
-   Windows Server 2012 필수 패키지  
  
AD DS 또한 다음과 같은 서버 역할 나 역할 서비스를 실행 하는 서버에 설치할 수 없습니다.  
  
-   Hyper-v 서버  
  
-   원격 데스크톱 연결 중개 업체  
  
## <a name="BKMK_OpsMasters"></a>마스터 역할 작업  
Windows Server 2012에서 새로운 기능 몇 가지 작업 마스터 역할을 영향을 줍니다.  
  
-   PDC 에뮬레이터 가상 도메인 컨트롤러 복제 지원 하기 위해 Windows Server 2012를 실행 중 이어야 합니다. 추가 필수 Dc 복제할 가지가 있습니다. For more information, see [Active Directory Domain Services (AD DS) Virtualization](https://technet.microsoft.com/library/hh831734.aspx).  
  
-   새로운 보안 사용자 PDC 에뮬레이터 Windows Server 2012를 실행 될 때 생성 됩니다.  
  
-   지우려는 마스터 새로운 RID 발급 및 모니터링 기능에 있습니다. --비상시에 전체 RID 높일 수는 1 비트 할당 풀 및 개선 사항 포함 더 나은 이벤트 로깅 더 적합 한 제한 됩니다. 자세한 내용은 참조 [제거 발급 관리](../../ad-ds/manage/Managing-RID-Issuance.md)합니다.  
  
> [!NOTE]  
> 수 없지만 작업 마스터 역할을 다른 AD DS 설치에 변화가 DNS 서버 역할을 드 Windows Server 2012를 실행 하는 모든 도메인 컨트롤러에 기본적으로 설치 됩니다.  
  
## <a name="BKMK_Virtual"></a>도메인 컨트롤러 가상화  
AD DS 시작 하는 Windows Server 2012에서의 개선 도메인 컨트롤러의 안전 하 게 virtualization 및 도메인 컨트롤러 복제 하는 기능을 사용 합니다. 결과적 도메인 컨트롤러 복제 새 도메인 및 기타 혜택 추가 도메인 컨트롤러의 신속한 배포를 수 있습니다. 자세한 내용은 참조 [Active Directory 도메인 서비스 & #40; 소개 AD DS & #41; Virtualization & #40; 수준을 100 & #41; ](../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md).  
  
## <a name="BKMK_Admin"></a>Windows Server 2012 서버 관리  
Use the [Remote Server Administration Tools for Windows 8](https://www.microsoft.com/download/details.aspx?id=28972) to manage domain controllers and other servers that run  Windows Server 2012 . Windows 8을 실행 하는 컴퓨터에서 Windows Server 2012 원격 서버 관리 도구를 실행할 수 있습니다.  
  
## <a name="BKMK_AppCompat"></a>응용 프로그램 호환성  
다음 표에서 일반적인 Active Directory 통합 Microsoft 응용 프로그램에 설명 합니다. 표 어떤 버전의 응용 프로그램에 설치할 수 있는 Windows Server 및 Windows Server 2012 Dc 도입 응용 프로그램 호환성에 영향을 미칩니다 있는지 여부에 대해 설명 합니다.  
  
|제품|노트|  
|-----------|---------|  
|[Microsoft Configuration Manager 2007](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|S p 2 (Configuration Manager 2007 r 2와 Configuration Manager 2007 r 3 포함) configuration Manager 2007:<br /><br />Windows 8 Pro<br />Windows 8 Enterprise<br />Windows Server 2012 표준<br />-Windows Server 2012 Datacenter **참고:** 계획이 Configuration Manager 2007 운영 체제 배포 기능을 사용 하 여 배포이 운영 체제에 대 한 지원을 추가 하는 이러한는 클라이언트와 완벽 하 게 지원는, 있지만 합니다. 또한 없음 사이트 서버 또는 사이트 시스템 모든 SKU의 Windows Server 2012에서 지원 됩니다.|  
|[Microsoft SharePoint 2007](https://support.microsoft.com/kb/2728964)|Microsoft Office SharePoint Server 2007은 Windows Server 2012에 설치할 경우 지원 되지 않습니다.|  
|[Microsoft SharePoint 2010](https://support.microsoft.com/kb/2724471)|설치 및 운영 필요한 SharePoint 2010 서비스 팩 2 <br />Windows Server 2012 서버에 SharePoint 2010<br /><br />SharePoint 2010 Foundation 서비스 팩 2는 설치 하 고 Windows Server 2012 서버에 SharePoint 2010 Foundation 작동 하는 데 필요한는<br /><br />SharePoint Server 2010 서비스 팩을) (없음 설치 과정에서 Windows Server 2012에 실패<br /><br />SharePoint Server 2010 필수 installer (PrerequisiteInstaller.exe) 오류와 함께 실패 "이이 프로그램에 호환성 문제가 있습니다." "모으기 SharePoint 설치할 수 있으면 & #124; 오류를 표시"도움말 없이 프로그램 실행"클릭 SharePoint Server 2010 서비스 팩) (이 없는 Windows Server 2012.에 설치할 수 없습니다 "|  
|[Microsoft SharePoint 2013](https://technet.microsoft.com/library/cc262485(v=office.15).aspx)|데이터베이스 서버 농장의 위한 최소 요구 사항<br /><br />64 비트 버전의 Windows Server 2008 R2 서비스 팩 1 (SP1) 표준, Enterprise 또는 Datacenter 또는 64 비트 버전의 Windows Server 2012 표준 또는 데이터 센터<br /><br />기본 제공 데이터베이스와 단일 서버 위한 최소 요구 사항을 다음과 같습니다.<br /><br />64 비트 버전의 Windows Server 2008 R2 서비스 팩 1 (SP1) 표준, Enterprise 또는 Datacenter 또는 64 비트 버전의 Windows Server 2012 표준 또는 데이터 센터<br /><br />프런트 웹 서버 및 응용 프로그램 서버 농장을 위한 최소 요구 사항을:<br /><br />64 비트 버전의 Windows Server 2008 R2 서비스 팩 1 (SP1) 표준, Enterprise 또는 Datacenter 또는 64 비트 버전의 Windows Server 2012 표준 또는 Datacenter 합니다.|  
|[Microsoft System Center Configuration Manager 2012](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|System Center 2012 Configuration Manager 서비스 팩 1:<br /><br />Microsoft는 서비스 팩 1 발표와 함께 우리 클라이언트 지원 매트릭스에는 다음 운영 체제를 추가 합니다.<br /><br />Windows 8 Pro<br />Windows 8 Enterprise<br />Windows Server 2012 표준<br />Windows Server 2012 데이터 센터<br /><br />모든 사이트 역할-사이트 서버, SMS 공급자 관리 포인트 등-와 다음 운영 체제 버전 서버에 배포할 수 있습니다.<br /><br />Windows Server 2012 표준<br />Windows Server 2012 데이터 센터|  
|[Microsoft Lync Server 2013](https://technet.microsoft.com/library/gg412883.aspx)|Windows Server 2008 R2 또는 Windows Server 2012와 Lync Server 2013 필요합니다. 서버 Core 설치에서 실행할 수 없습니다. It can be run on [virtual servers](https://technet.microsoft.com/library/gg399035.aspx).|  
|[Lync Server 2010](https://support.microsoft.com/kb/2777359)|Lync Server 2010 can be installed on a new (not upgraded) installation Windows Server 2012 if [October 2012 cumulative updates for Lync Server](https://support.microsoft.com/?kbid=2493736) are installed. Windows Server 2012 운영 체제의 Lync Server 2010 기존 설치에 대 한 업그레이드 지원 되지 않습니다. Microsoft Lync Server 2010 Group 채팅 서버도 Windows Server 2012에서 지원 되지 않습니다.|  
|[System Center 2012 Endpoint Protection](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|시스템 Center 2012 Endpoint 보호 서비스 팩 1 다음 운영 체제를 포함 하도록 클라이언트 지원 매트릭스 업데이트할 예정<br /><br />Windows 8 Pro<br />Windows 8 Enterprise<br />Windows Server 2012 표준<br />Windows Server 2012 데이터 센터|  
|[System Center 2012 Forefront Endpoint Protection](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|업데이트 롤업 1 FEP 2010 클라이언트 지원 매트릭스 다음 운영 체제를 포함 하도록 업데이트 됩니다.<br /><br />Windows 8 Pro<br />Windows 8 Enterprise<br />Windows Server 2012 표준<br />Windows Server 2012 데이터 센터|  
|Forefront 위협 관리 게이트웨이 (TMG)|Windows Server 2008 및 Windows Server 2008 r 2에만 실행 TMG 지원 됩니다. For more information, see [System requirements for Forefront TMG](https://technet.microsoft.com/library/dd896981.aspx).|  
|Windows Server Update Services|WSUS이이 릴리스에 이미 클라이언트로 컴퓨터 Windows 8 또는 Windows Server 2012에서 발급 컴퓨터를 지원합니다.|  
|Windows Server Update Services 3.0|Update KB article [2734608](https://support.microsoft.com/kb/2734608) lets servers that are running Windows Server Update Services (WSUS) 3.0 SP2 provide updates to computers that are running Windows 8 or Windows Server 2012: **Note:** Customers with standalone WSUS 3.0 SP2 environments or System Center Configuration Manager 2007 Service Pack 2 environments with WSUS 3.0 SP2 require [2734608](https://support.microsoft.com/kb/2734608) to properly manage Windows 8-based computers or Windows Server 2012-based computers as clients.|  
|[Exchange 2013](https://technet.microsoft.com/library/bb691354.aspx)|Windows Server 2012 표준 및 Datacenter는 다음과 같은 역할에 대 한 지원: 스키마 마스터, 드 서버, 도메인 컨트롤러, 액세스 서버 역할 사서함 및 클라이언트<br /><br />숲 기능 수준: Windows Server 2003 이상<br /><br />소스: Exchange 2013 시스템 요구 사항|  
|Exchange 2010|[소스: Exchange 2010 서비스 팩 3](https://blogs.technet.com/b/exchange/archive/2012/09/25/announcing-exchange-2010-service-pack-3.aspx)<br /><br />Exchange 2010 서비스 팩 3 구성원 서버 Windows Server 2012에 설치할 수 있습니다.<br /><br />[Exchange 2010 System Requirements](https://technet.microsoft.com/library/aa996719(EXCHG.141).aspx) lists the latest supported schema master, global catalog and domain controller as Windows Server 2008 R2.<br /><br />숲 기능 수준: Windows Server 2003 이상|  
|SQL Server 2012|Source: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Windows Server 2012에서 SQL Server 2012 RTM 지원 됩니다.|  
|SQL Server 2008 R2|Source: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Windows Server 2012를 설치 하려면 SQL Server 2008 R2 서비스 팩 1 이상이 필요 합니다.|  
|SQL Server 2008|Source: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Windows Server 2012를 설치 하려면 SQL Server 2008 서비스 팩 3 이상이 필요 합니다.|  
|2005 SQL Server|Source: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Windows Server 2012에 설치할 수 없습니다.|  
  
## <a name="BKMK_KnownIssues"></a>알려진된 문제  
다음 표에서 광고 DS 설치와 관련 된 알려진된 문제입니다.  
  
||||  
|-|-|-|  
|KB 문서 번호 및 타이틀|영향을 기술 영역|문제가/설명|  
|[2830145](https://support.microsoft.com/kb/2830145): SID S-1-18-1 and SID S-1-18-2 can't be mapped on Windows 7 or Windows Server 2008 R2-based computers in a domain environment|광고 DS 관리/응용 프로그램 호환성|Windows Server 2012에서 접하는 1 18 1 SID S와 SID S-1 18 2, 매핑하는 응용 프로그램 Sid Windows 7 또는 Windows Server 2008 R2 기반 컴퓨터에서 확인할 수 없는 때문에 실패할 수 있습니다. 이 문제를 해결 하려면 Windows 7 및 Windows Server 2008 R2 기반 컴퓨터가 도메인에 핫픽스를 설치 합니다.|  
|[2737129](https://support.microsoft.com/kb/2737129): Group Policy preparation is not performed when you automatically prepare an existing domain for Windows Server 2012|광고 DS 설치|도메인에서 Windows Server 2012를 실행 하는 첫 번째 DC 설치의 일부로 Adprep 하십시오 자동으로 실행 되지 않습니다. 실행 하는 경우 것은 이전에 도메인의를 수동으로 실행할 해야 합니다.|  
|[2737416](https://support.microsoft.com/kb/2737416): Windows PowerShell-based domain controller deployment repeats warnings|광고 DS 설치|경고 필수 유효성 검사 과정에 표시 하 고 설치 하는 동안 다음 다시 나타날 수 있습니다.|  
|[2737424](https://support.microsoft.com/kb/2737424): "Format of the specified domain name is invalid" error when you try to remove Active Directory Domain Services from a domain controller|광고 DS 설치|이 오류는 미리 작성된 된 RODC 계정 여전히 존재 도메인에 있는 마지막 DC 제거 하는 경우 표시 됩니다. Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008 적용 됩니다.|  
|[2737463](https://support.microsoft.com/kb/2737463): Domain controller does not start, c00002e2 error occurs, or "Choose an option" is displayed|광고 DS 설치|DC 위해 도메인 컨트롤러 역할을 제거 하려면 관리자 사용 Dism.exe, Pkgmgr.exe, 또는 Ocsetup.exe 때문에 시작 되지 않습니다.|  
|[2737516](https://support.microsoft.com/kb/2737516): IFM verification limitations in Windows Server 2012 Server Manager|광고 DS 설치|KB 문서에서 설명한 대로 IFM 인증 제한 사항이 있을 수 있습니다.|  
|[2737535](https://support.microsoft.com/kb/2737535): Install-AddsDomainController cmdlet returns parameter set error for RODC|광고 DS 설치|이미 채워집니다 인수 RODC 미리 작성된 된 계정에 지정 서버 RODC 계정에 연결 하려고 할 때 오류를 받을 수 있습니다.|  
|[2737560](https://support.microsoft.com/kb/2737560): "Unable to perform Exchange schema conflict check" error, and prerequisites check fails|광고 DS 설치|필수 검사가 실패 Dc 누락 된는 SeServiceLogonRight 네트워크 서비스에 대 한 때문에 기존 도메인의 첫 번째 Windows Server 2012 DC 구성 또는 WMI 또는 DCOM 프로토콜 차단 되어 있습니다.|  
|[2737797](https://support.microsoft.com/kb/2737797): AddsDeployment module with the -Whatif argument shows incorrect DNS results|광고 DS 설치|-WhatIf 매개 변수 나타나지만 DNS 서버가 설치 되어 있지 것입니다 됩니다.|  
|[2737807](https://support.microsoft.com/kb/2737807): The Next button is not available on the Domain Controller Options page|광고 DS 설치|DC 대상의 IP 주소 기존 서브넷 또는 사이트에 매핑되며 하지 않는 있거나 DSRM 암호 입력 및 확인 제대로 되지 않는 때문 다음 단추는 도메인 컨트롤러 옵션 페이지에서 사용할 수 없습니다.|  
|[2737935](https://support.microsoft.com/kb/2737935): Active Directory installation stalls at the "Creating the NTDS settings object" stage|광고 DS 설치|설치 로컬 관리자 암호 일치 도메인 관리자 암호를 있거나 방지를 완료 중요 한 복제 네트워킹 문제 때문에 중단 됩니다.|  
|[2738060](https://support.microsoft.com/kb/2738060): "Access is denied" error message when you create a child domain remotely by using Install-AddsDomain|광고 DS 설치|잘못 된 암호는 DNSDelegationCredential 있으면 설치 ADDSDomain 호출 명령 cmdlet 함께 실행 하면 오류가 나타납니다.|  
|[2738697](https://support.microsoft.com/kb/2738697): "The server is not operational" domain controller configuration error when you configure a server by using Server Manager|광고 DS 설치|NTLM 인증을 사용 하지 않으므로 AD DS 작업 그룹 컴퓨터에 설치 하려는 경우이 오류가 발생 합니다.|  
|[2738746](https://support.microsoft.com/kb/2738746): You receive access denied errors after you log on to a local administrator domain account|광고 DS 설치|기본 제공 된 관리자 계정 보다는 로컬 관리자 계정을 사용 하 여 로그온 하 고 다음 새 도메인을 만들 때 계정은 도메인 관리자 그룹에 추가 되지 않습니다.|  
|[2743345](https://support.microsoft.com/kb/2743345): "The system cannot find the file specified" Adprep /gpprep error, or tool crashes|광고 DS 설치|이 오류가 발생 인프라 마스터 구현 하는 adprep /gpprep을 실행할 때 분리형 네임|  
|[2743367](https://support.microsoft.com/kb/2743367): Adprep "not a valid Win32 application" error on Windows Server 2003, 64-bit version|광고 DS 설치|Windows Server 2012 Adprep Windows Server 2003에서 실행할 수 없는 때문에이 오류가 발생 합니다.|  
|[2753560](https://support.microsoft.com/kb/2753560): ADMT 3.2 and PES 3.1 installation errors on Windows Server 2012|ADMT|ADMT 3.2 디자인 Windows Server 2012에 설치할 수 없습니다.|  
|[2750857](https://support.microsoft.com/kb/2750857): DFS Replication diagnostic reports do not display correctly in Internet Explorer 10|DFS 복제|진단 보고서 DFS 복제 Internet Explorer 10의 변경 내용으로 인해 올바르게 표시 되지 않습니다.|  
|[2741537](https://support.microsoft.com/kb/2741537): Remote Group Policy updates are visible to users|그룹 정책|예약 된 작업이 실행 로그온 한 각 사용자 때문입니다. Windows 작업 스케줄러 디자인이 시나리오에서 대화형 프롬프트가 필요합니다.|  
|[2741591](https://support.microsoft.com/kb/2741591): ADM files are not present in SYSVOL in the GPMC Infrastructure Status option|그룹 정책|GPMC 인프라 상태는 사용자 지정된 필터링 규칙 따르지 때문에 GP 복제 "복제 진행 중 에서" 보고할 수 있습니다.|  
|[2737880](https://support.microsoft.com/kb/2737880): "The service cannot be started" error during AD DS configuration|가상 DC 복제|DS 역할 서버 서비스를 사용 하지 않도록 설정 하는 동안 설치 또는 제거 AD DS 하거나 복제,이 오류가 발생 합니다.|  
|[2742836](https://support.microsoft.com/kb/2742836): Two DHCP leases are created for each domain controller when you use the VDC cloning feature|가상 DC 복제|이 복제 도메인 컨트롤러 임대 복제와 다시 복제가 완료 되 면 전에 받은 하기 때문에 발생 합니다.|  
|[2742844](https://support.microsoft.com/kb/2742844): Domain controller cloning fails and the server restarts in DSRM in Windows Server 2012|가상 DC 복제|KB 문서에 나열 된 이유는 여러 가지 중 하나로 실패 복제 복제 DC DSRM를 시작 합니다.|  
|[2742874](https://support.microsoft.com/kb/2742874): Domain controller cloning does not re-create all service principal names|가상 DC 복제|일부 3 부 Spn 도메인 이름 바꾸기 프로세스에 대 한 제한으로 인해 복제 DC에 다시 하지 않습니다.|  
|[2742908](https://support.microsoft.com/kb/2742908): "No logon servers are available" error after cloning domain controller|가상 DC 복제|실패 복제 하기 때문에 가상화 DC 복제 DC DSRM에서 시작 후에 로그온 할 때이 오류가 발생 합니다. 로 로그온 합니다. 복제 문제를 해결 하는 \administrator 합니다.|  
|[2742916](https://support.microsoft.com/kb/2742916): Domain controller cloning fails with error 8610 in dcpromo.log|가상 DC 복제|PDC 에뮬레이터 인바인드 복제가 도메인 파티션 역할 전송 된 것을 수행 하지 하기 때문에 실패 복제 합니다.|  
|[2742927](https://support.microsoft.com/kb/2742927): "Index was out of range" New-AdDcCloneConfig error|가상 DC 복제|새로 만들기 ADDCCloneConfigFile cmdlet cmdlet 관리자 명령 프롬프트에서 실행 되지 않았습니다 하거나 액세스 토큰 관리자가 그룹 포함 되어 있지 않으므로 가상 Dc 복제 하는 동안 실행 한 후 오류가 나타납니다.|  
|[2742959](https://support.microsoft.com/kb/2742959): Domain controller cloning fails with error 8437: "invalid parameter was specified for this replication operation"|가상 DC 복제|잘못 된 복제 이름이 나 중복 NetBIOS 이름이 지정 되었습니다 복제 실패 했습니다.|  
|[2742970](https://support.microsoft.com/kb/2742970): DC Cloning fails with no DSRM, duplicate source and clone computer|가상 DC 복제|복제 가상 DC 부팅에서 디렉터리 복구 모드 (DSRM 서비스)를 DCCloneConfig.xml 파일은 제자리에 만들어졌습니다 있거나 복제 전에 원본 DC 다시 부팅 된 때문 DC 원본으로 중복 이름이 사용 하 여 됩니다.|  
|[2743278](https://support.microsoft.com/kb/2743278): Domain controller cloning error 0x80041005|가상 DC 복제|복제 DC 하나만 WINS 서버 지정 했기 때문에 DSRM에 부팅 됩니다. 모든 WINS 서버 경우 기본 설정 및 암호 확인용 WINS 서버 지정 해야 합니다.|  
|[2745013](https://support.microsoft.com/kb/2745013): "Server is not operational" error message if you run New-AdDcCloneConfigFile in Windows Server 2012|가상 DC 복제|서버 드 서버에 연결할 수 없는 때문에 새 ADDCCloneConfigFile cmdlet 실행 한 후이 오류가 발생 합니다.|  
|[2747974](https://support.microsoft.com/kb/2747974): Domain controller cloning event 2224 provides incorrect guidance|가상 DC 복제|이벤트 ID 2224 올바르게 따르면 하지 복제 전에 관리 서비스 계정을 제거 해야 합니다. 독립 실행형 Msa를 제거 해야 하지만 그룹 Msa 복제 차단 하지 않습니다.|  
|[2748266](https://support.microsoft.com/kb/2748266): You cannot unlock a BitLocker-encrypted drive after you upgrade to Windows 8|BitLocker|Windows 7에서 업그레이드 된 컴퓨터에서 드라이브를 잠금 해제 하려고 할 때 "응용 프로그램을 찾을 수 없습니다" 오류가 발생 합니다.|  
  
## <a name="see-also"></a>참조 하십시오  
[Windows Server 2012 평가 리소스](https://technet.microsoft.com/evalcenter/hh708766.aspx)  
[Windows Server 2012 평가 가이드](https://download.microsoft.com/download/5/B/2/5B254183-FA53-4317-B577-7561058CEF42/WS%202012%20Evaluation%20Guide.pdf)  
[설치 및 Windows Server 2012를 배포 합니다.](https://technet.microsoft.com/library/hh831620.aspx)  
  


