---
ms.assetid: f964d056-11bf-4d9b-b5ab-dceaad8bfbc3
title: Windows Server 2016 기능 수준
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 10/29/2018
ms.topic: article
ms.prod: windows-server
ms.custom: it-pro
ms.reviewer: maheshu
ms.technology: identity-adds
ms.openlocfilehash: 7f16d58eb6c5074c75f49ba7936c4d312a3dbda4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390982"
---
# <a name="forest-and-domain-functional-levels"></a>포리스트 및 도메인 기능 수준

>적용 대상: Windows Server

기능 수준은 사용 가능한 Active Directory Domain Services (AD DS) 도메인 또는 포리스트 기능을 결정 합니다. 또한 도메인 또는 포리스트의 도메인 컨트롤러에서 실행할 수 있는 Windows Server 운영 체제를 결정 합니다. 그러나 기능 수준은 도메인 이나 포리스트에 가입 된 워크스테이션 및 구성원 서버에서 실행할 수 있는 운영 체제에 영향을 주지 않습니다.

AD DS를 배포할 때 도메인 및 포리스트 기능 수준을 사용자 환경에서 지원할 수 있는 가장 높은 값으로 설정 합니다. 이러한 방식으로 가능한 한 많은 AD DS 기능을 사용할 수 있습니다. 새 포리스트를 배포 하는 경우 포리스트 기능 수준을 설정 하 라는 메시지가 표시 된 다음 도메인 기능 수준을 설정 하 라는 메시지가 표시 됩니다. 도메인 기능 수준을 포리스트 기능 수준 보다 높은 값으로 설정할 수 있지만 도메인 기능 수준을 포리스트 기능 수준 보다 낮은 값으로 설정할 수는 없습니다.

Windows 2003의 기간이 끝나면 windows 2003 Dc (도메인 컨트롤러)를 Windows Server 2008, 2008 R2, 2012, 2012R2, 2016 또는 2019로 업데이트 해야 합니다. 결과적으로, Windows Server 2003을 실행 하는 도메인 컨트롤러가 도메인에서 제거 해야 합니다.

