---
ms.assetid: d92731f1-e4d8-4223-9b07-ca1f40bb0e1f
title: 연결되지 않은 네임 스페이스
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: c402e5519bc0e5c37cb6d3818c8def40d98d49e5
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81624261"
---
# <a name="disjoint-namespace"></a>연결되지 않은 네임 스페이스

> 적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

연결 되지 않은 네임 스페이스는 하나 이상의 도메인 구성원 컴퓨터에 컴퓨터가 구성원 인 Active Directory 도메인의 DNS 이름과 일치 하지 않는 주 DNS (도메인 이름 서비스) 접미사가 있을 때 발생 합니다. 예를 들어 이름이 na.corp.fabrikam.com 인 Active Directory 도메인에서 corp.fabrikam.com의 주 DNS 접미사를 사용 하는 구성원 컴퓨터는 비연속 네임 스페이스를 사용 합니다.

비연속 네임 스페이스는 연속 된 네임 스페이스 보다 관리, 유지 관리 및 문제 해결에 더 복잡 합니다. 연속 된 네임 스페이스에서 주 DNS 접미사는 Active Directory 도메인 이름과 일치 합니다. Active Directory 네임 스페이스가 모든 도메인 구성원 컴퓨터의 주 DNS 접미사와 동일 하다 고 가정 하도록 작성 된 네트워크 응용 프로그램은 연결 되지 않은 네임 스페이스에서 제대로 작동 하지 않습니다.

## <a name="support-for-disjoint-namespaces"></a>비연속 네임 스페이스 지원

도메인 컨트롤러를 포함 하는 도메인 구성원 컴퓨터는 비연속 네임 스페이스에서 작동할 수 있습니다. 도메인 구성원 컴퓨터는 연결 되지 않은 DNS 네임 스페이스에 호스트 (A) 리소스 레코드 및 IP 버전 6 (AAAA) 리소스 레코드를 등록할 수 있습니다. 도메인 구성원 컴퓨터가 이러한 방식으로 리소스 레코드를 등록 하면 도메인 컨트롤러는 DNS 영역에서 Active Directory 도메인 이름과 동일한 글로벌 및 사이트 관련 서비스 (SRV) 리소스 레코드를 계속 등록 합니다.

예를 들어 corp.fabrikam.com의 주 DNS 접미사를 사용 하는 na.corp.fabrikam.com 라는 Active Directory 도메인의 도메인 컨트롤러가 corp.fabrikam.com DNS 영역에서 호스트 (A) 및 IPv6 호스트 (AAAA) 리소스 레코드를 등록 한다고 가정 합니다. 도메인 컨트롤러는 na.corp.fabrikam.com 및 DNS 영역 _msdcs에서 글로벌 및 사이트 관련 서비스 (SRV) 리소스 레코드를 계속 등록 하 여 서비스 위치를 가능 하 게 합니다.

> [!IMPORTANT]
> Windows 운영 체제는 연결 되지 않은 네임 스페이스를 지원할 수 있지만, 주 DNS 접미사가 Active Directory 도메인 접미사가 동일한 환경에서 작동 하지 않는 것으로 가정 하 여 작성 된 응용 프로그램은 이러한 환경에서 작동 하지 않을 수 있습니다. 따라서 연결 되지 않은 네임 스페이스를 배포 하기 전에 모든 응용 프로그램 및 해당 운영 체제를 신중 하 게 테스트 해야 합니다.

연결 되지 않은 네임 스페이스는 다음과 같은 경우에 작동 합니다 (및 지원 됨).

- 여러 Active Directory 도메인을 포함 하는 포리스트가 DNS 영역이 라고도 하는 단일 DNS 네임 스페이스를 사용 하는 경우

    이 예는 na.corp.fabrikam.com, sa.corp.fabrikam.com 및 asia.corp.fabrikam.com와 같은 이름을 가진 지역 도메인을 사용 하 고 corp.fabrikam.com와 같은 단일 DNS 네임 스페이스를 사용 하는 회사입니다.

- 단일 Active Directory 도메인이 개별 DNS 네임 스페이스로 분할 된 경우

    이에 대 한 예는 hr.corp.contoso.com, production.corp.contoso.com 및 it.corp.contoso.com와 같은 DNS 영역을 사용 하는 corp.contoso.com의 Active Directory 도메인이 있는 회사입니다.

연결 되지 않은 네임 스페이스는 다음과 같은 상황에서 제대로 작동 하지 않습니다 (지원 되지 않음).

- 도메인 구성원에 사용 되는 연결 되지 않은 접미사가이 또는 다른 포리스트의 Active Directory 도메인 이름과 일치 합니다. 이렇게 하면 Kerberos 이름 접미사 라우팅이 중단 됩니다.

