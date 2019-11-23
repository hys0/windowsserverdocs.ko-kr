---
ms.assetid: 709353b0-b913-4367-8580-44745183e2bc
title: 디렉터리 복제를 지원하는 DNS 기능 확인
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.service: ''
ms.suite: na
ms.technology: identity-adds
ms.author: joflore
ms.date: 05/31/2017
ms.tgt_pltfrm: na
author: Femila
ms.openlocfilehash: 066f7ebe1cd8f981344e059797daa9d3f86bdf49
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71409054"
---
# <a name="verify-dns-functionality-to-support-directory-replication"></a>디렉터리 복제를 지원하는 DNS 기능 확인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

 Active Directory 복제를 방해할 수 있는 DNS (Domain Name System) 설정을 확인 하려면 먼저 도메인에 대해 DNS가 제대로 작동 하는지 확인 하는 기본 테스트를 실행 합니다. 기본 테스트를 실행 한 후에는 리소스 레코드 등록 및 동적 업데이트를 포함 하 여 DNS 기능의 다른 측면을 테스트할 수 있습니다.

모든 도메인 컨트롤러에서이 기본 DNS 기능 테스트를 실행할 수 있지만 일반적으로 복제 문제가 발생할 수 있는 도메인 컨트롤러 (예: 이벤트 Id 1844, 1925, 2087 또는를 보고 하는 도메인 컨트롤러)에서이 테스트를 실행 합니다. 2088 이벤트 뷰어 디렉터리 서비스 DNS 로그에 있습니다.



## <a name="running-the-domain-controller-basic-dns-testtitle"></a>도메인 컨트롤러 기본 DNS 테스트를 실행 하는</title>

기본 DNS 테스트는 DNS 기능의 다음 측면을 확인 합니다.


- **연결:** 이 테스트는 도메인 컨트롤러를 DNS에 등록할지 여부를 확인 하 고 <system>ping</system> 명령으로 연결할 수 있으며 LDAP/RPC (Lightweight Directory Access Protocol/remote procedure call) 연결을 포함 합니다. 도메인 컨트롤러에서 연결 테스트가 실패 하면 해당 도메인 컨트롤러에 대해 다른 테스트가 실행 되지 않습니다. 연결 테스트는 다른 DNS 테스트를 실행 하기 전에 자동으로 수행 됩니다.
- **필수 서비스:** 테스트를 통해 다음 서비스가 실행 중이 고 테스트 된 도메인 컨트롤러에서 사용할 수 있는지 확인 합니다. DNS 클라이언트 서비스, Net Logon service, 키 배포 센터 (KDC) 서비스 및 DNS 서버 서비스 (DNS가 도메인 컨트롤러에 설치 된 경우)
- **DNS 클라이언트 구성:**  테스트를 통해 DNS 클라이언트 컴퓨터의 모든 네트워크 어댑터에 있는 DNS 서버에 연결할 수 있는지 확인 합니다.
- **리소스 레코드 등록:** 테스트에서는 각 도메인 컨트롤러의 호스트 (A) 리소스 레코드가 클라이언트 컴퓨터에 구성 된 하나 이상의 DNS 서버에 등록 되어 있는지 확인 합니다.
- **영역 및 SOA (권한 시작):** 도메인 컨트롤러에서 DNS 서버 서비스를 실행 하는 경우 테스트에서는 Active Directory 도메인 영역에 대 한 SOA (권한 시작) 리소스 레코드와 Active Directory 도메인 영역이 있는지 확인 합니다.
- **루트 영역:** 루트 (.) 영역이 있는지 여부를 확인 합니다.

이러한 절차를 완료 하려면 최소한 Enterprise Admins의 구성원 이거나이에 해당 하는 권한이 있어야 합니다.

다음 절차를 사용 하 여 기본 DNS 기능을 확인할 수 있습니다.
     
### <a name="to-verify-basic-dns-functionality"></a>기본 DNS 기능을 확인 하려면:


