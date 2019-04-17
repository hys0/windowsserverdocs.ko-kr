---
title: "광고 숲 복구-초기 복구"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: fc2ec09c5b96b76229d532adc6a254c8108d8940
ms.sourcegitcommit: ac73f0f0dca04be731b928183bfdffc97d82c277
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="perform-initial-recovery"></a>초기 복구  

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

 이 섹션의 다음 단계에 포함 됩니다.  
  
-   [첫 번째 쓰기 도메인 컨트롤러 각 도메인에서 복원](#Restore-the-first-writeable-domain-controller-in-each-domain)  

-   [각 복원된 쓰기 도메인 컨트롤러 네트워크에 연결](#Reconnect-each-restored-writeable-domain-controller-to-a-common-network)  
  
-   [드 숲 루트 도메인에 있는 도메인 컨트롤러에 추가](#Add-the-global-catalog-to-a-domain-controller-in-the-forest-root-domain)  
  
  
## <a name="restore-the-first-writeable-domain-controller-in-each-domain"></a>첫 번째 쓰기 도메인 컨트롤러 각 도메인에서 복원  
 숲 루트 도메인에 쓰기 DC와 beginning 첫 번째 DC 복원 하는 데이 섹션의 단계를 완료 합니다. 스키마 관리자 및 Enterprise 관리자 그룹 저장 되므로 숲 루트 도메인이 중요 합니다. 또한 숲에서 보안 계층 유지할 수 있습니다. 또한 숲 루트 도메인 일반적으로 숲 속의 DNS 네임 스페이스 루트 DNS 서버를 보유합니다. 따라서 해당 도메인에 대 한 Active Directory 통합 DNS 영역 (CNAME) 별칭 리소스 레코드에 대 한 다른 모든 Dc 숲 (프로그램이 복제 하는 데 필요한) 및 드 DNS 리소스 기록에 포함 되어 있습니다.  
  
 숲 루트 도메인 복구 하는 숲 속의 나머지 도메인 복구 동일한 단계를 반복 합니다. 동시에 둘 이상의 도메인 복구할 수 있습니다. 그러나 보안 계층 또는 DNS 이름 해상도에서 든 중단을 방지 하기 위해 면 자녀 복구 하기 전에 복구 부모 도메인 항상 합니다.  
  
 복구 하는 도메인에 대 한 하나만 쓰기 DC 백업에서 복원 합니다. DC은 되어 영향을 받지 숲 원인을 실패 하는 데이터베이스 있어야 때문 복구 가장 중요 한 부분입니다. 신뢰할 수 있는 프로덕션 환경으로 도입 된 전에 철저 하 게 테스트 백업 하는 것이 중요 됩니다.  
  
 다음 단계를 수행 합니다. 몇 가지 단계를 수행 하기 위한 절차는에 [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)합니다.  
  
1.  실제 서버 복원 하려는 경우 네트워크 케이블 DC 연결 되어 있지 프로덕션 네트워크에 연결 되지는 대상에 확인 합니다. 가상 컴퓨터에 대 한 네트워크 어댑터를 제거 하거나 프로덕션 네트워크에서 격리 동안 복구 과정을 테스트할 수 있는 다른 네트워크에 연결 된 네트워크 어댑터를 사용 수 있습니다.  
  
2.  도메인의 첫 번째 쓰기 DC 때문 AD DS의 권한 없는 복원 및 sysvol 정식 복원을 수행 해야 합니다. 복원 작업 Active Directory-인식 백업을 사용 하 여 완료 해야 및 응용 프로그램 등 Windows Server 백업을 복원 (즉, 복원 해서는 DC VM 스냅숏을 복원 같은 지원된 방법을 사용 하 여).  
  
     Sysvol 신뢰할 수 있는 복원은 필요 SYSVOL의 복제 복제 장애가에서 복구 후 폴더를 시작 해야 합니다. 추가 하는 도메인의 모든 이후 Dc 다시 폴더 광고 수 전에 신뢰할 수를 선택 하는 폴더의 복사본과 SYSVOL 폴더를 동기화 해야 합니다.  
  
    > [!CAUTION]
    >  SYSVOL 숲 루트 도메인 복원 해야 하는 첫 번째 DC에 대해서만의 신뢰할 수 있는 (또는 주) 복원 작업을 수행 합니다. SYSVOL 데이터의 복제 충돌 올바르게 작업을 수행 하지 주 복원 SYSVOL의 다른 Dc에 나타납니다.  
  
     두 옵션 AD DS의 권한 없는 복원 및 sysvol 정식 복원을 수행는 다음과 같습니다.  
  
    -   그런 다음 다음 강제로 sysvol 신뢰할 수 있는 동기화 및 전체 서버 수행 합니다. 자세한 절차 참조 [전체 서버 수행](AD-Forest-Recovery-Perform-a-Full-Recovery.md) 및 [sysvol DFSR 복제 신뢰할 수 있는 동기화 수행](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)합니다.  
  
    -   전체 서버 복구 뒤에 상태 시스템 복원을 수행 합니다. 이 옵션을 사용 하려면 사전에 두 가지 유형의 백업 만드는: 전체 서버 백업 및 시스템 상태 백업 합니다. 자세한 절차 참조 [전체 서버 수행](AD-Forest-Recovery-Perform-a-Full-Recovery.md) 및 [신뢰할 수의 Active Directory Domain Services 복원을 수행](AD-Forest-Recovery-Nonauthoritative-Restore.md)합니다.  
  
3.  복원 하 고 쓸 DC 다시 시작 후 확인 실패 DC의 데이터에 영향을 주지 않습니다. DC 데이터 손상 된 경우 다른 백업으로 2 단계를 반복 합니다.  
  
     복원된 된 도메인 컨트롤러 호스트 작업 마스터 역할을 하는 경우 추가 AD DS 쓰기 디렉터리 파티션의 복제 완료 될 때까지 사용할 수 없는 방지 하려면 다음 레지스트리 항목이 활성화 된 해야 할 수 있습니다.  
  
     **HKLM\System\CurrentControlSet\Services\NTDS\Parameters\Repl 초기 동기화를 수행 합니다.**  
  
     데이터 형식으로 항목을 만들기 **REG_DWORD** 값을 하 고 **0**합니다. 이 항목을 가치를 다시 설정할 수 숲 완전히 복구 후 **1**작업을 성공적으로 AD DS 마스터 역할 돌아오는 보유 하 고 다시 시작 해야 하는 도메인 컨트롤러 필요 하 고 아웃 바운드 복제 알려진된 복제본와 파트너 관계를 맺고 도메인 컨트롤러 및 서비스를 제공 하는 클라이언트를 시작 자체 알립니다 하기 전에 합니다. 참조 KB 문서 초기 동기화 요구 사항에 대 한 자세한 내용은 [305476](https://support.microsoft.com/kb/305476)합니다.  
  
     복원 하 고 데이터를 확인 한 후에 및이 컴퓨터 프로덕션 네트워크에 연결 하기 전에 다음 단계를 계속 합니다.  
  
4.  숲 전체의 오류 네트워크 침입 또는 악의적인 공격 관련 된 것 같으면 구성원 엔터프라이즈 관리자, 도메인 관리, 스키마 관리, 서버 운영자, 계정 연산자 그룹 및 등을 포함 한 모든 관리자 계정에 계정 암호를 재설정 합니다. 관리자 계정 암호 재설정 추가 도메인 컨트롤러 숲 복구의 다음 단계 설치 하기 전에 완료 되어야 합니다.  
  
5.  첫 번째에서 복원된 DC 숲 루트 도메인에 있는 모든 도메인 및 숲 전체의 작업 마스터 역할을 중단 합니다. 엔터프라이즈 관리자 및 스키마 관리자 자격 증명 숲 수준 작업 마스터 역할을 중단 하 필요 합니다.  
  
     각 자녀의 도메인 도메인 전체 작업 마스터 역할을 중단 합니다. 이러한 역할 중단에 일시적으로 복원된 DC 작업 마스터 역할 유지 수 있지만 대 한 DC 호스트 하이 시점에서 숲 복구 과정을 보장 합니다. 필요에 따라 이후 복구 과정의 일환으로, 작업 마스터 역할을 재배포할 수 있습니다. 마스터 역할 작업 중단에 대 한 자세한 내용은 참조 [작업 마스터 역할 중단](AD-forest-recovery-seizing-operations-master-role.md)합니다. 작업 마스터 역할을 어디에 대 한 권장 참조 [작업 마스터 이란 무엇 인가요?](https://technet.microsoft.com/en-us/library/cc779716.aspx).  
  
6.  다른 모든 쓰기 Dc (도메인이 첫 번째 DC 제외 하 고 쓸 Dc 모든) 백업에서 복원 하지 않는 숲 루트 도메인에의 메타 데이터를 정리 합니다. Active Directory 사용자 및 컴퓨터 또는 Active Directory 사이트 및 서비스 이상 또는 Windows Server 2008와 함께 제공 되는 또는 Windows Vista에 대 한 RSAT의 버전을 사용 하거나 나중에 메타 데이터 정리는 자동으로 수행 DC 개체를 삭제 하면 됩니다. 또한 서버 개체와 컴퓨터 개체의 삭제 DC에 대 한도 자동으로 삭제 됩니다. 자세한 내용은 참조 [쓸 수 Dc 제거 메타 데이터를 청소](AD-Forest-Recovery-Cleaning-Metadata.md)합니다.  
  
     메타 데이터를 정리 AD DS 다른 사이트에 DC에 설치 된 경우 중복을 가능한 NTDS 설정 수 없습니다. 잠재적으로이 절약 될 수 있는 기술 검사기 KCC (일관성) 자체 Dc 나타나지 않을 때 복제 링크를 만드는 과정 합니다. 또한 메타 데이터 정리의 일환으로 DC Locator DNS 도메인에 있는 다른 모든 dc 리소스 레코드 DNS에서 삭제 됩니다.  
  
     도메인에 있는 다른 모든 Dc의 메타 데이터를 제거할 때까지이 DC 복구 하기 전에 RID 마스터 마치 RID 마스터 역할 가정 하지 않습니다 따라서 하지 수 있고 새로운 Rid 실행할 수 있습니다. 이벤트 ID 16650 시스템 로그에이 오류가 표시 된 이벤트 뷰어에서 표시 될 수 있지만 메타 데이터를 청소 한 후 성공을 시간이 나타내는 16648 이벤트 ID 나타납니다.  
  
7.  AD DS에 저장 된 DNS 영역을 사용 하는 경우 현지 DNS 서버 서비스 복원한 DC에서 실행 되 고 설치 인지 확인 합니다. 한 경우이 DC 숲 오류가 발생 하기 DNS 서버를 설치 하 고 DNS 서버를 구성 해야 합니다.  
  
    > [!NOTE]
    >  KB 문서에 핫픽스 설치 해야 할 복원된 DC 실행 될 경우 Windows Server 2008, [975654](https://support.microsoft.com/kb/975654) 하거나 DNS 서버를 설치 하려면 일시적으로 서버 있는 격리 된 네트워크에 연결 합니다. 핫픽스 다른 버전의 Windows Server에 대 한 필요 하지 않습니다.  
  
     이렇게, IP 주소 (또는 127.0.0.1 등 루프백 주소)의 기본 설정된 DNS 서버도 복원된 DC 구성 합니다. TCP/IP 속성 (lan) 어댑터의에서이 설정을 구성할 수 있습니다. 숲 속의의 첫 번째 DNS 서버입니다. 자세한 내용은 참조 [TCP/IP DNS 사용 하도록 구성](https://technet.microsoft.com/library/cc779282\(WS.10\).aspx)합니다.  
  
     각 자녀의 도메인에 복원된 DC 첫 번째 DNS 서버 숲 루트 도메인에 IP 주소와의 기본 설정된 DNS 서버를 구성 합니다. TCP/IP 속성 LAN 어댑터에서이 설정을 구성할 수 있습니다. 자세한 내용은 참조 [TCP/IP DNS 사용 하도록 구성](https://technet.microsoft.com/library/cc779282\(WS.10\).aspx)합니다.  
  
     _Msdcs 및 도메인 DNS 영역에서 더 이상 메타 데이터 정리 후 없는 dc NS 기록이 삭제 됩니다. 정리한 dc SRV 기록 제거 된 것을 확인 합니다. SRV DNS 레코드 제거를 신속 하 게 실행 합니다.  
  
    ```  
    nltest.exe /dsderegdns:server.domain.tld  
    ```  
  
8.  사용 가능한 RID 풀의 값 하 여 100, 000 발생 합니다. 자세한 내용은 참조 [의 사용 가능한 RID 온천이 값 발생](AD-Forest-Recovery-Raise-RID-Pool.md)합니다. 생각 하 여 100, 000 제거 풀 발생 하지 특정 상황에 대 한 충분 한 이유를 사용 하는 경우는 계속 안전 하 게 최저 증가 확인 해야 합니다. Rid 불필요를 사용 하지 않아야 하는 한정 리소스는 합니다.  
  
     새로운 보안 사용자 도메인에서 백업 복원에 사용 하는 시간 후 생성 된, 이러한 보안 사용자 할 경우 액세스 권한을 특정 개체 합니다. 이러한 보안 사용자 복구 후 백업,으로 되돌릴는 복구 하기 때문에 더 이상 존재 그러나 해당 액세스 권한을 여전히 있을 수 있습니다. 사용 가능한 RID 풀 복원 후 발생 하지 않은 경우 새 사용자 만들어진 후 숲 복구 동일한 보안 Sid (식별자)을 얻을 수 있습니다 개체를 처음 의도 하지 않은 이러한 물체에 액세스할 수 있는 될 수 있습니다.  
  
     을 설명 하기 위해 도입에서 언급 한 것 운동을 라는 새로운 직원 예제를 것이 좋습니다. 운동에 대 한 사용자 개체 도메인 복원 하는 데 사용 된 백업 후 작성 되었으므로 복원 작업 한 후 더 이상 존재 합니다. 그러나 해당 사용자 개체에 할당 된 액세스 권한을 복원 작업 후 유지 될 수 있습니다. 해당 사용자 개체 SID 새 개체 복원 작업 한 후 다시 할당는, 새 개체 액세스 권리 얻게 됩니다.  
  
9. 현재 RID 풀을 무효화 됩니다. 현재 RID 풀 시스템 상태로 복원 무효화 됩니다. 하지만 현재 RID 풀 복원된 DC 다시 Rid 백업을 만든 시간에 할당 된 RID 풀에서 실행 되지 않도록 하려면 무효화 필요할 경우 상태 시스템 복원을 수행 되지 않았습니다. 자세한 내용은 참조 [현재 RID 풀 무효화](AD-Forest-Recovery-Invaildate-RID-Pool.md)합니다.  
  
    > [!NOTE]
    >  처음으로 RID 풀 무효화 후 SID 개체를 시도 하는 하면 오류가 발생 합니다. 개체를 트리거하 새로운 RID 풀에 대 한 요청 합니다. 작업을 다시 시도 성공 새 RID 풀 할당 합니다.  
  
10. 두 번이 dc 컴퓨터 계정 암호 다시 설정 합니다. 자세한 내용은 참조 [도메인 컨트롤러의 컴퓨터 계정 암호를 재설정할 때](AD-Forest-Recovery-Reset-Computer-Account-DC.md)합니다.  
  
11. 두 번 krbtgt 암호 다시 설정 합니다. 자세한 내용은 참조 [krbtgt 암호를 재설정할 때](AD-Forest-Recovery-Resetting-the-krbtgt-password.md)합니다.  
  
     Krbtgt 암호 기억 두 암호가 이기 때문에 두 번에서 암호 기억 원래 (오류 전) 암호를 제거 하는 데 암호 다시 설정 합니다.  
  
    > [!NOTE]
    >  숲 복구 중인 경우 보안 위험이에 대 한 응답, 보안 암호 다시 설정도 있습니다. 자세한 내용은 참조 [한쪽 신뢰 신뢰 암호를 재설정할 때](AD-Forest-Recovery-Reset-Trust.md)합니다.  
  
12. 숲 도메인이 여러 개 복원된 DC 된 오류가 발생 하기 전에 드 서버 선택을 취소 하 고 **드** DC 드 제거 NTDS 설정 속성에서 확인란을 선택 합니다. 이 규칙에 대 한 예외 한 도메인 숲 속의 일반적인 경우 합니다. 이 경우 드 제거 필요 하지 않습니다. 자세한 내용은 참조 [드 제거](AD-Forest-Recovery-Remove-GC.md)합니다.  
  
     글로벌 카탈로그 더 많은 백업에서 복원 하 여 다른 도메인에 있는 Dc 복원 하는 데 사용 하는 다른 백업을 보다 최신 발생할 수도 있습니다 느린 개체 합니다. 다음 예를 것이 좋습니다. 도메인 A d c 1 t 1 시간에 수행 된 백업에서 복원 됩니다. 도메인 B d c 2 t 2 시간에 수행 된 드 백업에서 복원 됩니다. 가정 t 2 t 1 보다 최신 되며 일부 개체 t 1과 t 2 사이 만든 합니다. 이러한 Dc 복원 된 후 d c 2는 글로벌 카탈로그 보유 도메인 A 보류 보다 부분 복제 A's 도메인에 대 한 최신 데이터 자체 합니다. 이 경우 d c 2, 이러한 물체는 d c 1에 되므로 느린 개체를 보유 합니다.  
  
     느린 개체의 존재 문제가 발생할 수 있습니다. 예를 들어 메일 메시지 인 사용자 개체 도메인 간에 이동 되었습니다 사용자에 게 배달 되지 않을 수 있습니다. 오래 된 DC 또는 드 서버를 다시 온라인, 돌아오는 두 개 사용자 개체 드에 표시 됩니다. 두 물체는 동일한 메일 주소입니다. 전자 메일 메시지를 전달할 수 없습니다.  
  
     두 번째 문제가 더 이상 사용자 계정 전체 주소 목록에 나타나지 여전히입니다. 세 번째 문제는 더 이상 있는 범용 그룹에서 사용자의 액세스 토큰 여전히 나타날 수 없습니다.  
  
     글로벌 카탈로그를 DC 복원 않은 경우-중 하나 실수로 또는 된 신뢰할 수 있는 사용자 벡 백업을-드 복원 작업이 완료 된 후에 빨리 해제 하 여 개체 느린의 항목을 방지 하는 것이 좋습니다. 드 플래그 비활성화 모든 부분 복제 (파티션)를 유지 하 고 이동 하면 다음과 같은 자체 일반 DC 상태를 컴퓨터에 발생 합니다.  
  
13. Windows 시간 서비스를 구성 합니다. 이렇게, 외부 시간 소스에서 시간을 동기화 하려면 PDC 에뮬레이터를 구성 합니다. 자세한 내용은 참조 [Windows 시간 서비스 숲 루트 도메인 PDC 에뮬레이터 구성](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29)합니다.  
  
 

## <a name="reconnect-each-restored-writeable-domain-controller-to-a-common-network"></a>각 복원된 쓰기 도메인 컨트롤러에는 일반적인 네트워크 연결  
 이 단계에서 있어야 복원 한 DC (및 복구 단계를 수행)의 이렇게 및 각 나머지 도메인에 합니다. 이러한 Dc 나머지 환경에서에서 분리 되는 일반적인 네트워크에 가입 하 고 숲 건강 및 복제를 확인 하려면 다음 단계를 완료 합니다.  
  
> [!NOTE]
>  실제 Dc 격리 된 네트워크에 참여 하면 해당 IP 주소를 변경 해야 합니다. 결과적으로, IP 주소 DNS 레코드 잘못 된 됩니다. 드 서버를 사용할 수 없기 때문에 DNS에 대 한 동적 보안 업데이트가 실패 합니다. 가상 Dc 하 고 더이 경우에 IP 주소를 변경 하지 않고 새 가상 네트워크에 연결 합니다. 왜 가상 Dc 권장 되는 첫 번째 도메인 컨트롤러를 숲 복구 하는 동안 복원할 수는 요인 중 하나입니다.  
  
 유효성 검사 후 Dc 프로덕션 네트워크에 가입 하 고 숲 복제 상태를 확인 하는 단계를 완료 합니다.  
  
-   이름 해상도 수정 하려면 위임 DNS 레코드 만들고 DNS 전달 및 루트 힌트 필요에 따라를 구성 합니다. 실행 **repadmin /replsum** Dc 간의 복제 확인 합니다.  
  
-   복원된 DC 직접 복제 파트너 없으면 복제 복구가 됩니다 훨씬 더 빨라지고 서로 임시 연결 개체 만들어.  
  
-   정리 메타 데이터 유효성 검사를 실행 **Repadmin /viewlist \ *** 는 숲 속의 모든 Dc 목록은 합니다. 실행 **Nltest /DCList:***< domain\ >* 도메인에 있는 모든 Dc 목록은 합니다.  
  
-   DC 및 DNS 상태를 확인 하려면 DCDiag /v 오류 보고는 숲 속의 모든 Dc에서 실행 합니다.  
  
  

## <a name="add-the-global-catalog-to-a-domain-controller-in-the-forest-root-domain"></a>드 숲 루트 도메인에 있는 도메인 컨트롤러에 추가  
 글로벌 카탈로그 이러한 및 다른 이유로 필요 합니다.  
  
-   사용자에 대 한 로그온 수 있도록 합니다.  
  
-   서비스를 사용 하도록 Netlogon Dc 각 자녀의 도메인에 등록 하 고 루트 도메인에는 DNS 서버에 기록 제거를 실행 합니다.  
  
 설정 되어 있어도 숲 루트 DC 현상이 글로벌 카탈로그 있음을 복원 dc 글로벌 카탈로그를 선택할 수는 있습니다.  
  
> [!NOTE]
>  DC는 숲 속의 모든 디렉터리 파티션 전체 동기화가 완료 될 때까지 드 서버로 작동 되지 않습니다. 따라서 DC 각각의 숲 속의 복원된 Dc 복제할 강제 해야 합니다.  
>   
>  디렉터리 서비스 이벤트 로그에서 모니터링 이벤트 뷰어에서 ID 1119 이벤트에 대 한 하다는 것이 DC 드 서버, 하거나 다음 레지스트리 키가 1 확인 합니다.  
>   
>  **완료 HKLM\System\CurrentControlSet\Services\NTDS\Parameters\Global 카탈로그 프로 모션**  
  
 자세한 내용은 참조 [드 추가](AD-Forest-Recovery-Add-GC.md)합니다.  
  
 이 단계에서 있어야 한 드 하 고 각 도메인에 대 한 DC로 안정적인 숲 속의 숲 속의 합니다. 방금 복원한 dc 각각의 새로운 백업을 해야 합니다. 이제 AD DS을 설치 하 여 다른 Dc 숲에 배포를 시작할 수 있습니다.  

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
  
