---
ms.assetid: 709353b0-b913-4367-8580-44745183e2bc
title: "디렉터리 복제 지원 하기 위해 DNS 기능을 확인"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: 
ms.suite: na
ms.technology: identity-adds
ms.author: billmath
ms.date: 05/31/2017
ms.tgt_pltfrm: na
author: Femila
ms.openlocfilehash: 49f2795e1042438a50850fcb7fd8224eff2cca37
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="verify-dns-functionality-to-support-directory-replication"></a>디렉터리 복제 지원 하기 위해 DNS 기능을 확인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

 Active Directory 복제 방해가 될 수 있는 시스템 DNS (도메인 이름) 설정을 확인 하려면 DNS 도메인에 대 한 제대로 작동 하는지 확인 하 고 기본 테스트를 실행 하 여 시작할 수 있습니다. 기본 테스트를 실행 한 후에 기타 리소스 녹화 등록와 동적 업데이트를 포함 하 여 DNS 기능을 테스트할 수 있습니다.

도메인 컨트롤러에서 기본 DNS 기능의이 테스트를 실행 수 있지만 일반적으로 실행이 테스트 발생할 수 복제 문제 등 도메인 컨트롤러 이벤트 Id 1844 1925, 2087, 또는 2088를 보고 하 이벤트 뷰어 디렉터리 서비스 DNS 로그에 보고 있는 도메인 컨트롤러에 있습니다.



## <a name="running-the-domain-controller-basic-dns-testtitle"></a>도메인 컨트롤러 기본적인 DNS 테스트를 실행</title>

기본 DNS 테스트 DNS 기능의 다음과 같은 측면을 확인합니다.


- **연결이:** 테스트 도메인 컨트롤러, dns에서 등록 하 여 연결할 수 있는지 여부를 결정는 <system>ping</system> 명령을 실행 하 고 있는 경량 디렉터리 Access Protocol / 원격 프로시저 호출 LDAP/RPC () 연결 합니다. 연결 테스트 도메인 컨트롤러에 실패 하는 경우 해당 도메인 컨트롤러에 대해 다른 테스트 실행 됩니다. 다른 DNS 테스트를 실행 하기 전에 연결 테스트 자동으로 수행 됩니다.
- **필수 서비스:** 테스트 다음 서비스를 실행 중이 고 거친된 도메인 컨트롤러에서 사용할 수 있는지 확인: DNS 클라이언트 서비스, Netlogon 서비스, 키 메일 센터 (KDC) 서비스 및 DNS 서버 서비스 (경우 DNS 도메인 컨트롤러에 설치 됩니다).
- **DNS 클라이언트 구성:** 테스트 DNS 서버 DNS 클라이언트 컴퓨터의 모든 네트워크 어댑터에는 연결할 수 있는지 확인 합니다.
- **리소스 레코드 등록:** 테스트 각 도메인 컨트롤러의 (A) 호스트 리소스 레코드 DNS 서버 클라이언트 컴퓨터에서 구성 된 중 하나에 등록 되어 있는지 확인 합니다.
- **영역을 시작 하면 (soa)의:** 도메인 컨트롤러 DNS 서버 서비스를 실행 하는 경우 테스트 Active Directory 도메인 영역과 시작 Active Directory 도메인 영역에 대 한 리소스 레코드 (soa) 있는지를 확인 합니다.
- **루트 영역:** 루트 (.) 영역 있는지 여부를 확인 합니다.

오른쪽 단추를 또는 엔터프라이즈 관리자의 회원이이 절차를 수행 하는 데 필요한 최소입니다.

기본 DNS 기능을 확인 하려면 다음 절차에 사용할 수 있습니다.
     
### <a name="to-verify-basic-dns-functionality"></a>기본 DNS 기능을 확인 합니다.


