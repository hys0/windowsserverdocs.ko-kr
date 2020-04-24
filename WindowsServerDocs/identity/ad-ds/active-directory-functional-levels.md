---
ms.assetid: f964d056-11bf-4d9b-b5ab-dceaad8bfbc3
title: Windows Server 2016 기능 수준
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 10/29/2018
ms.topic: article
ms.prod: windows-server
ms.custom: it-pro
ms.reviewer: maheshu
ms.technology: identity-adds
ms.openlocfilehash: 5f7a8f08ff10102fbc04b6f8272320bd3b77785d
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80825496"
---
# <a name="forest-and-domain-functional-levels"></a>포리스트 및 도메인 기능 수준

>적용 대상: Windows Server

기능 수준에 따라 사용 가능한 AD DS(Active Directory Domain Services) 도메인 또는 포리스트 기능이 결정됩니다. 또한 기능 수준에 따라 도메인 또는 포리스트의 도메인 컨트롤러에서 실행할 수 있는 Windows Server 운영 체제가 결정됩니다. 그러나 기능 수준은 도메인이나 포리스트에 조인된 워크스테이션 및 구성원 서버에서 실행할 수 있는 운영 체제에는 영향을 주지 않습니다.

AD DS를 배포할 때 도메인 및 포리스트 기능 수준을 현재 환경에서 지원할 수 있는 가장 높은 값으로 설정하세요. 그러면 최대한 많은 AD DS 기능을 사용할 수 있습니다. 새 포리스트를 배포할 때 포리스트 기능 수준을 설정한 다음, 도메인 기능 수준을 설정하라는 메시지가 표시됩니다. 도메인 기능 수준을 포리스트 기능 수준보다 높은 값으로 설정할 수 있지만, 도메인 기능 수준을 포리스트 기능 수준보다 낮은 값으로 설정할 수는 없습니다.

Windows 2003의 수명이 끝나면 Windows 2003 DC(도메인 컨트롤러)를 Windows Server 2008, 2008R2, 2012, 2012R2, 2016 또는 2019로 업데이트해야 합니다. 결과적으로, Windows Server 2003을 실행 하는 도메인 컨트롤러가 도메인에서 제거 해야 합니다.

