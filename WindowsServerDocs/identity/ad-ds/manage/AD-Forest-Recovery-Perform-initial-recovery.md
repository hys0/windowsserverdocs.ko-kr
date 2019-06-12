---
title: AD 포리스트 복구-초기 복구를 수행 합니다.
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: 9883d337520c3920f8638ddfe5f6bd393e31fd2f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442867"
---
# <a name="perform-initial-recovery"></a>초기 복구를 수행 합니다.  

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

이 섹션에는 다음 단계가 포함 됩니다.  

- [각 도메인의 첫 번째 쓰기 가능한 도메인 컨트롤러 복원](#restore-the-first-writeable-domain-controller-in-each-domain)  
- [각 복원 된 쓰기 가능한 도메인 컨트롤러 네트워크에 다시 연결](#reconnect-each-restored-writeable-domain-controller-to-a-common-network)  
- [포리스트 루트 도메인의 도메인 컨트롤러를 글로벌 카탈로그 추가](#add-the-global-catalog-to-a-domain-controller-in-the-forest-root-domain)  

## <a name="restore-the-first-writeable-domain-controller-in-each-domain"></a>각 도메인의 첫 번째 쓰기 가능한 도메인 컨트롤러 복원  

포리스트 루트 도메인의 쓰기 가능한 DC와 beginning, 첫 번째 DC를 복원 하려면이 섹션의 단계를 완료 합니다. 포리스트 루트 도메인의 Schema Admins 및 Enterprise Admins 그룹을 저장 하기 때문에 반드시 합니다. 포리스트의 트러스트 계층 구조를 유지 하기도 합니다. 또한 포리스트 루트 도메인에는 일반적으로 포리스트 DNS 네임 스페이스에 대 한 DNS 루트 서버를 보유합니다. 결과적으로 해당 도메인에 대 한 Active Directory 통합 DNS 영역 (임 복제에 필요) 포리스트 및 글로벌 카탈로그 DNS 리소스 레코드의 다른 모든 Dc에 대 한 별칭 (CNAME) 리소스 레코드를 포함 합니다. 
  
포리스트 루트 도메인을 복구한 후에 나머지 도메인 포리스트를 복구 하는 동일한 단계를 반복 합니다. 동시에 둘 이상의 도메인을 복구할 수 있습니다. 그러나 트러스트 계층 구조 또는 DNS 이름 확인에서 모든 중단을 방지 하기 위해 자식 복구 하기 전에 부모 도메인을 복구 합니다. 
  
복구 하는 각 도메인에 대 한 쓰기 가능한 DC가 하나만 백업에서 복원 합니다. 하기 때문에 DC가 된 영향을 받지 않습니다 포리스트 원인을 실패 하는 데이터베이스 복구의 가장 중요 한 부분입니다. 프로덕션 환경에 도입 된 전에 철저히 테스트 하는 신뢰할 수 있는 백업이 두는 것이 반드시 합니다. 
  
다음 단계를 수행 합니다. 에 특정 단계를 수행 하는 절차 [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)합니다. 
  
1. 물리적 서버를 복원 하려는 경우 대상 DC 연결 되어 있지 않으므로 프로덕션 네트워크에 연결 되지 않은 네트워크 케이블을 확인 합니다. 가상 컴퓨터에 대 한 네트워크 어댑터를 제거할 수도 있고 다른 네트워크에 연결 된 네트워크 어댑터를 사용 하 여 프로덕션 네트워크에서 격리 하는 동안 복구 프로세스를 테스트할 수 있습니다. 
  
2. 도메인에 첫 번째 쓰기 가능한 DC 이기 때문에 AD DS의 신뢰할 수 없는 복원 및 SYSVOL의 정식 복원을 수행 해야 합니다. 복원 작업 Active Directory에서 인식 백업을 사용 하 여 완료 해야 하 고 Windows Server Backup 등의 응용 프로그램 복원 (즉, 복원 해서는 DC VM 스냅숏 복원 같은 지원된 되는 메서드를 사용 하 여). 
   - SYSVOL의 신뢰할 수 있는 복원 하는 경우 반드시 SYSVOL 복제에서 복제 하기 때문에 재해에서 복구 후 폴더를 시작 해야 합니다. 도메인에 추가 되는 모든 후속 Dc가 SYSVOL 폴더 폴더를 알릴 수 전에 신뢰할 수 있는 선택 된 폴더의 복사본을 사용 하 여 다시 동기화 해야 합니다. 

   > [!CAUTION]
   > 포리스트 루트 도메인에서 복원할 첫 번째 DC에 대해서만 SYSVOL의 신뢰할 수 있는 (또는 기본) 복원 작업을 수행 합니다. SYSVOL 데이터의 복제 충돌 발생 시키는 다른 Dc에서 올바르게 SYSVOL의 기본 복원 작업을 수행 합니다. 

   - AD DS의 신뢰할 수 없는 복원 및 SYSVOL의 신뢰할 수 있는 복원 하는 경우 두 가지 옵션을 수행할 수 있습니다.  
   - 전체 서버 복구를 수행 하 고 SYSVOL의 신뢰할 수 있는 동기화를 강제 적용 합니다. 자세한 절차를 참조 하세요. [전체 서버 복구를 수행](AD-Forest-Recovery-Perform-a-Full-Recovery.md) 하 고 [DFSR 복제 SYSVOL의 신뢰할 수 있는 동기화가 수행](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)합니다. 
   - 시스템 상태 복원을 뒤에 전체 서버 복구를 수행 합니다. 이 옵션을 사용 하려면 사전에 두 유형의 백업 만드는: 전체 서버 백업 및 시스템 상태 백업 합니다. 자세한 절차를 참조 하세요. [전체 서버 복구를 수행](AD-Forest-Recovery-Perform-a-Full-Recovery.md) 하 고 [Active Directory Domain Services의 신뢰할 수 없는 복원을 수행](AD-Forest-Recovery-Nonauthoritative-Restore.md)합니다. 
  
3. 복원 하 고 쓰기 가능 DC를 다시 시작 후 오류 DC에 데이터에 영향을 주지 않은 확인 합니다. DC 데이터 손상 된 경우 다른 백업으로 2 단계를 반복 합니다. 
   - 복원된 된 도메인 컨트롤러는 작업 마스터 역할을 호스트 하는 경우 쓰기 가능한 디렉터리 파티션의 복제를 완료할 때까지 사용할 수 없게 하는 AD DS를 방지 하려면 다음 레지스트리 항목을 추가 해야 할 수 있습니다.  

      **HKLM\System\CurrentControlSet\Services\NTDS\Parameters\Repl 초기 동기화를 수행 합니다.**  
  
      데이터 형식을 사용 하 여 항목을 만들 **REG_DWORD** 값 **0**합니다. 이 항목의 값을 다시 설정할 수 있습니다 포리스트의 완전히 복구 되 면 **1**, 다시 시작 하는 도메인 컨트롤러 필요 및 성공적인 AD DS를 사용 하는 작업 마스터 역할 인바운드 및 아웃 바운드 복제를 해당 도메인 컨트롤러 자체를 보급 하 고 클라이언트에 서비스를 제공 하기 시작 하기 전에 복제본 파트너 알려져 있습니다. 초기 동기화 요구 사항, 기술 자료 문서를 참조 하는 방법에 대 한 자세한 내용은 [305476](https://support.microsoft.com/kb/305476)합니다. 
  
      복원 하 고 데이터를 확인 한 후에 하 고 프로덕션 네트워크에이 컴퓨터를 가입 하기 전에 다음 단계를 계속 합니다. 
  
4. 포리스트 오류 네트워크 침입 또는 악의적인 공격 관련 된 의심 되는 경우 Enterprise Admins, Domain Admins, Schema Admins, Server Operators, 계정의 멤버를 포함 하는 모든 관리 계정에 대 한 계정 암호를 다시 설정 연산자 그룹 및 등입니다. 관리자 계정 암호 다시 설정 하 고 추가 도메인 컨트롤러는 포리스트 복구의 다음 단계 중에 설치 하기 전에 완료 되어야 합니다. 
5. 포리스트 루트 도메인의 첫 번째 복원된 DC의 모든 도메인 및 포리스트 차원의 작업 마스터 역할 점유 합니다. 포리스트 전체 작업 마스터 역할 점유에 Enterprise Admins 및 Schema Admins 자격 증명이 필요 합니다. 
  
     각 자식 도메인에 도메인 수준의 작업 마스터 역할 점유 합니다. 이러한 역할을 점유 일시적 으로만 복원 된 DC에서 작업 마스터 역할 유지할 수 있지만 결정 DC에서에서 호스트를 시점에서 해당 포리스트 복구 프로세스를 보장 합니다. 복구 후 프로세스의 일부로, 필요에 따라 작업 마스터 역할을 재배포할 수 있습니다. 작업 마스터 역할 점유에 대 한 자세한 내용은 참조 하십시오 [작업 마스터 역할 점유](AD-forest-recovery-seizing-operations-master-role.md)합니다. 작업 마스터 역할을 배치 하는 위치에 대 한 권장 사항을 참조 하세요 [작업 마스터란?](https://technet.microsoft.com/library/cc779716.aspx)합니다. 
  
6. (모든 쓰기 가능한 Dc 도메인에서이 첫 번째 DC 제외한) 백업에서 복원 하지 않는 하는 포리스트 루트 도메인의 다른 모든 쓰기 가능한 Dc의 메타 데이터를 정리 합니다. Active Directory 사용자 및 컴퓨터 또는 Active Directory 사이트 및 이상 또는 Windows Server 2008을 사용 하 여 포함 된 서비스 또는 Windows Vista 용 RSAT 버전을 사용 하거나 나중에 메타 데이터 정리는 자동으로 수행 DC 개체를 삭제 하는 경우. 또한 서버 개체와 삭제 된 DC에 대 한 컴퓨터 개체도 자동으로 삭제 됩니다. 자세한 내용은 [쓰기 가능한 Dc 제거의 메타 데이터를 정리](AD-Forest-Recovery-Cleaning-Metadata.md)합니다. 
  
     메타 데이터 정리 AD DS는 다른 사이트의 DC에 설치 되어 있으면 NTDS 설정 개체의 가능한 중복이 되지 않습니다. 잠재적으로 줄일 수 있을 수도 지식 일관성 검사기 (KCC) 자체 Dc 나타나지 않을 경우 복제 링크를 만드는 프로세스입니다. 또한 메타 데이터 정리의 일부로 도메인의 다른 모든 Dc에 대 한 DC 로케이터 DNS 리소스 레코드 DNS에서 삭제 됩니다. 
  
     도메인의 다른 모든 Dc의 메타 데이터가 제거 될 때까지이 DC를 복구 하기 전에 RID 마스터를 마치 RID 마스터 역할을 가정 하지는 및 따라서 됩니다 새 Rid를 발급할 수 있습니다. 이벤트 ID 16650 시스템 로그에서이 오류를 나타내는 이벤트 뷰어에 표시 될 수 있습니다 하지만 이벤트 ID 메타 데이터를 지운 후 성공 하는 동안 잠시 나타내는 16648 표시 되어야 합니다. 
  
7. AD DS에 저장 되는 DNS 영역에 있는 경우에 로컬 DNS 서버 서비스를 설치 하 고 복원한 DC에서 실행 인지 확인 합니다. 이 DC 포리스트 실패 하기 전에 DNS 서버를 하지 않았으면 설치 하 고 DNS 서버를 구성 해야 합니다. 
  
    > [!NOTE]
    > 기술 자료 문서에서 핫픽스를 설치 해야 하는 복원된 된 DC가 Windows Server 2008을 실행 하는 경우 [975654](https://support.microsoft.com/kb/975654) 또는 DNS 서버를 설치 하기 위해 일시적으로 서버 격리 된 네트워크에 연결 합니다. 핫픽스 다른 버전의 Windows Server에 대 한 필요 하지 않습니다. 
  
     포리스트 루트 도메인에 자체 IP 주소 (또는 루프백 주소를 127.0.0.1 등)를 사용 하 여 복원된 된 DC의 기본 DNS 서버로 구성 합니다. 로컬 영역 네트워크 (LAN) 어댑터의 TCP/IP 속성에서이 설정을 구성할 수 있습니다. 포리스트의 첫 번째 DNS 서버입니다. 자세한 내용은 [DNS를 사용 하려면 TCP/IP 구성](https://technet.microsoft.com/library/cc779282\(WS.10\).aspx)합니다. 
  
     각 자식 도메인의 기본 DNS 서버로 포리스트 루트 도메인의 첫 번째 DNS 서버의 IP 주소를 사용 하 여 복원 된 DC를 구성 합니다. LAN 어댑터의 TCP/IP 속성에서이 설정을 구성할 수 있습니다. 자세한 내용은 [DNS를 사용 하려면 TCP/IP 구성](https://technet.microsoft.com/library/cc779282\(WS.10\).aspx)합니다. 
  
     _Msdcs 및 도메인 DNS 영역에서 더 이상 메타 데이터 정리 후 존재 하는 Dc의 NS 레코드를 삭제 합니다. SRV 레코드를 정리 된 dc가 제거 된 것을 확인 합니다. DNS SRV 레코드 제거 속도 위해 다음을 실행 합니다.  
  
    ```  
    nltest.exe /dsderegdns:server.domain.tld  
    ```  
  
8. 100,000 하 여 사용 가능한 RID 풀의 값을 올립니다. 자세한 내용은 [사용 가능한 RID 풀의 값을 발생 시키는](AD-Forest-Recovery-Raise-RID-Pool.md)합니다. RID 풀을 사용 하 여 100,000 거듭제곱는 충분 하지 않음을 특정 상황에 대 한 생각에 있는 경우에 여전히 안전 하 게 하는 가장 낮은 증가 결정 합니다. Rid는 한정 된 리소스를 불필요 하 게를 사용 하지 않아야 합니다. 
  
     새 보안 주체 복원에 사용할 백업 시간 이후 도메인에 생성 된 경우 이러한 보안 주체 특정 개체에 액세스 권한의 있을 것입니다. 이러한 보안 주체 복구 후 복구; 백업으로 되돌려 졌음을 하기 때문에 더 이상 존재 그러나 해당 액세스 권한을 계속 존재할 수 있습니다. 복원 후 사용 가능한 RID 풀을 발생 하지 않은 경우 새 사용자 포리스트 복구와 동일한 Sid (보안 Id)를 가져올 수 있습니다 후 생성 된 개체 및 해당 개체에 원래 의도 하지 않은 액세스 있을 수 있습니다. 
  
     를 설명 하기 위해 소개에서 언급 된 Amy 라는 새 직원의 예제를 살펴보겠습니다. Amy에 대 한 사용자 개체는 도메인을 복원 하는 데 사용 된 백업 후 만들어졌기 때문에 복원 작업 후 더 이상 없습니다. 그러나 복원 작업 후 해당 사용자 개체에 할당 된 모든 액세스 권한을 유지할 수 있습니다. 복원 작업 후 새 개체에 해당 사용자 개체에 대 한 SID를 다시 할당 하는 경우 새 개체는 해당 액세스 권한을 가져옵니다. 
  
9. 현재 RID 풀을 무효화 합니다. 시스템 상태 복원 후에 현재 RID 풀 무효화 됩니다. 하지만 현재 RID 풀을 다시 백업 생성 시 할당 된 RID 풀에서 Rid 발급에서 복원된 된 DC를 방지 하기 위해 무효화 될 해야 경우 시스템 상태 복원을 수행 되지 않았습니다. 자세한 내용은 [현재 RID 풀 무효화](AD-Forest-Recovery-Invaildate-RID-Pool.md)합니다. 
  
    > [!NOTE]
    > 처음 후 RID 풀을 무효화 하는 SID를 사용 하 여 개체를 만들려고 하면 오류가 표시 됩니다. 개체를 만드는 데 새 RID 풀 요청을 트리거합니다. 새 RID 풀을 할당할 성공할 수 작업을 다시 시도 합니다. 
  
10. 이 DC의 컴퓨터 계정 암호를 두 번 다시 설정 합니다. 자세한 내용은 [도메인 컨트롤러의 컴퓨터 계정 암호를 재설정](AD-Forest-Recovery-Reset-Computer-Account-DC.md)합니다. 
  
11. Krbtgt 암호를 두 번 다시 설정 합니다. 자세한 내용은 [krbtgt 암호를 재설정](AD-Forest-Recovery-Resetting-the-krbtgt-password.md)합니다. 
  
     Krbtgt 암호 기록이 두 개의 암호가 이기 때문에 두 번 암호 기록에서 원래 (오류 전) 암호를 제거 하는 암호를 다시 설정 합니다. 
  
    > [!NOTE]
    > 보안 위반에 대 한 응답에 포리스트 복구를 트러스트 암호도 다시 설정할 수 있습니다. 자세한 내용은 [트러스트의 한 쪽에서 트러스트 암호를 재설정](AD-Forest-Recovery-Reset-Trust.md)합니다. 
  
12. 포리스트의 여러 도메인에 복원 된 DC가 글로벌 카탈로그 서버가 실패 하기 전에 선택을 취소 하는 **글로벌 카탈로그** 글로벌 카탈로그 DC를 제거할 NTDS 설정 속성의 확인란 합니다. 이 규칙의 예외는 한 도메인 포리스트의 일반적인 사례입니다. 이 경우 필요가 글로벌 카탈로그를 제거 합니다. 자세한 내용은 [글로벌 카탈로그 제거](AD-Forest-Recovery-Remove-GC.md)합니다. 
  
     더 많은 백업에서 글로벌 카탈로그를 복원 하 여 다른 도메인의 Dc를 복원 하는 데 사용 되는 다른 백업 보다 최근 발생할 수도 있습니다 느린 개체입니다. 다음 예제를 살펴보세요. DC1은 도메인 A에서 T1 시점에 수행 된 백업에서 복원 됩니다. 도메인 B에서 DC2 T2 시점에 수행 된 글로벌 카탈로그 백업에서 복원 됩니다. T2는 T1에 보다 최신 일부 개체는 T1과 T2 간에 생성 된 만든다고 가정 합니다. 이러한 Dc을 복원한 후 DC2는 글로벌 카탈로그를 보유 도메인 A는 보다 도메인 A의 일부 복제본에 대 한 최신 데이터 자체입니다. DC2는이 예제의 경우 이러한 개체를 DC1에 없기 때문에 느린 개체를 보유 합니다. 
  
     느린 개체의 현재 상태 문제가 발생할 수 있습니다. 예를 들어 전자 메일 메시지 사용자 개체가 도메인 간 이동 된 사용자에 게 배달할 수 있습니다. 오래 된 DC를 글로벌 카탈로그 서버를 다시 온라인 상태로 사용자 개체의 두 인스턴스는 글로벌 카탈로그에 표시 됩니다. 두 개체에 동일한 전자 메일 주소입니다. 따라서 전자 메일 메시지를 배달할 수 없습니다. 
  
     두 번째 문제는는 더 이상 존재 하는 사용자 계정 전체 주소 목록에 여전히 나타날 수 없습니다. 세 번째 문제는는 더 이상 존재 하는 유니버설 그룹 사용자의 액세스 토큰에 여전히 나타날 수 없습니다. 
  
     DC는 글로벌 카탈로그를 복원 않은 경우-하거나 실수로 신뢰할 수 있는 독립 백업 기 때문에 또는-복원 작업 후에 곧 글로벌 카탈로그를 사용 하지 않도록 설정 하 여 느린 개체가 발생을 방지 하는 것이 좋습니다 완료 합니다. 글로벌 카탈로그 플래그를 사용 하지 않도록 설정 하면 모든 해당 부분 복제본 (파티션)을 손실 하 고 이동 하면 다음과 같은 자체 일반 DC 상태 컴퓨터 발생 합니다. 
  
13. Windows 시간 서비스를 구성 합니다. 포리스트 루트 도메인의 외부 시간 원본에서 시간을 동기화 하도록 PDC 에뮬레이터를 구성 합니다. 자세한 내용은 [포리스트 루트 도메인의 PDC 에뮬레이터에서 Windows 시간 서비스를 구성할](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29)합니다. 
  
## <a name="reconnect-each-restored-writeable-domain-controller-to-a-common-network"></a>공용 네트워크 각 복원 된 쓰기 가능한 도메인 컨트롤러를 다시 연결

이 단계에서 해야 복원 DC가 하나 (및 복구 단계 수행) 나머지 도메인의 각 포리스트 루트 도메인에 있습니다. 이러한 Dc 환경의 나머지 부분에서 격리 된 공용 네트워크에 조인 하 고 포리스트의 상태 및 복제의 유효성을 검사 하려면 다음 단계를 완료 합니다.

> [!NOTE]
> 격리 된 네트워크를 실제 Dc에 연결한 경우 해당 IP 주소를 변경 해야 합니다. 결과적으로, DNS 레코드의 IP 주소가 잘못 됩니다. 글로벌 카탈로그 서버를 사용할 수 없는 때문에 DNS에 대 한 보안 동적 업데이트 실패 합니다. 가상 Dc는 더 유리이 경우 해당 IP 주소를 변경 하지 않고 새 가상 네트워크에 조인할 수 있습니다. 이것이 첫 번째 도메인 컨트롤러로 포리스트 복구 동안 복원 될 가상 Dc는 권장 하는 이유는 한 가지 이유입니다. 
  
유효성이 검사 되 면 dc가 프로덕션 네트워크에 연결 하 고 포리스트 복제 상태를 확인 하는 단계를 완료 합니다.

- 이름 확인을 해결 하려면 DNS 위임 레코드를 만들고 DNS 전달 및 루트 힌트 필요에 따라 구성 합니다. 실행할 **repadmin /replsum** Dc 간 복제를 확인 합니다. 
- 복원된 된 DC의 직접 복제 파트너 없으면 복제 복구 더 빠를 것 간에 임시 연결 개체를 만들어 합니다. 
- 메타 데이터 정리의 유효성을 검사 하려면 **Repadmin /viewlist \\** * 포리스트에서 모든 Dc의 목록은 합니다. 실행할 **Nltest /DCList:** *< 도메인\>*  도메인의 모든 Dc의 목록은 합니다. 
- DC 및 DNS 상태를 확인 하려면 오류를 보고할 DCDiag /v 포리스트에서 모든 Dc에서 실행 합니다. 

## <a name="add-the-global-catalog-to-a-domain-controller-in-the-forest-root-domain"></a>포리스트 루트 도메인의 도메인 컨트롤러를 글로벌 카탈로그 추가

글로벌 카탈로그는 이러한 및 기타 이유로 필요 합니다.  
  
- 사용자에 대 한 로그온 수 있도록 합니다. 
- Net Logon 서비스를 사용 하도록 등록 하 고 루트 도메인의 DNS 서버에서 레코드를 제거 하기 위해 각 자식 도메인의 Dc를 실행 합니다. 
  
기본 설정 이지만 포리스트 루트 DC는 글로벌 카탈로그를 있을 경우 복원 된 dc는 글로벌 카탈로그를 선택할 수는 있습니다. 
  
> [!NOTE]
> 포리스트에 있는 모든 디렉터리 파티션의 전체 동기화가 완료 될 때까지 DC는 글로벌 카탈로그 서버로 보급 하지 합니다. 따라서 DC 포리스트의 dc가 복원 된 각 복제 되도록 강제 해야 합니다. 
>
> 디렉터리 서비스 이벤트 로그 이벤트 뷰어에서 이벤트 ID 1119 하다는 것이 DC는 글로벌 카탈로그 서버를 모니터링 하거나 다음 레지스트리 키에 값이 1 확인:  
>
> **전체 HKLM\System\CurrentControlSet\Services\NTDS\Parameters\Global 카탈로그 프로 모션**  
  
자세한 내용은 [글로벌 카탈로그 추가](AD-Forest-Recovery-Add-GC.md)합니다. 
  
이 단계에서 각 도메인에 대 한 DC가 하나를 사용 하 여 안정적인 포리스트 및 하나의 글로벌 카탈로그가 포리스트 있어야 합니다. 방금 복원한 dc가 각각의 새 백업을 만들어야 합니다. 이제 AD DS를 설치 하 여 다른 포리스트의 Dc를 다시 배포를 시작할 수 있습니다. 

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 - 필수 조건](AD-Forest-Recovery-Prerequisties.md)  
- [사용자 지정 포리스트 복구 계획을 고안 AD 포리스트 복구-](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD 포리스트 복구 문제를 식별 합니다.](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD 포리스트 Recovery-복구 하는 방법 결정](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD 포리스트 복구-초기 복구를 수행 합니다.](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)  
- [AD 포리스트 복구-질문과 대답](AD-Forest-Recovery-FAQ.md)  
- [AD 포리스트 복구-Multidomain 포리스트에 단일 도메인 복구](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [AD 포리스트 복구-Windows Server 2003 도메인 컨트롤러를 사용 하 여 포리스트 복구](AD-Forest-Recovery-Windows-Server-2003.md)  