1. 테스트 하 고 싶은 도메인 컨트롤러에서 또는 DS Active Directory 도메인 서비스 (AD) 도구가 설치 되어 있는 도메인 회원 컴퓨터에서 관리자 권한으로 명령 프롬프트를 엽니다. 관리자 권한으로 명령 프롬프트를 열을 클릭 **시작**합니다. 
2. 검색 시작에서 명령 프롬프트에 입력 합니다. 
3. 시작 메뉴 맨 명령 프롬프트를 마우스 오른쪽 단추로 클릭 한 다음 관리자 권한으로 실행을 클릭 합니다. 사용자 계정 컨트롤 대화 상자가 표시 되 면 원하는, 작업이 표시 되는지 확인 하 고 클릭 계속 합니다.
4. 명령 프롬프트에서 다음 명령을 입력 하 고 enter 다음과 같습니다. `dcdiag /test:dns /v /s: &lt;DCName&gt; /DnsBasic f:/dcdiagreport.txt`
</br></br>실제 고유 이름, NetBIOS 이름 또는 DNS 도메인 컨트롤러에 이름을 대체 &lt;DCName&gt;합니다. 다른 방법으로 /e: /s: 대신를 입력 하 여 모든 도메인 컨트롤러의 숲 속의 테스트할 수 있습니다. /F 스위치는 이전 명령에서 dcdiagreport.txt 파일 이름을 지정 합니다. 현재 작업 디렉터리 다른 위치에 있는 파일을 저장 하려면 /f:c:reportsdcdiagreport.txt 등 파일 경로 지정할 수 있습니다.

5. 메모장 또는 다른 텍스트 편집기에 dcdiagreport.txt 파일을 엽니다. 파일을 열려고 메모장에서 명령 프롬프트를 메모장 dcdiagreport.txt 입력 한 다음 ENTER 키를 누릅니다. 다른 작업 디렉터리에 파일을 저장 하는 경우 해당 파일에 대 한 경로 포함 됩니다. 예를 들어, c:reports에 파일을 저장 하는 경우 메모장 c:reportsdcdiagreport.txt 입력 한 다음 ENTER 키를 누릅니다.
6. 해당 파일의 아래쪽에 있는 요약 표 스크롤하십시오. 
</br></br>요약 표에 "경고" 또는 "실패" 상태를 보고 하는 모든 도메인 컨트롤러의 이름을 note 합니다.  자세한 분리 섹션 DCName은 도메인 컨트롤러의 실제 이름 문자열 "DC:: DCName"을 검색 하 여 검색 하 여 문제가 도메인 컨트롤러 되었는지 확인 하십시오.

필요한 확실 한 구성 변경 표시 되 면를 적절 하 게 확인 합니다. 예를 들어, 명백히 잘못 된 IP 주소를는 도메인 컨트롤러 중 하나를 발견 하면 해결할 수 있습니다. 그런 다음 다시 테스트를 실행 합니다.

구성 변경 유효성을 검사 하기 다시 /e: 또는 /s: 스위치를 적절 하 게 Dcdiag /test:DNS /v 명령을 실행 합니다. 호스트 (AAAA) 유효성 검사에 실패 테스트 일부 됩니까 IP IPv6 버전 6 () 도메인 컨트롤러에서 사용할 수 없는 경우 하지만 IPv6에서 네트워크를 사용 하지 않는 경우이 레코드 필요 하지 않습니다.
            
## <a name="verifying-resource-record-registration"></a>리소스 기록 등록 확인
    
대상 도메인 컨트롤러 DNS (CNAME) 별칭 리소스 레코드를 사용 하 여 도메인 컨트롤러 복제 파트너 소스를 찾을 수 있습니다. 또는 Windows Server (서비스 팩 1 (SP1) Windows Server 2003로 시작)를 실행 하는 도메인 컨트롤러 정식된 Fqdn (도메인 이름)을 사용 하 여 복제 파트너 소스를 찾을 수 있지만 실패 하는 경우, NetBIOS namesthe 출현 (CNAME) 별칭 리소스 기록의 예상 되는 작동 하는 올바른 dns 확인 해야 합니다. 
      
다음 절차 리소스 기록 등록을 리소스 기록 등록 별칭 (CNAME)를 포함 하 여 확인 하기 위해 사용할 수 있습니다.
      
### <a name="to-verify-resource-record-registrationtitle"></a>리소스 녹화 등록을 확인 하려면</title>