1. 테스트 하려는 도메인 컨트롤러 또는 Active Directory Domain Services (AD DS) 도구가 설치 된 도메인 구성원 컴퓨터에서 관리자 권한으로 명령 프롬프트를 엽니다. 관리자 권한으로 명령 프롬프트를 열려면 **시작**을 클릭합니다. 
2. 검색 시작에 명령 프롬프트를 입력 합니다. 
3. 시작 메뉴 위쪽에서 명령 프롬프트를 마우스 오른쪽 단추로 클릭 한 다음 관리자 권한으로 실행을 클릭 합니다. 사용자 계정 컨트롤 대화 상자가 나타나면 표시되는 작업이 원하는 작업인지 확인한 다음 계속을 클릭합니다.
4. 명령 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다. `dcdiag /test:dns /v /s:<DCName> /DnsBasic /f:dcdiagreport.txt`
</br></br>&lt;DCName&gt;에 대 한 도메인 컨트롤러의 실제 고유 이름, NetBIOS 이름 또는 DNS 이름을 대체 합니다. 또는/s: 대신/e:를 입력 하 여 포리스트의 모든 도메인 컨트롤러를 테스트할 수 있습니다. /F 스위치는 파일 이름을 지정 합니다 .이 이름은 이전 명령에서 dcdiagreport입니다. 현재 작업 디렉터리 이외의 위치에 파일을 배치 하려는 경우 파일 경로 (예:/f: c:reportsdcdiagreport.txt.)를 지정할 수 있습니다.

5. 메모장 이나 유사한 텍스트 편집기에서 dcdiagreport 파일을 엽니다. 메모장에서 파일을 열려면 명령 프롬프트에 notepad dcdiagreport를 입력 한 다음 ENTER 키를 누릅니다. 다른 작업 디렉터리에 파일을 저장 한 경우 파일 경로를 포함 합니다. 예를 들어 파일을 c:reports에 배치한 경우 notepad c:reportsdcdiagreport.txt를 입력 한 다음 ENTER 키를 누릅니다.
6. 파일 아래쪽의 요약 테이블로 스크롤합니다. 
</br></br>요약 테이블에서 "경고" 또는 "실패" 상태를 보고 하는 모든 도메인 컨트롤러의 이름을 적어둡니다.  "DC: DCName" 문자열을 검색 하 여 자세한 브레이크 아웃 섹션을 찾아 문제가 있는 도메인 컨트롤러가 있는지 확인 하십시오. 여기서 DCName는 도메인 컨트롤러의 실제 이름입니다.

필요한 명확한 구성 변경이 표시 되는 경우 적절 하 게 구성 합니다. 예를 들어 도메인 컨트롤러 중 하나에 잘못 된 IP 주소가 있는 경우이를 수정할 수 있습니다. 그런 다음 테스트를 다시 실행 합니다.

구성 변경 내용의 유효성을 검사 하려면 적절 하 게/e: 또는/s: 스위치를 사용 하 여 Dcdiag/test: DNS/v 명령을 다시 실행 합니다. 도메인 컨트롤러에서 IPv6 (IP 버전 6)을 사용 하도록 설정 하지 않은 경우에는 테스트의 호스트 (AAAA) 유효성 검사 부분이 실패 하는 것으로 간주 되지만 네트워크에서 i p v 6을 사용 하지 않는 경우에는 이러한 레코드가 필요 하지 않습니다.
            
## <a name="verifying-resource-record-registration"></a>리소스 레코드 등록 확인
    
대상 도메인 컨트롤러는 DNS 별칭 (CNAME) 리소스 레코드를 사용 하 여 원본 도메인 컨트롤러 복제 파트너를 찾습니다. Windows server를 실행 하는 도메인 컨트롤러 (Windows Server 2003 SP1 (서비스 팩 1)로 시작)는 Fqdn (정규화 된 도메인 이름)을 사용 하 여 원본 복제 파트너를 찾을 수 있지만, 실패할 경우 NetBIOS namesthe의 별칭 (CNAME)을 사용 하 여 원본 복제 파트너를 찾을 수 있습니다. 리소스 레코드가 필요 하며 적절 한 DNS 기능이 제대로 작동 하는지 확인 해야 합니다. 
      
다음 절차를 사용 하 여 별칭 (CNAME) 리소스 레코드 등록을 비롯 한 리소스 레코드 등록을 확인할 수 있습니다.
      
### <a name="to-verify-resource-record-registrationtitle"></a>리소스 레코드 등록을 확인 하려면</title>