- 다른 포리스트에서는 동일한 분리 된 접미사를 사용 합니다. 이렇게 하면 포리스트 간에 이러한 접미사를 고유 하 게 라우팅할 수 없습니다.

- 도메인 구성원 CA (인증 기관) 서버에서 FQDN (정규화 된 도메인 이름)을 변경 하면 CA 서버가 구성원 인 도메인의 도메인 컨트롤러에서 사용 하는 것과 동일한 주 DNS 접미사를 더 이상 사용 하지 않습니다. 이 경우 CRL 배포 지점의 DNS 이름에 따라 CA 서버가 발급 한 인증서의 유효성을 검사 하는 데 문제가 있을 수 있습니다. 하지만 CA 서버를 안정적인 연결 되지 않은 네임 스페이스에 저장 하면 제대로 작동 하 고 지원 됩니다.

## <a name="considerations-for-disjoint-namespaces"></a>비연속 네임 스페이스에 대 한 고려 사항

다음 고려 사항은 연결 되지 않은 네임 스페이스를 사용 해야 하는지 여부를 결정 하는 데 도움이 될 수 있습니다.

### <a name="application-compatibility"></a>애플리케이션 호환성

앞에서 설명한 것 처럼 연결 되지 않은 네임 스페이스는 컴퓨터의 주 DNS 접미사가 구성원 인 도메인 이름의 이름과 동일할 것으로 가정 하 여 작성 된 모든 응용 프로그램 및 서비스에 문제를 일으킬 수 있습니다. 연결 되지 않은 네임 스페이스를 배포 하기 전에 응용 프로그램에서 호환성 문제를 확인 해야 합니다. 또한 분석을 수행할 때 사용 하는 모든 응용 프로그램의 호환성을 확인 해야 합니다. 여기에는 Microsoft와 기타 소프트웨어 개발자의 응용 프로그램이 포함 됩니다.

### <a name="advantages-of-disjoint-namespaces"></a>비연속 네임 스페이스의 장점

비연속 네임 스페이스를 사용 하면 다음과 같은 이점이 있습니다.

- 컴퓨터의 주 DNS 접미사는 다른 정보를 나타낼 수 있으므로 Active Directory 도메인 이름과 별도로 DNS 네임 스페이스를 관리할 수 있습니다.

- 비즈니스 구조 또는 지리적 위치에 따라 DNS 네임 스페이스를 구분할 수 있습니다. 예를 들어 대륙, 국가/지역, 빌딩 등의 비즈니스 단위 이름 또는 실제 위치에 따라 네임 스페이스를 구분할 수 있습니다.

### <a name="disadvantages-of-disjoint-namespaces"></a>비연속 네임 스페이스의 단점

비연속 네임 스페이스를 사용 하면 다음과 같은 단점이 있을 수 있습니다.

- 연결 되지 않은 네임 스페이스를 사용 하는 구성원 컴퓨터가 있는 포리스트의 각 Active Directory 도메인에 대해 별도의 DNS 영역을 만들고 관리 해야 합니다. 즉, 좀 더 복잡 한 추가 구성이 필요 합니다.

- 도메인 구성원이 지정 된 기본 DNS 접미사를 사용할 수 있도록 하는 Active Directory 특성을 수정 하 고 관리 하려면 수동 단계를 수행 해야 합니다.

- 이름 확인을 최적화 하려면 수동 단계를 수행 하 여 다른 주 DNS 접미사로 구성원 컴퓨터를 구성 하는 그룹 정책 수정 및 유지 관리 해야 합니다.

> [!NOTE]
> WINS (Windows Internet Name Service)는 단일 레이블 이름을 확인 하 여이 단점을 상쇄 하는 데 사용할 수 있습니다. WINS에 대 한 자세한 내용은 [Wins 기술 참조](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc736411(v=ws.10))를 참조 하십시오.

- 환경에 여러 기본 DNS 접미사가 필요한 경우 포리스트의 모든 Active Directory 도메인에 대해 DNS 접미사 검색 순서를 적절 하 게 구성 해야 합니다.

    DNS 접미사 검색 순서를 설정 하려면 그룹 정책 개체 또는 DHCP (Dynamic Host Configuration Protocol) 서버 서비스 매개 변수를 사용할 수 있습니다. 레지스트리를 수정할 수도 있습니다.

- 모든 응용 프로그램의 호환성 문제를 신중 하 게 테스트 해야 합니다.

