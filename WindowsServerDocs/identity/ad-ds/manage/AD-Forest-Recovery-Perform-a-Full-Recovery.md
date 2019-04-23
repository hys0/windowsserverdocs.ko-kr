---
title: AD 포리스트 복구-전체 서버 복구를 수행 합니다.
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 1a1182a6-4462-4a13-806e-0e642a0d5db2
ms.technology: identity-adds
ms.openlocfilehash: 6f600ade3d07130d4e1fb3b1a254cb1073f592e9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874234"
---
# <a name="ad-forest-recovery---performing-a-full-server-recovery"></a>AD 포리스트 복구-전체 서버 복구를 수행 합니다. 

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

Windows Server 2016, 2012 R2 또는 2012에 대 한 전체 서버 복구를 수행 하려면 다음 절차를 따르십시오. 

## <a name="active-directory-full-server-recovery"></a>Active Directory 전체 서버 복구

전체 서버 복구는 다른 하드웨어 또는 다른 운영 체제 인스턴스로 복원 하는 경우에 필요 합니다. 다음 사항을 기억하세요.

- 백업에 수와 동일 해야 대상 서버 요구 사항에 드라이브 수 및 크기 이상 동일 하도록 필요한 합니다.
- 대상 서버에 액세스 하기 위해 운영 체제 DVD에서에서 시작 해야 합니다 **컴퓨터 복구** 옵션입니다. 
- 대상 DC가 Hyper-v 및 백업에는 VM에서 실행 중에 네트워크 위치에 저장 된 경우 레거시 네트워크 어댑터를 설치 해야 합니다. 
- 전체 서버 복구를 수행한 후 별도로 수행 해야 SYSVOL의 신뢰할 수 있는 복원 하는 경우에 설명 된 대로 [DFSR 복제 SYSVOL의 신뢰할 수 있는 동기화를 수행할 AD 포리스트 복구](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)합니다.

시나리오에 따라 전체 복원을 수행 하려면 다음 절차 중 하나를 사용 합니다. 
  
## <a name="perform-a-full-server-restore-with-a-local-backup-with-the-latest-image"></a>최신 이미지를 사용 하 여 로컬 백업 사용 하 여 전체 서버 복원을 수행합니다
  
1. Windows 설치 프로그램을 시작 하 고, 언어, 시간 및 통화 형식 및 키보드 옵션을 지정 하 고, 클릭 **다음**합니다. 
2. **컴퓨터 복구**를 클릭합니다.
   ![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore1.png)
3. **문제 해결**을 클릭합니다.</br>
   ![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore2.png)
4. 클릭 **시스템 이미지 복구**합니다.</br>
   ![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore3.png)
5. 클릭 **Windows Server 2016**합니다. 
   ![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore4.png)
6. 최신 로컬 백업을 복원 하는 경우 클릭 **가능한 최신 시스템 이미지 사용 (권장)** 누릅니다 **다음**합니다.
   ![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore5.png)
7. 옵션을 제공 이제 됩니다.
   -  디스크 포맷 및 다시 분할
   -  드라이버 설치
   -  선택을 취소 하는 **고급** 기능의 자동으로 다시 시작 하 고 확인 하는 디스크 오류입니다. 이러한 옵션은 기본적으로 설정 됩니다.
   ![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore6.png)
8. **다음**을 클릭합니다.
9. **마침**을 클릭합니다. 계속 하 시겠습니까 묻는 라는 메시지가 표시 됩니다. **예**를 클릭합니다. 
   ![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore11.png) 
10. 이 작업이 완료 되 면 수행 SYSVOL의 신뢰할 수 있는 복원 하는 경우에 설명 된 대로 [DFSR 복제 SYSVOL의 신뢰할 수 있는 동기화를 수행할 AD 포리스트 복구](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)합니다.

## <a name="perform-a-full-server-restore-with-any-image-local-or-remote"></a>로컬 또는 원격 이미지를 사용 하 여 전체 서버 복원을 수행합니다

