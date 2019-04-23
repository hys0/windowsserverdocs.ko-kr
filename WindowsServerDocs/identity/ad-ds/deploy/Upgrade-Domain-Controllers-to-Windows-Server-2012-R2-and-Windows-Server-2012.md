---
ms.assetid: e4c31187-f15f-410b-bb79-8d63e2f2b421
title: Windows Server 2012 R2 및 Windows Server 2012로 도메인 컨트롤러 업그레이드
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e3b44dbc1c869680db91f5e9732a50504d80e7b8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877504"
---
# <a name="upgrade-domain-controllers-to-windows-server-2012-r2-and-windows-server-2012"></a>Windows Server 2012 R2 및 Windows Server 2012로 도메인 컨트롤러 업그레이드

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 Windows Server 2012 R2 및 Windows Server 2012에서 Active Directory Domain Services에 대 한 배경 정보를 제공 하 고 Windows Server 2008 또는 Windows Server 2008 R2에서 도메인 컨트롤러를 업그레이드 하기 위한 과정을 설명 합니다.  
  
## <a name="BKMK_UpgradeWorkflow"></a>도메인 컨트롤러 업그레이드 단계  
도메인을 업그레이드하기 위해 권장되는 방법은 최신 Windows Server 버전을 실행하는 도메인 컨트롤러의 수준을 올리고 필요에 따라 이전 도메인 컨트롤러의 수준을 내리는 것입니다. 기존 도메인 컨트롤러의 운영 체제를 업그레이드할 때 이 방법이 선호됩니다. 이 목록에서는 최신 버전의 Windows Server를 실행 하는 도메인 컨트롤러의 수준을 올리기 전에 수행 하려면 일반 단계를 다룹니다.  
  