이러한 단점을 해결 하기 위해 수행할 수 있는 단계에 대 한 자세한 내용은 연결 되지 않은 [네임 스페이스 만들기](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc755926(v=ws.10))를 참조 하세요.

### <a name="planning-a-namespace-transition"></a>네임 스페이스 전환 계획

네임 스페이스를 수정 하기 전에 연속 된 네임 스페이스에서 비연속 네임 스페이스 (또는 역방향)로의 전환에 적용 되는 다음 고려 사항을 검토 합니다.

- 네임 스페이스를 변경한 후 수동으로 구성 된 Spn (서비스 사용자 이름)이 DNS 이름과 더 이상 일치 하지 않을 수 있습니다. 이로 인해 인증이 실패할 수 있습니다.

    자세한 내용은 [spn이 잘못 설정 되어 서비스 로그온 실패를](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc772897(v=ws.10))참조 하세요.

    - 제한 된 위임을 사용 하는 Windows Server 2003 기반 컴퓨터를 사용 하는 경우 Spn을 변경 하려면 해당 컴퓨터에 추가 구성이 필요할 수 있습니다. 자세한 내용은 Microsoft 기술 자료 문서 936628 (영문)을 참조 하십시오. Microsoft 기술 자료에서 Windows Server 2003 (404)를 [실행 하는 컴퓨터에서 제한 된 위임을 구성 하려고 할 때 계정에 위임 될 수 있는 서비스 목록에는 SPN이 표시 되지](https://support.microsoft.com/help/936628) 않습니다.

    - Spn을 종속 관리자로 수정 하는 권한을 위임 하려면 [spn을 수정할 수](https://technet.microsoft.com/library/cc772895(WS.10).aspx)있는 권한 위임을 참조 하세요.

- 연결 되지 않은 네임 스페이스에 구성 된 도메인 컨트롤러를 포함 하는 배포에서 CA를 사용 하 여 SSL(Secure Sockets Layer) LDAP (Lightweight Directory Access Protocol) (LDAPS)를 사용 하는 경우에는 LDAPS 인증서를 구성할 때 적절 한 Active Directory 도메인 이름과 주 DNS 접미사를 사용 해야 합니다.

    도메인 컨트롤러 인증서 요구 사항에 대 한 자세한 내용은 Microsoft 기술 자료 문서 321051, [타사 인증 기관에서 SSL을 통해 LDAP를 사용 하도록 설정 하는 방법](https://support.microsoft.com/help/321051/)을 참조 하세요.

    > [!NOTE]
    > LDAPS에 인증서를 사용 하는 도메인 컨트롤러는 인증서를 다시 배포 해야 할 수 있습니다. 이렇게 하면 도메인 컨트롤러가 다시 시작 될 때까지 적절 한 인증서를 선택 하지 못할 수 있습니다. Windows Server 2003에 대 한 SSL (Lightweight Directory Access SSL(Secure Sockets Layer) Protocol) (LDAPS) 인증에 대 한 자세한 내용은 Microsoft 기술 자료 문서 938703 ( [ssl 연결 문제를 통해 ldap 문제를 해결 하는 방법](https://support.microsoft.com/help/938703/))을 참조 하세요.

### <a name="planning-for-disjoint-namespace-deployments"></a>비연속 네임 스페이스 배포 계획

비연속 네임 스페이스가 있는 환경에서 컴퓨터를 배포 하는 경우 다음과 같은 예방 조치를 취해야 합니다.

1. 회사에서 사용자가 연결 되지 않은 네임 스페이스를 테스트 하 고 지원 해야 하는 모든 소프트웨어 공급 업체에 게 알립니다. 연결 되지 않은 네임 스페이스를 사용 하는 환경에서 응용 프로그램이 지원 되는지 확인 하도록 요청 합니다.

2. 비연속 네임 스페이스 랩 환경에서 모든 버전의 운영 체제 및 응용 프로그램을 테스트 합니다. 이렇게 하면 다음 권장 사항을 따릅니다.

    1. 사용자 환경에 소프트웨어를 배포 하기 전에 모든 소프트웨어 문제를 해결 하십시오.

    2. 가능 하면 연결 되지 않은 네임 스페이스에 배포 하려는 운영 체제 및 응용 프로그램의 베타 테스트에 참여 하세요.

3. 관리자와 기술 지원팀 담당자가 연결 되지 않은 네임 스페이스와 그 영향을 인식 하는지 확인 합니다.

4. 필요한 경우 연결 되지 않은 네임 스페이스에서 연속 네임 스페이스로 전환할 수 있도록 하는 계획을 만듭니다.

5. 전도는 네임 스페이스 지원과 운영 체제 및 응용 프로그램 공급자의 중요도를 바꿉니다.
