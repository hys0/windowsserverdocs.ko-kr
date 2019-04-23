---
ms.assetid: 709353b0-b913-4367-8580-44745183e2bc
title: 디렉터리 복제를 지원하는 DNS 기능 확인
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: ''
ms.suite: na
ms.technology: identity-adds
ms.author: joflore
ms.date: 05/31/2017
ms.tgt_pltfrm: na
author: Femila
ms.openlocfilehash: a55b95ee516abda8bdbae6e9829a161ef060012e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871874"
---
# <a name="verify-dns-functionality-to-support-directory-replication"></a>디렉터리 복제를 지원하는 DNS 기능 확인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

 Active Directory 복제를 방해 하는 도메인 이름 시스템 (DNS) 설정을 확인 하려면 도메인에 대 한 DNS가 올바르게 작동 하는지 확인 하는 기본 테스트를 실행 하 여 시작할 수 있습니다. 기본 테스트를 실행 한 후에 리소스 레코드 등록 및 동적 업데이트를 포함 하 여 DNS 기능의 다른 측면을 테스트할 수 있습니다.

일반적으로 생각 하는 도메인 컨트롤러에서이 테스트를 실행 하면 모든 도메인 컨트롤러에 기본 DNS 기능이이 테스트를 실행할 수 있지만 복제 문제, 예를 들어 이벤트 Id 1844, 1925, 2087, 보고 하는 도메인 컨트롤러에서 발생할 수 있습니다. 또는 이벤트 뷰어 디렉터리 서비스 DNS 로그에 2088 합니다.



## <a name="running-the-domain-controller-basic-dns-testtitle"></a>도메인 컨트롤러 기본 DNS 테스트 실행</title>

기본 DNS 테스트에는 DNS 기능의 다음 측면을 확인합니다.


- **연결:** 테스트에서 컨트롤러를 DNS에 등록 된 도메인에 연결할 수 있는지 여부를 결정 합니다 <system>ping</system> Lightweight Directory Access Protocol을 있고 명령을 원격 프로시저 호출 (LDAP/RPC) 연결 /입니다. 연결 테스트에 도메인 컨트롤러에 실패 하면 해당 도메인 컨트롤러에 대해 다른 테스트가 실행 됩니다. 연결 테스트는 다른 DNS 테스트를 실행 하기 전에 자동으로 수행 됩니다.
- **필수 서비스:** 테스트 실행 및 테스트 된 도메인 컨트롤러에서 사용 가능한 다음 서비스는 확인 합니다. DNS 클라이언트 서비스, Net Logon 서비스에서 키 배포 센터 (KDC) 서비스 및 DNS 서버 서비스 (DNS는 도메인 컨트롤러에 설치 된) 경우입니다.
- **DNS 클라이언트 구성:**  테스트는 DNS 서버의 DNS 클라이언트 컴퓨터의 모든 네트워크 어댑터에 연결할 수 있는지 확인 합니다.
- **리소스 레코드 등록:** 테스트는 각 도메인 컨트롤러의 호스트 (A) 리소스 레코드 하나 이상의 클라이언트 컴퓨터에 구성 되어 있는 DNS 서버에 등록 되어 있는지 확인 합니다.
- **영역 및 시작 (soa):** 도메인 컨트롤러에서 DNS 서버 서비스를 실행 중인 경우 테스트 시작 (soa) 리소스 레코드는 Active Directory 도메인 영역에 대 한 확인 하 고 Active Directory 도메인 영역 있는지 확인 합니다.
- **루트 영역:** 영역 루트 (.)가 있는지 여부를 확인 합니다.

엔터프라이즈 관리자 또는 이와 동등한 자격이 이러한 절차를 완료 하는 데 필요한 최소를입니다.

기본 DNS 기능을 확인 하려면 다음 절차를 사용할 수 있습니다.
     
### <a name="to-verify-basic-dns-functionality"></a>기본 DNS 기능을 확인 합니다.


