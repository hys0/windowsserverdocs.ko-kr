---
title: AD 포리스트 복구-전체 서버 복구 수행
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 1a1182a6-4462-4a13-806e-0e642a0d5db2
ms.technology: identity-adds
ms.openlocfilehash: bf321ae769aa6f0da1cebce7700ea429161a0956
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80824016"
---
# <a name="ad-forest-recovery---performing-a-full-server-recovery"></a>AD 포리스트 복구-전체 서버 복구 수행 

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

Windows Server 2016, 2012 R2 또는 2012에 대 한 전체 서버 복구를 수행 하려면 다음 절차를 따르십시오. 

## <a name="active-directory-full-server-recovery"></a>전체 서버 복구 Active Directory

다른 하드웨어 또는 다른 운영 체제 인스턴스로 복원 하는 경우 전체 서버 복구가 필요 합니다. 다음 사항을 기억하세요.

- 대상 서버의 번호 드라이브는 백업의 숫자와 동일 해야 하며, 크기 이상 이어야 합니다.
- **컴퓨터 복구** 옵션에 액세스 하려면 운영 체제 DVD에서 대상 서버를 시작 해야 합니다. 
- 대상 DC가 Hyper-v의 VM에서 실행 중이 고 백업이 네트워크 위치에 저장 된 경우에는 레거시 네트워크 어댑터를 설치 해야 합니다. 
- 전체 서버 복구를 수행한 후에는 [AD 포리스트 복구-DFSR 복제 sysvol의 신뢰할](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)수 있는 동기화를 수행 하는 방법에 설명 된 대로 SYSVOL의 신뢰할 수 있는 복원을 개별적으로 수행 해야 합니다.

시나리오에 따라 다음 절차 중 하나를 사용 하 여 전체 복원을 수행 합니다. 
  
## <a name="perform-a-full-server-restore-with-a-local-backup-with-the-latest-image"></a>최신 이미지를 사용 하 여 로컬 백업으로 전체 서버 복원 수행
  
1. Windows 설치 프로그램 시작 하 고 언어, 시간 및 통화 형식 및 키보드 옵션을 지정한 후 **다음**을 클릭 합니다. 
2. **컴퓨터 복구**를 클릭합니다.
   ![Server 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore1.png)
3. **문제 해결**을 클릭합니다.</br>
   ![Server 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore2.png)
4. **시스템 이미지 복구**를 클릭 합니다.</br>
   ![Server 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore3.png)
5. 클릭 **Windows Server 2016**합니다. 
   ![Server 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore4.png)
6. 가장 최근의 로컬 백업을 복원 하는 경우 사용 **가능한 최신 시스템 이미지 사용 (권장)** 을 클릭 하 고 **다음**을 클릭 합니다.
   ![Server 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore5.png)
7. 이제 다음 옵션이 제공 됩니다.
   -  디스크 포맷 및 다시 분할
   -  드라이버 설치
   -  자동으로 다시 시작 하 고 디스크 오류를 확인 하는 **고급** 기능을 선택 취소 합니다. 이러한 설정은 기본적으로 사용 하도록 설정 되어 있습니다.
   ![Server 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore6.png)
8. **다음**을 클릭합니다.
9. **마침**을 클릭합니다. 계속 하 시겠습니까? 라는 메시지가 표시 됩니다. **예**를 클릭합니다. 
   ![Server 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore11.png) 
10. 이 작업이 완료 되 면 [AD 포리스트 복구-DFSR 복제 sysvol의 신뢰할 수 있는 동기화 수행](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)에 설명 된 대로 SYSVOL의 정식 복원을 수행 합니다.

## <a name="perform-a-full-server-restore-with-any-image-local-or-remote"></a>로컬 또는 원격 이미지를 사용 하 여 전체 서버 복원 수행