1. 관리자 권한으로 명령 프롬프트를 엽니다. 관리자 권한으로 명령 프롬프트를 열려면 시작을 클릭 합니다. 검색 시작에서 명령 프롬프트에 입력 합니다. 
2. 시작 메뉴 맨 명령 프롬프트를 마우스 오른쪽 단추로 클릭 한 다음 관리자 권한으로 실행을 클릭 합니다. 사용자 계정 컨트롤 대화 상자가 표시 되 면 원하는, 작업이 표시 되는지 확인 하 고 클릭 계속 합니다.  </br></br>Dcdiag 도구를 사용 하 여 실행 하는 도메인 컨트롤러 위치에 대 한 필요한 모든 리소스 기록의 등록을 확인 하 고 `dcdiag /test:dns /DnsRecordRegistration` 명령을 합니다.

이 명령을 다음 리소스 레코드 dns에서 등록을 사항을 확인합니다.


- **별칭 (CNAME):** 고유 식별자 (GUID)-복제 파트너 찾는 리소스 기록 기반
- **호스트 (A):** 도메인 컨트롤러의 IP 주소를 포함 하 고 호스트 리소스 기록
- **LDAP SRV:** LDAP 서버를 찾습니다 (SRV) 서비스 리소스 레코드
- **GC SRV**: 전 세계를 찾습니다 (SRV) 서비스 리소스 레코드 카탈로그 서버
- **PDC SRV**: 주 도메인 컨트롤러 (PDC) 에뮬레이터가 작업 마스터 찾고 있는 서비스 (SRV) 리소스 기록

다음 절차 등록을 확인 하려면 (CNAME) 별칭 리소스 기록만 사용할 수 있습니다.

### <a name="to-verify-alias-cname-resource-record-registration"></a>(CNAME) 별칭 리소스 녹화 등록을 확인 하려면

1. DNS 끌기 기능을 엽니다. DNS를 열려면 시작을 클릭 합니다. 검색 시작에서 dnsmgmt.msc 입력 한 다음 ENTER 키를 누릅니다. 사용자 계정 컨트롤 대화 상자가 표시 되 고 계속을 클릭 한 다음 원하는 조치를 표시 되는지 확인 합니다.
2. DNS 스냅인을 사용 하 여 서버 Active Directory 도메인 도메인 컨트롤러의 이름이 같은 DNS 영역을 호스트 DNS 서버 서비스가 실행 되는 도메인 컨트롤러를 찾습니다.
3. 콘솔 트리에서 _msdcs 라고 하는 영역을 클릭 합니다. Dns_Domain_Name 합니다.
4. 세부 정보 창에서 다음 리소스 레코드 있는지 확인: Dsa_Guid._msdcs 라는 (CNAME) 별칭 리소스 레코드 합니다. <placeholder>Dns_Domain_Name</placeholder> DNS 서버 이름에 대 한 리소스 레코드 (를)는 해당 호스트 하 고 있습니다.

(CNAME) 별칭 리소스 기록 등록 되지 않은 경우 해당 동적 업데이트 제대로 작동 확인 합니다. 동적 업데이트를 확인 하는 다음 섹션에서 테스트를 수행 합니다.
    
## <a name="verifying-dynamic-update"></a>동적 업데이트 확인
    
기본 DNS 테스트 리소스 레코드 DNS에 존재 하지 않는 프로그램, 동적 업데이트 테스트를 사용 하 여 이유 Netlogon 서비스 등록 하지 않은 리소스 레코드 자동으로 확인 합니다. 다음 절차를 사용 하 Active Directory 도메인 영역 동적 보안 업데이트를 허용 하도록 하 고 테스트 기록 (_dcdiag_test_record) 등록 하도록 구성 되어 있는지 확인 합니다. 테스트 레코드 테스트 완료 한 후 자동으로 삭제 됩니다.

### <a name="to-verify-dynamic-updatetitle"></a>동적 업데이트를 확인 하려면</title>


1. 관리자 권한으로 명령 프롬프트를 엽니다. 관리자 권한으로 명령 프롬프트를 열려면 시작을 클릭 합니다. 검색 시작에서 명령 프롬프트에 입력 합니다. 시작 메뉴 맨 명령 프롬프트를 마우스 오른쪽 단추로 클릭 한 다음 관리자 권한으로 실행을 클릭 합니다. 사용자 계정 컨트롤 대화 상자가 표시 되 면 원하는, 작업이 표시 되는지 확인 하 고 클릭 계속 합니다.
2. 명령 프롬프트에서 다음 명령을 입력 하 고 enter 다음과 같습니다. 

    dcdiag /test:dns /v /s:&lt;DCName&gt; /DnsDynamicUpdate