1. 테스트 하려는 도메인 컨트롤러에서 또는 Active Directory Domain Services (AD DS) 도구가 설치 되어 있는 도메인 구성원 컴퓨터에서 관리자 권한으로 명령 프롬프트를 엽니다. 관리자 권한으로 명령 프롬프트를 열려면 **시작**을 클릭합니다. 
2. 검색 시작에 명령 프롬프트를 입력 합니다. 
3. 시작 메뉴의 맨 위에 있는 명령 프롬프트를 마우스 오른쪽 단추로 클릭 하 고 관리자 권한으로 실행을 클릭 합니다. 사용자 계정 컨트롤 대화 상자가 나타나면 표시되는 작업이 원하는 작업인지 확인한 다음 계속을 클릭합니다.
4. 명령 프롬프트에서 다음 명령을 입력 하 고 ENTER를 누릅니다. `dcdiag /test:dns /v /s:<DCName> /DnsBasic /f:dcdiagreport.txt`
</br></br>실제 고유 이름, NetBIOS 이름 또는 도메인 컨트롤러의 DNS 이름으로 대체 &lt;DCName&gt;합니다. 대신 /s: 대신 /e:를 입력 하 여 포리스트의 모든 도메인 컨트롤러를 테스트할 수 있습니다. /F 스위치는 이전 명령에서 dcdiagreport.txt 파일 이름을 지정 합니다. 현재 작업 디렉터리와 다른 위치에 파일을 배치 하려는 경우 /f:c:reportsdcdiagreport.txt 같은 파일 경로 지정할 수 있습니다.

5. 메모장 이나 다른 텍스트 편집기에서 dcdiagreport.txt 파일을 엽니다. 파일을 메모장에서 명령 프롬프트를 열려면 메모장 dcdiagreport.txt를 입력 한 다음 ENTER를 누릅니다. 다른 작업 디렉터리에 파일을 배치 하면, 파일 경로 포함 합니다. 예를 들어 c:reports에 파일을 배치 하면 메모장 c:reportsdcdiagreport.txt를 입력 한 다음 ENTER를 누릅니다.
6. 요약 테이블에는 파일의 아래쪽으로 스크롤하십시오. 
</br></br>모든 도메인 컨트롤러의 이름을 보고서 요약 테이블에서 "경고" 또는 "실패" 상태 note 합니다.  문자열을 검색 하 여 자세한 분석 섹션을 검색 하 여 문제 도메인 컨트롤러 인지 확인 하려고 "DC: DCName,"여기서 DCName은 도메인 컨트롤러의 실제 이름입니다.

필요한 확실 한 구성 변경 내용을 표시 되 면, 적절 하 게 확인 합니다. 예를 들어, 도메인 컨트롤러 중 하나는 분명히 잘못 된 IP 주소에 보면이 수정할 수 있습니다. 그런 다음 테스트를 다시 실행 합니다.

구성 변경 내용을 확인을 위해 적절 하 게 /e: 또는 /s: 스위치를 사용 하 여 Dcdiag /test:DNS /v 명령을 다시 실행 합니다. 호스트 (AAAA) 유효성 검사 부분 실패 테스트를 기대할 수 IP 버전 6(ipv6) 도메인 컨트롤러에서 사용할 수 없으면 하지만 네트워크에서 IPv6을 사용 하지 않는 경우 이러한 레코드가 필요 하지 않습니다.
            
## <a name="verifying-resource-record-registration"></a>리소스 레코드 등록 확인
    
대상 도메인 컨트롤러 DNS 별칭 (CNAME) 리소스 레코드를 사용 하 여 원본 도메인 컨트롤러 복제 파트너를 찾습니다. Windows Server (Windows Server 2003 서비스 팩 1(sp1)부터 시작)를 실행 하는 도메인 컨트롤러 정규화 된 도메인 이름 (Fqdn)을 사용 하 여 원본 복제 파트너를 찾을 수 있지만, 못하는 경우 NetBIOS namesthe 있는지 별칭 (CNAME) 리소스 레코드는 고 작동 하는 적절 한 dns 확인 해야 합니다. 
      
별칭 (CNAME) 리소스 레코드 등록이 포함 되는 리소스 레코드 등록을 확인 하려면 다음 절차를 사용할 수 있습니다.
      
### <a name="to-verify-resource-record-registrationtitle"></a>리소스 레코드 등록을 확인 하려면</title>