1. 관리자 권한으로 명령 프롬프트를 엽니다. 관리자 권한으로 명령 프롬프트를 열려면 시작을 클릭 합니다. 검색 시작에 명령 프롬프트를 입력 합니다. 
2. 시작 메뉴 위쪽에서 명령 프롬프트를 마우스 오른쪽 단추로 클릭 한 다음 관리자 권한으로 실행을 클릭 합니다. 사용자 계정 컨트롤 대화 상자가 나타나면 표시되는 작업이 원하는 작업인지 확인한 다음 계속을 클릭합니다.  </br></br>Dcdiag 도구를 사용 하 여 `dcdiag /test:dns /DnsRecordRegistration` 명령을 실행 하 여 도메인 컨트롤러 위치에 필요한 모든 리소스 레코드의 등록을 확인할 수 있습니다.

이 명령은 DNS의 다음 리소스 레코드에 대 한 등록을 확인 합니다.


- **별칭 (CNAME):** 복제 파트너를 찾는 guid (globally unique identifier) 기반 리소스 레코드
- **호스트 (A):** 도메인 컨트롤러의 IP 주소를 포함 하는 호스트 리소스 레코드
- **LDAP srv:** ldap 서버를 찾는 서비스 (SRV) 리소스 레코드
- **GC SRV**: 글로벌 카탈로그 서버를 찾는 서비스 (SRV) 리소스 레코드
- **PDC SRV**: 주 도메인 컨트롤러 (pdc) 에뮬레이터 작업 마스터를 찾는 서비스 (SRV) 리소스 레코드

다음 절차를 사용 하 여 별칭 (CNAME) 리소스 레코드 등록만을 확인할 수 있습니다.

### <a name="to-verify-alias-cname-resource-record-registration"></a>별칭 (CNAME) 리소스 레코드 등록을 확인 하려면

1. DNS 스냅인을 엽니다. DNS를 열려면 시작을 클릭 합니다. 검색 시작에 dnsmgmt.msc를 입력 한 다음 ENTER 키를 누릅니다. 사용자 계정 컨트롤 대화 상자가 나타나면 원하는 작업이 표시 되는지 확인 한 다음 계속을 클릭 합니다.
2. Dns 스냅인을 사용 하 여 DNS 서버 서비스를 실행 하는 도메인 컨트롤러를 찾습니다. 여기서 서버는 도메인 컨트롤러의 Active Directory 도메인과 동일한 이름을 사용 하 여 DNS 영역을 호스트 합니다.
3. 콘솔 트리에서 _msdcs 이름이 지정 된 영역을 클릭 합니다. Dns_Domain_Name.
4. 세부 정보 창에서 다음 리소스 레코드가 있는지 확인 합니다. 별칭 (CNAME) 리소스 레코드 Dsa_Guid. _msdcs. DNS 서버의 이름에 대 한 해당 호스트 (A) 리소스 레코드를 <placeholder>Dns_Domain_Name</placeholder> 합니다.

별칭 (CNAME) 리소스 레코드가 등록 되어 있지 않으면 동적 업데이트가 제대로 작동 하 고 있는지 확인 합니다. 다음 섹션의 테스트를 사용 하 여 동적 업데이트를 확인 합니다.
    
## <a name="verifying-dynamic-update"></a>동적 업데이트 확인
    
기본 DNS 테스트에서 리소스 레코드가 DNS에 존재 하지 않는 것으로 표시 되는 경우 동적 업데이트 테스트를 사용 하 여 Net Logon 서비스에서 리소스 레코드를 자동으로 등록 하지 않은 이유를 확인 합니다. Active Directory 도메인 영역이 보안 동적 업데이트를 수락 하 고 테스트 레코드 (_dcdiag_test_record)의 등록을 수행 하도록 구성 되어 있는지 확인 하려면 다음 절차를 따르십시오. 테스트 레코드는 테스트 후 자동으로 삭제 됩니다.

### <a name="to-verify-dynamic-updatetitle"></a>동적 업데이트</title> 확인 하려면