1. Windows 설치 프로그램을 시작 하 고, 언어, 시간 및 통화 형식 및 키보드 옵션을 지정 하 고, 클릭 **다음**합니다. 
2. **컴퓨터 복구**를 클릭합니다.</br>
3. 클릭 **문제 해결**, 클릭 **시스템 이미지 복구**를 클릭 하 고 **Windows Server 2016**합니다. 
4. 최신 로컬 백업을 복원 하는 경우 클릭 **시스템 이미지 선택** 누릅니다 **다음**합니다.
5. 이제 복원 하려는 백업 위치를 선택할 수 있습니다. 이미지 로컬인 경우에 목록에서 선택할 수 있습니다. 
6. 이미지를 네트워크 공유에 있으면 선택 **고급**합니다. 선택할 수도 있습니다 **고급** 드라이버를 설치 해야 할 경우.
   ![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore7.png)
7. 클릭 한 후 네트워크에서 복원 하는 경우 **Advanced** 선택 **네트워크에서 시스템 이미지 검색**합니다. 네트워크 연결을 복원 하 라는 메시지가 표시 될 수 있습니다. 확인을 선택 합니다. </br>
   ![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore8.png)
8. 백업 공유 위치에 UNC 경로 입력 (예를 들어 \\\server1\backups)를 누릅니다 **확인**합니다. 입력할 수도 있습니다 대상 서버의 IP 주소와 같은 \\\192.168.1.3\backups 합니다. 
   ![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore9.png)
10. 클릭 하 고 공유에 액세스 하는 데 필요한 자격 증명을 입력 합니다. 
11. 이제 **복원할 날짜 및 시간 시스템 이미지 선택** 누릅니다 **다음**합니다.
12. 옵션을 제공 이제 됩니다.
   - 디스크 포맷 및 다시 분할
   - 드라이버 설치
   - 선택을 취소 하는 **고급** 기능의 자동으로 다시 시작 하 고 확인 하는 디스크 오류입니다. 이러한 옵션은 기본적으로 설정 됩니다.
13. **다음**을 클릭합니다.
14. **마침**을 클릭합니다. 계속 하 시겠습니까 묻는 라는 메시지가 표시 됩니다. **예**를 클릭합니다.  
15. 이 작업이 완료 되 면 수행 SYSVOL의 신뢰할 수 있는 복원 하는 경우에 설명 된 대로 [DFSR 복제 SYSVOL의 신뢰할 수 있는 동기화를 수행할 AD 포리스트 복구](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)합니다.

## <a name="enabling-the-network-adapter-for-a-network-backup"></a>네트워크 백업에 대 한 네트워크 어댑터를 사용 하도록 설정

네트워크 공유에서 복원 하려면 명령 프롬프트에서 네트워크 어댑터를 사용 하도록 설정 해야 할 경우 다음 단계를 사용 합니다.

1. Windows 설치 프로그램을 시작 하 고, 언어, 시간 및 통화 형식 및 키보드 옵션을 지정 하 고, 클릭 **다음**합니다. 
2. **컴퓨터 복구**를 클릭합니다. I
3. 클릭 **문제 해결**, 클릭 **명령 프롬프트**합니다. 
4. 다음 명령을 입력한 후 Enter 키를 누릅니다.  

   ```  
   wpeinit  
   ```

5. 네트워크 어댑터의 이름을 확인 하려면 다음을 입력 합니다.  

   ```  
   show interfaces  
   ```  

   다음 명령을 입력 하 고 각 명령 후 enter 키를 누릅니다.  

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

   예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
   ```  
   set address "Local Area Connection" static 192.168.1.2 255.0.0.0 192.168.1.1 1  
   ```  

   형식 `quit` 명령 프롬프트로 돌아갑니다. 형식 `ipconfig /all` 확인 네트워크 어댑터에 IP 주소 및 연결을 확인 하려면 백업 공유를 호스팅하는 서버의 IP 주소를 ping 해 보세요. 완료 되 면 명령 프롬프트를 닫습니다. 

6. 네트워크 어댑터를 사용할 했으므로 복원을 완료 하려면 위의 단계를 선택 합니다.

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)
