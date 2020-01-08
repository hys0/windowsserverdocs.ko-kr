---
title: 저속 SMB 파일 전송 속도
description: SMB 파일 전송 성능 문제를 해결 하는 방법을 소개 합니다.
author: Deland-Han
manager: dcscontentpm
audience: ITPro
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 0e6c049404f464eba872075a8ef5060b303920c8
ms.sourcegitcommit: 8cf04db0bc44fd98f4321dca334e38c6573fae6c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/03/2020
ms.locfileid: "75654564"
---
# <a name="slow-smb-files-transfer-speed"></a>저속 SMB 파일 전송 속도

이 문서에서는 SMB를 통한 저속 파일 전송 속도에 대 한 권장 되는 문제 해결 절차를 제공 합니다.

## <a name="large-file-transfer-is-slow"></a>대량 파일 전송 속도가 느립니다.

대량 파일의 전송 속도가 느려지는 경우 다음 단계를 고려 하십시오.

- 버퍼링 되지 않은 IO에 대 한 파일 복사 명령 (**xcopy/j** 또는 **robocopy/j**)을 시도 합니다.

- 저장소 속도를 테스트 합니다. 이는 파일 복사 속도가 저장소 속도로 제한 되기 때문입니다.

- 파일 복사는 빠르게 시작 되 고 속도가 저하 되는 경우가 있습니다. 이러한 상황을 확인 하려면 다음 지침을 따르세요.
    
  - 이는 일반적으로 초기 복사본이 캐시 되거나 버퍼링 될 때 (메모리 나 RAID 컨트롤러의 메모리 캐시에 있는 경우) 캐시를 실행 하는 경우에 발생 합니다. 이렇게 하면 데이터를 디스크에 직접 쓸 수 있습니다. 이는 속도가 느린 프로세스입니다.
    
  - 저장소 성능 모니터 카운터를 사용 하 여 시간이 지남에 따라 저장소 성능이 저하 되는지 여부를 확인할 수 있습니다. 자세한 내용은 [SMB 파일 서버에 대 한 성능 튜닝](https://docs.microsoft.com/windows-server/administration/performance-tuning/role/file-server/smb-file-server)을 참조 하세요.

- SysInternals (지 수 맵)를 사용 하 여 메모리 부족으로 인해 메모리의 "매핑된 파일" 사용이 증가 하 고 있는지 여부를 확인 합니다.

- 추적에서 패킷 손실을 찾습니다. 이로 인해 TCP 정체 공급자에 의해 제한 될 수 있습니다.

- SMBv3 이상 버전의 경우 SMB 다중 채널을 사용 하도록 설정 하 고 작동 하는지 확인 합니다.

- SMB 클라이언트에서 SMB의 large MTU를 사용 하도록 설정 하 고 대역폭 제한을 사용 하지 않도록 설정 합니다. 이렇게 하려면 다음 명령을 실행합니다.  
  
  ```PowerShell
  Set-SmbClientConfiguration -EnableBandwidthThrottling 0 -EnableLargeMtu 1
  ```

## <a name="small-file-transfer-is-slow"></a>작은 파일 전송 속도가 느립니다.

SMB를 통한 작은 파일의 저속 전송은 많은 파일이 있는 경우 가장 일반적으로 발생 합니다. 이는 정상적인 동작입니다.

파일을 전송 하는 동안 파일을 만들면 높은 프로토콜 오버 헤드와 높은 파일 시스템 오버 헤드가 발생 합니다. 대량 파일 전송의 경우 이러한 비용은 한 번만 발생 합니다. 많은 수의 작은 파일을 전송 하는 경우 비용이 반복적으로 발생 하 여 전송 속도가 느려집니다.

이 문제에 대 한 기술적인 세부 정보는 다음과 같습니다.

- SMB는 create 명령을 호출 하 여 파일을 만들도록 요청 합니다. 일부 코드는 파일이 있는지 여부를 확인 한 다음 파일을 만듭니다. 또는 create 명령의 일부 변형으로 실제 파일이 생성 됩니다.

- 각 create 명령은 파일 시스템에 대 한 작업을 생성 합니다.

- 데이터를 쓴 후 파일을 닫습니다.

- 이 프로세스는 항상 네트워크 대기 시간 및 SMB 서버 대기 시간을 통해 발생 합니다. 이는 SMB 요청이 먼저 파일 시스템 명령으로 변환 된 후 작업을 완료 하기 위해 실제 파일 시스템 대기 시간으로 변환 되기 때문입니다.

- 바이러스 백신 프로그램이 실행 중인 경우 훨씬 더 느리게 전송 됩니다. 일반적으로 데이터는 패킷 탐지기에서 한 번 검색 되 고 디스크에 기록 될 때 두 번째로 검색 되기 때문입니다. 이러한 작업은 수천 번 반복 되는 경우도 있습니다. 1 m b/초 미만의 속도가 관찰 될 수 있습니다.

## <a name="opening-office-documents-is-slow"></a>Office 문서 열기 속도가 느립니다.

이 문제는 일반적으로 WAN 연결에서 발생 합니다. 일반적으로이는 Office 앱 (특히 Microsoft Excel)에서 데이터를 액세스 하 고 읽는 방식에 의해 발생 합니다.

Office 및 SMB 이진 파일이 최신 상태 인지 확인 하 고 SMB 서버에서 임대를 사용 하지 않도록 설정 하 여 테스트 하는 것이 좋습니다. 이렇게 하려면 다음 단계를 따르세요.
   
1. Windows 8 및 windows Server 2012 이상 버전의 windows에서 다음 PowerShell 명령을 실행 합니다.
      
   ```PowerShell
   Set-SmbServerConfiguration -EnableLeasing $false  
   ```
      
   또는 관리자 권한 명령 프롬프트 창에서 다음 명령을 실행 합니다.  

   ```cmd
   REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\lanmanserver\parameters /v DisableLeasing /t REG\_DWORD /d 1 /f  
   ```
      
   > [!NOTE]
   > 이 레지스트리 키를 설정 하면 SMB2 임대가 더 이상 부여 되지 않지만 oplock는 계속 사용할 수 있습니다. 이 설정은 주로 문제 해결에 사용 됩니다.
    
2. 파일 서버를 다시 시작 하거나 **서버** 서비스를 다시 시작 하십시오. 서비스를 다시 시작 하려면 다음 명령을 실행 합니다.

   ```cmd  
   NET STOP SERVER 
   NET START SERVER
   ```

이 문제를 방지 하려면 파일을 로컬 파일 서버에 복제할 수도 있습니다. 자세한 내용은 [EFS를 사용 하는 경우 Aving Office documents to a network server 느림](https://docs.microsoft.com/office/troubleshoot/office/saving-file-to-network-server-slow)을 참조 하세요.