Windows Server 2008 및 더 높은 도메인 기능 수준에서 서비스 DFS (분산 파일) 복제 도메인 컨트롤러 간에 SYSVOL 폴더 내용을 복제 하는 데 사용 됩니다. Windows Server 2008 도메인 기능 수준 이상의 새 도메인을 만들면 DFS 복제 SYSVOL을 복제 하는 데 자동으로 사용 됩니다. 더 낮은 기능 수준에서 도메인을 만든 경우 FRS를 사용 하 여 SYSVOL에 대 한 DFS 복제에서 마이그레이션할 해야 합니다. 마이그레이션 단계의 경우 [TechNet의 프로시저](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx)를 따르거나 [스토리지 팀 파일 캐비닛 블로그의 간소화된 단계 집합](https://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx)을 참조할 수 있습니다.

## <a name="windows-server-2019"></a>시작

이 릴리스에는 새로운 포리스트 또는 도메인 기능 수준이 추가되지 않았습니다.

Windows Server 2019 도메인 컨트롤러를 추가하기 위한 최소 요구 사항은 Windows Server 2008 기능 수준입니다. 또한 도메인에서 SYSVOL을 복제하는 엔진으로 DFS-R을 사용해야 합니다.

## <a name="windows-server-2016"></a>Windows Server 2016

지원되는 도메인 컨트롤러 운영 체제:

* 시작
* Windows Server 2016

### <a name="windows-server-2016-forest-functional-level-features"></a>Windows Server 2016 포리스트 기능 수준 기능

* Windows Server 2012R2 포리스트 기능 수준에서 제공되는 모든 기능과 다음 기능을 사용할 수 있습니다.
   * [MIM(Microsoft Identity Manager)를 사용하는 PAM(권한 있는 액세스 관리)](https://docs.microsoft.com/windows-server/identity/whats-new-active-directory-domain-services#a-namebkmkpamaprivileged-access-management)

### <a name="windows-server-2016-domain-functional-level-features"></a>Windows Server 2016 도메인 기능 수준 기능

* 모든 기본 Active Directory 기능, Windows Server 2012R2 도메인 기능 수준의 모든 기능 및 다음 기능:
   * DC는 PKI 인증을 요구하도록 구성된 사용자 계정에서 NTLM 및 기타 암호 기반 비밀의 자동 롤링을 지원할 수 있습니다. 이 구성을 "대화형 로그온에 필요한 스마트 카드"라고도 합니다.
   * 사용자가 특정 도메인에 조인된 디바이스로 제한되면 DC에서 네트워크 NTLM을 허용하도록 지원할 수 있습니다.
   * Kerberos 클라이언트에서 PKInit Freshness Extension으로 성공적으로 인증하면 새로운 공개 키 ID SID를 얻게 됩니다.

    자세한 내용은 [Kerberos 인증의 새로운 기능](https://docs.microsoft.com/windows-server/security/kerberos/whats-new-in-kerberos-authentication) 및 [자격 증명 보호의 새로운 기능](https://docs.microsoft.com/windows-server/security/credentials-protection-and-management/whats-new-in-credential-protection)을 참조하세요.

## <a name="windows-server-2012r2"></a>Windows Server 2012R2

지원되는 도메인 컨트롤러 운영 체제:

* 시작
* Windows Server 2016
* Windows Server 2012 R2

### <a name="windows-server-2012r2-forest-functional-level-features"></a>Windows Server 2012R2 포리스트 기능 수준 기능

* Windows Server 2012 포리스트 기능 수준에서 제공되는 모든 기능을 사용할 수 있지만, 추가 기능은 없습니다.

### <a name="windows-server-2012r2-domain-functional-level-features"></a>Windows Server 2012R2 도메인 기능 수준 기능

* 모든 기본 Active Directory 기능, Windows Server 2012 도메인 기능 수준의 모든 기능 및 다음 기능:
   * 보호된 사용자에 대한 DC쪽 보호. Windows Server 2012 R2 도메인에 인증하는 보호된 사용자는 더 이상 다음을 수행할 수 없습니다.
      * NTLM 인증을 통한 인증
      * Kerberos 사전 인증에 DES 또는 RC4 암호 그룹 사용
      * 제한 없는 위임 또는 제한된 위임을 사용한 위임
      * 초기 4시간의 수명이 지난 후 사용자 티켓(TGT) 갱신
   * Authentication Policies
      * Windows Server 2012 R2 도메인의 계정에 적용하여 계정이 로그온할 수 있는 호스트를 제어하고 계정으로 실행되는 서비스 인증에 대한 액세스 제어 조건을 적용할 수 있는 새로운 포리스트 기반 Active Directory 정책입니다.
   * Authentication Policy Silos
      * 사용자, 관리형 서비스 및 컴퓨터 간에 관계를 만들 수 있는 새로운 포리스트 기반 Active Directory 개체이며, 인증 정책 또는 인증 격리를 위해 계정을 분류하는 데 사용됩니다.

## <a name="windows-server-2012"></a>Windows Server 2012

지원되는 도메인 컨트롤러 운영 체제:

* 시작
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012

### <a name="windows-server-2012-forest-functional-level-features"></a>Windows Server 2012 포리스트 기능 수준 기능

* Windows Server 2008 R2 포리스트 기능 수준에서 제공되는 모든 기능을 사용할 수 있지만, 추가 기능은 없습니다.

### <a name="windows-server-2012-domain-functional-level-features"></a>Windows Server 2012 도메인 기능 수준 기능

* 모든 기본 Active Directory 기능, Windows Server 2008R2 도메인 기능 수준의 모든 기능 및 다음 기능:
   * 클레임, 복합 인증 및 Kerberos 아머링 KDC 관리 템플릿 정책에 대한 KDC 지원에는 Windows Server 2012 도메인 기능 수준이 필요한 두 가지 설정(항상 클레임 제공 및 아머링되지 않은 인증 요청 실패)이 포함됩니다. 자세한 내용은 [Kerberos 인증의 새로운 기능](https://technet.microsoft.com/library/hh831747.aspx)을 참조하세요.

## <a name="windows-server-2008r2"></a>Windows Server 2008R2

지원되는 도메인 컨트롤러 운영 체제:

* 시작
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2

### <a name="windows-server-2008r2-forest-functional-level-features"></a>Windows Server 2008R2 포리스트 기능 수준 기능

* Windows Server 2003 포리스트 기능 수준에서 사용할 수 있는 모든 기능과 다음과 같은 추가 기능을 제공합니다.
   * AD DS가 실행 주일 때 삭제된 개체를 전체 복원할 수 있는 기능을 제공하는 Active Directory 휴지통

### <a name="windows-server-2008r2-domain-functional-level-features"></a>Windows Server 2008R2 도메인 기능 수준 기능

* 모든 기본 Active Directory 기능, Windows Server 2008 도메인 기능 수준의 모든 기능 및 다음 기능:
   * 각 사용자의 Kerberos 토큰 내에서 도메인 사용자를 인증하는 데 사용되는 로그온 방법 유형(스마트 카드 또는 사용자 이름/암호)에 대한 정보가 포함된 인증 메커니즘 보증. 이 기능이 AD FS(Active Directory Federation Services)와 같은 페더레이션 ID 관리 인프라를 배포한 네트워크 환경에서 사용되는 경우 사용자의 로그온 방법을 기준으로 권한 부여를 결정하도록 개발된 클레임 인식 애플리케이션에 사용자가 액세스하려고 할 때마다 토큰의 정보가 추출될 수 있습니다.
   * 머신 계정의 이름 또는 DNS 호스트 이름이 변경될 때 관리형 서비스 계정의 컨텍스트에서 특정 컴퓨터에서 실행되는 서비스의 SPN 자동 관리. 관리형 서비스 계정에 대한 자세한 내용은 [서비스 계정 단계별 가이드](https://go.microsoft.com/fwlink/?LinkId=180401)를 참조하세요.

## <a name="windows-server-2008"></a>Windows Server 2008

지원되는 도메인 컨트롤러 운영 체제:

* 시작
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008

### <a name="windows-server-2008-forest-functional-level-features"></a>Windows Server 2008 포리스트 기능 수준 기능

* Windows Server 2003 포리스트 기능 수준에서 제공되는 모든 기능을 사용할 수 있지만, 추가 기능은 없습니다. 

### <a name="windows-server-2008-domain-functional-level-features"></a>Windows Server 2008 도메인 기능 수준 기능

* 모든 기본 AD DS 기능, Windows Server 2003 도메인 기능 수준의 모든 기능 및 다음 기능을 사용할 수 있습니다.
  * Windows Server 2003 SYSVOL(시스템 볼륨)에 대한 DFS(분산 파일 시스템) 복제 지원
    * DFS 복제 지원을 사용하면 SYSVOL 콘텐츠를 보다 견고하고 구체적으로 복제할 수 있습니다.

      > [!NOTE]
      > Windows Server 2012 R2부터 FRS(파일 복제 서비스)는 사용되지 않습니다. Windows Server 2012 R2 이상을 실행하는 도메인 컨트롤러에서 만들어진 새 도메인은 Windows Server 2008 도메인 기능 수준 이상으로 설정해야 합니다.

  * Windows Server 2008 모드에서 실행되는 도메인 기반 DFS 네임스페이스. 액세스 기반 열거형 및 향상된 확장성을 지원합니다. 또한 Windows Server 2008 모드의 도메인 기반 네임스페이스는 포리스트에서 Windows Server 2003 포리스트 기능 수준을 사용해야 합니다. 자세한 내용은 [네임스페이스 형식 선택](https://go.microsoft.com/fwlink/?LinkId=180400)을 참조하세요.
  * Kerberos 프로토콜에 대한 고급 암호화 표준(AES 128 및 AES 256) 지원. AES를 사용하여 TGT를 실행하려면 도메인 기능 수준이 Windows Server 2008 이상이어야 하고 도메인 암호를 변경해야 합니다. 
    * 자세한 내용은 [향상된 Kerberos](https://technet.microsoft.com/library/cc749438(ws.10).aspx)를 참조하세요.

      > [!NOTE]
      >도메인 컨트롤러에서 DFL 변경 사항을 이미 복제했지만 krbtgt 암호를 아직 새로 고치지 않은 경우 도메인 기능 수준을 Windows Server 2008 이상으로 올린 후에 도메인 컨트롤러에서 인증 오류가 발생할 수 있습니다. 이 경우 도메인 컨트롤러에서 KDC 서비스를 다시 시작하면 새 krbtgt 암호의 메모리 내 새로 고침이 트리거되고 관련 인증 오류가 해결됩니다.

  * [마지막 대화형 로그온](https://go.microsoft.com/fwlink/?LinkId=180387) 정보는 다음 정보를 표시합니다.
     * 도메인에 조인된 Windows Server 2008 서버 또는 Windows Vista 워크스테이션에서 실패한 총 로그온 횟수
     * Windows Server 2008 서버 또는 Windows Vista 워크스테이션에 성공적으로 로그온한 후 실패한 총 로그온 횟수
     * Windows Server 2008 또는 Windows Vista 워크스테이션에서 마지막으로 실패한 로그온 시간
     * Windows Server 2008 서버 또는 Windows Vista 워크스테이션에서 마지막으로 성공한 로그온 시간
  * 세분화된 암호 정책을 통해 도메인의 사용자 및 글로벌 보안 그룹에 대한 암호 및 계정 잠금 정책을 지정할 수 있습니다. 자세한 내용은 [세분화된 암호 및 계정 잠금 정책 구성에 대한 단계별 지침](https://go.microsoft.com/fwlink/?LinkID=91477)을 참조하세요.
  * 개인용 가상 데스크톱
     * 개인용 가상 데스크톱 탭에서 제공하는 추가 기능을 Active Directory 사용자 및 컴퓨터의 사용자 계정 속성 대화 상자에 사용하려면 AD DS 스키마를 Windows Server 2008 R2로 확장해야 합니다(스키마 개체 버전 = 47). 자세한 내용은 [RemoteApp 및 데스크톱 연결 단계별 가이드를 사용하여 개인용 가상 데스크톱 배포](https://go.microsoft.com/fwlink/?LinkId=183552)를 참조하세요.

## <a name="windows-server-2003"></a>Windows Server 2003

지원되는 도메인 컨트롤러 운영 체제:

* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003

### <a name="windows-server-2003-forest-functional-level-features"></a>Windows Server 2003 포리스트 기능 수준 기능

* 모든 기본 AD DS 기능 및 다음 기능을 사용할 수 있습니다.
   * 포리스트 트러스트
   * 도메인 이름 바꾸기
   * 연결된 값 복제
      - 연결된 값 복제를 사용하면 전체 구성원을 단일 단위로 복제하는 대신 개별 구성원의 값을 저장하고 복제하도록 그룹 멤버 자격을 변경할 수 있습니다. 개별 구성원의 값을 저장하고 복제하면 복제 중에 네트워크 대역폭과 프로세서 주기를 더 적게 사용하며, 여러 도메인 컨트롤러에서 동시에 여러 구성원을 추가하거나 제거할 때 업데이트가 손실되지 않습니다.
   * RODC(읽기 전용 도메인 컨트롤러)를 배포하는 기능
   * 개선된 KCC(정보 일관성 검사기) 알고리즘 및 확장성
      - ISTG(사이트 간 토폴로지 생성기)는 Windows 2000 포리스트 기능 수준에서 AD DS가 지원할 수 있는 것보다 더 많은 수의 사이트가 포함된 포리스트를 지원하도록 확장할 수 있는 향상된 알고리즘을 사용합니다. 향상된 ISTG 선택 알고리즘은 Windows 2000 포리스트 기능 수준에서 ISTG를 선택하는 메커니즘으로 침입 가능성이 낮습니다.
   * 도메인 디렉터리 파티션에 **dynamicObject**라는 동적 보조 클래스의 인스턴스를 만드는 기능
   * **inetOrgPerson** 개체 인스턴스를 **User** 개체 인스턴스로 변환하고, 반대 방향으로 변환을 완료하는 기능
   * 역할 기반 권한 부여를 지원하기 위해 새로운 그룹 유형 인스턴스를 만드는 기능 
      - 이러한 유형을 애플리케이션 기본 그룹 및 LDAP 쿼리 그룹이라고 합니다.
   * 스키마에 포함된 특성 및 클래스의 비활성화 및 다시 정의 ldapDisplayName, schemaIdGuid, OID 및 mapiID 특성을 다시 사용할 수 있습니다.
   * Windows Server 2008 모드에서 실행되는 도메인 기반 DFS 네임스페이스. 액세스 기반 열거형 및 향상된 확장성을 지원합니다. 자세한 내용은 [네임스페이스 형식 선택](https://go.microsoft.com/fwlink/?LinkId=180400)을 참조하세요.

### <a name="windows-server-2003-domain-functional-level-features"></a>Windows Server 2003 도메인 기능 수준 기능

* 모든 기본 AD DS 기능, Windows 2000 네이티브 도메인 기능 수준에서 제공되는 모든 기능 및 다음 기능을 사용할 수 있습니다.
   * 도메인 컨트롤러의 이름을 변경할 수 있는 도메인 관리 도구 Netdom.exe
   * 로그온 타임스탬프 업데이트
      * **lastLogonTimestamp** 특성이 사용자 또는 컴퓨터의 마지막 로그온 시간으로 업데이트됩니다. 이 특성은 도메인 내에서 복제됩니다.
   * **userPassword** 특성을 **inetOrgPerson** 및 사용자 개체의 유효한 암호로 설정하는 기능
   * Users 및 Computers 컨테이너를 리디렉션하는 기능
      * 기본적으로 컴퓨터 및 사용자 계정을 보유할 수 있도록 두 개의 잘 알려진 컨테이너가 제공됩니다(예: cn=Computers,<domain root> cn=Users,<domain root>). 이 기능을 사용하면 이러한 계정에 대한 새로운 잘 알려진 위치를 정의할 수 있습니다.
   * 권한 부여 관리자가 권한 부여 정책을 AD DS에 저장하는 기능
   * 제한된 위임
      * 제한된 위임을 사용하면 애플리케이션에서 Kerberos 기반 인증을 통해 사용자 자격 증명의 보안 위임을 활용할 수 있습니다.
      * 위임의 범위를 특정 대상 서비스로 제한할 수 있습니다.
   * 선택적 인증
      * 선택적 인증을 사용하면 트러스팅 포리스트의 리소스 서버에 인증할 수 있는 트러스트된 포리스트의 사용자 및 그룹을 지정할 수 있습니다.

## <a name="windows-2000"></a>Windows 2000

지원되는 도메인 컨트롤러 운영 체제:

* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003
* Windows 2000

### <a name="windows-2000-native-forest-functional-level-features"></a>Windows 2000 네이티브 포리스트 기능 수준 기능

* 모든 기본 AD DS 기능을 사용할 수 있습니다.

### <a name="windows-2000-native-domain-functional-level-features"></a>Windows 2000 네이티브 도메인 기능 수준 기능

* 모든 기본 AD DS 기능 및 다음 디렉터리 기능을 사용할 수 있습니다.
   * 배포 및 보안 그룹에 대한 유니버설 그룹
   * 그룹 중첩
   * 보안 그룹과 배포 그룹 간에 변환할 수 있는 그룹 변환
   * SID(보안 식별자) 기록

## <a name="next-steps"></a>다음 단계

* [도메인 기능 수준 올리기](https://technet.microsoft.com/library/cc753104.aspx)  
* [포리스트 기능 수준 올리기](https://technet.microsoft.com/library/cc730985.aspx)
