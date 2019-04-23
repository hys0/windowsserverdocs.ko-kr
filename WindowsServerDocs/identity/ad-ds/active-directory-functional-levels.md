---
ms.assetid: f964d056-11bf-4d9b-b5ab-dceaad8bfbc3
title: Windows Server 2016 기능 수준
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 10/29/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.custom: it-pro
ms.reviewer: maheshu
ms.technology: identity-adds
ms.openlocfilehash: ea56c718394d145a36145d32e5769661a62efd56
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841004"
---
# <a name="forest-and-domain-functional-levels"></a>포리스트 및 도메인 기능 수준

>적용 대상: Windows Server

기능 수준 사용 가능한 Active Directory Domain Services (AD DS) 도메인 또는 포리스트 기능을 결정합니다. 도메인 이나 포리스트의 도메인 컨트롤러에서 실행할 수 있는 Windows Server 운영 체제도 결정 합니다. 그러나 기능 수준 어떤 워크스테이션에서 실행할 수 있습니다 하는 운영 체제와 도메인 또는 포리스트에 가입 된 구성원 서버에는 적용 되지 않습니다.

AD DS를 배포 하는 경우 도메인 및 포리스트 기능 수준의 환경을 지원할 수 있는 가장 높은 값으로 설정 합니다. 이 이렇게 하면 최대한 많은 AD DS 기능을 사용할 수 있습니다. 새 포리스트를 배포할 때 포리스트 기능 수준을 설정 하 고 다음 도메인 기능 수준을 설정 하 라는 메시지가 표시 됩니다. 포리스트 기능 수준 보다 높은 값으로 도메인 기능 수준을 설정할 수 있습니다 하지만 도메인 기능 수준은 포리스트 기능 수준 보다 낮은 값으로 설정할 수 없습니다.

Windows 2003의 수명 끝을 사용 하 여 Windows 2003 도메인 컨트롤러 (Dc) 업데이트 해야 할 Windows server 2008, 2008R2, 2012, 2012R2 2016 또는 2019 합니다. 결과적으로, Windows Server 2003을 실행 하는 도메인 컨트롤러가 도메인에서 제거 해야 합니다.