</br></br>대체 고유 이름, NetBIOS 이름 또는 DNS 도메인 컨트롤러에 이름을 &lt;DCName&gt;합니다. 다른 방법으로 /e: /s: 대신를 입력 하 여 모든 도메인 컨트롤러의 숲 속의 테스트할 수 있습니다. IPv6 도메인 컨트롤러에서 사용할 수 없는 경우 호스트 (AAAA) 리소스 기록 일부 실패 하 고 테스트 IPv6 사용 하지 않는 경우 정상적인 현상입니다는 소요 될 수 있습니다.

동적 보안 업데이트를 구성 되지 않은 경우 다음 절차 구성에 사용할 수 있습니다.

### <a name="to-enable-secure-dynamic-updates"></a>동적 보안 업데이트를 사용 하도록 설정 하려면


1. DNS 끌기 기능을 엽니다. DNS를 열려면 시작을 클릭 합니다. 
2. 검색 시작에서 dnsmgmt.msc 입력 한 다음 ENTER 키를 누릅니다. 사용자 계정 컨트롤 대화 상자가 나타나면 작업을 계속을 클릭 한 다음를 표시 되는지 확인 합니다.
3. 콘솔 트리에서 해당 영역을 마우스 오른쪽 단추로 클릭 하 고 속성을 클릭 합니다.
4. 일반 탭 영역 종류 Active Directory 통합 인지 확인 합니다.
5. 동적 업데이트의 보안을만 누릅니다.

## <a name="registering-dns-resource-records"></a>DNS 레코드 리소스 등록
    
원본 도메인 컨트롤러에 대 한 리소스 DNS 레코드 DNS에 표시 되지 않으면, 동적 업데이트를 확인 한 리소스 DNS 레코드 즉시 등록할 다음 절차를 사용 하 여 수동으로 등록을 할 수 있습니다. 도메인 컨트롤러에 Netlogon 서비스에는 네트워크에 있는 도메인 컨트롤러에 필요한 리소스 DNS 레코드에 등록 합니다. DNS 클라이언트 서비스 호스트 (는) 리소스 레코드 별칭 (CNAME) 레코드가 가리키는 등록 합니다.

### <a name="to-register-dns-resource-records-manuallytitle"></a>수동으로 리소스 DNS 레코드 등록 하려면</title>


1. 관리자 권한으로 명령 프롬프트를 엽니다. 관리자 권한으로 명령 프롬프트를 열려면 시작을 클릭 합니다. 
2. 검색 시작에서 명령 프롬프트에 입력 합니다. 
3. 시작의 맨 명령 프롬프트를 마우스 오른쪽 단추로 클릭 한 다음 관리자 권한으로 실행을 클릭 합니다. 사용자 계정 컨트롤 대화 상자가 표시 되 면 원하는, 작업이 표시 되는지 확인 하 고 클릭 계속 합니다.
4. 도메인 컨트롤러 locator 리소스의 등록을 시작할 수 원본 도메인 컨트롤러 명령 프롬프트에서 수동으로 다음 명령을 입력 기록과 ENTER 키를 누릅니다. `net stop net logon &amp; net start net logon`
5. 호스트의 등록을 시작 하 리소스 레코드 (를) 수동으로 명령 프롬프트에서 다음 명령을 입력 하 고 enter: `ipconfig /flushdns &amp; ipconfig /registerdns`
6. 명령 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다: dcdiag /test:dns /v /s:&lt;DCName&gt; </br>,</br>대체 고유 이름, NetBIOS 이름 또는 DNS 도메인 컨트롤러에 이름을 &lt;DCName&gt;합니다. DNS 테스트 전달 되도록 테스트 출력을 검토 합니다. IPv6 도메인 컨트롤러에서 사용할 수 없는 경우 호스트 (AAAA) 리소스 기록 일부 실패 하 고 테스트 IPv6 사용 하지 않는 경우 정상적인 현상입니다는 소요 될 수 있습니다.
