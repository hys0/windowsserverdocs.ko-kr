---
ms.assetid: b11f7a65-ec7b-4c11-8dc4-d7cabb54cd94
title: "Active Directory 복제 문제 해결"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: eb93ea7cab297d70aa86b71bd5466004e47bfeaf
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshooting-active-directory-replication-problems"></a>Active Directory 복제 문제 해결

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


Active Directory 복제 문제는 여러 다양 한 소스 있을 수 있습니다. 예를 들어, 시스템 DNS (도메인 이름) 문제, 네트워킹 문제 또는 보안 문제의 발생할 수 있습니다 모두 Active Directory 복제 실패 합니다. 

이 항목의 나머지 부분 도구, Active Directory 복제 오류를 해결 하는 일반 방법을 설명 합니다. Active Directory 복제 문제를 해결 하는 방법을 보여 주는 실습을 참조 하세요. [가상 랩 TechNet: Active Directory 복제 오류 문제 해결](https://go.microsoft.com/?linkid=9844718)

다음 주제 증상, 원인 및 특정 복제 오류를 해결 하는 방법을 설명 합니다.
   
[수정 복제 느린 개체 문제 (이벤트 Id 1388, 1988 년 2042)](https://technet.microsoft.com/library/cc949124.aspx)
  
[복제 보안 문제 해결](https://technet.microsoft.com/library/cc949132.aspx)

[수정 복제 DNS 조회 문제 (이벤트 Id 1925 년 2087, 2088)](https://technet.microsoft.com/library/cc949133.aspx)
  
[(이벤트 ID 1925) 복제 연결 문제 해결](https://technet.microsoft.com/library/cc949131.aspx)
  
[(이벤트 ID 1311) 복제 토폴로지 문제 해결](https://technet.microsoft.com/library/cc949129.aspx)
  
[디렉터리 복제 지원 하기 위해 DNS 기능을 확인](https://technet.microsoft.com/library/dd728017.aspx)
  
[오류 복제 마지막이 서버 복제가 이후 때의 삭제 표시 기간 초과 했기 때문에이 서버와 8614 Active Directory 복제 수 없는](https://technet.microsoft.com/library/replication-error-8614-the-active-directory-cannot-replicate-with-this-server-because-the-time-since-the-last-replication-with-this-server-has-exceeded-the-tombstone-lifetime.aspx)
     
[복제 오류 8524 The DSA 작업이을 DNS 조회 실패 진행할 수 하지 않습니다.](https://technet.microsoft.com/library/replication-error-8524-the-dsa-operation-is-unable-to-proceed-because-of-a-dns-lookup-failure.aspx)
   
[소스 8456 또는 8457 복제 오류 | 현재 대상 서버 복제가 요청을 거부](https://technet.microsoft.com/library/replication-error-8456-the-source-server-is-currently-rejecting-replication-requests-or-replication-error-8457-the-destination-server-is-currently-rejecting-replication-requests.aspx)
   
[복제 오류 8453 복제 액세스 거부 된](https://technet.microsoft.com/library/replication-error-8453-replication-access-was-denied.aspx)
  
[복제 오류 8452 이름 컨텍스트 제거 하 고 또는 지정된 서버에서 복제 되지 않으면](https://technet.microsoft.com/library/replication-error-8452-the-naming-context-is-in-the-process-of-being-removed-or-is-not-replicated-from-the-specified-server.aspx)
   
[복제 오류 5 액세스 거부](https://technet.microsoft.com/library/replication-error-5-access-is-denied.aspx)
  

      
      

  
[복제 오류-2146893022 대상 사용자 이름이 잘못 하지 않습니다.](https://technet.microsoft.com/library/replication-error-2146893022-the-target-principal-name-is-incorrect.aspx)
  

      
      

  
[복제 오류 1753는 사용할 수 있는 더 많은 끝점 끝점 맵 편집기에서 사용할 수 있는](https://technet.microsoft.com/library/replication-error-1753-there-are-no-more-endpoints-available-from-the-endpoint-mapper.aspx)
  

      
      

  
[복제 1722 오류가 제공 됩니다.](https://technet.microsoft.com/library/replication-error-1722-the-rpc-server-is-unavailable.aspx)
  

      
      

  
[복제 오류 1396 로그온 실패 대상 계정 이름을 잘못 되었습니다.](https://technet.microsoft.com/library/replication-error-1396-logon-failure-the-target-account-name-is-incorrect.aspx)
  

      
      

  
[복제 오류 1-256 원격 시스템 사용할 수입니다.](https://technet.microsoft.com/library/replication-error-1256-the-remote-system-is-not-available.aspx)
  

      
      

  
[하드 디스크, 디스크 작업 액세스 하는 동안 복제 오류 1127 재시도 후에 실패](https://technet.microsoft.com/library/replication-error-1127-while-accessing-the-hard-disk-a-disk-operation-failed-even-after-retries.aspx)
  

      
      

  
[복제 오류 8451 복제 작업 데이터베이스 오류가 발생 했습니다.](https://technet.microsoft.com/library/replication-error-8451-the-replication-operation-encountered-a-database-error.aspx)
  

      
      

  
[개체를 만들려면이 제공 되었습니다 복제 오류 8606 부족 특성](https://technet.microsoft.com/library/replication-error-8606-insufficient-attributes-were-given-to-create-an-object.aspx)
  

## <a name="introduction-and-resources-for-troubleshooting-active-directory-replication"></a>소개 및 Active Directory 복제 문제 해결에 대 한 리소스

돌아오는 또는 아웃 바운드 복제 오류로 인해 복제 토폴로지, 복제 일정, 도메인 컨트롤러, 사용자가, 컴퓨터, 암호, 보안 그룹, 그룹 구성원 및 그룹 정책을 도메인 컨트롤러 간에 일치 하지 않을 수를 나타내는 Active Directory 개체 합니다. 디렉터리의 일관성 및 복제 실패 운영 오류 또는 된 작업에 연결 하는 도메인 컨트롤러에 따라 결과가 일관 발생 하 고 그룹 정책을 적용 하 않도록 고 액세스 제어 권한을 수 있습니다. Active Directory Domain Services (AD DS) 네트워크 연결, 이름 해상도, 인증 하 고 승인, 디렉터리 데이터베이스, 복제 토폴로지 복제 엔진에 따라 다릅니다. 복제 문제의 근본 원인의 확실 하지 않으면 원인 체계적으로 제거가 필요 많은 원인은 원인을 파악 합니다. 

복제를 모니터링 하 고 오류를 진단 하는 UI 기반 도구를 참조 하세요. [Active Directory 복제 상태 도구](https://www.microsoft.com/download/details.aspx?id=30005)합니다. 또한는 [실습](https://go.microsoft.com/?linkid=9844718) 오류를 해결 하 Active Directory 복제 상태 및 기타 도구를 사용 하는 방법을 보여 주는 합니다. 

전체 문서 Repadmin 도구를 사용 하 여 Active Directory 문제를 해결 하는 방법을 설명 하는 복제는 사용할 수 있습니다. 참조 [모니터링 하 고 문제를 해결 Active Directory 복제 사용 하 여 Repadmin](https://go.microsoft.com/fwlink/?LinkId=122830)합니다.

다음 기술 참조 Active Directory 복제 작동 하는 방법에 대 한 정보를 참조:


- [Active Directory 복제 모델 기술 참조](https://go.microsoft.com/fwlink/?LinkId=65958)
- [활성 디렉터 복제 토폴로지 기술 참조](https://go.microsoft.com/fwlink/?LinkId=93578)

## <a name="event-and-tool-solution-recommendations"></a>해결 방법으로 추천 이벤트 및 도구

것이 좋습니다 빨간색 (오류) 및 디렉터리 서비스 이벤트 로그에 노란색 (경고) 이벤트 특정 제약을 소스 또는 목적지 도메인 컨트롤러에서 복제 오류가 발생 하는 것이 좋습니다. 이벤트 메시지 단계는 해결 방법에 대 한 제안, 이벤트를 설명 하는 단계를 시도 합니다. Repadmin 도구 및 기타 진단 도구 또한 복제 오류를 해결 하는 데 도움이 되는 정보를 제공 합니다. 

Repadmin 복제 문제를 해결 하는 데 사용에 대 한 자세한 내용은 참조 [모니터링 하 고 문제를 해결 Active Directory 복제 사용 하 여 Repadmin](https://go.microsoft.com/fwlink/?LinkId=122830)합니다.

## <a name="ruling-out-intentional-disruptions-or-hardware-failures"></a>하드웨어 오류 또는 의도적 중단 배제

때때로 복제 오류 의도적 중단으로 인해 발생합니다. 예를 들어, Active Directory 복제 문제를 해결할 때 발생 하지 않도록 의도적 연결 끊기 및 하드웨어 오류 또는 업그레이드 먼저 합니다.

### <a name="intentional-disconnections"></a>의도 연결 끊기

복제 준비 사이트에서 빌드된 및 현재 오프 라인 기다리고 최종 생산 사이트 (원격 사이트를 지점 등)에 배포 하는 도메인 컨트롤러를 시도 하는 도메인 컨트롤러를 복제 오류 보고는 경우 해당 복제 오류 지급할 수 있습니다. 지속적인 오류를 일으키는 도메인 컨트롤러 다시 연결할 때까지 오랜 시간 동안 복제 토폴로지에서 도메인 컨트롤러를 구분 하 않도록 하려면 구성원 서버로 처음 해당 컴퓨터에 추가 하 고 설치 미디어 (IFM)를에서 사용 하 여 Active Directory Domain Services (AD DS)를 설치 하려면 것이 좋습니다. (예: CD, DVD 또는 기타 미디어) 이동식 미디어에 저장 하 고 대상 사이트를 제공할 수 있는 설치 미디어를 만드는 Ntdsutil 명령줄 도구를 사용할 수 있습니다. 그런 다음 복제 사용 하지 않으면 사이트에 도메인 컨트롤러의 AD DS 설치 설치 미디어를 사용할 수 있습니다. 

### <a name="hardware-failures-or-upgradestitle"></a>하드웨어 오류 또는 업그레이드</title>

하드웨어 오류가 (예를 들어, 실패 하드 드라이브, 마더보드 또는 디스크 하위 시스템)으로 인해 복제 문제가 발생 하는 경우 하드웨어 문제를 해결할 수 있도록 서버 소유자를 게 알립니다.

주기적으로 하드웨어를 업그레이드 되지 서비스에 도메인 컨트롤러 발생할 수 있습니다. 서버 소유자의 사전에 이러한 중단 통신 좋은 시스템 있는지 확인 합니다.

### <a name="firewall-configuration"></a>방화벽 구성

기본적으로 복제 원격 프로시저 호출 Active Directory (Rpc) 135 포트에서 RPC Endpoint 맵 편집기 (RPCSS)를 통해 사용 가능한 포트를 통해 동적으로 수행 합니다. 해당 고급 보안이 포함된 Windows 방화벽 및 기타 방화벽 복제 수 있도록 올바르게 구성 되어 있는지 확인 합니다. 지정 Active Directory 복제와 포트 설정에 대 한 포트에 대 한 내용은 [224196 Microsoft 기술 자료 문서](https://go.microsoft.com/fwlink/?LinkId=22578)합니다. 

사용 하 여 Active Directory 복제 포트에 대 한 정보를 참조 하세요. [Active Directory 복제 도구 및 설정](https://go.microsoft.com/fwlink/?LinkId=123774)합니다. 

방화벽을 통해 Active Directory 복제 관리에 대 한 내용은 [방화벽을 통해 Active Directory 복제](https://go.microsoft.com/fwlink/?LinkId=123775)합니다.

## <a name="responding-to-failure-of-an-outdated-server-running-windows-2000-server"></a>Windows 2000 Server 실행 하는 오래 서버의 오류에 대 한 응답

Windows 2000 Server 실행 하는 도메인 컨트롤러의 삭제 표시 기간 일 보다 오래 실패 한 경우 해결 항상 같습니다. 

1. 회사 네트워크에서 서버 사설망으로 이동 합니다.
2. 강제로 Active Directory를 제거 하거나 운영 체제를 다시 설치 합니다.
3. 서버 개체 다시 수 있도록 Active Directory에서 서버 메타 데이터를 제거 합니다. 

대부분의 Windows 운영 체제에 대 한 서버 메타 데이터를 정리 하려면 스크립트를 사용할 수 있습니다. 이 스크립트 사용에 대 한 내용은 [Active Directory 도메인 컨트롤러 메타 데이터를 제거](https://go.microsoft.com/fwlink/?LinkID=123599)합니다. 

기본적으로 삭제 된 NTDS 설정을 개체 14 일 동안 자동으로 다시 됩니다. 따라서 서버 메타 데이터를 제거 하지 않는 경우 (Ntdsutil 또는 정리 메타 데이터를 수행 하려면 앞에서 언급 한 스크립트 사용) 서버 메타 데이터 복제 시도 발생 하 라는 메시지가 표시 되는 디렉터리에 복원 됩니다. 이 경우 오류 누락 된 도메인 컨트롤러를 사용 하 여 복제 수 없기 때문 영구적으로 기록 됩니다.

## <a name="root-causes"></a>근본 원인

연결 끊기 의도적, 하드웨어 오류 및 오래 Windows 2000 도메인 컨트롤러 배제 복제 문제의 나머지 거의 언제나 있는지 다음 근본 원인 중 하나 다음과 같습니다. 


- 네트워크 연결: 네트워크 연결을 사용 하지 못할 또는 네트워크 설정 올바르게 구성 되지 않습니다.
- 이름 확인: DNS 구성 오류는 일반적인 원인 복제 실패 합니다.
- 인증과: 인증과 문제 도메인 컨트롤러의 복제 파트너에 연결 하려고 할 때 "액세스 거부" 오류가 발생 합니다.
- 디렉터리 데이터베이스 (스토어): 디렉터리 데이터베이스 복제 시간 초과를 유지할 빨리 거래를 처리 하지 못할 수도 있습니다.
- 복제 엔진: 간 복제 일정 너무 짧은 인 복제 큐 너무 커서 아웃 바운드 복제 일정에서 요구 하는 시간에를 처리할 수 있습니다. 이 경우 일부 변경의 복제 멈춘된 indefinitelypotentially 수를 초과 삭제 표시 기간 충분 한 시간입니다.
- 복제 토폴로지: 도메인 컨트롤러 (실제 넓게 네트워크) 또는 (VPN) 가상 개인 네트워크 연결에 매핑하는 간 AD DS 링크 있어야 합니다. 네트워크의 실제 사이트 토폴로지별 지원 되지 않는 복제 토폴로지의 AD DS의 개체를 만들 잘못 구성 된 토폴로지 필요한 복제 작동 하지 않습니다.

## <a name="general-approach-to-fixing-problems"></a>문제 해결에 대 한 일반 접근 방식

일반 방법을 복제 문제 해결에 사용: 


1. Repadmin.exe 매일 복제 상태를 사용 하 여 하거나 매일 복제 상태를 모니터링 합니다.
2. 이벤트 메시지 및이 가이드 설명 하는 방법을 사용 하 여 적절 한 시간에 보고 된 오류 해결 하려고 합니다. 소프트웨어 수 있는 문제를 일으키는 경우 다른 해결 방법으로 계속 하기 전에 소프트웨어를 제거 합니다.
3. 모든 알려진된 방법을 사용 하 여 복제 실패 하는 문제를 해결할 수 없는, AD DS 서버에서 제거 하 고 AD DS 다시 설치 합니다. AD DS 다시 설치에 대 한 자세한 내용은 참조 [도메인 컨트롤러 역할 해제](https://go.microsoft.com/fwlink/?LinkId=128290)합니다.
4. AD DS를 제거할 수 없는 정상적으로 서버 네트워크에 연결 되어 있는 동안 다음 방법 중 하나를 사용 하 여 문제를 해결 하려면:
 

    - 서버 메타 데이터를 정리 AD DS 제거에 DSRM 디렉터리 서비스 복원 모드 (), 강제로 고 AD DS 다시 설치 합니다.
    - 운영 체제를 다시 설치 하 고 다시 도메인 컨트롤러 합니다.

AD DS 제거 강제로 대 한 자세한 내용은 참조 [도메인 컨트롤러의 제거 강제로](https://go.microsoft.com/fwlink/?LinkId=128291)합니다.

## <a name="using-repadmin-to-retrieve-replication-statustitle"></a>Repadmin 복제 상태 검색을 사용 하 여</title>

복제 상태가 가장 좋은 방법은 디렉터리 서비스의 상태를 확인할 수 있습니다. 오류 없이 복제가 작동, 온라인 하는 도메인 컨트롤러 알 수 있습니다. 또한 다음과 같은 시스템과 서비스 작동 알고 다음과 같습니다.


- DNS infrastructure
- Kerberos 인증 프로토콜
- Windows 시간 (W32time) 서비스
- 원격 프로시저 호출, RPC)
- 네트워크에 연결

Repadmin를 사용 하 여 사용자 숲 속의 모든 도메인 컨트롤러의 복제 상태 심사 하 명령을 실행 하 여 매일 복제 상태를 모니터링 합니다. 절차 생성 복제 오류에 대 한 필터 및 Microsoft Excel에서 열 수 있는.csv 합니다.

다음 절차는 숲 속의 모든 도메인 컨트롤러의 복제 상태를 검색할 수 사용할 수 있습니다. 
      
요구 사항
      
회원 **엔터프라이즈 관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다. 

도구: 


- Repadmin.exe 
- Excel (Microsoft Office)

### <a name="to-generate-a-repadmin-showrepl-spreadsheet-for-domain-controllers"></a>한 repadmin 얻기 위해 /showrepl 도메인 컨트롤러의 스프레드시트



1. 관리자 권한으로 명령 프롬프트를 열고: 시작 메뉴에서 명령 프롬프트를 마우스 오른쪽 단추로 클릭 한 다음 관리자 권한으로 실행을 클릭 합니다. 사용자 계정 컨트롤 대화 상자가 나타나면 필요한 경우 엔터프라이즈 관리자 자격 증명을 입력 한 다음 계속을 클릭 합니다. 
2. 명령 프롬프트에서 다음 명령을 입력 하 고 enter 다음과 같습니다.`repadmin /showrepl * /csv &gt;showrepl.csv`
3. Excel을 엽니다.
4. Office 단추, 열기를 클릭 하 고 showrepl.csv 이동 다음 열기를 클릭 합니다.
5. 숨기 거 나 열 A 뿐만 아니라 전송 형식을 열 다음과 같이 삭제 합니다.
6. 숨기 거 나 삭제 하려는 열을 선택 합니다.
      

    - 열을 숨기려면 열을 마우스 오른쪽 단추로 클릭 한 다음 숨기기를 클릭 합니다.
    - 열을 삭제, 선택한 열을 마우스 오른쪽 단추로 클릭 한 다음 삭제를 클릭 합니다.
7. 아래에 있는 열 머리글 행 1 행을 선택 합니다. 보기 탭 틀 고정을 클릭 하 고 행 고정 위쪽을 클릭 합니다.
8. 전체 스프레드시트를 선택 합니다. 데이터 탭에서 필터를 클릭 합니다.
9. 성공 지난번 열에서 아래쪽 화살표를 클릭 한 다음 오름차순를 클릭 합니다.
10. 소스 DC 열에서 필터 아래쪽 화살표를 클릭 하 고 텍스트 필터를 가리킨 클릭 한 다음 사용자 지정 필터 합니다.
11. 사용자 지정 필터 대화 상자의 클릭에를 포함 하지 않음 행을 표시 합니다. 옆에 있는 텍스트 상자에 입력 <userInput>델</userInput> 삭제 도메인 컨트롤러에 대 한 결과 보기에서 제거 합니다.
12. 오류 지난번 열 있지만 값 동일, 하지 않으며 0 값을 입력 한 다음 사용에 대 한 11 단계를 반복 합니다.
13. 복제 오류를 해결 합니다.

스프레드시트 숲 모든 도메인 컨트롤러에 대 한 소스 복제 파트너 표시 시간 복제가 마지막 발생 한 마지막 복제 오류가 발생 하는 각 명명 컨텍스트 (파티션)에 대 한 시간입니다. Excel에서 필터를 사용 하 여 실패 도메인 컨트롤러만 또는 최소 또는 대부분 현재 있는 도메인 컨트롤러 작업 도메인 컨트롤러에만 위한 복제 건강 볼 수 있으며 성공적으로 복제 하는 복제 파트너 볼 수 있습니다.

## <a name="replication-problems-and-resolutions"></a>복제 문제 및 해결 방법
    
이벤트 메시지 및 응용 프로그램 또는 서비스가 작업을 시도 때 발생 하는 다양 한 오류 메시지에 복제 문제가 보고 됩니다. 이 가장 좋습니다 이러한 메시지 복제 상태를 검색할 때 나 모니터링 응용 프로그램에 의해 수집 됩니다.

대부분의 복제 문제 디렉터리 서비스 이벤트 로그에 기록 된 이벤트 메시지가 표시 됩니다. 출력에서 오류 메시지 중 형식으로 복제 문제를 식별도 수 있는 <system>repadmin /showrepl</system> 명령 합니다. 

### <a name="repadmin-showrepl-error-messages-that-indicate-replication-problems"></a>Repadmin /showrepl 복제 문제가 있음을 나타내는 오류 메시지가

Active Directory 복제 문제를 식별 하기 위해 사용 하는 <system>repadmin /showrepl</system> 이전 섹션에 설명 된 대로 명령을 합니다. 다음 표에서 오류 및 오류에 대 한 해결 방법을 제공 하는 링크를 근본 원인을 함께이 명령을 생성 하는 오류 메시지가 표시 됩니다.


|Repadmin 오류|근본 원인|해결 방법|
| --- | --- | --- |
|이 지난 복제 이후 시간 서버 삭제 표시 기간을 초과 했습니다.|도메인 컨트롤러 AD DS에서 가비지 수집한 및 복제, 삭제, 삭제 된를 대 한 충분 긴 명명된 소스 도메인 컨트롤러의 인바인드 복제가 실패 했습니다.|이벤트 ID 2042: 지났습니다 너무 오래 걸림 복제이 컴퓨터|
|인바인드 이웃 없습니다.|항목이 표시 되지 않으면 repadmin에서 생성 되는 결과의 "환경 돌아오는" 섹션에서 /showrepl, 도메인 컨트롤러 다른 도메인 컨트롤러 복제 링크를 설정할 수 없습니다.|(이벤트 ID 1925) 복제 연결 문제 해결| 
|액세스할 수 없습니다.|두 명의 도메인 컨트롤러 사이 복제 링크가 있지만 인증 오류로 인해 복제를 올바르게 수행할 수 없습니다.|복제 보안 문제 해결| 
|마지막 못했습니다 < 날짜-시간 >에서 "대상 계정 이름이 잘못."와|이 문제 연결, DNS 또는 인증 문제에와 관련 된 문제일 수 있습니다. 로컬 도메인 컨트롤러의 고유 식별자 (GUID) 확인할 수 없습니다. DNS 오류 이면-복제 파트너의 DNS 이름을 기반으로 합니다.|수정 복제 DNS 조회 (이벤트 Id 1925 년 2087, 2088) 문제를 수정 복제 보안 문제 (이벤트 ID 1925) 복제 연결 문제 해결| 
|LDAP 오류 49 합니다.|도메인 컨트롤러 컴퓨터 계정 키 메일 센터 (KDC)와 동기화 되지 될 수 있습니다.|복제 보안 문제 해결| 
|LDAP 연결 로컬 호스트를 열 수 없습니다|관리 도구 AD DS 연결할 수 없습니다.|수정 복제 DNS 조회 문제 (이벤트 Id 1925 년 2087, 2088)| 
|Active Directory 복제 우선 되었습니다.|인바인드 복제가 진행률 repadmin /sync 명령을 사용 하 여 수동으로 생성 된 요청 등의 더 높은 우선 순위 복제 요청에 따라 중단 되었습니다.|복제가 완료 될 때까지 기다립니다. 이 정보 메시지가 나타냅니다 정상적으로 작동 합니다.| 
|대기 복제 게시 합니다.| 도메인 컨트롤러 복제 요청 게시 되 고 응답을 기다리는 합니다. 복제가 원본의 진행 중입니다.|복제가 완료 될 때까지 기다립니다. 이 정보 메시지가 나타냅니다 정상적으로 작동 합니다.| 

다음 표에서 문제를 복제 루트 함께 문제와 문제에 대 한 해결 방법을 제공 하는 링크를 사용 하면 Active Directory 했을 수 있는 일반적인 이벤트를 표시 합니다. 

|이벤트 ID 및 소스|근본 원인|해결 방법|
| --- | --- | --- | 
|1311 NTDS KCC|AD DS의 복제 구성 정보는 네트워크의 실제 토폴로지에 정확 하 게 반영 되지 않습니다.|(이벤트 ID 1311) 복제 토폴로지 문제 해결| 
|1388 NTDS 복제|느린 개체 도메인 컨트롤러 복제 된 및 무과실 복제 일관성을 적용 되지 않습니다.|수정 복제 느린 개체 문제 (이벤트 Id 1388, 1988 년 2042)|
|1925 NTDS KCC|쓰기 파티션에 대 한 복제 링크를 설정 하지 못했습니다. 이 이벤트 오류에 따라 여러 가지 원인이 있을 수 있습니다.| 수정 복제 연결 (이벤트 ID 1925) 문제를 수정 복제 DNS 조회 문제 (이벤트 Id 1925 년 2087, 2088)| 
|1988 NTDS 복제|로컬 도메인 컨트롤러 고 있기 때문에 수 있는 된 삭제 이미 가비지 수집 로컬 도메인 컨트롤러의 존재 하지 않는 원본 도메인 컨트롤러에서 개체를 복제 하려고 했습니다. 문제 해결 될 때까지이 파트너와 디렉터리 파티션이에 대 한 복제 진행 되지 않습니다.|수정 복제 느린 개체 문제 (이벤트 Id 1388, 1988 년 2042)|
|2042 NTDS 복제|복제가 삭제 표시 기간에 대 한이 파트너와 발생 하지 않은 한 복제 계속할 수 없습니다.|수정 복제 느린 개체 문제 (이벤트 Id 1388, 1988 년 2042)| 
|2087 NTDS 복제|AD DS DNS 호스트 이름 원본 도메인 컨트롤러의 IP 주소 및 복제 실패를 확인할 수 없습니다.|수정 복제 DNS 조회 문제 (이벤트 Id 1925 년 2087, 2088)| 
|2088 NTDS 복제 |AD DS DNS 호스트 이름 원본 도메인 컨트롤러의 IP 주소가 있지만 복제 성공 확인할 수 없습니다.|수정 복제 DNS 조회 문제 (이벤트 Id 1925 년 2087, 2088)|
|네트워크 로그온 5805|시스템 계정을 두 여러 개 같은 컴퓨터 이름 또는 모든 도메인 컨트롤러에 하지 복제 컴퓨터 이름을 일반적으로 발생 하는 인증, 하지 못했습니다.|복제 보안 문제 해결| 

복제 개념에 대 한 자세한 내용은 참조 [Active Directory 복제 기술을](https://go.microsoft.com/fwlink/?LinkId=41950)합니다.
  
