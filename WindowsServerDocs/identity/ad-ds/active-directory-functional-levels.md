---
ms.assetid: f964d056-11bf-4d9b-b5ab-dceaad8bfbc3
title: "Windows Server 2016 기능 수준"
description: 
author: MicrosoftGuyJFlo
ms.author: joflore
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.custom: it-pro
ms.reviewer: maheshu
ms.technology: identity-adds
ms.openlocfilehash: a39955cf088ce7ce8bef20c70b83d49c6d508497
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="forest-and-domain-functional-levels"></a>숲 및 도메인 기능 수준

>Windows Server에 적용 됩니다.

Windows 2003의 끝으로 Windows 2003 Dc (도메인 컨트롤러) Windows Server 2008, 2012 또는 2016로 업데이트 해야 합니다. 결과적으로, Windows Server 2003을 실행 하는 도메인 컨트롤러에서 도메인 제거 해야 합니다. 도메인 및 숲 기능 수준을 기울여야 최소한의 환경에 추가 되지 이전 버전의 Windows Server를 실행 하는 도메인 컨트롤러를 방지 하기 위해 Windows Server 2008 합니다.

고객 해당 도메인 기능 수준을 (DFL) 및 기능 수준 숲 (FFL)이의 일부로 업데이트를 릴리스 2003 DFL 및 FFL 되지 Windows Server 2016에 포함 되는 더 이상 지원 되지 나중에 것이 좋습니다.

자녀가 DFL 및 2003에서 FFL 이동 평가 하는 데 추가 시간이 필요한 하는 고객 2003 DFL 및 FFL는 계속 해 서 Windows 10에서는 지원 될 것 이며 Windows Server 2016은 Windows Server 2008, 2008R2, 도메인 및 숲 속의 모든 도메인 컨트롤러 제공 2012R2, 2012 2016 또는 합니다.

