---
title: "광고 숲 복구-숲 복구 하는 방법을 확인"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: cc2525068225644b0964a2726bd9c0dcf2e0cba0
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="determine-how-to-recover-the-forest"></a>숲 복구 하는 방법을 확인합니다  

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

 전체 Active Directory 숲 복구 백업에서 복원 하거나 숲 모든 도메인 컨트롤러 (DC)에 Active Directory Domain Services (AD DS)을 다시 설치 해야 합니다. 숲 복구 각 도메인 숲에서 상태로 마지막 신뢰할 수 있는 백업에서 복원 합니다. 따라서 복원 작업 발생 됩니다 손실 이상 다음 Active Directory 데이터.  
  
-   신뢰할 수 있는 백업한 후 추가한 모든 개체 (예: 사용자와 컴퓨터)  
  
-   모든 업데이트에 대 한 기존 개체 마지막 신뢰할 수 있는 이후 백업  
  
-   마지막 신뢰할 수 있는 백업 이후 구성 파티션 또는 AD DS 스키마 파티션을 (예: 스키마 변경 내용)에 대 한 모든 변경  
  
 각 도메인 숲에 대해 관리자 도메인 계정 암호를 알고 있어야 합니다. 사용 하지 않아야 하는 기본 제공 된 관리자 계정 암호입니다. 또한 dc 상태 시스템 복원을 수행 하려면 DSRM 암호를 알고 있어야 합니다. 일반적으로 것이 백업이 되는 유효한, 즉, 또는 삭제 된 Active Directory 휴지통 활성화 된 경우 수명 동안 개체의 삭제 표시 기간 동안 내 관리자 계정과 DSRM 암호 기억을 안전한 장소에 보관 하는 것이 좋습니다. 도메인 사용자 계정으로 DSRM 암호를 동기화 할 기억 하기 쉽게 설정 하려면 수도 있습니다. 자세한 내용은 참조 KB 문서 [961320](https://support.microsoft.com/kb/961320)합니다. 숲 복구 준비 과정의 일환으로 하기 전에 DSRM 계정 동기화 수행 해야 합니다.  
  
> [!NOTE]
>  관리자 계정을 도메인 관리자 및 Enterprise 관리자 그룹이 기본적으로 기본 관리자가 그룹의 회원입니다. 이 그룹 도메인에 있는 모든 Dc의 모든 권한을 가집니다.  
  
## <a name="determining-which-backups-to-use"></a>어떤 백업을 사용 하 여 확인 합니다.  
 각 도메인에 대 한 두 개 이상의 쓰기 Dc 정기적으로 백업 여러 백업에서 선택할 수 있도록 합니다. Note 쓰기 DC 복원 하는 읽기 전용 RODC (도메인 컨트롤러) 백업을 사용할 수 없습니다. Dc 오류가 발생 하기 전에 며칠 찍은 백업을 사용 하 여 복원 하는 것이 좋습니다. 일반적으로 recentness 및 복원된 된 데이터의 safeness 간에 절충을 확인 해야 합니다. 최신 백업을 더 유용 하 게 데이터 복구 있지만 위험한 데이터를 복원된 숲 다시 초래 위험이 적으면 선택 합니다.  
  
 시스템 상태 백업을 복원 원래 운영 체제 및 백업 서버에 따라 다릅니다. 예를 들어, 다른 서버로 시스템 상태 백업을 복원 하지 해야 합니다. 이 경우에 다음과 같은 경고가 표시 될 수 있습니다.  
  
 "현재 아닌 다른 서버의 지정된 백업이입니다. 서버를 사용할 수 없게 될 수 있으므로 대체 서버에 백업으로 시스템 상태 복구를 수행 하지 않는 것이 좋습니다. 당신이이 백업을 사용 하 여 현재 서버 복구 하기 위한 하 시겠습니까 "?  
  
 다른 하드웨어 Active Directory 복원 하려는 경우 전체 서버를 수행 하 고 서버 전체 백업을 만듭니다.  
  
> [!IMPORTANT]
>  Windows Server 2008부터, 없습니다 새로운 하드웨어나 같은 하드웨어에서 Windows Server를 새로 설치를 시스템 상태 백업을 복원 해야 합니다. 이 가이드 뒷부분에서 권장 같은 하드웨어에서 Windows Server를 다시 설치 하는 경우을이 순서 대로 도메인 컨트롤러를 복원할 수 있습니다.  
>   
>  1.  운영 체제 모든 파일 및 응용 프로그램을 복원 하기 위해 전체 서버 복원을 수행 합니다.  
> 2.  시스템 상태로 복원 wbadmin.exe SYSVOL 신뢰할 수 있는 상태로 표시 하기 위해 사용 하 여 수행 합니다.  
>   
>  자세한 내용은 참조 Microsoft 기술 자료 문서 [249694](https://support.microsoft.com/kb/249694)합니다.  
  
 오류가 발생할 때를 알 수 없는 경우 조사해 숲 마지막 안전 상태가 백업 식별 합니다. 이 방법은 덜 것이 좋습니다. 따라서 오류의 시간을 확인할 수 숲 전체 실패 하는 경우 되도록 매일 AD DS의 상태에 대 한 자세한 로그를 유지 하는 것이 좋습니다. 또한 로컬 빠른 복구할 수 있도록 백업 복사본을 유지 해야 합니다.  
  
 백업 수명은 같지 Active Directory 휴지통 사용 하는 경우는 **deletedObjectLifetime** 값 또는 **tombstoneLifetime** 가치, 더 작은 합니다. 자세한 내용은 참조 [Active Directory 휴지통 Step-by-Step 가이드](https://go.microsoft.com/fwlink/?LinkId=178657) (https://go.microsoft.com/fwlink/?LinkId=178657).  
  
 다른 방법으로 도구 (Dsamain.exe) 탑재 Active Directory 데이터베이스를 사용할 수도 있습니다 있고 Ldp.exe 또는 Active Directory 사용자 및 컴퓨터 백업을 식별 하는 등 LDAP(Lightweight Directory Access Protocol) (LDAP) 도구를 안전 하 게 마지막 숲의 상태입니다. Windows Server 2008 및 Windows Server 운영 체제 나중에 포함 된 Active Directory 데이터베이스 장착 도구 LDAP 서버로 스냅숏을 또는 백업에 저장 된 Active Directory 데이터를 제공 합니다. 그런 다음 LDAP 도구 찾아보기 데이터를 사용할 수 있습니다. 이 방법에 모든 DC에 DSRM 디렉터리 서비스 복원 모드 () AD DS 백업의 콘텐츠를 검사 하려면 다시 시작 필요 하지 활용 합니다.  
  
 도구 장착 Active Directory 데이터베이스 사용에 대 한 자세한 내용은 참조는 [Active Directory 데이터베이스 장착 도구 Step-by-Step 가이드](https://technet.microsoft.com/library/cc753609\(WS.10\).aspx)합니다.  
  
 사용할 수도 있습니다는 **ntdsutil 스냅숏을** Active Directory 데이터베이스의 스냅숏을 만드는 명령을 합니다. 주기적으로 스냅숏을 만드는 작업을 예약 하 여 시간이 지남에 따라 Active Directory 데이터베이스의 복사본을 추가로 얻을 수 있습니다. 더 나은 숲 전체 오류가 발생 했을 때 사용자의 신원을 확인 한 다음 가장 백업을 복원 하려면 이러한 복사본을 사용할 수 있습니다. 스냅숏을 만드는, 버전을 사용 하 여 **ntdsutil** 에서 서버 관리 RSAT (원격 도구) Windows Vista에 대 한 이상 또는 Windows Server 2008와 함께 제공 되는 합니다. DC 대상 모든 버전의 Windows Server를 실행할 수 있습니다. 사용에 대 한 자세한 내용은 **ntdsutil 스냅숏을** 명령, 참조 [스냅숏을](https://technet.microsoft.com/library/cc731620\(WS.10\).aspx)합니다.  
  
  
## <a name="determining-which-domain-controllers-to-restore"></a>복원 하는 도메인 컨트롤러 결정  
 복원 하는 프로세스 접근성 중요 한 요소 때 복원 하는 도메인 컨트롤러를 결정 합니다. 기본 설정 복원 dc 각 도메인 전용된 DC 하는 것이 좋습니다. DC 쉽게 안정적 계획 하 고 실행 숲 복구 수행 하는 데 사용 된 것과 동일한 소스 구성 사용 하기 때문에 전용된 복원 복원 테스트 합니다. 복구를 스크립트 고 여부 GC 또는 DNS 서버를 사용 하는 것이 든 또는 여부 DC 보유 작업 마스터 역할 여부와 같은 다양 한 구성와 경쟁 하지 않을 수 있습니다.  
  
> [!NOTE]
>  하지 단순하게 관련 작업 마스터 역할 소유자 복원 하는 것이 좋습니다, 동안 일부 조직 다른 이점도 대 한 복원 하도록 선택할 수 있습니다. 예를 들어 RID 마스터 복원는 복구 하는 동안 Rid 관리 문제를 방지할 수 있습니다.  
  
 다음 조건을 가장 잘 맞는 DC 선택 합니다.  
  
-   DC는 쓸 수는 있습니다. 이 옵션은 필수입니다.  
  
-   가상 컴퓨터 Windows Server 2012에서 지 원하는 VM-GenerationID 하이퍼바이저 실행 DC 합니다. 이 DC 복제할 원본으로 사용할 수 있습니다.  
  
-   DC는 물리적으로 또는 가상 네트워크에 액세스할 수 있는 데이터 센터에 있는 것이 좋습니다. 이런 방법이으로 분리할 수 있습니다 쉽게 하면 네트워크에서 숲 복구 하는 동안 합니다.  
  
-   좋은 전체 서버 백업 된 DC 합니다. 적절 한 백업을 성공적으로 복원할 수, 촬영 몇 일 전 오류를 포함 하 고 가능한 서 매우 유용 데이터가 백업이입니다.  
  
-   오류가 발생 하기 전에 시스템 DNS (도메인 이름) 서버에 DC 합니다. 이렇게 하면 DNS 다시 설치 하는 데 걸리는 시간은 저장 합니다.  
  
-   또한 Windows 배포 서비스를 사용할 경우 BitLocker 네트워크 잠금 해제를 사용 하 여 구성 되지 않은 DC 선택 합니다. 이 경우 BitLocker 네트워크 잠금 해제 숲 복구 하는 동안 백업에서 복원 하는 첫 번째 DC에 사용 되는 지원 되지 않습니다.  
  
     BitLocker 네트워크 잠금 해제로 *만* 키 보호기 *수 없는* 에서 사용할 수 Dc 이렇게 시나리오에서 때문에 Windows 배포 서비스 (WDS) 배포 있는 위치에 처음 DC 필요한 Active Directory 및 WDS 잠금을 해제 하기 위해 작업을 합니다. 하지 않으면이 첫 번째 DC 복원 하기 전에 Active Directory 아직 WDS에 사용할 수 있으므로 잠금을 해제할 수 없습니다.  
  
     DC BitLocker 네트워크 잠금 해제를 사용 하도록 구성 된 경우를 확인 하려면 다음 레지스트리 키에서 네트워크 잠금 해제 인증서 확인 된를 확인 합니다.  
  
     HKEY_LOCAL_MACHINESoftwarePoliciesMicrosoftSystemCertificatesFVE_NKP  
  
 처리 Active Directory 포함 된 파일 백업 복원 하거나 절차 보안을 유지 합니다. 실수로 긴급 숲 복구와 함께 제공 되는 유용한 보안 간과 발생할 수 있습니다. 자세한 내용은의 "설정 도메인 컨트롤러 백업 및 복원 전략" 섹션 참조 [보안 Active Directory를 설치 하 고 Day-to-Day 작업에 대 한 최상의 방법을: 일부 II](https://technet.microsoft.com/library/bb727066.aspx)합니다.  
  
## <a name="identify-the-current-forest-structure-and-dc-functions"></a>현재 숲 구조 및 DC 기능을 식별  
 현재 숲 구조 숲 모든 도메인을 식별 하 여 확인 합니다. 백업, Dc 및 복제에 대 한 소스 될 수 있는 가상화 Dc 특히 각 도메인에 있는 모든 Dc 목록을 확인 합니다. 먼저이 도메인을 복구할 복구할 수 있는 이렇게 Dc 목록이 가장 중요 한 됩니다. 숲 루트 도메인을 복원한 후 Active Directory 끌기 기능을 사용 하 여 다른 도메인, Dc 및 숲에서 사이트 목록을 얻을 수 있습니다.  
  
 다음과 같이 도메인에 있는 각 DC 기능을 보여 주는 표를 준비 합니다. 복구 후 숲의 사전 오류 구성으로 되돌릴 수는 데 도움이 됩니다.  
  
|DC 이름|운영 체제|FSMO|GC|RODC|백업|DNS|서버 Core|VM|VM-GenID|  
|-------------|----------------------|----------|--------|----------|------------|---------|-----------------|--------|---------------|  
|DC_1|Windows Server 2012|마스터 스키마 도메인 이름 지정 마스터|예|아니요|예|아니요|아니요|예|예|  
|DC_2|Windows Server 2012|없음|예|아니요|예|예|아니요|예|예|  
|DC_3|Windows Server 2012|Infrastructure 마스터|아니요|아니요|아니요|예|예|예|예|  
|DC_4|Windows Server 2012|지우려는 마스터 PDC 에뮬레이터|예|아니요|아니요|아니요|아니요|예|아니요|  
|DC_5|Windows Server 2012|없음|아니요|아니요|예|예|아니요|예|예|  
|RODC_1|Windows Server 2008 R2|없음|예|예|예|예|예|예|아니요|  
|RODC_2|Windows Server 2008|없음|예|예|아니요|예|예|예|아니요|  
  
 각 도메인 숲에 대 한 해당 도메인에 대 한 Active Directory 데이터베이스 신뢰할 수 있는 백업을 있는 단일 쓰기 DC을 확인 합니다. DC 복원 하려면 백업이 선택할 때는 주의 해야 합니다. 날짜와 오류 원인을 알 약 경우 해당 날짜 몇 일 만든 백업을 사용 하는 일반적인 좋습니다.  
  
 여기서에서는 4 백업 후보: DC_1, DC_2, DC_4, 및 DC_5 합니다. 이러한 백업 지원자 중 하나를 복원할만 합니다. 권장된 DC DC_5 다음과 같은 경우에 다음과 같습니다.  
  
-   가상화 DC 복제에 대 한 소스도 사용 되는 요구 사항을 충족, 지원 VM-GenerationID 실행 소프트웨어를 하이퍼바이저에서 가상 DC 복제할 허용 되는 Windows Server 2012를 실행 (될 수 없는 경우 제거할 수 있는 또는 복제). 복원 후 PDC 에뮬레이터 역할 확보 됩니다에 도메인에 대 한 복제할 수 도메인 컨트롤러 그룹에 서버를 추가할 수 있습니다.  
  
-   Windows Server 2012를 설치 하는 전체 실행 됩니다. DC 서버 Core 설치를 자동으로 실행 하는 대상으로 위해 복구를 위해 편리한 될 수 있습니다.  
  
-   DNS 서버 것이 있습니다. 따라서 DNS 다시 설치할 필요가 없습니다.  
  
> [!NOTE]
>  DC_5 드 서버 아니므로 있다는 장점은 드 복원 후 제거 필요가 없습니다. 하지만 모든 Dc는 기본적으로 제거 했다가 복원이 숲 복구 과정의 일부로 어떤 경우에 권장 후 드를 추가 하 여 드 서버 여부 DC 드 서버는 명확한 인수 일부 터 Windows Server 2012와 이기도 합니다.  
  
## <a name="recover-the-forest-in-isolation"></a>격리에서 숲 복구  
 기본 시나리오 첫 번째 복원된 DC 하기 전에 모든 쓰기 Dc 종료 하는으로 돌아가지 프로덕션 것입니다. 이렇게 하면 모든 위험한 데이터 복구 숲으로 다시 복제 하지 않습니다. 것이 특히 중요 작업 하는 모든 마스터 역할 사용자를 종료할 수 있습니다.  
  
> [!NOTE]
>  경우에 시스템 작동 중단을 최소화 하려면 온라인 상태를 유지할 다른 Dc 허용 하면서도 각 격리 된 네트워크 도메인에 대 한 복구 계획 하는 첫 번째 DC 이동 위치 있을 수 있습니다. 예를 들어, 실패 한 스키마 업그레이드를 복구 하는 경우 격리에서 복구 단계를 수행 하는 동안 제품 네트워크에서 실행 되는 도메인 컨트롤러를 유지 하도록 선택할 수 있습니다.  
  
 가상화 Dc를 실행 하는 경우 사용자 이동할 수 프로덕션 네트워크에서 격리 된 가상 네트워크에 복구를 수행 합니다. 다른 네트워크 가상화 Dc 이동 두 가지 이점을 제공 합니다.  
  
-   숲 복구 격리 있기 때문에 발생 하는 문제가 다시 발생에서 복구 Dc 수 없습니다.  
  
-   DC 가상화 복제 중요 한 다양 한 Dc 실행 될 수 있도록 별도 네트워크에 수행 및 테스트할 수 프로덕션 네트워크에 다시 전환 전에 합니다.  
  
 Dc 물리적 하드웨어를 실행 하는 경우 여러분의 계획을 숲 루트 도메인 복원 하는 첫 번째 dc 네트워크 케이블을 분리 합니다. 가능 하면도 케이블을 분리 네트워크의 다른 모든 Dc 합니다. 실수로 숲 복구 과정에서 시작 되는 경우에의 복제, Dc 방지 합니다.  
  
 여러 위치에서 손가락을 펼치고 되는 숲, 모든 쓰기 Dc 종료 보장 하기 어려울 수 있습니다. 이러한 이유로 복구 단계-로 다시 설정 하면 컴퓨터 계정과 krbtgt 계정이 뿐만 아니라 메타 데이터 정리 같은-(경우에 숲 속의 일부는 아직 온라인) 복구 쓰기 Dc 위험한 쓰기 Dc와 복제 하지 않는 보장 하기 위한 합니다.  
  
 하지만 오프 라인 쓰기 Dc 해야만 보장할 수 복제가 발생 하지 않습니다? 따라서 가능 종료 하 고 실제로 쓰기 Dc 숲 복구 하는 동안 구분 하는 데 도움이 되는 원격 관리 기술을 배포 해야 합니다.  
  
 Rodc 계속 작동할 쓰기 Dc 오프 라인 상태일 수 있습니다. 다른 DC는 모든 RODC에서 변경 내용을 복제 직접-스키마 또는 구성 컨테이너 변경 특히,-복구 하는 동안 쓰기 Dc로 동일한 위험 심각 하지 하도록 합니다. 모든 쓰기 Dc 복구 및 온라인 후 모든 Rodc을 다시 해야 합니다.  
  
 Rodc 동시에 복구 작업이 진행 되는 동안 해당 광고주 사이트에 캐시 로컬 리소스에 액세스할 수 있도록 계속 됩니다. 캐시 RODC에 되지 않은 리소스 로컬 쓰기 DC 전달 인증 요청 해야 합니다. 이러한 요청 쓰기 Dc 오프 라인일 실패 합니다. 암호 변경 등 일부 작업 쓰기 Dc 복구할 때까지 하지 작업 수도 있습니다.  
  
 허브 스포크 네트워크 아키텍처를 사용 하는 경우에 쓰기 Dc hub 사이트에서 복구 먼저 집중할 수 있습니다. 나중에 Rodc 원격 사이트에서 다시 빌드할 수 있습니다.  
  
## <a name="next-steps"></a>다음 단계
-   [광고 숲 복구 필수](AD-Forest-Recovery-Prerequisties.md)  
-   [사용자 지정 숲 복구 계획 고안-광고 숲 복구](AD-Forest-Recovery-Devising-a-Plan.md)  
- [광고 숲 복구-문제 식별](AD-Forest-Recovery-Identify-the-Problem.md)
-   [광고 숲 복구-복구 하는 방법을 확인](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [광고 숲 복구-초기 복구](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)  
-   [광고 숲 복구-질문과 대답](AD-Forest-Recovery-FAQ.md)  
-   [광고 숲 복구-Multidomain 숲 내 단일 도메인 복구](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [광고 숲 복구-Windows Server 2003 도메인 컨트롤러 관련 숲 복구](AD-Forest-Recovery-Windows-Server-2003.md)  