1. Windows 설치 프로그램 시작 하 고 언어, 시간 및 통화 형식 및 키보드 옵션을 지정한 후 **다음**을 클릭 합니다. 
2. **컴퓨터 복구**를 클릭합니다.</br>
3. **문제 해결**을 클릭 하 고 **시스템 이미지 복구**를 클릭 한 다음 **Windows Server 2016**을 클릭 합니다. 
4. 가장 최근의 로컬 백업을 복원 하는 경우 **시스템 이미지 선택** 을 클릭 하 고 **다음**을 클릭 합니다.
5. 이제 복원 하려는 백업의 위치를 선택할 수 있습니다. 로컬 이미지의 경우 목록에서 선택할 수 있습니다. 
6. 이미지가 네트워크 공유에 있는 경우 **고급**을 선택 합니다. 드라이버를 설치 해야 하는 경우 **고급** 을 선택할 수도 있습니다.
   ![Server 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore7.png)
7. **고급** 을 클릭 한 후 네트워크에서 복원 하는 경우 **네트워크에서 시스템 이미지 검색**을 선택 합니다. 네트워크 연결을 복원 하 라는 메시지가 표시 될 수 있습니다. 확인을 선택 합니다. </br>
   ![Server 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore8.png)
8. 백업 공유 위치의 UNC 경로를 입력 하 고 (예: \\\server1\sta\\server\\\\\server1\\\\\\ **OK** \\\192.168.1.3\backups. 같은 대상 서버의 IP 주소를 입력할 수도 있습니다. 
   ![Server 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore9.png)
9. 공유에 액세스 하는 데 필요한 자격 증명을 입력 하 고 확인을 클릭 합니다. 
10. 이제 **복원할 시스템 이미지의 날짜와 시간을 선택** 하 고 **다음**을 클릭 합니다.
11. 이제 다음 옵션이 제공 됩니다.
    - 디스크 포맷 및 다시 분할
    - 드라이버 설치
    - 자동으로 다시 시작 하 고 디스크 오류를 확인 하는 **고급** 기능을 선택 취소 합니다. 이러한 설정은 기본적으로 사용 하도록 설정 되어 있습니다.
12. **다음**을 클릭합니다.
13. **마침**을 클릭합니다. 계속 하 시겠습니까? 라는 메시지가 표시 됩니다. **예**를 클릭합니다.  
14. 이 작업이 완료 되 면 [AD 포리스트 복구-DFSR 복제 sysvol의 신뢰할 수 있는 동기화 수행](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)에 설명 된 대로 SYSVOL의 정식 복원을 수행 합니다.

## <a name="enabling-the-network-adapter-for-a-network-backup"></a>네트워크 백업에 네트워크 어댑터를 사용 하도록 설정

명령 프롬프트에서 네트워크 어댑터를 사용 하도록 설정 하 여 네트워크 공유에서 복원 해야 하는 경우 다음 단계를 사용 합니다.

1. Windows 설치 프로그램 시작 하 고 언어, 시간 및 통화 형식 및 키보드 옵션을 지정한 후 **다음**을 클릭 합니다. 
2. **컴퓨터 복구**를 클릭합니다. I
3. **문제 해결**을 클릭 하 고 **명령 프롬프트**를 클릭 합니다. 
4. 다음 명령을 입력한 후 Enter 키를 누릅니다.  

   ```  
   wpeinit  
   ```

5. 네트워크 어댑터의 이름을 확인 하려면 다음을 입력 합니다.  

   ```  
   show interfaces  
   ```  

   다음 명령을 입력 하 고 각 명령 다음에 ENTER 키를 누릅니다.  

   ```  
   netsh  
   ```  

   ```  
   interface  
   ```  
  
   ```  
   tcp  
   ```  

   ```  
   ipv4  
   ```  
  
   ```  
   set address "Name of Network Adapter" static IPv4 Address SubnetMask IPv4 Gateway Address 1  
   ```  

   예를 들면 다음과 같습니다.  
  
   ```  
   set address "Local Area Connection" static 192.168.1.2 255.0.0.0 192.168.1.1 1  
   ```  

   `quit`를 입력 하 여 명령 프롬프트로 돌아갑니다. `ipconfig /all`를 입력 하 여 네트워크 어댑터에 IP 주소가 있는지 확인 하 고 연결을 확인 하기 위해 백업 공유를 호스팅하는 서버의 IP 주소를 ping 해 봅니다. 작업이 완료 되 면 명령 프롬프트를 닫습니다. 

6. 네트워크 어댑터가 제대로 작동 하 고 있습니다. 위의 단계를 선택 하 여 복원을 완료 합니다.

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)