Windows Server 2008 및 높은 도메인 기능 수준에서 배포 서비스 (DFS 파일) 복제 SYSVOL 폴더 내용 도메인 컨트롤러 간에 복제 하는 데 사용 됩니다. Windows Server 2008 도메인 기능 수준을 이상 새 도메인 만들면 DFS 복제 SYSVOL 복제할 자동으로 사용 됩니다. 낮은 기능 수준 도메인을 만든 경우 FRS DFS 복제 sysvol를 사용 하 여 마이그레이션을 해야 합니다. 마이그레이션 단계에 따라 중 하나 수 있습니다는 [technet 절차](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx) 하거나를 참조할 수는 [저장소 팀 생겼습니다 블로그에서 단계 효율성을 높였습니다](http://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx)합니다.

Windows Server 2003 도메인 및 숲 기능 수준 계속 지원 될 수 있지만 조직 기능 수준을 (또는 이상 가능한 경우) Windows Server 2008를 발생 시켜 SYSVOL 복제 호환 되도록 하는 앞으로 지원 합니다. 또한, 그 외 여러 혜택와 기능 사용할 수 있는 방법이 클수록 높은 기능 수준에서 합니다. 다음 리소스에 대 한 자세한 내용 보려면

## <a name="windows-server-2016"></a>Windows Server 2016

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2016

### <a name="windows-server-2016-forest-functional-level-features"></a>Windows Server 2016 숲 수준 기능

* 모든는 Windows Server 2012R2 숲 기능 수준에서 사용할 수 있는 기능 및 다음과 같은 기능을 사용할 수 있습니다.
    * [권한 관리 (PAM) Microsoft Identity Manager (MIM)를 사용 하 여 액세스] (https://docs.microsoft.com/windows-server/identity/what's-new-active-directory-domain-services#a-namebkmkpamaprivileged-access-management)

### <a name="windows-server-2016-domain-functional-level-features"></a>Windows Server 2016 도메인 수준 기능

* 모든 기본 Active Directory 기능, Windows Server 2012R2 도메인 기능 수준의 모든 기능 및 다음과 같은 기능:
    * Dc 공개 키만 사용자의 NTLM 비밀 배포 지원할 수 있습니다. 
    * 사용자는 특정으로 제한 도메인에 가입 장치 Dc 수 있도록 네트워크 NTLM 지원할 수 있습니다. 
    * 성공적으로 인증 PKInit 새로 고침 확장 된 Kerberos 클라이언트 신선한 공개 키 id SID 얻게 됩니다.

    자세한 내용은 참조 [Kerberos 인증의 새로운](https://docs.microsoft.com/windows-server/security/kerberos/whats-new-in-kerberos-authentication) 및 [자격 증명 보호의 새로운 기능](https://docs.microsoft.com/windows-server/security/credentials-protection-and-management/whats-new-in-credential-protection)

## <a name="windows-server-2012r2"></a>Windows Server 2012R2

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2016
* Windows Server 2012 r 2

### <a name="windows-server-2012r2-forest-functional-level-features"></a>Windows Server 2012R2 숲 기능 수준 기능

* Windows Server 2012에서 사용할 수 있는 기능을 모두 포리스트에 했지만 더 추가 기능입니다.

### <a name="windows-server-2012r2-domain-functional-level-features"></a>Windows Server 2012R2 도메인 수준 기능

* 모든 기본 Active Directory 기능, Windows Server 2012 도메인 기능 수준에서 일부 기능 및 다음과 같은 기능:
    * DC 측 보호 사용자를 보호 합니다. 사용자가 인증 하는 Windows Server 2012 R2 도메인 더 이상 수 보호:
        * 인증 된 NTLM 인증
        * Kerberos 미리 인증에서 DES 또는 r c 4 암호 그룹을 사용 하 여
        * 무제한 또는 제한 된 위임와 위임
        * 초기 4 시간 수명 이상의 사용자 티켓 (Tgt) 갱신
    * 인증 정책
        * 어떤 호스트 제어 하기 위해 Windows Server 2012 R2 도메인에 있는 계정에 적용할 수 있는 새 숲 기반 Active Directory 정책을 계정을 수 sign-on에서 및 인증에 대 한 액세스를 제어 조건 계정으로 실행 되는 서비스에 적용 합니다.
    * 인증 정책 사일로
        * Active Directory 개체 새 숲 기반-사용자, 관리 되는 서비스와 컴퓨터 인증 격리 또는 인증 정책에 대 한 계정을 분류 하는 데 사용할 계정을 관계를 만들 수 있습니다.

## <a name="windows-server-2012"></a>Windows Server 2012

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2016
* Windows Server 2012 r 2
* Windows Server 2012

### <a name="windows-server-2012-forest-functional-level-features"></a>Windows Server 2012 숲 수준 기능

* Windows Server 2008 r 2에 사용할 수 있는 기능을 모두 포리스트에 했지만 더 추가 기능입니다.

### <a name="windows-server-2012-domain-functional-level-features"></a>Windows Server 2012 도메인 수준 기능

* 모든 기본 Active Directory 기능, Windows Server 2008R2 도메인 기능 수준의 모든 기능 및 다음과 같은 기능:
    * KDC는 클레임, 복합 인증 및 Kerberos armoring KDC 관리 템플릿 정책에 Windows Server 2012 도메인 기능 수준 해야 하는 두 가지 설정이 (항상 클레임 제공 하 고 무방비 인증 요청이 실패)에 대 한 지원 합니다. 자세한 내용은 참조 [Kerberos 인증의 새로운](https://technet.microsoft.com/en-us/library/hh831747.aspx)

## <a name="windows-server-2008r2"></a>Windows Server 2008R2

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2016
* Windows Server 2012 r 2
* Windows Server 2012
* Windows Server 2008 R2

### <a name="windows-server-2008r2-forest-functional-level-features"></a>Windows Server 2008R2 숲 기능 수준 기능

* Windows Server 2003에 사용할 수 있는 기능을 모두 포리스트 기능 수준 이용 다음과 같은 기능:
    * Active Directory 휴지통, AD DS 실행 되는 동안 삭제 개체 전체적으로 복원 하는 기능을 제공 하는 합니다.

### <a name="windows-server-2008r2-domain-functional-level-features"></a>Windows Server 2008R2 도메인 수준 기능

* 모든 기본 Active Directory 기능, Windows Server 2008 도메인 기능 수준에서 일부 기능 및 다음과 같은 기능:
    * 로그온 하는 방법입니다 (스마트 카드 또는 사용자 이름/암호) 도메인 사용자 내에서 각 사용자 Kerberos 토큰 인증 하는 데 사용 형식에 대 한 정보가 포함 된 인증 메커니즘 보증 합니다. AD FS(Active Directory Federation Services) 등 연합된 id 관리 인프라를 배포한 네트워크 환경에서이 기능을 활성화 하면 사용자 클레임 인식 사용자의 로그온 방법에 따라 권한을 확인 하려면 개발 된 응용 프로그램에 액세스 하려고 할 때마다 토큰에서 정보 추출 다음 수 있습니다.
    * 컴퓨터 계정 변경의 이름을 개최 된 이름 또는 DNS 때 관리 서비스 계정에서 특정 컴퓨터에서 실행 되는 서비스에 대 한 자동 SPN 관리 합니다. 관리 서비스 계정에 대 한 자세한 내용은 참조 [서비스 계정 Step-by-Step 가이드](https://go.microsoft.com/fwlink/?LinkId=180401)합니다.

## <a name="windows-server-2008"></a>Windows Server 2008

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2016
* Windows Server 2012 r 2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008

### <a name="windows-server-2008-forest-functional-level-features"></a>Windows Server 2008 숲 수준 기능

* Windows Server 2003 숲 기능 수준에서 사용할 수 있는 기능을 모두 하지만 추가 기능 없음 사용할 수 있습니다. 

### <a name="windows-server-2008-domain-functional-level-features"></a>Windows Server 2008 도메인 수준 기능

* 모든 기본 AD DS 기능, Windows Server 2003 도메인 기능 수준의 기능을 모두 및 다음과 같은 기능을 사용할 수 있습니다.
    * 분산된 파일 시스템 (DFS) 복제 Windows Server 2003 시스템 볼륨 (SYSVOL)에 대 한 지원
        * DFS 복제 지원 더 강력 하 고 자세 복제 SYSVOL 콘텐츠를 제공합니다.
        [!NOTE]>
        >Windows Server 2012 r 2 부터는 파일 FRS (복제 서비스) 사용 되지 않습니다. 이상 실행 하는 도메인 컨트롤러에서 생성 되는 새로운 도메인 Windows Server 2012 r 2는 Windows Server 2008 도메인 기능 수준으로 이상 설정 해야 합니다.

    * 따라 도메인 DFS 네임 스페이스 액세스 기반 정책과 확장성에 대 한 지원을 포함 하는 Windows Server 2008 모드에서 실행 됩니다. Windows Server 2008 모드로 도메인 기반 네임은 또한 Windows Server 2003 숲 기능 수준을 사용 하려면 숲이 필요 합니다. 자세한 내용은 참조 [Namespace 유형 선택](https://go.microsoft.com/fwlink/?LinkId=180400)합니다.
    * 고급 Kerberos 프로토콜에 대 한 암호화 표준 (AES 128 및 AES 256) 지원 합니다. AES 사용 하 여 발급 Tgt 도메인 기능 수준 Windows Server 2008 이상 이어야 합니다 하 고 도메인 암호를 변경 해야 합니다. 
        * 자세한 내용은 참조 [Kerberos 향상](https://technet.microsoft.com/library/cc749438(ws.10).aspx)합니다.
        [!NOTE]>
        >인증 오류가 발생할 수 있습니다 도메인 컨트롤러에서 Windows Server 2008 이상 도메인 기능 수준을 발생 한 후 도메인 컨트롤러 DFL 변경 이미 복제에 있지만 아직 새로 고치지 krbtgt 암호입니다. 이 경우 도메인 컨트롤러에 KDC 서비스를 다시 시작 되며 krbtgt 새 암호의 메모리에 새로 트리거하 관련된 인증 오류를 해결 합니다.

    * [대화형 로그온 마지막](https://go.microsoft.com/fwlink/?LinkId=180387) 정보는 다음과 같은 정보가 표시 됩니다.
        * 도메인 가입 Windows Server 2008 서버 또는 Windows Vista 워크스테이션 로그온 실패 총
        * 총 실패 로그온 시도가 Windows Server 2008 서버 또는 Windows Vista 워크스테이션 성공적인 로그온 한 후
        * 지난 실패 로그온 시도가 Windows Server 2008 또는 Windows Vista 워크스테이션 시간
        * 마지막으로 성공한 로그온 시간 서버 Windows Server 2008 또는 Windows Vista 워크스테이션 시도
    * 정교한 암호 정책을 확인 도메인에서 암호 및 계정 잠금 정책을 사용자 및 그룹 글로벌 보안에 대 한 지정할 수 있습니다. 자세한 내용은 참조 [세분화 암호 및 사용자 계정 잠금 정책 구성에 대 한 단계별 가이드](https://go.microsoft.com/fwlink/?LinkID=91477)합니다.
    * 개인 가상 데스크톱
        * Windows Server 2008 r 2에 대 한 추가 해야 AD DS 스키마 Active Directory 사용자 및 컴퓨터 사용자 계정 속성 대화 상자에서 가상 데스크톱 개인 탭 하 여 제공 되는 추가 기능을 사용 하려면 (스키마 개체 버전 47 =). 자세한 내용은 참조 [데스크톱 연결 RemoteApp 사용 하 여 개인 가상 데스크톱 배포 Step-by-Step 가이드](https://go.microsoft.com/fwlink/?LinkId=183552)합니다.

## <a name="windows-server-2003"></a>Windows Server 2003

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2012 r 2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003

### <a name="windows-server-2003-forest-functional-level-features"></a>Windows Server 2003 숲 기능 수준 기능

* 기본 AD DS 기능 및 다음과 같은 기능을 모두 사용할 수 있습니다.
    * 숲 보안
    * 도메인 이름 바꾸기
    * 연결 된 값 복제
        - 연결 된 값 복제 저장 하 고 개별 구성원은 하나의 단위로 전체 구성원 복제 하는 대신에 대 한 값 복제 그룹 구성원을 변경할 수 있습니다. 저장 하 고 개별 회원 값 복제 네트워크 대역폭을 덜 및를 복제 하는 동안 적은 프로세서 주기를 사용 하 고 사용자를 추가 하거나 제거 여러 도메인 컨트롤러에서 동시에 여러 회원 때 업데이트 손실 하지 않도록 합니다.
    * 읽기 전용 도메인 컨트롤러 (RODC)를 배포 하는 기능
    * 향상 된 알고리즘 기술 검사기 KCC (일관성) 및 확장성
        - 간 토폴로지 generator (ISTG) AD DS Windows 2000 숲 기능 수준 지원할 수 있는 것 보다 더 많은 수의 사이트와 숲 지원 하 게 크기가 조정 하는 향상 된 알고리즘을 사용 합니다. Windows 2000 숲 기능 수준 ISTG 선택 하기 위한 덜 침입 장치가 개선 된 ISTG 선거 알고리즘이입니다.
    * 라는 동적 보조 클래스 인스턴스 만들 수 **dynamicObject** 도메인 디렉터리 파티션에
    * 변환할 수 있는 **inetOrgPerson** 개체 인스턴스도는 **사용자** 개체 인스턴스 반대 방향으로 변환 완료 하 고
    * 새 그룹 종류 역할 기반 인증을 지원 하기 위해 인스턴스를 만들 수 있습니다. 
        - 이러한 종류 기본 그룹 응용 프로그램 및 LDAP 쿼리 그룹 이라고 합니다.
    * 비활성화 및 특성과 스키마에서 클래스 재정의 합니다. 다음과 같은 특성을 다시 사용할 수 있습니다: ldapDisplayName 재 OID, 활성화할 수 없습니다 mapiID 하 고 있습니다.
    * 따라 도메인 DFS 네임 스페이스 액세스 기반 정책과 확장성에 대 한 지원을 포함 하는 Windows Server 2008 모드에서 실행 됩니다. 자세한 내용은 참조 [Namespace 유형 선택](https://go.microsoft.com/fwlink/?LinkId=180400)합니다.

### <a name="windows-server-2003-domain-functional-level-features"></a>Windows Server 2003 도메인 수준 기능

* 기본 AD DS 기능, Windows 2000 네이티브 도메인 기능 수준에서 사용할 수 있는 모든 기능 및 다음과 같은 기능을 사용할 수 있습니다.
    * Netdom.exe 도메인 컨트롤러의 이름을 바꾸려면 수 있게 하는 도메인 관리 도구
    * 로그온 타임 스탬프 업데이트
        * **최종 로그온 시간 스탬프** 특성 사용자 또는 컴퓨터의 마지막 로그온 시간으로 업데이트 됩니다. 이 특성 도메인 내 복제 됩니다.
    * 설정 하는 기능은 **유효성** 효과적인 암호도 특성 **inetOrgPerson** 사용자 개체와
    * 사용자가 및 컴퓨터를 이동 하는 기능 컨테이너
        * 기본적으로 유명 두 컨테이너 주택 컴퓨터와 사용자 계정에 대 한 제공 cn 즉, 컴퓨터 =<domain root> 및 cn = 사용자를<domain root>합니다. 이 기능을 사용 하면 해당이 계정에 대 한 새로운, 유명 위치 정의 합니다.
    * 권한 관리자에 대 한 권한 정책 AD DS에 저장 하는 기능
    * 제한 된 위임
        * 제한 된 위임 Kerberos 기반 인증을 사용 하 여 안전 하 게 위임 사용자 자격 증명을 이용 하도록 응용 프로그램에 대 한 수 있습니다.
        * 특정 대상 서비스에만 위임을 제한할 수 있습니다.
    * 선택 인증
        * 선택 인증 하면은 사용자 및 그룹 신뢰할 수 있는 숲 속의 신뢰 숲 속의 리소스 서버 인증을 허용을 지정할 수 있습니다.

## <a name="windows-2000"></a>Windows 2000

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003
* Windows 2000

### <a name="windows-2000-native-forest-functional-level-features"></a>Windows 2000 기본 숲 기능 수준 기능

* 기본 AD DS 기능을 모두 사용할 수 있습니다.

### <a name="windows-2000-native-domain-functional-level-features"></a>Windows 2000 기본 도메인 수준 기능

* 기본 AD DS 기능과 다음 디렉터리 기능 모두 포함 하 여 사용할 수 있습니다.
    * 메일 및 보안 그룹에 대 한 그룹 유니버설 합니다.
    * 그룹 중첩
    * 보안 및 메일 그룹 간에 변환할 수 있는 그룹 변환
    * 보안 SID (식별자) 기록

## <a name="next-steps"></a>다음 단계

* [도메인 기능 수준을](https://technet.microsoft.com/library/cc753104.aspx)  
* [숲 기능 수준 높이기](https://technet.microsoft.com/library/cc730985.aspx)