Windows Server 2008 및 더 높은 도메인 기능 수준에서 서비스 DFS (분산 파일) 복제 도메인 컨트롤러 간에 SYSVOL 폴더 내용을 복제 하는 데 사용 됩니다. Windows Server 2008 도메인 기능 수준 이상의 새 도메인을 만들면 DFS 복제 SYSVOL을 복제 하는 데 자동으로 사용 됩니다. 더 낮은 기능 수준에서 도메인을 만든 경우 FRS를 사용 하 여 SYSVOL에 대 한 DFS 복제에서 마이그레이션할 해야 합니다. 마이그레이션 단계 중 하나에 따라 수는 [technet 프로시저](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx) 또는를 참조할 수 있는 [저장소 팀 파일 캐비닛 블로그 단계를 간소화](http://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx).

## <a name="windows-server-2019"></a>Windows Server 2019

새 포리스트 또는 도메인 기능 수준이이 릴리스에서 추가 없는 합니다.

Windows Server 2019 도메인 컨트롤러를 추가 하기 위해서는 최소한 Windows Server 2008R2 기능 수준입니다.

## <a name="windows-server-2016"></a>Windows Server 2016

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2019
* Windows Server 2016

### <a name="windows-server-2016-forest-functional-level-features"></a>Windows Server 2016 포리스트 기능 수준 기능

* 모든 Windows Server 2012R2 포리스트 기능 수준, 사용할 수 있는 기능 및 다음 기능을 사용할 수 있습니다.
   * [MIM Microsoft Identity Manager ()를 사용 하 여 권한 있는 액세스 관리 (PAM)](https://docs.microsoft.com/windows-server/identity/whats-new-active-directory-domain-services#a-namebkmkpamaprivileged-access-management)

### <a name="windows-server-2016-domain-functional-level-features"></a>Windows Server 2016 도메인 기능 수준 기능

* 모든 기본 Active Directory 기능, Windows Server 2012R2 도메인 기능 수준에서 모든 기능 및 다음 기능:
   * Dc에서 NTLM의 자동 배포를 지원할 수 있습니다 및 기타 사용자 계정에 암호 기반 암호 PKI 인증을 요구 하도록 구성 합니다. 이 구성은 "스마트 카드 대화형 로그온에 필요한" 라고도 하며
   * Dc는 사용자가 특정 제한 된 도메인에 가입 된 장치 허용 네트워크 NTLM을 지원할 수 있습니다.
   * PKInit 새로 고침 확장을 사용 하 여 성공적으로 인증 하는 Kerberos 클라이언트는 새로운 공용 키 id SID를 받게 됩니다.

    자세한 내용은 참조 [What's New in Kerberos Authentication](https://docs.microsoft.com/windows-server/security/kerberos/whats-new-in-kerberos-authentication) 고 [자격 증명 보호의 새로운 기능](https://docs.microsoft.com/windows-server/security/credentials-protection-and-management/whats-new-in-credential-protection)

## <a name="windows-server-2012r2"></a>Windows Server 2012R2

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2

### <a name="windows-server-2012r2-forest-functional-level-features"></a>Windows Server 2012R2 포리스트 기능 수준 기능

* 모든 Windows Server 2012에서 사용할 수 있는 기능의 포리스트 기능 수준에 있지만 더 추가 기능.

### <a name="windows-server-2012r2-domain-functional-level-features"></a>Windows Server 2012 r2 도메인 기능 수준 기능

* 모든 기본 Active Directory 기능, Windows Server 2012 도메인 기능 수준에서 모든 기능 및 다음 기능:
   * 보호 된 사용자에 대 한 DC 쪽 보호 합니다. 도메인 수를 더 이상 Windows Server 2012 R2로 인증 하는 사용자를 보호 합니다.
      * NTLM 인증을 사용 하 여 인증
      * Kerberos 사전 인증에서 DES 또는 RC4 암호 그룹 사용
      * 무제한 또는 제한 된 위임을 사용한 위임
      * 초기 4 시간 수명을 넘도록 사용자 티켓 (Tgt) 갱신
   * Authentication Policies
      * Windows Server 2012 R2 호스트를 제어 하는 도메인의 계정에 적용할 수 있는 새 포리스트 기반 Active Directory 정책 수에서 sign-on 계정과 계정으로 실행 되는 서비스 인증에 대 한 액세스 제어 조건을 적용할 합니다.
   * Authentication Policy Silos
      * 새 포리스트 기반 Active Directory 개체입니다 사용자, 관리 되는 서비스 및 컴퓨터 계정 인증 격리 또는 인증 정책에 대 한 분류 하는 데 사용할 계정 간의 관계를 만들 수 있습니다.

## <a name="windows-server-2012"></a>Windows Server 2012

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012

### <a name="windows-server-2012-forest-functional-level-features"></a>Windows Server 2012 포리스트 기능 수준 기능

* 모든 Windows Server 2008 R2에서 사용할 수 있는 기능의 포리스트 기능 수준에 있지만 더 추가 기능.

### <a name="windows-server-2012-domain-functional-level-features"></a>Windows Server 2012 도메인 기능 수준 기능

* 모든 기본 Active Directory 기능, Windows Server 2008R2 도메인 기능 수준에서 모든 기능 및 다음 기능:
   * 클레임, 복합 인증 및 Kerberos 아머 KDC 관리 템플릿 정책에 Windows Server 2012 도메인 기능 수준이 필요로 하는 두 가지 설정이 (항상 클레임 제공 및 아머 링 되지 않은 인증 요청 실패)에 대 한 KDC 지원 합니다. 자세한 내용은 참조 하세요. [Kerberos 인증의 새로운 기능](https://technet.microsoft.com/library/hh831747.aspx)

## <a name="windows-server-2008r2"></a>Windows Server 2008R2

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2

### <a name="windows-server-2008r2-forest-functional-level-features"></a>Windows Server 2008 r2 포리스트 기능 수준 기능

* Windows Server 2003 포리스트 기능 수준에서 사용할 수 있는 모든 기능과 다음과 같은 추가 기능을 제공합니다.
   * AD DS가 실행 주일 때 삭제된 개체를 전체 복원할 수 있는 기능을 제공하는 Active Directory 휴지통

### <a name="windows-server-2008r2-domain-functional-level-features"></a>Windows Server 2008 r2 도메인 기능 수준 기능

* 모든 기본 Active Directory 기능, Windows Server 2008 도메인 기능 수준에서 모든 기능 및 다음 기능:
   * 각 사용자의 Kerberos 토큰 내에서 도메인 사용자를 인증하는 데 사용되는 로그온 방법 유형(스마트 카드 또는 사용자 이름/암호)에 대한 정보가 포함된 인증 메커니즘 보증. Active Directory Federation Services (AD FS)와 같은 페더레이션된 id 관리 인프라를 배포한 네트워크 환경에서이 기능이 설정 된 경우 토큰의 정보 다음 추출할 수는 사용자가 액세스 하려고 할 때마다 사용자 로그온 방법을 기준으로 하는 권한 부여를 확인 하려면 개발 된 클레임 인식 응용 프로그램입니다.
   * 이름 또는 DNS 호스트 이름을 컴퓨터 계정 변경 하는 경우 관리 서비스 계정의 컨텍스트 내에서 특정 컴퓨터에서 실행 되는 서비스에 대 한 자동 SPN 관리 합니다. 관리 서비스 계정에 대 한 자세한 내용은 참조 하세요. [서비스 계정 단계별 가이드](https://go.microsoft.com/fwlink/?LinkId=180401)합니다.

## <a name="windows-server-2008"></a>Windows Server 2008

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008

### <a name="windows-server-2008-forest-functional-level-features"></a>Windows Server 2008 포리스트 기능 수준 기능

* 모든 Windows Server 2003 포리스트 기능 수준에서 사용할 수 있는 기능 이지만 추가 기능은 제공 하지 사용할 수 있습니다. 

### <a name="windows-server-2008-domain-functional-level-features"></a>Windows Server 2008 도메인 기능 수준 기능

* 모든 기본 AD DS 기능을 모든 Windows Server 2003 도메인 기능 수준에서 기능 및 다음 기능은 사용할 수 있습니다.
   * 분산된 파일 시스템 (DFS) 복제 Windows Server 2003 시스템 볼륨 (SYSVOL)에 대 한 지원
      * DFS 복제 지원 SYSVOL 내용의 보다 강력 하 고 세부적인 복제를 제공합니다.
        [!NOTE]>
        >Windows Server 2012 R2 부터는 파일 복제 서비스 FRS () 사용 되지 않습니다. 이상을 실행 하는 도메인 컨트롤러에서 만들어진 새 도메인을 Windows Server 2012 R2 Windows Server 2008 도메인 기능 수준 이상으로 설정 되어야 합니다.

   * 도메인 기반 DFS 네임 스페이스 액세스 기반 열거 및 향상 된 확장성에 대 한 지원을 포함 하는 Windows Server 2008 모드에서 실행 합니다. Windows Server 2008 모드에서 도메인 기반 네임 스페이스는 Windows Server 2003 포리스트 기능 수준을 사용 하려면 포리스트의 필요 합니다. 자세한 내용은 [Namespace 유형을 선택](https://go.microsoft.com/fwlink/?LinkId=180400)합니다.
   * Kerberos 프로토콜에 대 한 고급 암호화 표준 (AES 128 및 AES 256) 지원입니다. AES를 사용 하 여 발급 되는 Tgt에 대 한 순서 대로 도메인 기능 수준이 Windows Server 2008 이상 이어야 합니다. 및 도메인 암호를 변경 해야 합니다. 
      * 자세한 내용은 [Kerberos 기능이 향상](https://technet.microsoft.com/library/cc749438(ws.10).aspx)합니다.
        [!NOTE]>
        >인증 오류가 발생할 수 있습니다 도메인 컨트롤러에서 Windows Server 2008 이상 도메인 기능 수준을 발생 한 후 도메인 컨트롤러가 이미 DFL 변경 복제 되지만 아직 krbtgt 암호 새로 고쳐지지 않았습니다. 이 경우 도메인 컨트롤러에서 KDC 서비스를 다시 시작 되며 새 krbtgt 암호의 메모리에 새로 고침을 트리거할 관련된 인증 오류를 해결 합니다.

   * [대화형 로그온 마지막](https://go.microsoft.com/fwlink/?LinkId=180387) 정보에는 다음 정보가 표시 됩니다.
      * 도메인에 가입 된 Windows Server 2008 서버 또는 Windows Vista 워크스테이션에서 실패 한 로그온 시도의 총 수
      * Windows Vista 워크스테이션 또는 Windows Server 2008 서버에 성공적으로 로그온 한 후 실패 한 로그온 시도의 총 수
      * Windows Server 2008 또는 Windows Vista 워크스테이션에서 마지막 실패 한 로그온 시도의 시간
      * Windows Server 2008 서버 또는 Windows Vista 워크스테이션에서 마지막으로 성공한 로그온 시간을 시도 합니다.
   * 세분화 된 암호 정책을 사용 하면 도메인의 사용자 및 글로벌 보안 그룹에 대 한 암호 및 계정 잠금 정책을 지정할 수 있습니다. 자세한 내용은 [세분화 된 암호 및 계정 잠금 정책 구성에 대 한 단계별 가이드](https://go.microsoft.com/fwlink/?LinkID=91477)합니다.
   * 개인용 가상 데스크톱
      * Active Directory 사용자 및 컴퓨터에서 사용자 계정 속성 대화 상자에서 개인 가상 데스크톱 탭에서 제공 하는 추가 기능을 사용 하려면 Windows Server 2008 R2 용 AD DS 스키마를 확장 (스키마 개체 버전 = 47). 자세한 내용은 [를 사용 하 여 RemoteApp 및 데스크톱 연결 단계별 가이드에서 개인용 가상 데스크톱 배포](https://go.microsoft.com/fwlink/?LinkId=183552)합니다.

## <a name="windows-server-2003"></a>Windows Server 2003

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003

### <a name="windows-server-2003-forest-functional-level-features"></a>Windows Server 2003 포리스트 기능 수준 기능

* 모든 AD DS 기본 기능과 다음 기능을 사용할 수 있습니다.
   * 포리스트 트러스트
   * 도메인 이름 바꾸기
   * 연결 된 값 복제
      - 연결 된 값 복제에서 저장 하 고 전체 구성원을 단일 단위로 복제 하는 대신 개별 멤버에 대 한 값을 복제 그룹 구성원을 변경할 수 있습니다. 저장 하 고 개별 멤버의 값을 복제 네트워크 대역폭을 덜 및 복제 하는 동안 프로세서 사이클을 적게 사용 하 여 있으며 추가 하거나 여러 도메인 컨트롤러에서 동시에 여러 멤버를 제거 하면 업데이트 손실 방지할 수 있습니다.
   * 읽기 전용 도메인 컨트롤러 (RODC)를 배포 하는 기능
   * 지식 일관성 검사기 (KCC) 알고리즘 및 확장성 향상
      - 사이트 간 토폴로지 생성기 ISTG ()는 AD DS는 Windows 2000 포리스트 기능 수준에서 지원할 수 있는 수보다 더 많은 사이트를 사용 하 여 포리스트를 지원 하도록 확장할 수 있는 향상 된 알고리즘을 사용 합니다. 향상 된 ISTG 선택 알고리즘에는 Windows 2000 포리스트 기능 수준에서 ISTG 선택 하기 위한 덜 침입적 인 메커니즘입니다.
   * 라는 동적 보조 클래스의 인스턴스를 만들 수 있습니다 **dynamicObject** 도메인 디렉터리 파티션에
   * 변환할 수 있습니다는 **inetOrgPerson** 개체 인스턴스를 **사용자** 개체 인스턴스 및 반대 방향으로 변환을 완료 하려면
   * 역할 기반 권한 부여를 지원 하도록 새로운 그룹 유형의 인스턴스를 만들 수 있습니다. 
      - 이러한 형식은 응용 프로그램 기본 그룹 및 LDAP 쿼리 그룹 이라고 합니다.
   * 스키마에 포함된 특성 및 클래스의 비활성화 및 다시 정의 다음 특성을 다시 사용할 수 있습니다: ldapDisplayName, schemaIdGuid, OID 및 mapiID 합니다.
   * 도메인 기반 DFS 네임 스페이스 액세스 기반 열거 및 향상 된 확장성에 대 한 지원을 포함 하는 Windows Server 2008 모드에서 실행 합니다. 자세한 내용은 [Namespace 유형을 선택](https://go.microsoft.com/fwlink/?LinkId=180400)합니다.

### <a name="windows-server-2003-domain-functional-level-features"></a>Windows Server 2003 도메인 기능 수준 기능

* 모든 기본 AD DS 기능, Windows 2000 기본 도메인 기능 수준에서 사용할 수 있는 모든 기능 및 다음 기능이 제공 됩니다.
   * 도메인 관리 도구인 Netdom.exe 도메인 컨트롤러의 이름을 바꿀 수 있도록 하는
   * 로그온 타임 스탬프 업데이트
      * **lastLogonTimestamp** 특성이 사용자 또는 컴퓨터의 마지막 로그온 시간으로 업데이트됩니다. 이 특성은 도메인 내에서 복제됩니다.
   * 설정 하는 기능을 **userPassword** 유효한 암호로 특성 **inetOrgPerson** 과 사용자 개체
   * 사용자 및 컴퓨터를 리디렉션할 수 컨테이너
      * 기본적으로 컴퓨터 및 사용자 계정을 보유할 수 있도록 두 개의 잘 알려진 컨테이너가 나와 즉, cn = 컴퓨터,<domain root> 와 cn = Users,<domain root>합니다. 이 기능에는 이러한 계정에 대 한 잘 알려진 새 위치를 정의할 수 있습니다.
   * 권한 부여 관리자에 대 한 권한 부여 정책을 AD DS에 저장할 수 있는 기능
   * 제한된 위임
      * 제한 된 위임을 활용 하기 위해 사용자 자격 증명의 보안 위임을 Kerberos 기반 인증을 사용 하 여 응용 프로그램에 대 한 수 있습니다.
      * 특정 대상 서비스에 대 한 위임을 제한할 수 있습니다.
   * 선택적 인증
      * 선택적 인증 하면 사용자와 트러스팅 포리스트의 리소스 서버를 인증할 수 있도록 허용 된 트러스트 된 포리스트의 그룹을 지정 하는 것이 가능 합니다.

## <a name="windows-2000"></a>Windows 2000

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003
* Windows 2000

### <a name="windows-2000-native-forest-functional-level-features"></a>Windows 2000 네이티브 포리스트 기능 수준 기능

* 기본 AD DS 기능을 모두 사용할 수 있습니다.

### <a name="windows-2000-native-domain-functional-level-features"></a>Windows 2000 기본 도메인 기능 수준 기능

* 기본 AD DS 기능 및 다음 디렉터리 기능 모두 포함 하 여 사용할 수 있습니다.
   * 배포와 보안 그룹에 대 한 유니버설 그룹입니다.
   * 그룹 중첩
   * 보안 및 배포 그룹 사이 변환할 수 있는 그룹 변환
   * 보안 식별자 (SID) 기록

## <a name="next-steps"></a>다음 단계

* [도메인 기능 수준 올리기](https://technet.microsoft.com/library/cc753104.aspx)  
* [포리스트 기능 수준 올리기](https://technet.microsoft.com/library/cc730985.aspx)