1. 관리자 권한으로 명령 프롬프트를 엽니다. 관리자 권한으로 명령 프롬프트를 열려면 시작을 클릭 합니다. 검색 시작에 명령 프롬프트를 입력 합니다. 
2. 시작 메뉴의 맨 위에 있는 명령 프롬프트를 마우스 오른쪽 단추로 클릭 하 고 관리자 권한으로 실행을 클릭 합니다. 사용자 계정 컨트롤 대화 상자가 나타나면 표시되는 작업이 원하는 작업인지 확인한 다음 계속을 클릭합니다.  </br></br>Dcdiag 도구를 사용 하 여 실행 하 여 도메인 컨트롤러 위치에 필수적인 모든 리소스 레코드의 등록을 확인 하려면를 `dcdiag /test:dns /DnsRecordRegistration` 명령입니다.

이 명령은 DNS에서 다음 리소스 레코드의 등록을 확인합니다.


- **별칭 (CNAME):** 전역적으로 고유 식별자 (GUID)-리소스 레코드를 복제 파트너를 찾는 기반
- **호스트 (A):** 도메인 컨트롤러의 IP 주소를 포함 하는 호스트 리소스 레코드
- **LDAP SRV:** LDAP 서버를 찾는 서비스 (SRV) 리소스 레코드
- **GC SRV**: 전역 찾기 서비스 (SRV) 리소스 레코드를 카탈로그 서버
- **PDC SRV**: 주 도메인 컨트롤러 (PDC) 에뮬레이터 작업 마스터를 찾는 서비스 (SRV) 리소스 레코드

별칭 (CNAME) 리소스 레코드 등록만 확인 하려면 다음 절차를 사용할 수 있습니다.

### <a name="to-verify-alias-cname-resource-record-registration"></a>별칭 (CNAME) 리소스 레코드 등록을 확인 하려면

1. DNS 스냅인을 엽니다. DNS를 열려면 시작을 클릭 합니다. 검색 시작에 dnsmgmt.msc를 입력 한 다음 ENTER를 누릅니다. 사용자 계정 컨트롤 대화 상자가 나타나면 표시를 하 고 계속을 클릭 한 다음 작업을 확인 합니다.
2. DNS 스냅인을 사용 하 여 DNS 서버 서비스를 실행 하는 서버가 도메인 컨트롤러의 Active Directory 도메인과 동일한 이름 사용 하 여 DNS 영역을 호스팅하는 모든 도메인 컨트롤러를 찾으려고 합니다.
3. 콘솔 트리에서 라는 _msdcs 영역을 클릭 합니다. Dns_Domain_Name 합니다.
4. 세부 정보 창에서 다음 리소스 레코드 있는지를 확인 합니다: Dsa_Guid._msdcs 라는 별칭 (CNAME) 리소스 레코드입니다. <placeholder>Dns_Domain_Name</placeholder> 및 해당 호스트 (A) 리소스 레코드를 DNS 서버의 이름입니다.

별칭 (CNAME) 리소스 레코드를 등록 하지 않은 경우 동적 업데이트를 제대로 작동을 확인 합니다. 동적 업데이트를 확인 하려면 다음 섹션에는 테스트를 사용 합니다.
    
## <a name="verifying-dynamic-update"></a>동적 업데이트를 확인합니다.
    
리소스 레코드가 DNS에 존재 하지 않도록 표시 하는 기본 DNS 테스트, 이유는 Net Logon 서비스를 등록 하지 않은 리소스 레코드를 자동으로 결정 하는 동적 업데이트 테스트를 사용 합니다. 보안 동적 업데이트를 허용 하 고 테스트 레코드 (_dcdiag_test_record)의 등록을 수행 하는 Active Directory 도메인 영역 구성 되어 있는지를 확인 하려면 다음 절차를 따르십시오. 테스트 레코드는 테스트 후 자동으로 삭제 됩니다.

### <a name="to-verify-dynamic-updatetitle"></a>동적 업데이트를 확인 하려면</title>


