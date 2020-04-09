---
title: 기록 데이터를 사용 하 여 원격 클라이언트에 대 한 사용 현황 보고서를 생성 합니다.
description: 이 항목은 Windows Server 2016의 원격 액세스 모니터링 및 계정에 대 한 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 0305467b-ce39-4532-a05a-2cc5ff946f55
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ae862b596ff8c3d222c8f448f9b81b3c6bea05be
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860566"
---
# <a name="generate-a-usage-report-for-remote-clients-using-historical-data"></a>기록 데이터를 사용 하 여 원격 클라이언트에 대 한 사용 현황 보고서를 생성 합니다.

>적용 대상: Windows Server(반기 채널), Windows Server 2016

**참고:** Windows Server 2012 DirectAccess 및 라우팅 및 원격 액세스 서비스 (RRAS)를 단일 원격 액세스 역할로 결합 합니다.  
  
원격 액세스 서버에서 관리 콘솔에 액세스 하는 서버는 원격 클라이언트에 대 한 사용 현황 보고서 생성 데 사용할 수 있습니다. 원격 클라이언트에 대 한 사용 현황 보고서를 생성 하려면 먼저 계정에 원격 액세스 서버를 사용 합니다. 보고서를 생성 한 후에 서버에 부하 통계를 보려면 원격 액세스 서버에서 관리 콘솔에서 사용할 수 있는 모니터링 대시보드를 사용할 수 있습니다.  
  
> [!NOTE]  
> 이 항목에 설명 된 작업을 완료 하려면 Domain Admins 그룹의 구성원 또는 각 컴퓨터에서 Administrators 그룹의 구성원으로 로그인 해야 합니다. Administrators 그룹의 구성원 인 계정으로 로그인 하는 동안에 작업을 완료할 수 없는 경우에 Domain Admins 그룹의 구성원 인 계정으로 로그인 하는 동안 작업을 수행해 봅니다.  
  
#### <a name="to-enable-accounting-on-the-remote-access-server"></a>계정에 원격 액세스 서버를 사용 하도록 설정 하려면  
  
1.  **서버 관리자**, 클릭 **도구**, 를 클릭 하 고 **원격 액세스 관리**합니다.  
  
2.  클릭 **보고** 탐색할 **원격 액세스 보고** 에 **원격 액세스 관리 콘솔**합니다.  
  
3.  클릭 **계정 구성** 에 **원격 액세스 보고** 작업창 합니다.  
  
4.  선택 된 **받은 편지함 계정을 사용 하 여** 계정에 원격 액세스 서버를 사용 하려면 확인란입니다.  
  
5.  클릭 **적용** 서버에서 계정 구성을 사용 하도록 한 다음 클릭 **닫기** 서버에 적용 된 후 구성을 성공적으로 합니다.  
  
#### <a name="to-generate-the-usage-report"></a>사용 현황 보고서를 생성 하려면  
  
1.  **서버 관리자**, 클릭 **도구**, 를 클릭 하 고 **원격 액세스 관리**합니다.  
  
2.  클릭 **보고** 탐색할 **원격 액세스 보고** 에 **원격 액세스 관리 콘솔**합니다.  
  
3.  가운데 창에서 보고서 기간을 선택 하는 달력에 날짜를 클릭 합니다. **시작 날짜:** 및 **종료 날짜:** , 를 클릭 하 고 **보고서 생성**합니다.  
  
4.  선택한 시간 및에 대 한 자세한 통계를 내 원격 액세스 서버에 연결 된 사용자 목록이 표시 됩니다. 목록에서 첫 번째 행을 클릭 합니다. 행을 선택 하면 원격 사용자 활동은 미리 보기 창에 표시 됩니다. 이제 선택 된 **서버 로드 통계** 서버의 기록 부하를 보려면 미리 보기 창에서 탭 합니다.  
  
    클릭 된 **서버 로드 통계** 서버의 기록 부하를 보려면 미리 보기 창에서 탭.  
  
> [!NOTE]  
> **세션 이해**  
>   
> 원격 액세스 계정 관리의 개념에 기반 **세션**합니다. 달리는 **연결**,  **세션** 원격 클라이언트 IP 주소와 사용자 이름의 조합으로 고유 하 게 식별 됩니다. 예를 들어 한 컴퓨터 터널이 client1, 원격 클라이언트에서 형식이 아니면 세션을 만든 계정 데이터베이스에 저장 합니다. 일정 시간이 지난 후 해당 클라이언트에서 연결 하는 명명 된 User1 사용자 전달 제외한 컴퓨터 터널이 아직 활성 상태인, 세션이 별도 세션으로 기록 됩니다. 세션의 차이 유지 하는 컴퓨터 터널이 사용자 터널을 구분 합니다.  
  
![Windows PowerShell](../../../media/Generate-a-usage-report-for-remote-clients-using-historical-data/PowerShellLogoSmall.gif)***<em>windows powershell 해당 명령</em>***  
  
다음 Windows PowerShell cmdlet은 이전 절차와 동일한 기능을 수행합니다. 서식 조건 때문에 각 cmdlet이 여러 줄로 자동 줄 바꿈되어 표시되더라도 한 줄에 입력합니다.  
  
다음 스크립트에서 검색할 보고서에서 날짜 범위를 변경 된 **-StartDateTime** 및 **-EndDateTime** 매개 변수입니다.  
  
```  
PS> Get-RemoteAccessConnectionStatisticsSummary -StartDateTime "1 October 2010 00:00:00" -EndDateTime "14 October 2010 00:00:00"  
Shows server load statistics.  
PS> Get-RemoteAccessUserActivity -HostIPAddress 10.0.0.1 -StartDateTime "1 October 2010 00:00:00" -EndDateTime "14 October 2010 00:00:00"  
```  
  