Windows Server 2008 및 더 높은 도메인 기능 수준에서 서비스 DFS (분산 파일) 복제 도메인 컨트롤러 간에 SYSVOL 폴더 내용을 복제 하는 데 사용 됩니다. Windows Server 2008 도메인 기능 수준 이상의 새 도메인을 만들면 DFS 복제 SYSVOL을 복제 하는 데 자동으로 사용 됩니다. 더 낮은 기능 수준에서 도메인을 만든 경우 FRS를 사용 하 여 SYSVOL에 대 한 DFS 복제에서 마이그레이션할 해야 합니다. 마이그레이션 단계 중 하나에 따라 수는 [technet 프로시저](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx) 또는를 참조할 수 있는 [저장소 팀 파일 캐비닛 블로그 단계를 간소화](http://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx).

## <a name="windows-server-2019"></a>Windows Server 2019

이 릴리스에는 새로운 포리스트 또는 도메인 기능 수준이 추가 되지 않았습니다.

Windows Server 2019 도메인 컨트롤러를 추가 하기 위한 최소 요구 사항은 Windows Server 2008 기능 수준입니다. 또한 도메인은 SYSVOL을 복제 하는 엔진으로 DFS를 사용 해야 합니다.

## <a name="windows-server-2016"></a>Windows Server 2016

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2019
* Windows Server 2016

### <a name="windows-server-2016-forest-functional-level-features"></a>Windows Server 2016 포리스트 기능 수준 기능

* Windows Server 2012R2 포리스트 기능 수준에서 사용할 수 있는 모든 기능과 다음 기능을 사용할 수 있습니다.
   * [MIM (권한 있는 액세스 관리)을 Microsoft Identity Manager 사용한 PAM (권한 있는 액세스 관리)](https://docs.microsoft.com/windows-server/identity/whats-new-active-directory-domain-services#a-namebkmkpamaprivileged-access-management)

### <a name="windows-server-2016-domain-functional-level-features"></a>Windows Server 2016 도메인 기능 수준 기능

* 모든 기본 Active Directory 기능, Windows Server 2012R2 도메인 기능 수준에서 제공 되는 모든 기능 및 다음 기능이 있습니다.
   * Dc는 PKI 인증을 요구 하도록 구성 된 사용자 계정에서 NTLM 및 기타 암호 기반 암호의 자동 롤링을 지원할 수 있습니다. 이 구성을 "대화형 로그온에 필요한 스마트 카드" 라고도 합니다.
   * 사용자가 특정 도메인에 가입 된 장치로 제한 되 면 Dc에서 네트워크 NTLM을 허용 하도록 지원할 수 있습니다.
   * Kerberos 클라이언트에서 PKInit Freshness Extension으로 성공적으로 인증 하면 새로운 공개 키 id SID를 가져옵니다.

    자세한 내용은 [Kerberos 인증의 새로운 기능](https://docs.microsoft.com/windows-server/security/kerberos/whats-new-in-kerberos-authentication) 및 [자격 증명 보호의 새로운](https://docs.microsoft.com/windows-server/security/credentials-protection-and-management/whats-new-in-credential-protection) 기능을 참조 하세요.

## <a name="windows-server-2012r2"></a>Windows Server 2012R2

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2

### <a name="windows-server-2012r2-forest-functional-level-features"></a>Windows Server 2012R2 포리스트 기능 수준 기능

* Windows Server 2012 포리스트 기능 수준에서 사용할 수 있는 모든 기능을 제공 하지만 추가 기능은 제공 하지 않습니다.

### <a name="windows-server-2012r2-domain-functional-level-features"></a>Windows Server 2012R2 도메인 기능 수준 기능

* 모든 기본 Active Directory 기능, Windows Server 2012 도메인 기능 수준에서 제공 되는 모든 기능 및 다음 기능이 있습니다.
   * 보호 된 사용자에 대 한 DC 쪽 보호. Windows Server 2012 R2 도메인을 인증 하는 보호 된 사용자는 더 이상 다음을 수행할 수 없습니다.
      * NTLM 인증을 사용 하 여 인증
      * Kerberos 사전 인증에서 DES 또는 RC4 암호 그룹 사용
      * 제한 없는 위임 또는 제한 된 위임을 사용 하 여 위임
      * 초기 4 시간 동안 사용자 티켓 (Tgt) 갱신
   * Authentication Policies
      * Windows Server 2012 R2 도메인의 계정에 적용 하 여 계정이 로그온 할 수 있는 호스트를 제어 하 고 계정으로 실행 되는 서비스에 대 한 인증을 위한 액세스 제어 조건을 적용할 수 있는 새로운 포리스트 기반 Active Directory 정책입니다.
   * Authentication Policy Silos
      * 사용자, 관리 서비스 및 컴퓨터 간에 관계를 만들 수 있는 새 포리스트 기반 Active Directory 개체입니다 .이 개체는 인증 정책 또는 인증 격리를 위해 계정을 분류 하는 데 사용 됩니다.

## <a name="windows-server-2012"></a>Windows Server 2012

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012

### <a name="windows-server-2012-forest-functional-level-features"></a>Windows Server 2012 포리스트 기능 수준 기능

* Windows Server 2008 R2 포리스트 기능 수준에서 사용할 수 있는 모든 기능 이지만 추가 기능은 없습니다.

### <a name="windows-server-2012-domain-functional-level-features"></a>Windows Server 2012 도메인 기능 수준 기능

* 모든 기본 Active Directory 기능, Windows Server 2008 R2 도메인 기능 수준에서 제공 되는 모든 기능 및 다음 기능이 있습니다.
   * 클레임, 복합 인증 및 Kerberos 아머 링 (armoring)에 대 한 KDC 지원 KDC 관리 템플릿 정책에는 Windows Server 2012 도메인 기능 수준을 필요로 하는 두 개의 설정 (항상 클레임 제공 및 아머 링 해제 인증 요청 실패)이 있습니다. 자세한 내용은 [Kerberos 인증의 새로운 기능](https://technet.microsoft.com/library/hh831747.aspx) 을 참조 하세요.

## <a name="windows-server-2008r2"></a>Windows Server 2008 R2

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2

### <a name="windows-server-2008r2-forest-functional-level-features"></a>Windows Server 2008 R2 포리스트 기능 수준 기능

* Windows Server 2003 포리스트 기능 수준에서 사용할 수 있는 모든 기능과 다음과 같은 추가 기능을 제공합니다.
   * AD DS가 실행 주일 때 삭제된 개체를 전체 복원할 수 있는 기능을 제공하는 Active Directory 휴지통

### <a name="windows-server-2008r2-domain-functional-level-features"></a>Windows Server 2008 R2 도메인 기능 수준 기능

* 모든 기본 Active Directory 기능, Windows Server 2008 도메인 기능 수준에서 제공 되는 모든 기능 및 다음 기능이 있습니다.
   * 인증 메커니즘 보증-각 사용자의 Kerberos 토큰 내에서 도메인 사용자를 인증 하는 데 사용 되는 로그온 방법 (스마트 카드 또는 사용자 이름/암호)의 유형에 대 한 정보를 패키지 합니다. Active Directory Federation Services (AD FS)와 같은 페더레이션된 id 관리 인프라를 배포한 네트워크 환경에서이 기능을 사용 하도록 설정 하면 사용자가 다음에 액세스 하려고 할 때마다 토큰의 정보를 추출할 수 있습니다. 사용자의 로그온 방법에 따라 권한 부여를 결정 하기 위해 개발 된 클레임 인식 응용 프로그램입니다.
   * 컴퓨터 계정의 이름 또는 DNS 호스트 이름이 변경 될 때 관리 서비스 계정의 컨텍스트에서 특정 컴퓨터에서 실행 되는 서비스에 대 한 자동 SPN 관리 관리 서비스 계정에 대 한 자세한 내용은 [서비스 계정 단계별 가이드](https://go.microsoft.com/fwlink/?LinkId=180401)를 참조 하세요.

## <a name="windows-server-2008"></a>Windows Server 2008

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008

### <a name="windows-server-2008-forest-functional-level-features"></a>Windows Server 2008 포리스트 기능 수준 기능

* Windows Server 2003 포리스트 기능 수준에서 사용할 수 있는 모든 기능을 사용할 수 있지만 추가 기능은 사용할 수 없습니다. 

### <a name="windows-server-2008-domain-functional-level-features"></a>Windows Server 2008 도메인 기능 수준 기능

* 모든 기본 AD DS 기능, Windows Server 2003 도메인 기능 수준의 모든 기능 및 다음 기능을 사용할 수 있습니다.
  * Windows Server 2003 시스템 볼륨에 대 한 분산 파일 시스템 (DFS) 복제 지원 (SYSVOL)
    * DFS 복제 지원은 SYSVOL 콘텐츠의 보다 강력 하 고 세부적인 복제를 제공 합니다.

      > [!NOTE]
      > Windows Server 2012 R2부터 FRS (파일 복제 서비스)는 더 이상 사용 되지 않습니다. 최소 Windows Server 2012 r 2를 실행 하는 도메인 컨트롤러에서 만들어진 새 도메인은 Windows Server 2008 도메인 기능 수준 이상으로 설정 해야 합니다.

  * Windows Server 2008 모드에서 실행 되는 도메인 기반 DFS 네임 스페이스입니다. 여기에는 액세스 기반 열거 및 확장성 향상을 위한 지원이 포함 됩니다. Windows Server 2008 모드의 도메인 기반 네임 스페이스에는 또한 Windows Server 2003 포리스트 기능 수준을 사용 해야 합니다. 자세한 내용은 [네임 스페이스 형식 선택](https://go.microsoft.com/fwlink/?LinkId=180400)을 참조 하세요.
  * Kerberos 프로토콜에 대 한 AES(Advanced Encryption Standard) (AES 128 및 AES 256) 지원입니다. AES를 사용 하 여 Tgt를 실행 하려면 도메인 기능 수준이 Windows Server 2008 이상 이어야 하 고 도메인 암호를 변경 해야 합니다. 
    * 자세한 내용은 [Kerberos의 향상 된 기능](https://technet.microsoft.com/library/cc749438(ws.10).aspx)을 참조 하세요.

      > [!NOTE]
      >도메인 컨트롤러에서 DFL 변경 사항을 이미 복제 했지만 krbtgt 암호를 아직 새로 고치지 않은 경우 도메인 기능 수준을 Windows Server 2008 이상으로 올린 후에 도메인 컨트롤러에서 인증 오류가 발생할 수 있습니다. 이 경우 도메인 컨트롤러에서 KDC 서비스를 다시 시작 하면 새 krbtgt 암호의 메모리 내 새로 고침이 트리거되고 관련 인증 오류가 해결 됩니다.

  * [마지막 대화형 로그온](https://go.microsoft.com/fwlink/?LinkId=180387) 정보는 다음 정보를 표시 합니다.
     * 도메인에 가입 된 Windows Server 2008 서버 또는 Windows Vista 워크스테이션에서 실패 한 총 로그온 횟수입니다.
     * Windows Server 2008 서버 또는 Windows Vista 워크스테이션에 성공적으로 로그온 한 후 실패 한 총 로그온 횟수
     * Windows Server 2008 또는 Windows Vista 워크스테이션에서 마지막으로 실패 한 로그온 시도 시간
     * Windows Server 2008 서버 또는 Windows Vista 워크스테이션에서 마지막으로 성공한 로그온 시도 시간
  * 세분화 된 암호 정책을 통해 도메인의 사용자 및 글로벌 보안 그룹에 대 한 암호 및 계정 잠금 정책을 지정할 수 있습니다. 자세한 내용은 [세분화 된 암호 및 계정 잠금 정책 구성에 대 한 단계별 가이드](https://go.microsoft.com/fwlink/?LinkID=91477)를 참조 하세요.
  * 개인용 가상 데스크톱
     * 사용자 및 컴퓨터 Active Directory의 사용자 계정 속성 대화 상자에서 개인용 가상 데스크톱 탭에서 제공 하는 추가 기능을 사용 하려면 AD DS 스키마를 Windows Server 2008 r 2 용으로 확장 해야 합니다 (스키마 개체 버전 = 47). 자세한 내용은 [RemoteApp 및 데스크톱 연결 단계별 가이드를 사용 하 여 개인 가상 데스크톱 배포](https://go.microsoft.com/fwlink/?LinkId=183552)를 참조 하세요.

## <a name="windows-server-2003"></a>Windows Server 2003

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003

### <a name="windows-server-2003-forest-functional-level-features"></a>Windows Server 2003 포리스트 기능 수준 기능

* 모든 기본 AD DS 기능 및 다음 기능을 사용할 수 있습니다.
   * 포리스트 트러스트
   * 도메인 이름 바꾸기
   * 연결 된 값 복제
      - 연결 된 값 복제를 사용 하면 전체 멤버 자격을 단일 단위로 복제 하는 대신 그룹 멤버 자격을 변경 하 여 개별 구성원에 대 한 값을 저장 하 고 복제할 수 있습니다. 개별 구성원 값을 저장 하 고 복제 하는 경우 복제 중에 더 작은 네트워크 대역폭과 더 작은 프로세서 주기가 사용 되며 여러 도메인 컨트롤러에서 동시에 여러 구성원을 추가 하거나 제거 하는 경우 업데이트가 손실 되지 않습니다.
   * RODC (읽기 전용 도메인 컨트롤러)를 배포 하는 기능
   * 향상 된 지식 일관성 검사기 (KCC) 알고리즘 및 확장성
      - ISTG (사이트 간 토폴로지 생성기)는 Windows 2000 포리스트 기능 수준에서 지원할 수 있는 것 AD DS 보다 더 많은 수의 사이트가 포함 된 포리스트를 지원 하도록 확장 된 향상 된 알고리즘을 사용 합니다. 향상 된 ISTG 선택 알고리즘은 Windows 2000 포리스트 기능 수준에서 ISTG를 선택 하는 데 방해가 되지 않는 메커니즘입니다.
   * 도메인 디렉터리 파티션에서 **Dynamicobject** 라는 동적 보조 클래스의 인스턴스를 만들 수 있습니다.
   * **InetOrgPerson** 개체 인스턴스를 **사용자** 개체 인스턴스로 변환 하 고 반대 방향으로 변환을 완료 하는 기능
   * 역할 기반 권한 부여를 지원 하기 위해 새 그룹 형식의 인스턴스를 만들 수 있습니다. 
      - 이러한 유형을 응용 프로그램 기본 그룹 및 LDAP 쿼리 그룹 이라고 합니다.
   * 스키마에 포함된 특성 및 클래스의 비활성화 및 다시 정의 LdapDisplayName,의 schemaidguid, OID 및 mapiID 특성은 다시 사용할 수 있습니다.
   * Windows Server 2008 모드에서 실행 되는 도메인 기반 DFS 네임 스페이스입니다. 여기에는 액세스 기반 열거 및 확장성 향상을 위한 지원이 포함 됩니다. 자세한 내용은 [네임 스페이스 형식 선택](https://go.microsoft.com/fwlink/?LinkId=180400)을 참조 하세요.

### <a name="windows-server-2003-domain-functional-level-features"></a>Windows Server 2003 도메인 기능 수준 기능

* 모든 기본 AD DS 기능, Windows 2000 기본 도메인 기능 수준에서 사용할 수 있는 모든 기능 및 다음 기능을 사용할 수 있습니다.
   * 도메인 컨트롤러의 이름을 바꿀 수 있도록 하는 Netdom .exe 도메인 관리 도구
   * 로그온 타임 스탬프 업데이트
      * **lastLogonTimestamp** 특성이 사용자 또는 컴퓨터의 마지막 로그온 시간으로 업데이트됩니다. 이 특성은 도메인 내에서 복제됩니다.
   * **InetOrgPerson** 및 user 개체에 대 한 유효 암호로 **userPassword** 특성을 설정 하는 기능
   * 사용자 및 컴퓨터 컨테이너를 리디렉션하는 기능
      * 기본적으로 컴퓨터 및 사용자 계정, 즉 cn = Computers<domain root> 및 cn =<domain root>Users에 대 한 두 개의 잘 알려진 컨테이너가 제공 됩니다. 이 기능을 사용 하면 이러한 계정에 대해 잘 알려진 새 위치를 정의할 수 있습니다.
   * 권한 부여 관리자에서 권한 부여 정책을 저장 하는 기능 AD DS
   * 제한된 위임
      * 제한 된 위임을 사용 하면 응용 프로그램에서 Kerberos 기반 인증을 통해 사용자 자격 증명의 보안 위임을 활용할 수 있습니다.
      * 특정 대상 서비스만 위임을 제한할 수 있습니다.
   * 선택적 인증
      * 선택적 인증을 사용 하면 트러스팅 포리스트의 리소스 서버에 대 한 인증을 허용 하는 신뢰할 수 있는 포리스트의 사용자 및 그룹을 지정할 수 있습니다.

## <a name="windows-2000"></a>Windows 2000

지원 되는 도메인 컨트롤러 운영 체제:

* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003
* Windows 2000

### <a name="windows-2000-native-forest-functional-level-features"></a>Windows 2000 기본 포리스트 기능 수준 기능

* 모든 기본 AD DS 기능을 사용할 수 있습니다.

### <a name="windows-2000-native-domain-functional-level-features"></a>Windows 2000 기본 도메인 기능 수준 기능

* 기본 AD DS 기능과 다음 디렉터리 기능을 모두 사용할 수 있습니다.
   * 배포 및 보안 그룹에 대 한 유니버설 그룹
   * 그룹 중첩
   * 보안 및 배포 그룹 간의 변환을 허용 하는 그룹 변환
   * SID (보안 식별자) 기록

## <a name="next-steps"></a>다음 단계

* [도메인 기능 수준 올리기](https://technet.microsoft.com/library/cc753104.aspx)  
* [포리스트 기능 수준 올리기](https://technet.microsoft.com/library/cc730985.aspx)
