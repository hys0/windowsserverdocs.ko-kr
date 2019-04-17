---
title: "광고 숲 복구-전체 서버 복구"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 1a1182a6-4462-4a13-806e-0e642a0d5db2
ms.technology: identity-adfs
ms.openlocfilehash: 5de71cc005e9ec4c1425f9fa805b3c043ab4ea36
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---performing-a-full-server-recovery"></a>광고 숲 복구-전체 서버 복구 

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.
 
다음 절차를 사용 하 여 Windows Server 2016 년 2012 r 2 또는 2012에 대 한 전체 서버를 수행 합니다. 

## <a name="active-directory-full-server-recovery"></a>전체 서버 active Directory 복구
전체 서버는 다양 한 하드웨어 또는 다른 운영 체제 인스턴스를 복원 하는 경우 필요 합니다. 유념 다음.

- 드라이브를 백업에 수와 같은 대상 서버 요구에 수 및 크기 이상 동일 하 게 필요한 합니다.
- 대상 서버를에 액세스 하기 위해 운영 체제 DVD에서에서 시작 필요 하다는 **컴퓨터 복구** 옵션입니다. 
- DC 백업을 켜고 Hyper-v VM에서 실행 중인 대상 네트워크 위치에 저장 되 면 레거시 네트워크 어댑터를 설치 해야 합니다.  
- 전체 서버를 수행한 후 수행 해야 할 별도로 SYSVOL의 정식 복원을에 설명 된 대로 [광고 숲 복구-DFSR 복제 sysvol 신뢰할 수 있는 동기화 수행](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)합니다.


시나리오에 따라 전체 복원을 수행 하려면 다음 절차 중 하나를 사용 합니다.  
  
### <a name="perform-a-full-server-restore-with-a-local-backup-with-the-latest-image"></a>최신 이미지 로컬 백업 사용 하 여 전체 서버 복원을 수행합니다
  
1.  Windows 설치를 시작 하 고 언어, 시간 및 통화 형식 및 키보드 옵션 지정한 클릭 **다음**합니다.  
2.  클릭 **컴퓨터 복구**합니다.</br>
![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore1.png)
3.  클릭 **해결**합니다.</br>
![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore2.png)
4.  클릭 **시스템 이미지 복구**합니다.</br>
![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore3.png)
5.  클릭 **Windows Server 2016**합니다.  
![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore4.png)
6.  가장 최근 로컬 백업을 복원 하는 경우 클릭 **(권장) 최신 사용할 수 있는 시스템 이미지를 사용 하 여** 클릭 **다음**합니다.
![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore5.png)
7.  하는 옵션이 제공 이제 됩니다.
    -  디스크를 포맷 및 다시 분할
    -  드라이버 설치
    -  선택을 취소 하 고 **고급** 디스크 오류 기능 자동으로 다시 시작 하 고 있는지 확인 합니다.  이 기본적으로 활성화 됩니다.
![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore6.png)
8. 클릭 **다음**합니다.
9. 클릭 **완료**합니다.  계속할 것인지 확인 하 라는 메시지가 표시 되는 합니다.  클릭 **예**합니다.  
![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore11.png) 
10. 이 작업이 완료 되 면에 설명 된 대로 sysvol, 정식 복원을 수행 [광고 숲 복구-DFSR 복제 sysvol 신뢰할 수 있는 동기화 수행](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)합니다.
 

### <a name="perform-a-full-server-restore-with-any-image-local-or-remote"></a>로컬 또는 원격 이미지를 사용 하 여 전체 서버 복원을 수행합니다
1.  Windows 설치를 시작 하 고 언어, 시간 및 통화 형식 및 키보드 옵션 지정한 클릭 **다음**합니다.  
2.  클릭 **컴퓨터 복구**합니다.</br>
3.  클릭 **문제 해결**, 클릭 **시스템 이미지 복구**를 클릭 하 고 **Windows Server 2016**합니다.  
4.  가장 최근 로컬 백업을 복원 하는 경우 클릭 **시스템 이미지를 선택** 클릭 **다음**합니다.

5.  지금 백업 복원 하려는 위치를 선택할 수 있습니다.  이미지가 로컬 목록에서 선택할 수 있습니다.  
6.  네트워크 공유에서 이미지가 있으면 선택 **고급**합니다.  선택할 수도 있습니다 **고급** 드라이버를 설치 해야 합니다.
![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore7.png)
7.  클릭 한 후 네트워크에서 복원 하는 경우 **고급** 선택 **네트워크에 시스템 이미지에 대 한 검색**합니다.  네트워크 연결을 복원 하 라는 메시지가 표시 될 수 있습니다.  확인을 선택 합니다. </br>
![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore8.png)
8. UNC 경로 공유 백업 위치 (예를 들어 \\\server1\backups)를 입력 하 고 클릭 **확인**합니다.  또한 대상 서버 \\\192.168.1.3\backups 등의 IP 주소를 입력할 수 있습니다.  
![서버 복원](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore9.png)
10. 공유에 액세스 하 고 확인을 클릭 하는 데 필요한 자격 증명을 입력 합니다.  
11. 이제 **복원 하려면 날짜 및 시간 시스템 이미지의 선택** 클릭 **다음**합니다.
12. 하는 옵션이 제공 이제 됩니다.
    1.   디스크를 포맷 및 다시 분할
    2.   드라이버 설치
    3.   선택을 취소 하 고 **고급** 디스크 오류 기능 자동으로 다시 시작 하 고 있는지 확인 합니다.  이 기본적으로 활성화 됩니다.
13. 클릭 **다음**합니다.
14. 클릭 **완료**합니다.  계속할 것인지 확인 하 라는 메시지가 표시 되는 합니다.  클릭 **예**합니다.   
15. 이 작업이 완료 되 면에 설명 된 대로 sysvol, 정식 복원을 수행 [광고 숲 복구-DFSR 복제 sysvol 신뢰할 수 있는 동기화 수행](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)합니다.


### <a name="enabling-the-network-adapter-for-a-network-backup"></a>네트워크 백업에 네트워크 어댑터 사용
네트워크 공유에서 복원 하는 명령 프롬프트에서 네트워크 어댑터를 사용 하려는 경우 다음 단계를 사용 합니다.

1.  Windows 설치를 시작 하 고 언어, 시간 및 통화 형식 및 키보드 옵션 지정한 클릭 **다음**합니다.  
2.  클릭 **컴퓨터 복구**합니다. 저는
3.  클릭 **문제 해결**, 클릭 **명령 프롬프트**합니다.  
4.  다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
    ```  
    wpeinit  
    ```   
5.  네트워크 어댑터의 이름을 확인 하려면 다음을 입력 합니다.  
  
    ```  
    show interfaces  
    ```  
  
     다음 명령을 입력 하 고 각 명령 뒤 enter 키를 누릅니다.  
  
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
  
     예를 들어:  
  
    ```  
    set address "Local Area Connection" static 192.168.1.2 255.0.0.0 192.168.1.1 1  
    ```  
  
     입력 `quit`명령 프롬프트도 돌아갑니다. 입력 `ipconfig /all`네트워크를 확인 하려면 어댑터의 IP 주소와 연결을 확인 하 고 백업 공유 호스트 하는 서버의 IP 주소를 다시 ping 해 보세요. 완료 되 면 명령 프롬프트를 닫습니다.  
  
6.  네트워크 어댑터가 작동 하는 복원 하려면 위의 단계를 선택 합니다.

## <a name="next-steps"></a>다음 단계

- [광고 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)