1. 관리자 권한으로 명령 프롬프트를 엽니다. 관리자 권한으로 명령 프롬프트를 열려면 시작을 클릭 합니다. 검색 시작에 명령 프롬프트를 입력 합니다. 시작 메뉴 위쪽에서 명령 프롬프트를 마우스 오른쪽 단추로 클릭 한 다음 관리자 권한으로 실행을 클릭 합니다. 사용자 계정 컨트롤 대화 상자가 나타나면 표시되는 작업이 원하는 작업인지 확인한 다음 계속을 클릭합니다.
2. 명령 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다. `dcdiag /test:dns /v /s:<DCName> /DnsDynamicUpdate`
   </br></br>&lt;DCName&gt;에 대 한 도메인 컨트롤러의 고유 이름, NetBIOS 이름 또는 DNS 이름을 대체 합니다. 또는/s: 대신/e:를 입력 하 여 포리스트의 모든 도메인 컨트롤러를 테스트할 수 있습니다. 도메인 컨트롤러에서 i p v 6을 사용 하도록 설정 하지 않은 경우에는 테스트의 호스트 (AAAA) 리소스 레코드 부분이 실패할 것으로 간주 됩니다 .이는 i p v 6을 사용 하지 않는 경우 정상적인 상태입니다.

보안 동적 업데이트가 구성 되지 않은 경우 다음 절차를 사용 하 여 구성할 수 있습니다.

### <a name="to-enable-secure-dynamic-updates"></a>보안 동적 업데이트를 사용 하도록 설정 하려면


1. DNS 스냅인을 엽니다. DNS를 열려면 시작을 클릭 합니다. 
2. 검색 시작에 dnsmgmt.msc를 입력 한 다음 ENTER 키를 누릅니다. 사용자 계정 컨트롤 대화 상자가 나타나면 원하는 작업이 표시 되는지 확인 한 다음 계속을 클릭 합니다.
3. 콘솔 트리에서 적절 한 영역을 마우스 오른쪽 단추로 클릭 한 다음 속성을 클릭 합니다.
4. 일반 탭에서 영역 유형이 Active Directory 통합 되었는지 확인 합니다.
5. 동적 업데이트에서 보안만을 클릭 합니다.

## <a name="registering-dns-resource-records"></a>DNS 리소스 레코드 등록
    
Dns 리소스 레코드가 원본 도메인 컨트롤러에 대 한 DNS에 표시 되지 않으면 동적 업데이트를 확인 하 고 DNS 리소스 레코드를 즉시 등록 하려면 다음 절차를 사용 하 여 수동으로 등록을 강제 적용할 수 있습니다. 도메인 컨트롤러의 Net Logon 서비스는 도메인 컨트롤러를 네트워크에 배치 하는 데 필요한 DNS 리소스 레코드를 등록 합니다. DNS 클라이언트 서비스는 별칭 (CNAME) 레코드가 가리키는 호스트 (A) 리소스 레코드를 등록 합니다.

### <a name="to-register-dns-resource-records-manuallytitle"></a>DNS 리소스 레코드를 수동으로 등록 하려면</title>


1. 관리자 권한으로 명령 프롬프트를 엽니다. 관리자 권한으로 명령 프롬프트를 열려면 시작을 클릭 합니다. 
2. 검색 시작에 명령 프롬프트를 입력 합니다. 
3. 시작 위쪽에서 명령 프롬프트를 마우스 오른쪽 단추로 클릭 한 다음 관리자 권한으로 실행을 클릭 합니다. 사용자 계정 컨트롤 대화 상자가 나타나면 표시되는 작업이 원하는 작업인지 확인한 다음 계속을 클릭합니다.
4. 원본 도메인 컨트롤러에서 도메인 컨트롤러 로케이터 리소스 레코드의 등록을 수동으로 시작 하려면 명령 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다. `net stop netlogon && net start netlogon`
5. 호스트 (A) 리소스 레코드의 등록을 수동으로 시작 하려면 명령 프롬프트에서 다음 명령을 입력 한 후 ENTER 키를 누릅니다. `ipconfig /flushdns && ipconfig /registerdns`
6. 명령 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다. `dcdiag /test:dns /v /s:<DCName>` </br></br>&lt;DCName&gt;에 대 한 도메인 컨트롤러의 고유 이름, NetBIOS 이름 또는 DNS 이름을 대체 합니다. 테스트의 출력을 검토 하 여 DNS 테스트가 통과 했는지 확인 합니다. 도메인 컨트롤러에서 i p v 6을 사용 하도록 설정 하지 않은 경우에는 테스트의 호스트 (AAAA) 리소스 레코드 부분이 실패할 것으로 간주 됩니다 .이는 i p v 6을 사용 하지 않는 경우 정상적인 상태입니다.