1. 대상 서버가 [시스템 요구 사항](https://technet.microsoft.com/library/dn303418.aspx)을 충족하는지 확인합니다.  
2. [Application compatibility](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_AppCompat)을 확인합니다.  
3. 보안 설정을 확인합니다. 자세한 내용은 [Windows Server 2012의 AD DS에 관련 된 사용 되지 않는 기능 및 동작 변경 내용](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_DeprecatedFeatures) 및 [Windows Server 2008 및 Windows Server 2008 R2의 기본 설정 보안](https://technet.microsoft.com/library/upgrade-domain-controllers-to-windows-server-2008-r2(WS.10).aspx#BKMK_SecureDefault).  
4. 설치하려고 계획 중인 컴퓨터에서 대상 서버로 연결된 상태를 확인합니다.  
5. 필요한 작업 마스터 역할의 가용성을 확인합니다.  

   - 설치를 실행 하는 컴퓨터에서 기존 도메인 및 포리스트를 Windows Server 2012를 실행 하는 첫 번째 DC를 설치 하려면 adprep을 실행 하려면 인프라 마스터와 adprep /forestprep을 실행 하려면 스키마 마스터에 대 한 연결을 해야 / domainprep 합니다.  
   - 포리스트 스키마가 이미 확장된 도메인에 첫 번째 DC를 설치하려면 인프라 마스터에만 연결하면 됩니다.  
   - 기존 포리스트에서 도메인을 설치 또는 제거하려면 도메인 명명 마스터에 연결해야 합니다.  
   - 모든 도메인 컨트롤러를 설치할 경우 RID 마스터에도 연결해야 합니다.  
   - 기존 포리스트에 첫 번째 읽기 전용 도메인 컨트롤러를 설치할 경우에는 비도메인 명명 컨텍스트 또는 NDNC라고도 하는 각 응용 프로그램 디렉터리 파티션용 인프라 마스터에 연결해야 합니다.  

6. AD DS를 설치하는 데 필요한 자격 증명을 입력해야 합니다.  

   |설치 작업|자격 증명 요구 사항|  
   |-----------------------|---------------------------|  
   |새 포리스트 설치|대상 서버의 로컬 관리자|  
   |기존 포리스트에 새 도메인 설치|Enterprise Admins|  
   |기존 도메인에 추가 DC 설치|Domain Admins|  
   |adprep /forestprep 실행|Schema Admins, Enterprise Admins 및 Domain Admins|  
   |adprep /domainprep 실행|Domain Admins|  
   |adprep /domainprep /gpprep 실행|Domain Admins|  
   |adprep /rodcprep 실행|Enterprise Admins|  

   AD DS 설치 권한을 위임할 수 있습니다. 자세한 내용은 [설치 관리 작업](https://technet.microsoft.com/library/cc773327(WS.10).aspx)을 참조하세요.  

Windows PowerShell cmdlet와 서버 관리자를 사용하여 신규/복제 Windows Server 2012 도메인 컨트롤러를 승격하기 위한 단계별 지침은 다음 링크에서 확인할 수 있습니다.  

- [Active Directory Domain Services (수준 100)를 설치 합니다.](https://technet.microsoft.com/library/hh472162.aspx)  
- [새 Windows Server 2012 Active Directory 포리스트 (수준 200)를 설치 합니다.](https://technet.microsoft.com/library/jj574166.aspx)  
- [기존 도메인 (수준 200)에 복제 Windows Server 2012 도메인 컨트롤러 설치](https://technet.microsoft.com/library/jj574134.aspx)  
- [새 Windows Server 2012 Active Directory 자식 또는 트리 도메인 (수준 200)를 설치 합니다.](https://technet.microsoft.com/library/jj574105.aspx)  
- [Windows Server 2012 Active Directory 읽기 전용 도메인 컨트롤러 (RODC) (수준 200)를 설치 합니다.](https://technet.microsoft.com/library/jj574152.aspx)  
- [설정 구성 Windows Server 2012 도메인 컨트롤러 (EN-US)에 대 한 단계별 가이드](https://social.technet.microsoft.com/wiki/contents/articles/12370.step-by-step-guide-for-setting-up-windows-server-2012-domain-controller-en-us.aspx)  

## <a name="windows-update-considerations"></a>Windows 업데이트 고려 사항

Windows 8이 출시되기 전에는 Windows 업데이트에서 업데이트를 확인하고 이를 다운로드하여 설치하는 자체 내부 일정을 관리했습니다. 이를 위해서는 Windows 업데이트 에이전트가 항상 백그라운드에서 실행되어야 하므로 메모리 및 기타 시스템 리소스가 사용되었습니다.  
  
Windows 8 및 Windows Server 2012는 [자동 유지 관리](https://msdn.microsoft.com/library/windows/desktop/hh848037(v=vs.85).aspx)라는 새로운 기능을 도입했습니다. 자동 유지 관리는 각각 자체 일정 및 실행 논리를 관리하는 다양한 기능을 통합합니다. 이 통합을 통해 이러한 구성 요소가 모두 훨씬 적은 시스템 리소스를 사용하고, 일관성 있게 작동하며, 새로운 장치 유형에 대해 [연결된 대기 상태](https://msdn.microsoft.com/library/windows/hardware/jj248729.aspx) 를 유지하고, 휴대용 장치의 배터리를 적게 소모합니다.  
  
Windows 업데이트는 Windows 8 및 Windows Server 2012에서 자동 유지 관리의 일부이므로 업데이트 설치 날짜 및 시간을 설정하는 자체 내부 일정이 더 이상 적용되지 않습니다. Windows 8 및 Windows Server 2012를 실행하는 장치와 컴퓨터를 포함하여 엔터프라이즈의 모든 장치와 컴퓨터에서 일관되고 예측 가능한 다시 시작 동작을 보장하려면 Microsoft 기술 자료 문서 [2885694](https://support.microsoft.com/kb/2885694) (또는 2013년 10월 누적 롤업 [2883201](https://support.microsoft.com/kb/2883201)참조)를 참조한 다음 WSUS 블로그 게시물 [Windows 8 및 Windows Server 2012에 보다 예측 가능한 Windows 업데이트 환경 사용(KB 2885694)](http://blogs.technet.com/b/wsus/archive/2013/10/08/enabling-a-more-predictable-windows-update-experience-for-windows-8-and-windows-server-2012-kb-2885694.aspx)에 설명된 정책 설정을 구성하세요.  

## <a name="BKMK_NewWS2012R2"></a>Windows Server 2012 R2에서 AD DS의 새로운 기능은 무엇입니까?

다음 표에는 Windows Server 2012 R2 AD DS의 새로운 기능이 요약되어 있으며, 자세한 정보에 연결해 주는 링크(사용 가능한 경우)가 나와 있습니다. 요구 사항을 비롯한 몇 가지 기능에 대한 자세한 설명은 [Windows Server 2012 R2에서 Active Directory의 새로운 기능](https://technet.microsoft.com/library/dn268294.aspx)을 참조하세요.  

|기능|설명|  
|-----------|---------------|  
|[작업 공간 연결](https://technet.microsoft.com/library/dn280945.aspx)|정보 관리자가 개인 장치를 회사에 연결하여 회사 리소스 및 서비스에 액세스할 수 있도록 해줍니다.|  
|[웹 응용 프로그램 프록시](https://technet.microsoft.com/library/dn280942.aspx)|새로운 원격 액세스 역할 서비스를 사용하여 웹 응용 프로그램에 대한 액세스를 제공합니다.|  
|[Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx)|AD FS는 간소화된 배포 및 향상된 기능을 통해 사용자가 개인 장치에서 리소스에 액세스할 수 있도록 하고 IT 부서에서 액세스 제어를 관리할 수 있도록 지원합니다.|  
|[SPN 및 UPN 고유성](https://technet.microsoft.com/library/dn535779.aspx)|Windows Server 2012 R2를 실행하는 도메인 컨트롤러에서는 중복된 SPN(서비스 사용자 이름) 및 UPN(사용자 계정 이름)을 만들지 못합니다.|  
|[Winlogon ARSO(자동 다시 시작 로그온)](https://technet.microsoft.com/library/dn535772.aspx)|잠금 화면 응용 프로그램을 다시 시작하고 Windows 8.1 장치에서 사용할 수 있도록 합니다.|  
|[TPM 키 증명](https://technet.microsoft.com/library/dn581921.aspx)|인증서 요청자 개인 키가 실제로 TPM(신뢰할 수 있는 플랫폼 모듈)으로 보호된 발급된 인증서를 CA에서 암호화된 방식으로 증명할 수 있도록 합니다.|  
|[자격 증명 보호 및 관리](https://technet.microsoft.com/library/dn408190.aspx)|자격 증명 도난을 방지하는 새로운 자격 증명 보호 및 도메인 인증 제어 기능입니다.|  
|[FRS (파일 복제 서비스)의 사용 중단](https://technet.microsoft.com/library/dn535775.aspx)|Windows Server 2003 도메인 기능 수준에서는 FRS가 SYSVOL을 복제하는 데 사용되므로 이 기능 수준도 더 이상 사용되지 않습니다. 따라서 Windows Server 2012 R2를 실행하는 서버에서 새 도메인을 만들려면 도메인 기능 수준이 Windows Server 2008 이상이어야 합니다. Windows Server 2003 도메인 기능 수준이;는 기존 도메인에 Windows Server 2012 R2를 실행 하는 도메인 컨트롤러를 추가할 수 있습니다. 만 해당 수준에서 새 도메인을 만들 수 없습니다.|  
|[새 도메인 및 포리스트 기능 수준](../active-directory-functional-levels.md)|Windows Server 2012 R2에 대한 새로운 기능 수준이 있습니다. 새로운 기능은 Windows Server 2012 R2 DFL에서 사용할 수 있습니다.|  
|[LDAP 쿼리 최적화 프로그램 변경](https://technet.microsoft.com/library/dn535775.aspx)|LDAP 검색 효율성 및 LDAP 복잡한 쿼리 검색 시간 성능이 향상되었습니다.|  
|[1644 이벤트 개선 사항](https://technet.microsoft.com/library/dn535775.aspx)|문제 해결을 지원하기 위해 LDAP 검색 결과 통계가 이벤트 ID 1644에 추가되었습니다.|  
|[Active Directory 복제 처리량 개선 사항](https://technet.microsoft.com/library/dn535775.aspx)|최대 AD 복제 처리량이 40Mbps에서 약 600Mbps로 조정되었습니다.|  

## <a name="BKMK_WhatsNewAD"></a>Windows Server 2012의 AD DS의 새로운 기능은 무엇입니까?

다음 표에는 Windows Server 2012 AD DS의 새로운 기능이 요약되어 있으며, 자세한 정보에 연결해 주는 링크(사용 가능한 경우)가 나와 있습니다. 요구 사항을 비롯 한 몇 가지 기능에 대 한 자세한 설명은 대해서 [What's New in Active Directory Domain Services (AD DS)](https://technet.microsoft.com/library/hh831477.aspx)합니다.  
  
|기능|설명|  
|-----------|---------------|  
|AD BA(Active Directory 기반 정품 인증)는 [볼륨 정품 인증 개요](https://technet.microsoft.com/library/hh831612.aspx)를 참조하세요.|볼륨 소프트웨어 라이선스의 배포 및 관리 구성 작업을 간소화합니다.|  
|[Active Directory Federation Services (AD FS)](https://technet.microsoft.com/library/hh831502.aspx)|서버 관리자, 간소화된 신뢰 설정, 자동 신뢰 관리, SAML 프로토콜 지원 등을 통해 설치 역할을 추가합니다.|  
|Active Directory의 손실된 페이지 플러시 이벤트|NTDS ISAM 이벤트 530(Jet 오류 - 1119)이 Active Directory 데이터베이스에 손실된 페이지 플러시 이벤트를 감지할 수 있도록 기록됩니다.|  
|[Active Directory 휴지통 사용자 인터페이스](https://technet.microsoft.com/library/hh831702.aspx#ad_recycle_bin_mgmt)|ADAC(Active Directory Administrative Center)에서 원래 Windows Server 2008 R2에 도입된 휴지통의 GUI 관리 기능을 추가합니다.|  
|[Active Directory 복제 및 토폴로지 Windows PowerShell cmdlet](https://technet.microsoft.com/library/hh831757.aspx)|Windows PowerShell을 사용하여 Active Directory 사이트, 사이트 링크, 연결 개체 등의 생성 및 관리 작업을 지원합니다.|  
|[동적 액세스 제어](https://technet.microsoft.com/library/hh831717.aspx)|기존 액세스 제어 모델이 향상된 새로운 클레임 기반 인증 플랫폼입니다.|  
|[세분화 된 암호 정책 사용자 인터페이스](https://technet.microsoft.com/library/hh831702.aspx#fine_grained_pswd_policy_mgmt)|ADAC에는 GUI 지원 기능이 추가되어 원래 Windows Server 2008에 추가된 PSO를 생성, 편집 및 할당할 수 있습니다.|  
|[GMSA (그룹 관리 서비스 계정)](https://technet.microsoft.com/library/hh831782.aspx)|gMSA라는 새로운 보안 주체 유형으로, 여러 호스트에서 실행되는 서비스를 동일한 gMSA 계정으로 실행할 수 있습니다.|  
|[DirectAccess 오프 라인 도메인 가입](https://technet.microsoft.com/library/jj574150.aspx)|DirectAccess 필수 구성 요소를 포함시킴으로써 오프라인 도메인 가입이 확장됩니다.|  
|[가상 도메인 컨트롤러 (DC) 복제를 통한 신속한 배포](https://technet.microsoft.com/library/hh831734.aspx#virtualized_dc_cloning)|가상화된 DC는 Windows PowerShell cmdlet을 사용해 기존의 가상 도메인 컨트롤러를 복제함으로써 신속하게 배포될 수 있습니다.|  
|[RID 풀 변경 사항](https://technet.microsoft.com/library/jj574229.aspx)|새로운 모니터링 이벤트와 할당량을 추가하여 전역 RID 풀이 과도하게 사용되지 않도록 보호합니다. 필요에 따라 풀을 모두 사용한 경우 전역 RID 풀 크기를 두 배로 만듭니다.|  
|보안 시간 서비스|와이어 암호와 MD5 해시 기능을 제거하고 Windows 8 시간 클라이언트를 인증하는 데 필요한 서버를 요청하여 W32tm의 보안 성능을 향상시킵니다.|  
|[가상화 된 Dc의 USN 롤백 보호](https://technet.microsoft.com/library/hh831734.aspx#safe_virt_dc)|실수로 가상화된 DC의 스냅샷 백업을 복원하면 더 이상 USN이 롤백되지 않습니다.|  
|[Windows PowerShell 기록 뷰어](https://technet.microsoft.com/library/hh831702.aspx#windows_powershell_history_viewer)|관리자가 ADAC를 사용하면 실행되는 Windows PowerShell 명령을 볼 수 있습니다.|  
  
### <a name="BKMK_"></a>자동 유지 관리 및 변경 내용을 업데이트가 Windows 업데이트에서 적용 된 후 다시 시작 동작

Windows 8이 출시되기 전에는 Windows 업데이트에서 업데이트를 확인하고 이를 다운로드하여 설치하는 자체 내부 일정을 관리했습니다. 이를 위해서는 Windows 업데이트 에이전트가 항상 백그라운드에서 실행되어야 하므로 메모리 및 기타 시스템 리소스가 사용되었습니다.  
  
Windows 8 및 Windows Server 2012는 [자동 유지 관리](https://msdn.microsoft.com/library/windows/desktop/hh848037(v=vs.85).aspx)라는 새로운 기능을 도입했습니다. 자동 유지 관리는 각각 자체 일정 및 실행 논리를 관리하는 다양한 기능을 통합합니다. 이 통합을 통해 이러한 구성 요소가 모두 훨씬 적은 시스템 리소스를 사용하고, 일관성 있게 작동하며, 새로운 장치 유형에 대해 [연결된 대기 상태](https://msdn.microsoft.com/library/windows/hardware/jj248729.aspx) 를 유지하고, 휴대용 장치의 배터리를 적게 소모합니다.  
  
Windows 업데이트는 Windows 8 및 Windows Server 2012에서 자동 유지 관리의 일부이므로 업데이트 설치 날짜 및 시간을 설정하는 자체 내부 일정이 더 이상 적용되지 않습니다. Windows 8 및 Windows Server 2012를 실행하는 장치와 컴퓨터를 포함하여 엔터프라이즈의 모든 장치와 컴퓨터에서 일관되고 예측 가능한 다시 시작 동작을 유지하기 위해 다음 그룹 정책 설정을 구성할 수 있습니다.  

- **컴퓨터 구성 | 정책 | 관리 템플릿 | Windows 구성 요소 | Windows 업데이트 | 자동 업데이트 구성**  
- **컴퓨터 구성 | 정책 | 관리 템플릿 | Windows 구성 요소 | Windows 업데이트 | 로그온 한 사용자로 자동 다시 시작**  
- **컴퓨터 구성 | 정책 | 관리 템플릿 | Windows 구성 요소 | 유지 관리 Scheduler | 유지 관리 임의 지연**  

다음 표에는 원하는 다시 시작 동작을 제공하도록 이러한 설정을 구성하는 방법에 대한 몇 가지 예가 나와 있습니다.  

|||  
|-|-|  
|**시나리오**|**권장된 구성**|  
|**WSUS 관리**<br /><br />--일주일에 한 번 업데이트를 설치 하는 중<br />-금요일 오후 11 시 재부팅|자동 설치되도록 컴퓨터 설정, 원하는 시간까지 자동 다시 부팅 방지<br /><br />**정책**: 자동 업데이트 구성(사용)<br /><br />자동 업데이트 구성: 4-자동으로 다운로드 하 고 설치 예약<br /><br />**정책**: 로그온 사용자 (사용 안 함)를 사용 하 여 자동 다시 시작<br /><br />**WSUS 기한**: 금요일 오후 11시로 설정|  
|**WSUS 관리**<br /><br />-다른 시간/일 지그재그 설치|함께 업데이트해야 하는 여러 그룹의 컴퓨터에 대해 대상 그룹 설정<br /><br />이전 시나리오에 위 단계 사용<br /><br />대상 그룹마다 다른 기한 설정|  
|**WSUS 관리-지원 되지 않습니다 기한**<br /><br />-서로 다른 시간에 지그재그 설치|**정책**: 자동 업데이트 구성(사용)<br /><br />자동 업데이트 구성: 4-자동으로 다운로드 하 고 설치 예약<br /><br />**레지스트리 키:** Microsoft 기술 자료 문서에 설명 된 레지스트리 키를 사용 하도록 설정 [2835627](https://support.microsoft.com/kb/2835627)<br /><br />**정책:** 자동 유지 관리 임의 지연(사용)<br /><br />다음 동작을 제공하도록 **정기 유지 관리 임의 지연** 을 PT6H(6시간 임의 지연)로 설정:<br /><br />구성 된 유지 관리 시간 임의 지연을 더한 시점에서 업데이트 설치는<br /><br />-다시 시작에 대 한 각 컴퓨터는 내부 정확히 3 일 후<br /><br />또는 각 그룹의 컴퓨터에 대해 서로 다른 유지 관리 시간 설정|  

Windows 엔지니어링 팀이 이러한 변경 내용을 구현한 이유에 대한 자세한 내용은 [Windows 업데이트에서 자동으로 업데이트한 후 다시 시작 최소화](http://blogs.msdn.com/b/b8/archive/2011/11/14/minimizing-restarts-after-automatic-updating-in-windows-update.aspx)를 참조하세요.  

## <a name="BKMK_InstallationChanges"></a>AD DS 서버 역할 설치 변경 사항

Windows Server 2003부터 Windows Server 2008 R2까지는 x86 또는 X64 버전의 Adprep.exe 명령줄 도구를 실행한 후에 Active Directory 설치 마법사, Dcpromo.exe 및 미디어나 무인 설치를 통해 설치할 수 있는 선택적 변형이 포함된 Dcpromo.exe를 실행했습니다.  
  
Windows Server 2012부터 Windows PowerShell의 ADDSDeployment 모듈을 사용하여 명령줄이 설치됩니다. GUI 기반의 승격 작업은 새로운 AD DS 구성 마법사를 완전히 사용하는 서버 관리자에서 수행됩니다. 설치 프로세스를 간소화하기 위해 ADPREP가 AD DS 설치에 통합되었으며, 필요에 따라서는 자동으로 실행됩니다. Windows PowerShell 기반의 AD DS 구성 마법사에 Dc 추가 되는 다음, 필수 ADPREP 명령을 관련 도메인 컨트롤러에서 원격으로 실행 위치는 도메인의 스키마와 인프라 마스터 역할 자동으로 대상으로 합니다.  
  
AD DS 설치 마법사의 필수 구성 요소를 검사하여 잠재적인 오류를 확인한 후 설치를 시작합니다. 오류 상태를 수정하여 일부 전체 업그레이드의 문제를 제거할 수 있습니다. 또한 마법사는 그래픽 설치 중에 지정된 모든 옵션이 포함되어 있는 Windows PowerShell 스크립트를 내보냅니다.  
  
그러므로 모두 종합해 볼 때 AD DS 설치를 변경하면, 특히 전 세계 지역 및 도메인에 여러 도메인 컨트롤러를 배포하려는 경우 관리상의 오류 발생 가능성을 줄이고 DC 역할 설치 프로세스를 간소화할 수 있습니다.  
명령줄 구문과 단계별 마법사 지침을 포함하여 GUI 및 Windows PowerShell 기반 설치에 대한 자세한 내용은 [Active Directory 도메인 서비스 설치](https://technet.microsoft.com/library/hh472162.aspx)를 참조하세요. 기존 포리스트의 Windows Server 2012 DC 설치 작업과는 별도로 Active Directory 포리스트 스키마 변경 사항의 도입을 제어하려는 관리자는 계속해서 Adprep.exe 명령을 관리자 권한 명령 프롬프트에서 실행할 수 있습니다.  

## <a name="BKMK_DeprecatedFeatures"></a>사용 되지 않는 기능 및 Windows Server 2012의 AD DS 관련 동작 변경 내용

AD DS와 관련된 몇 가지 변경 사항은 다음과 같습니다.  

- **Adprep32.exe의 사용 중단**
   - Adprep.exe에는 한 가지 버전만 있는데, 이 버전은 필요에 따라 Windows Server 2008 이상을 실행하는 64비트 서버에서 실행할 수 있습니다. 이 버전은 원격으로 실행할 수 있으며, 대상이 되는 해당 작업의 마스터 역할이 32비트 운영 체제나 Windows Server 2003에서 호스팅되는 경우 원격으로 실행해야 합니다.  
- **Dcpromo.exe의 사용 중단**
   - Dcpromo는 Windows Server 2012에만 계속 실행할 수 있지만 응답 파일 또는 조직으로 전환할 시간을 기존 자동화는 새로운 Windows PowerShell 설치 옵션을 제공 하는 명령줄 매개 변수를 사용 하 여 사용 되지 않습니다.  
-   **Lm 해시는 사용자 계정에 사용 하지 않도록 설정**
   - Windows Server 2008, Windows Server 2008 R2 및 Windows Server 2012의 보안 템플릿에서 보안 기본값은 Windows 2000 및 Windows Server 2003 도메인 컨트롤러의 보안 템플릿에서 사용하지 않도록 설정된 NoLMHash 정책을 사용합니다. 필요한 경우 기술 자료 문서 [946405](https://support.microsoft.com/kb/946405)의 단계를 사용하여 LMHash 종속 클라이언트의 NoLMHash 정책을 사용하지 않도록 설정합니다.  

Windows Server 2008부터 도메인 컨트롤러도 포함 되어 Windows Server 2003 또는 Windows 2000을 실행 하는 도메인 컨트롤러에 비해 다음과 같은 보안 기본 설정 합니다.

|||||  
|-|-|-|-|  
|암호화 유형 또는 정책|Windows Server 2008 기본값|Windows Server 2012 및 Windows Server 2008 R2 기본값|설명|  
|AllowNT4Crypto|사용 안 함|사용 안 함|타사 SMB(서버 메시지 블록) 클라이언트는 도메인 컨트롤러에서 안전한 기본 설정과 호환되지 않을 수 있습니다. 어떠한 경우든 이러한 설정을 완화하여 호환되도록 할 수는 있지만 보안이 취약해질 수 있습니다. 자세한 내용은 [문서 942564](https://go.microsoft.com/fwlink/?LinkId=164558) Microsoft 기술 자료 (https://go.microsoft.com/fwlink/?LinkId=164558)합니다.|  
|DES|Enabled|사용 안 함|[문서 977321](https://go.microsoft.com/fwlink/?LinkId=177717) Microsoft 기술 자료 (https://go.microsoft.com/fwlink/?LinkId=177717)|  
|통합 인증에 대한 CBT/확장된 보호|해당 사항 없음|Enabled|참조 [Microsoft 보안 공지 (937811)](https://go.microsoft.com/fwlink/?LinkId=164559) (https://go.microsoft.com/fwlink/?LinkId=164559) 하 고 [문서 976918](https://go.microsoft.com/fwlink/?LinkId=178251) Microsoft 기술 자료 (https://go.microsoft.com/fwlink/?LinkId=178251)합니다.<br /><br />검토 하 고 핫픽스를 설치 [문서 977073](https://go.microsoft.com/fwlink/?LinkId=186394) (https://go.microsoft.com/fwlink/?LinkId=186394) 필요에 따라 Microsoft 기술 자료에서 합니다.|  
|LMv2|Enabled|사용 안 함|[문서 976918](https://go.microsoft.com/fwlink/?LinkId=178251) Microsoft 기술 자료 (https://go.microsoft.com/fwlink/?LinkId=178251)|  

## <a name="BKMK_SysReqs"></a>운영 체제 요구 사항

Windows Server 2012의 최소 시스템 요구 사항은 다음 표에 나열 됩니다. 시스템 요구 사항과 사전 설치 정보에 대한 자세한 내용은 [Windows Server 2012 설치](https://technet.microsoft.com/library/jj134246.aspx)를 참조하세요. 새로운 Active Directory 포리스트를 설치하는 데 필요한 추가 시스템 요구 사항은 없지만 도메인 컨트롤러, LDAP 클라이언트 요청 및 Active Directory 사용 응용 프로그램의 성능을 향상시키려면 Active Directory 데이터베이스의 콘텐츠를 캐시할 수 있는 메모리를 충분하게 추가해야 합니다. 새 도메인 컨트롤러를 기존 포리스트에 추가하거나 기존 도메인 컨트롤러를 업그레이드하는 경우, 다음 섹션을 참조하여 서버가 디스크 공간 요구 사항을 충족하는지 확인하세요.  

|||  
|-|-|  
|프로세서|1.4Ghz 64비트 프로세서|  
|RAM|512MB|  
|사용 가능한 디스크 공간 요구 사항|32GB|  
|화면 해상도|800 x 600 이상|  
|기타|DVD 드라이브, 키보드, 인터넷 액세스|  

### <a name="BKMK_DiskSpaceDCWin8"></a>도메인 컨트롤러를 업그레이드 하는 것에 대 한 디스크 공간 요구 사항

이 섹션에서는 Windows Server 2008 또는 Windows Server 2008 R2에서 업그레이드 하는 도메인 컨트롤러에만 디스크 공간 요구 사항을 다룹니다. 도메인 컨트롤러를 이전 버전의 Windows Server로 업그레이드하는 데 필요한 디스크 공간에 대한 자세한 내용은 [Windows Server 2008로 업그레이드하는 데 필요한 디스크 공간](https://technet.microsoft.com/library/cc754463(WS.10).aspx#BKMK_2008) 또는 [Windows Server 2008 R2로 업그레이드하는 데 필요한 디스크 공간](https://technet.microsoft.com/library/cc754463(WS.10).aspx#BKMK_2008R2)을 참조하세요.  
  
Active Directory 데이터베이스와 로그 파일을 호스트하는 디스크 크기를 조정하면 사용자 지정/응용 프로그램 구동 스키마 확장, 응용 프로그램 및 관리자가 시작한 인덱스 외에도 도메인 컨트롤러의 배포 수명(일반적으로 5~8년) 기간 동안 디렉터리에 추가되는 개체와 특성의 공간 요구 사항을 모두 수용할 수 있습니다. 배포할 때 크기를 알맞게 조정하는 것이 배포 후 디스크 저장소를 확장하는 데 필요한 작업 비용을 훨씬 더 많이 소비하는 것보다 현명한 투자 방법입니다. 자세한 내용은 [Active Directory 도메인 서비스의 용량 계획](https://social.technet.microsoft.com/wiki/contents/articles/14355.capacity-planning-for-active-directory-domain-services.aspx)을 참조하세요.  
  
업그레이드하려는 도메인 컨트롤러에서 운영 체제를 업그레이드하기 전에 Active Directory 데이터베이스(NTDS.DIT)를 호스트하는 드라이브에 사용 가능한 디스크 공간이 NTDS.DIT 파일의 20% 이상 있는지 확인합니다. 볼륨에서 사용 가능한 디스크 공간이 충분하지 않으면 업그레이드에 실패할 수 있으며, 업그레이드 호환성 보고서에 사용 가능한 디스크 공간이 부족함을 나타내는 오류가 반환됩니다.  
  
이 경우 Active Directory 데이터베이스에 대해 오프라인 조각 모음을 수행하여 추가 공간을 재수집한 후 업그레이드를 다시 시도하세요. 자세한 내용은 [디렉터리 데이터베이스 파일 압축(오프라인 조각 모음)](https://technet.microsoft.com/library/cc794920(v=WS.10).aspx)을 참조하세요.  
  
### <a name="available-skus"></a>사용 가능한 SKU

Windows Server는 Foundation, Essentials, Standard 및 Datacenter의 4가지 에디션이 있습니다.
AD DS 역할을 지원하는 두 가지 버전은 Standard와 Datacenter입니다.  
  
이전 릴리스에서 Windows Server 버전은 서버 역할의 지원 기능과 프로세서 수, 대량 메모리 지원 기능 등의 측면에서 차이를 보였습니다. Standard edition에 대 한 가상 인스턴스가 두 개 허용은 Windows Server Standard 및 Datacenter 버전 모든 기능과 기본 하드웨어를 지원 하지만, 가상화 권한에-다 되며 데이터 센터에 대 한 가상 인스턴스가 무제한으로 허용 버전입니다.  
  
### <a name="windows-client-and-windows-server-operating-systems-that-are-supported-to-join-windows-server-domains"></a>Windows Server 도메인 가입이 지원되는 Windows 클라이언트와 Windows Server 운영 체제

다음 Windows 클라이언트와 Windows Server 운영 체제는 Windows Server 2012 이상을 실행하는 도메인 컨트롤러가 포함된 도메인 구성원 컴퓨터를 지원합니다.  
  
- 클라이언트 운영 체제: Windows 8.1, Windows 8, Windows 7, Windows Vista
   - Windows 8.1 또는 Windows 8을 실행하는 컴퓨터는 Windows Server 2003 이상을 비롯한 이전 버전의 Windows Server를 실행하는 도메인 컨트롤러가 있는 도메인에 가입할 수도 있습니다. 그러나 이 경우 일부 Windows 8 기능을 사용할 수 없거나 추가 구성이 필요할 수 있습니다. 이러한 기능 및 하위 도메인에서 Windows 8 클라이언트를 관리하기 위한 기타 권장 사항에 대한 자세한 내용은 [Windows Server 2003 도메인에서 Windows 8 구성원 컴퓨터 실행](https://social.technet.microsoft.com/wiki/contents/articles/17361.running-windows-8-member-computers-in-windows-server-2003-domains.aspx)을 참조하세요.  
- 서버 운영 체제: Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2, Windows Server 2003  

## <a name="BKMK_UpgradePaths"></a>지원 되는 현재 위치 업그레이드 경로

64 비트 버전의 Windows Server 2008 또는 Windows Server 2008 R2를 실행 하는 도메인 컨트롤러는 Windows Server 2012로 업그레이드할 수 있습니다. Windows Server 2003 또는 32비트 버전의 Windows Server 2008을 실행하는 도메인 컨트롤러는 업그레이드할 수 없습니다. 이 컨트롤러를 바꾸려면 도메인에 이후 버전의 Windows Server를 실행하는 도메인 컨트롤러를 설치한 후 Windows Server 2003을 실행하는 도메인 컨트롤러를 제거하세요.  

|이러한 버전을 실행 중인 경우|이러한 버전으로 업그레이드 가능|  
|-------------------------------------|-------------------------------------|  
|Windows Server 2008 Standard SP2<br /><br />또는<br /><br />Windows Server 2008 Enterprise SP2|Windows Server 2012 Standard<br /><br />또는<br /><br />Windows Server 2012 Datacenter|  
|Windows Server 2008 Datacenter SP2|Windows Server 2012 Datacenter|  
|Windows Web Server 2008|Windows Server 2012 Standard|  
|Windows Server 2008 R2 Standard SP1<br /><br />또는<br /><br />Windows Server 2008 R2 Enterprise SP1|Windows Server 2012 Standard<br /><br />또는<br /><br />Windows Server 2012 Datacenter|  
|Windows Server 2008 R2 Datacenter SP1|Windows Server 2012 Datacenter|  
|Windows Web Server 2008 R2|Windows Server 2012 Standard|  
  
지원되는 업그레이드 경로에 대한 자세한 내용은 [Windows Server 2012의 평가 버전 및 업그레이드 옵션](https://go.microsoft.com/fwlink/?LinkId=260917)을 참조하세요. Windows Server 2012의 평가판을 실행하는 도메인 컨트롤러는 일반 정품으로 바로 전환할 수 없습니다. 대신 서버에 일반 정품을 실행하는 서버에서 도메인 컨트롤러를 추가로 설치하고 평가판을 실행하는 도메인 컨트롤러에서 AD DS를 제거합니다.  
  
알려진된 문제로 인해 Windows Server 2012의 Server Core 설치로 Windows Server 2008 R2의 Server Core 설치를 실행 하는 도메인 컨트롤러를 업그레이드할 수 없습니다. 업그레이드 프로세스 후반부에 검은색 화면이 나타나면서 업그레이드가 중단됩니다. 해당 DC를 재부팅하면 이전 운영 체제 버전으로 롤백하는 boot.ini 파일의 옵션이 표시됩니다. 추가로 재부팅하면 이전 운영 체제 버전으로 자동 롤백 작업이 시작됩니다. 솔루션을 사용할 수 있는 되기 것이 좋습니다 내부 Windows Server의 Server Core 설치를 실행 하는 기존 도메인 컨트롤러를 업그레이드 하는 대신 Windows Server 2012의 Server Core 설치를 실행 하는 새 도메인 컨트롤러를 설치 하는 2008 R2입니다. 자세한 내용은 기술 자료 문서 [2734222](https://support.microsoft.com/kb/2734222)를 참조하세요.  

## <a name="BKMK_FunctionalLevels"></a>기능 수준 기능 및 요구 사항

Windows Server 2012에 Windows Server 2003 포리스트 기능 수준이 필요합니다. 즉, 기존 Active Directory 포리스트에 Windows Server 2012를 실행 하는 도메인 컨트롤러를 추가 하려면 먼저 포리스트 기능 수준을 Windows Server 2003 이상 이어야 합니다. 이는 Windows Server 2008 R2, Windows Server 2008 또는 Windows Server 2003을 실행하는 도메인 컨트롤러가 동일한 포리스트에서 작동할 수 있다는 뜻입니다. 그러나 이 경우 Windows 2000 Server를 실행하는 도메인 컨트롤러가 지원되지 않고, Windows Server 2012를 실행하는 도메인 컨트롤러의 설치가 차단됩니다. 포리스트에 Windows Server 2003 이상을 실행하는 도메인 컨트롤러가 포함되지만 포리스트 기능 수준이 여전히 Windows 2000인 경우에는 설치도 차단됩니다.  
  
Windows 2000 도메인 컨트롤러를 제거한 후에 Windows Server 2012 도메인 컨트롤러를 포리스트에 추가해야 합니다. 이 경우 다음 단계를 따르는 것이 좋습니다.  

1. Windows Server 2003 이상을 실행하는 도메인 컨트롤러를 설치합니다. 이러한 도메인 컨트롤러는 Windows Server의 평가판에 배포될 수 있습니다. 이 단계에서는 반드시 해당 운영 체제 릴리스에 적합한 [adprep.exe를 실행](https://technet.microsoft.com/library/dd464018(WS.10).aspx) 해야 합니다.  
2. Windows 2000 도메인 컨트롤러를 제거합니다. 특히 제거된 모든 도메인 컨트롤러의 도메인 컨트롤러 계정을 제거하려면 도메인 및 사용된 Active Directory 사용자, 컴퓨터에서 Windows Server 2000 도메인 컨트롤러를 강제로 제거하거나 적절하게 해당 컨트롤러의 수준을 내립니다.  
3. 포리스트 기능 수준을 Windows Server 2003 이상으로 올립니다.  
4. Windows Server 2012를 실행하는 도메인 컨트롤러를 설치합니다.  
5. 이전 버전의 Windows Server를 실행하는 도메인 컨트롤러를 제거합니다.  

새 Windows Server 2012 도메인 기능 수준이 새로운 기능 중 하나를 사용 하도록 설정: 합니다 **KDC의 클레임, 복합 인증 및 Kerberos 아머 링 지원** KDC 관리 템플릿 정책에 두 가지 설정이 (**항상 클레임 제공** 하 고 **아머 링 되지 않은 인증 요청 실패**)는 Windows Server 2012 도메인 기능 수준이 필요 합니다.  
  
Windows Server 2012 포리스트 기능 수준이 새로운 모든 기능을 제공 하지는 않지만 포리스트에서 만들어진 새 도메인이 Windows Server 2012 도메인 기능 수준에서 자동으로 작동 되도록 보장 합니다. Windows Server 2012 도메인 기능 수준을 클레임, 복합 인증 및 Kerberos 아머 링에 대 한 KDC 지원 이외에 다른 새 기능을 제공 하지 않습니다. 하지만 모든 도메인 컨트롤러는 도메인에서 Windows Server 2012를 실행 하는 것이 되도록 합니다. 다양한 기능 수준에서 사용할 수 있는 기타 기능에 대한 자세한 내용은 [AD DS(Active Directory 도메인 서비스) 기능 수준 이해](../active-directory-functional-levels.md)를 참조하세요.  
  
포리스트 기능 수준을 특정 값으로 설정한 후 롤백할 수 없거나 다음 예외를 사용 하 여 포리스트 기능 수준은 낮출: Windows Server 2012로 포리스트 기능 수준을 올린 후 Windows Server 2008 R2로 낮출 수 있습니다. Active Directory 휴지통을 사용할 수 없는 경우 포리스트 기능 수준을 Windows Server 2008 R2 또는 Windows Server 2008에 Windows Server 2012 또는 Windows Server 2008 R2에서 Windows Server 2008까지 낮출 수도 있습니다. 포리스트 기능 수준을 Windows Server 2008 R2로 하는 경우 해당 롤백할 수 없습니다 다시 예를 들어, Windows Server 2003.  
  
도메인 기능 수준을 특정 값으로 설정한 후 롤백할 수 없거나 다음 예외를 사용 하 여 도메인 기능 수준은 낮출: Windows Server 2008 R2 또는 Windows Server 2012 도메인 기능 수준을 올릴 때 포리스트 함수 nal 수준이 Windows Server 2008 않았거나 이하인 롤링 도메인 기능 수준을 Windows Server 2008 또는 Windows Server 2008 R2의 옵션입니다. 도메인 기능 수준이 Windows Server 2008 R2 또는 Windows Server 2008에 Windows Server 2012 또는 Windows Server 2008 R2 Windows Server 2008로만 낮출 수 있습니다. 도메인 기능 수준이 Windows Server 2008 R2로 하는 경우 해당 롤백할 수 없습니다 다시 예를 들어, Windows Server 2003.  
  
낮은 기능 수준에서 사용할 수 있는 기능에 대한 자세한 내용은 [AD DS(Active Directory 도메인 서비스) 기능 수준 이해](../active-directory-functional-levels.md)를 참조하세요.  
  
기능 수준 이외 Windows Server 2012를 실행 하는 도메인 컨트롤러는 이전 버전의 Windows Server를 실행 하는 도메인 컨트롤러에서 사용할 수 없는 추가 기능을 제공 합니다. 예를 들어 Windows Server 2012를 실행 하는 도메인 컨트롤러를 사용할 수 있습니다 가상 도메인 컨트롤러 복제에 대 한 반면 이전 버전의 Windows Server를 실행 하는 도메인 컨트롤러 수 없습니다. 없는 가상 도메인 컨트롤러 복제 및 Windows Server 2012에서 가상 도메인 컨트롤러 보호 시 필요한 기능 수준 요구 합니다.  

> [!NOTE]  
> Microsoft Exchange Server 2013에는 Windows server 2003 이상의 포리스트 기능 수준이 필요합니다.  

## <a name="BKMK_ServerRoles"></a>다른 서버 역할 및 Windows 운영 체제를 사용 하 여 AD DS의 상호 운용성

AD DS는 다음과 같은 Windows 운영 체제에서는 지원되지 않습니다.  
  
- Windows MultiPoint Server  
- Windows Server 2012 Essentials  
  
AD DS는 다음과 같은 서버 역할 또는 역할 서비스도 실행하는 서버에는 설치할 수 없습니다.  
  
- Hyper-V 서버  
- 원격 데스크톱 연결 브로커  
  
## <a name="BKMK_OpsMasters"></a>작업 마스터 역할

Windows Server 2012의 새로운 기능 일부 작업 마스터 역할을 영향을 줍니다.  

- PDC 에뮬레이터에는 가상 도메인 컨트롤러 복제를 지원 하려면 Windows Server 2012 실행 되어야 합니다. 또한 DC를 복제하는 데 추가 필수 구성 요소가 필요합니다. 자세한 내용은 [AD DS(Active Directory 도메인 서비스) 가상화](https://technet.microsoft.com/library/hh831734.aspx)를 참조하세요.  
- 새 보안 주체는 PDC 에뮬레이터 Windows Server 2012를 실행 하는 경우에 생성 됩니다.  
- RID 마스터에는 새 RID 발급 및 모니터링 기능이 포함됩니다. 개선된 기능으로는 향상된 이벤트 로깅 및 제한 및 비상시 1비트별 전체 RID 풀 할당 증가 기능 등이 있습니다. 자세한 내용은 [Managing RID Issuance](../../ad-ds/manage/Managing-RID-Issuance.md)를 참조하세요.  

> [!NOTE]  
> 작업 마스터 역할 되지 않아도, AD DS 설치의 또 다른 변경 Windows Server 2012를 실행 하는 모든 도메인 컨트롤러에 기본적으로 DNS 서버 역할 및 글로벌 카탈로그를 설치 한다는 것입니다.  

## <a name="BKMK_Virtual"></a>도메인 컨트롤러 가상화

도메인 컨트롤러의 안전한 가상화 및 도메인 컨트롤러를 복제 하는 기능부터 Windows Server 2012의 AD DS의에서 향상 된 기능을 사용 하도록 설정 합니다. 도메인 컨트롤러를 복제하면 새로운 도메인에서 추가 도메인 컨트롤러를 신속하게 배포할 수 있으며, 다른 장점도 얻을 수 있습니다. 자세한 내용은 [Active Directory Domain Services 소개 &#40;AD DS&#41; 가상화 &#40;수준 100&#41;](../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md)합니다.  

## <a name="BKMK_Admin"></a>Windows Server 2012 서버 관리

사용 합니다 [원격 서버 관리 도구에 대 한 Windows 8](https://www.microsoft.com/download/details.aspx?id=28972) 도메인 컨트롤러와 Windows Server 2012를 실행 하는 다른 서버를 관리할 수 있습니다. Windows 8을 실행 하는 컴퓨터에서 Windows Server 2012 원격 서버 관리 도구를 실행할 수 있습니다.  

## <a name="BKMK_AppCompat"></a>응용 프로그램 호환성

다음 표에는 일반적인 Active Directory 통합 Microsoft 응용 프로그램이 나와 있습니다. 이 표에서는 Windows Server에 설치 가능한 버전과 Windows Server 2012 DC를 도입하면 응용 프로그램 호환성에 영향을 주는지에 대해 설명합니다.  

|Product|참고|  
|-----------|---------|  
|[Microsoft Configuration Manager 2007](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|Configuration Manager 2007 SP2(Configuration Manager 2007 R2 및 Configuration Manager 2007 R3 포함):<br /><br />-   Windows 8 Pro<br />-   Windows 8 Enterprise<br />-   Windows Server 2012 Standard<br />-Windows Server 2012 Datacenter **참고 합니다.** 이러한 버전이 클라이언트로 완벽하게 지원되더라도 Configuration Manager 2007 운영 체제 배포 기능을 사용하여 해당 버전을 운영 체제로 배포하는 데 필요한 지원을 추가할 계획은 없습니다. 또한 사이트 서버나 사이트 시스템은 Windows Server 2012의 SKU에서 지원되지 않습니다.|  
|[Microsoft SharePoint 2007](https://support.microsoft.com/kb/2728964)|Microsoft Office SharePoint Server 2007은 Windows Server 2012 설치 시 지원되지 않습니다.|  
|[Microsoft SharePoint 2010](https://support.microsoft.com/kb/2724471)|SharePoint 2010 서비스 팩 2 설치 및 작동 하는 데 필요한가 <br />Windows Server 2012 서버에서 SharePoint 2010<br /><br />SharePoint 2010 Foundation 서비스 팩 2는 Windows Server 2012 서버에서 SharePoint 2010 Foundation을 설치 및 작동하는 데 필요합니다.<br /><br />SharePoint Server 2010(서비스 팩 제외) 설치 프로세스는 Windows Server 2012에서 설치되지 않습니다.<br /><br />SharePoint Server 2010 필수 구성 요소 설치 관리자 (PrerequisiteInstaller.exe) "이이 프로그램에 호환성 문제가 있습니다." 오류와 함께 실패 "도움을 받지 않고 프로그램 실행"을 클릭 하면 오류가 표시 됩니다. "SharePoint를 설치할 수 있는지 확인 &#124; SharePoint Server 2010 (서비스 팩 제외)는 Windows에 설치할 수 없는 서버 2012입니다."|  
|[Microsoft SharePoint 2013](https://technet.microsoft.com/library/cc262485(v=office.15).aspx)|팜에 있는 데이터베이스 서버의 최소 요구 사항<br /><br />64비트 버전의 Windows Server 2008 R2 SP1(서비스 팩 1) Standard, Enterprise, Datacenter 또는 64비트 버전의 Windows Server 2012 Standard, Datacenter<br /><br />데이터베이스가 기본 제공되는 단일 서버의 최소 요구 사항:<br /><br />64비트 버전의 Windows Server 2008 R2 SP1(서비스 팩 1) Standard, Enterprise, Datacenter 또는 64비트 버전의 Windows Server 2012 Standard, Datacenter<br /><br />팜에 있는 프런트 엔드 웹 서버 및 응용 프로그램 서버의 최소 요구 사항:<br /><br />64비트 버전의 Windows Server 2008 R2 SP1(서비스 팩 1) Standard, Enterprise, Datacenter 또는 64비트 버전의 Windows Server 2012 Standard, Datacenter|  
|[Microsoft System Center Configuration Manager 2012](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|System Center 2012 Configuration Manager 서비스 팩 1:<br /><br />Microsoft는 서비스 팩 1 릴리스와 함께 다음 운영 체제를 클라이언트 지원 매트릭스에 추가할 예정입니다.<br /><br />-   Windows 8 Pro<br />-   Windows 8 Enterprise<br />-   Windows Server 2012 Standard<br />-   Windows Server 2012 Datacenter<br /><br />사이트 서버, SMS 공급자 및 관리 지점 등의 모든 사이트 서버 역할을 다음 운영 체제 버전과 함께 서버에 배포할 수 있습니다.<br /><br />-   Windows Server 2012 Standard<br />-   Windows Server 2012 Datacenter|  
|[Microsoft Lync Server 2013](https://technet.microsoft.com/library/gg412883.aspx)|Lync Server 2013에는 Windows Server 2008 R2 또는 Windows Server 2012가 필요합니다. Server Core 설치 시 실행할 수 없으며, [가상 서버](https://technet.microsoft.com/library/gg399035.aspx)에서도 실행할 수 있습니다.|  
|[Lync Server 2010](https://support.microsoft.com/kb/2777359)|Lync Server 2010은 [2012년 10월 Lync Server의 누적 업데이트](https://support.microsoft.com/?kbid=2493736) 가 설치되어 있으면 새로운(업그레이드되지 않은) 설치 Windows Server 2012에 설치할 수 있습니다. 기존에 설치된 Lync Server 2010에서 Windows Server 2012로 운영 체제를 업그레이드할 수는 없습니다. Microsoft Lync Server 2010 Group Chat Server는 Windows Server 2012에서도 지원되지 않습니다.|  
|[System Center 2012 Endpoint Protection](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|System Center 2012 Endpoint Protection 서비스 팩 1은 다음 운영 체제를 포함하도록 클라이언트 지원 매트릭스를 업데이트할 예정입니다.<br /><br />-   Windows 8 Pro<br />-   Windows 8 Enterprise<br />-   Windows Server 2012 Standard<br />-   Windows Server 2012 Datacenter|  
|[System Center 2012 Forefront Endpoint Protection](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|FEP 2010 업데이트 롤업 1은 다음 운영 체제를 포함하도록 클라이언트 지원 매트릭스를 업데이트할 예정입니다.<br /><br />-   Windows 8 Pro<br />-   Windows 8 Enterprise<br />-   Windows Server 2012 Standard<br />-   Windows Server 2012 Datacenter|  
|Forefront TMG(위험 관리 게이트웨이)|TMG는 Windows Server 2008과 Windows Server 2008 R2에서만 실행할 수 있습니다. 자세한 내용은 [Forefront TMG 시스템 요구 사항](https://technet.microsoft.com/library/dd896981.aspx)을 참조하세요.|  
|Windows Server Update Services|이 WSUS 릴리스는 이미 Windows 8 기반 컴퓨터나 Windows Server 2012 기반 컴퓨터를 클라이언트로 지원하고 있습니다.|  
|Windows Server Update Services 3.0|KB 업데이트 문서 [2734608](https://support.microsoft.com/kb/2734608)을 통해 WSUS(Windows Server Update Services) 3.0 SP2를 실행하는 서버에서 Windows 8 또는 Windows Server 2012를 실행하는 컴퓨터로 업데이트할 수 있습니다. **참고:** WSUS 3.0 SP2를 사용하여 독립 실행형 WSUS 3.0 SP2 환경 또는 System Center Configuration Manager 2007 서비스 팩 2 환경을 갖춘 고객이 Windows 8 기반 컴퓨터나 Windows Server 2012 기반 컴퓨터를 클라이언트로 제대로 관리하려면 [2734608](https://support.microsoft.com/kb/2734608)이 필요합니다.|  
|[Exchange 2013](https://technet.microsoft.com/library/bb691354.aspx)|Windows Server 2012 Standard 및 Datacenter에서는 스키마 마스터, 글로벌 카탈로그 서버, 도메인 컨트롤러, 사서함 및 클라이언트 액세스 서버 역할 등을 지원합니다.<br /><br />포리스트 기능 수준: Windows Server 2003 이상<br /><br />출처: Exchange 2013 시스템 요구 사항|  
|Exchange 2010|[원본: Exchange 2010 서비스 팩 3](https://blogs.technet.com/b/exchange/archive/2012/09/25/announcing-exchange-2010-service-pack-3.aspx)<br /><br />Exchange 2010 서비스 팩 3은 Windows Server 2012 구성원 서버에 설치할 수 있습니다.<br /><br />[Exchange 2010 시스템 요구 사항](https://technet.microsoft.com/library/aa996719(EXCHG.141).aspx) 에는 Windows Server 2008 R2로 최근에 지원된 스키마 마스터, 글로벌 카탈로그 및 도메인 컨트롤러가 나와 있습니다.<br /><br />포리스트 기능 수준: Windows Server 2003 이상|  
|SQL Server 2012|출처: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />SQL Server 2012 RTM은 Windows Server 2012에서 지원됩니다.|  
|SQL Server 2008 R2|출처: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Windows Server 2012를 설치하려면 SQL Server 2008 R2 서비스 팩 1 이상이 필요합니다.|  
|SQL Server 2008|출처: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Windows Server 2012를 설치하려면 SQL Server 2008 서비스 팩 3 이상이 필요합니다.|  
|SQL Server 2005|출처: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Windows Server 2012에서는 설치할 수 없습니다.|  

## <a name="BKMK_KnownIssues"></a>알려진된 문제

다음 표에는 AD DS 설치와 관련해 알려진 문제가 나와 있습니다.  

||||  
|-|-|-|  
|KB 문서 번호 및 제목|영향받는 기술 영역|문제/설명|  
|[2830145](https://support.microsoft.com/kb/2830145): 도메인 환경의 Windows 7 또는 Windows Server 2008 R2 기반 컴퓨터에서 SID S-1-18-1 및 SID S-1-18-2를 매핑할 수 없음|AD DS 관리/응용 프로그램 호환성|Windows 7 기반 또는 Windows Server 2008 R2 기반 컴퓨터에서 SID를 확인할 수 없으므로 Windows Server 2012의 새로운 기능인 SID S-1-18-1 및 SID S-1-18-2를 매핑하는 응용 프로그램이 실패할 수 있습니다. 이 문제를 해결하려면 도메인의 Windows 7 기반 및 Windows Server 2008 R2 기반 컴퓨터에 핫픽스를 설치하세요.|  
|[2737129](https://support.microsoft.com/kb/2737129): Windows Server 2012용으로 기존 도메인을 자동으로 준비할 때 그룹 정책이 준비되지 않음|AD DS 설치|Adprep /domainprep /gpprep는 한 도메인에서 Windows Server 2012를 실행하는 첫 번째 DC를 설치의 일부로 자동 실행하지 않습니다. 이전에 해당 도메인에서 실행된 적이 없으면 수동으로 실행해야 합니다.|  
|[2737416](https://support.microsoft.com/kb/2737416): Windows PowerShell 기반 도메인 컨트롤러 배포에서 경고가 반복됨|AD DS 설치|필수 구성 요소의 유효성 검사가 진행되는 동안 경고가 나타났다가 설치할 때 다시 나타날 수 있습니다.|  
|[2737424](https://support.microsoft.com/kb/2737424): 도메인 컨트롤러에서 Active Directory Domain Services를 제거하려고 할 때 "지정된 도메인 이름의 형식이 올바르지 않습니다." 오류가 발생함|AD DS 설치|사전에 만든 RODC 계정이 여전히 존재하는 도메인에서 마지막 DC를 제거하면 이 오류가 나타납니다. 이 오류는 Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008에 영향을 줍니다.|  
|[2737463](https://support.microsoft.com/kb/2737463): 도메인 컨트롤러가 시작되지 않거나, c00002e2 오류가 발생하거나, "옵션을 선택하십시오." 메시지가 표시됨|AD DS 설치|DC는 관리자가 DirectoryServices-DomainController 역할을 제거하는 데 Dism.exe, Pkgmgr.exe 또는 Ocsetup.exe를 사용했기 때문에 시작되지 않습니다.|  
|[2737516](https://support.microsoft.com/kb/2737516): Windows Server 2012 서버 관리자의 IFM 검증 제한 사항|AD DS 설치|KB 문서에 설명된 것처럼 IFM 검증에는 몇 가지 제한 사항이 있을 수 있습니다.|  
|[2737535](https://support.microsoft.com/kb/2737535): Install-AddsDomainController cmdlet에서 RODC에 대해 매개 변수 집합 오류를 반환함|AD DS 설치|사전에 만든 RODC 계정에 이미 입력된 인수를 지정한 경우 RODC 계정에 서버를 연결하려고 하면 오류가 발생할 수 있습니다.|  
|[2737560](https://support.microsoft.com/kb/2737560): "Exchange 스키마 충돌 검사를 수행할 수 없습니다." 오류가 발생하며 필수 구성 요소 검사에 실패함|AD DS 설치|DC에 Network Service용 SeServiceLogonRight가 누락되거나 WMI 또는 DCOM 프로토콜이 차단되어 있기 때문에 기존 도메인에서 첫 번째 Windows Server 2012 DC를 구성할 때 필수 구성 요소를 검사할 수 없습니다.|  
|[2737797](https://support.microsoft.com/kb/2737797): AddsDeployment 모듈에 -Whatif 인수를 사용하면 잘못된 DNS 결과가 표시됨|AD DS 설치|-WhatIf 매개 변수 서버를 설치할 수는 있지만 DNS를 보여 줍니다.|  
|[2737807](https://support.microsoft.com/kb/2737807): 도메인 컨트롤러 옵션 페이지에서 다음 단추를 사용할 수 없음|AD DS 설치|다음 단추는 대상 DC의 IP 주소가 기존 서브넷 또는 사이트로 매핑되지 않거나, DSRM 암호를 입력하지 않아도 올바르게 확인되기 때문에 도메인 컨트롤러 옵션 페이지에서 사용할 수 없습니다.|  
|[2737935](https://support.microsoft.com/kb/2737935): Active Directory 설치가 "NTDS 설정 개체 만들기" 단계에서 지연됨|AD DS 설치|로컬 관리자 암호가 도메인 관리자 암호와 일치하거나 네트워킹 문제 때문에 중요한 복제 작업이 완료되지 않아 설치가 중단됩니다.|  
|[2738060](https://support.microsoft.com/kb/2738060): Install-AddsDomain을 사용하여 하위 도메인을 원격으로 생성할 때 "액세스가 거부되었습니다." 오류 메시지가 표시됨|AD DS 설치|DNSDelegationCredential에 잘못된 암호가 있을 때 Invoke-Command cmdlet을 사용하여 Install-ADDSDomain을 실행하면 오류가 표시됩니다.|  
|[2738697](https://support.microsoft.com/kb/2738697): 서버 관리자를 사용하여 서버를 구성할 때 "서버를 사용할 수 없습니다." 도메인 컨트롤러 구성 오류가 발생함|AD DS 설치|NTLM 인증을 사용하지 않도록 설정했기 때문에 작업 그룹 컴퓨터에서 AD DS를 설치하려고 하면 이 오류가 표시됩니다.|  
|[2738746](https://support.microsoft.com/kb/2738746): 로컬 관리자 도메인 계정에 로그온하면 액세스 거부 오류가 발생함|AD DS 설치|기본 제공된 관리자 계정이 아닌 로컬 관리자 계정을 사용하여 로그온한 다음 새 도메인을 만들면 해당 계정이 Domain Admins 그룹에 추가되지 않습니다.|  
|[2743345](https://support.microsoft.com/kb/2743345): "시스템에서 지정된 파일을 찾을 수 없습니다." Adprep /gpprep 오류가 발생하거나 도구 작동이 중단됨|AD DS 설치|인프라 마스터가 비연속 네임스페이스를 구현하기 때문에 adprep /gpprep를 실행하면 이 오류가 표시됩니다.|  
|[2743367](https://support.microsoft.com/kb/2743367): Windows Server 2003, 64비트 버전에서 Adprep "올바른 Win32 응용 프로그램이 아닙니다." 오류가 발생함|AD DS 설치|Windows Server 2012 Adprep를 Windows Server 2003에서 실행할 수 없기 때문에 이 오류가 표시됩니다.|  
|[2753560](https://support.microsoft.com/kb/2753560): Windows Server 2012에서 ADMT 3.2 및 PES 3.1 설치 오류가 발생함|ADMT|ADMT 3.2를 의도한 대로 Windows Server 2012에 설치할 수 없습니다.|  
|[2750857](https://support.microsoft.com/kb/2750857): DFS 복제 진단 보고서가 Internet Explorer 10에 올바르게 표시되지 않음|DFS 복제|Internet Explorer 10에 변경된 사항이 있기 때문에 DFS 복제 진단 보고서가 올바르게 표시되지 않습니다.|  
|[2741537](https://support.microsoft.com/kb/2741537): 원격 그룹 정책 업데이트가 사용자에게 표시됨|그룹 정책|로그온한 각 사용자 컨텍스트에서 예정된 작업이 실행되기 때문입니다. 이 시나리오에서는 Windows 작업 스케줄러를 설계할 때 대화형 프롬프트가 필요합니다.|  
|[2741591](https://support.microsoft.com/kb/2741591): ADM 파일이 GPMC 인프라 상태 옵션의 SYSVOL에 표시되지 않음|그룹 정책|GP 복제 GPMC 인프라 상태는 사용자 지정된 필터링 규칙을 따르지 않습니다 때문에 "복제 진행 중"을 보고할 수 있습니다.|  
|[2737880](https://support.microsoft.com/kb/2737880): AD DS 구성 중에 "서비스를 시작할 수 없습니다." 오류가 발생함|가상 DC 복제|DS 역할 서버 서비스를 사용하지 않도록 설정했기 때문에 AD DS 또는 복제를 설치하거나 제거하면 이 오류가 표시됩니다.|  
|[2742836](https://support.microsoft.com/kb/2742836): VDC 복제 기능을 사용할 때 두 개의 DHCP 임대가 각 도메인 컨트롤러에 생성됨|가상 DC 복제|복제된 도메인 컨트롤러에서 복제하기 전에 임대를 수신하고 복제가 완료되면 다시 수신하기 때문에 이와 같은 현상이 발생합니다.|  
|[2742844](https://support.microsoft.com/kb/2742844): 도메인 컨트롤러 복제에 실패하고 서버가 Windows Server 2012의 DSRM에서 다시 시작됨|가상 DC 복제|복제된 DC가 KB 문서에 열된 다양한 이유로 인해 복제되지 않아 DSRM에서 시작됩니다.|  
|[2742874](https://support.microsoft.com/kb/2742874): 도메인 컨트롤러 복제 시 일부 서비스 주체 이름이 다시 생성되지 않음|가상 DC 복제|세 부분으로 구성된 일부 SPN은 도메인 이름 바꾸기 프로세스가 제한되어 복제된 DC에서 다시 생성되지 않습니다.|  
|[2742908](https://support.microsoft.com/kb/2742908): 도메인 컨트롤러를 복제한 후 "로그온 서버를 사용할 수 없습니다." 오류가 발생함|가상 DC 복제|복제에 실패하면 DC가 DSRM에서 시작되기 때문에 가상화된 DC를 복제한 후 로그온하려고 하면 이 오류가 표시됩니다. .\administrator로 로그온하여 복제 실패 관련 문제를 해결합니다.|  
|[2742916](https://support.microsoft.com/kb/2742916): dcpromo.log에 8610 오류가 로깅되고 도메인 컨트롤러 복제에 실패함|가상 DC 복제|역할이 전송되어 PDC 에뮬레이터에서 도메인 파티션에 대한 인바운드 복제가 수행되지 않기 때문에 복제되지 않습니다.|  
|[2742927](https://support.microsoft.com/kb/2742927): "인덱스 범위를 벗어났습니다." New-AdDcCloneConfig 오류|가상 DC 복제|가상 DC를 복제하는 동안에는 cmdlet가 상승된 명령 프롬프트에서 실행되지 않거나 액세스 토큰에 관리자 그룹이 포함되지 않기 때문에 New-ADDCCloneConfigFile cmdlet를 실행하면 오류가 표시됩니다.|  
|[2742959](https://support.microsoft.com/kb/2742959): 도메인 컨트롤러 복제 오류로 인해 실패 8437: "잘못 된 매개 변수는이 복제 연산에 지정 했습니다."|가상 DC 복제|복제 이름이 잘못되었거나 중복된 NetBIOS 이름이 지정되었으므로 복제에 실패했습니다.|  
|[2742970](https://support.microsoft.com/kb/2742970): DSRM, 중복된 원본 및 복제 컴퓨터가 없어 DC 복제에 실패함|가상 DC 복제|DCCloneConfig.xml 파일이 올바른 위치에서 생성되지 않거나 원본 DC가 복제 전 다시 부팅되었기 때문에 복제된 가상 DC가 중복된 이름을 원본 DC로 사용하여 DSRM(디렉터리 서비스 복구 모드)에서 부팅됩니다.|  
|[2743278](https://support.microsoft.com/kb/2743278): 도메인 컨트롤러 복제 오류 0x80041005|가상 DC 복제|WINS 서버가 하나만 지정되었기 때문에 복제된 DC가 DSRM으로 부팅됩니다. WINS 서버가 지정된 경우 기본/대체 WINS 서버가 모두 지정되어 있어야 합니다.|  
|[2745013](https://support.microsoft.com/kb/2745013): Windows Server 2012에서 New-AdDcCloneConfigFile을 실행하는 경우 "서버가 작동하지 않습니다." 오류 메시지가 표시됨|가상 DC 복제|New-ADDCCloneConfigFile cmdlet을 실행하면 서버를 글로벌 카탈로그 서버에 연결할 수 없기 때문에 이 오류가 표시됩니다.|  
|[2747974](https://support.microsoft.com/kb/2747974): 도메인 컨트롤러 복제 이벤트 2224에서 잘못된 지침을 제공함|가상 DC 복제|이벤트 ID 2224에서 복제하기 전 관리 서비스 계정을 제거해야 한다고 잘못 표시합니다. 독립 실행형 MSA는 제거해야 하지만 그룹 MSA가 복제를 차단하지는 않습니다.|  
|[2748266](https://support.microsoft.com/kb/2748266): Windows 8로 업그레이드한 후 BitLocker로 암호화된 드라이브의 잠금을 해제할 수 없음|BitLocker|Windows 7에서 업그레이드 된 컴퓨터의 드라이브 잠금을 해제 하려고 할 때 "응용 프로그램을 찾을 수 없습니다." 오류가 표시 됩니다.|  

## <a name="see-also"></a>관련 항목

[Windows Server 2012 평가 리소스](https://technet.microsoft.com/evalcenter/hh708766.aspx)  
[Windows Server 2012 평가 가이드](https://download.microsoft.com/download/5/B/2/5B254183-FA53-4317-B577-7561058CEF42/WS%202012%20Evaluation%20Guide.pdf)  
[Windows Server 2012 설치 및 배포](https://technet.microsoft.com/library/hh831620.aspx)  