1. 관리자 권한으로 명령 프롬프트를 엽니다. 관리자 권한으로 명령 프롬프트를 열려면 시작을 클릭 합니다. 검색 시작에 명령 프롬프트를 입력 합니다. 시작 메뉴의 맨 위에 있는 명령 프롬프트를 마우스 오른쪽 단추로 클릭 하 고 관리자 권한으로 실행을 클릭 합니다. 사용자 계정 컨트롤 대화 상자가 나타나면 표시되는 작업이 원하는 작업인지 확인한 다음 계속을 클릭합니다.
2. 명령 프롬프트에서 다음 명령을 입력 하 고 ENTER를 누릅니다. `dcdiag /test:dns /v /s:<DCName> /DnsDynamicUpdate`
   </br></br>고유 이름, NetBIOS 이름 또는 도메인 컨트롤러의 DNS 이름으로 대체 &lt;DCName&gt;합니다. 대신 /s: 대신 /e:를 입력 하 여 포리스트의 모든 도메인 컨트롤러를 테스트할 수 있습니다. 도메인 컨트롤러에서 사용 하도록 설정 하는 IPv6가 없는 경우에 호스트 (AAAA) 리소스 레코드 부분 테스트가 실패 하 고, IPv6 사용 하지 않는 경우 정상적인 현상입니다는 하시면 됩니다.

보안 동적 업데이트 구성 되어 있지 않으면 다음 절차를 사용 하 여 구성 하 수 있습니다.

### <a name="to-enable-secure-dynamic-updates"></a>보안 동적 업데이트를 사용 하도록 설정 하려면


1. DNS 스냅인을 엽니다. DNS를 열려면 시작을 클릭 합니다. 
2. 검색 시작에 dnsmgmt.msc를 입력 한 다음 ENTER를 누릅니다. 사용자 계정 컨트롤 대화 상자가 나타나면 작업 표시를 확인 하는 경우 원하는 하 고 계속을 클릭 합니다.
3. 콘솔 트리에서 해당 영역을 마우스 오른쪽 단추로 클릭 하 고 속성을 클릭 합니다.
4. 일반 탭에서 Active Directory 통합 영역 종류 인지를 확인 합니다.
5. 동적 업데이트를 보안만 클릭 합니다.

## <a name="registering-dns-resource-records"></a>DNS 리소스 레코드를 등록합니다.
    
원본 도메인 컨트롤러에 대 한 DNS에서 DNS 리소스 레코드 표시 되지 않으면, 동적 업데이트를 확인 하 고 DNS 리소스 레코드를 즉시 등록 하려면, 다음 절차를 사용 하 여 등록 수동으로 적용할 수 있습니다. Net Logon 서비스가 도메인 컨트롤러에서 네트워크에 있는 도메인 컨트롤러에 대 한 필요한 DNS 리소스 레코드를 등록 합니다. DNS 클라이언트 서비스 호스트 (A) 리소스 레코드를 가리키는 별칭 (CNAME) 레코드를 등록 합니다.

### <a name="to-register-dns-resource-records-manuallytitle"></a>DNS 리소스 레코드를 수동으로 등록 하려면</title>


1. 관리자 권한으로 명령 프롬프트를 엽니다. 관리자 권한으로 명령 프롬프트를 열려면 시작을 클릭 합니다. 
2. 검색 시작에 명령 프롬프트를 입력 합니다. 
3. 시작의 맨 위에 있는 명령 프롬프트를 마우스 오른쪽 단추로 클릭 하 고 관리자 권한으로 실행을 클릭 합니다. 사용자 계정 컨트롤 대화 상자가 나타나면 표시되는 작업이 원하는 작업인지 확인한 다음 계속을 클릭합니다.
4. 도메인 컨트롤러 로케이터 리소스의 등록을 시작 하려면 명령 프롬프트에서 원본 도메인 컨트롤러에서 수동으로 레코드 다음 명령을 입력 하 고 ENTER를 누릅니다. `net stop netlogon && net start netlogon`
5. 호스트의 등록을 시작 하려면 (A) 리소스 레코드 수동으로 명령 프롬프트에서 다음 명령을 입력 하 고 enter 키를 눌러: `ipconfig /flushdns && ipconfig /registerdns`
6. 명령 프롬프트에서 다음 명령을 입력 하 고 ENTER를 누릅니다. `dcdiag /test:dns /v /s:<DCName>` </br></br>고유 이름, NetBIOS 이름 또는 도메인 컨트롤러의 DNS 이름으로 대체 &lt;DCName&gt;합니다. 통과 된 DNS 테스트 하도록 테스트의 출력을 검토 합니다. 도메인 컨트롤러에서 사용 하도록 설정 하는 IPv6가 없는 경우에 호스트 (AAAA) 리소스 레코드 부분 테스트가 실패 하 고, IPv6 사용 하지 않는 경우 정상적인 현상입니다는 하시면 됩니다.
