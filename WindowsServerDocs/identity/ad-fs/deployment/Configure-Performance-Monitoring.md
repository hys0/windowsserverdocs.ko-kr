---
ms.assetid: 67d8a8d7-2fbd-4ed7-bb41-75769f942024
title: "성능 모니터링 구성"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 6a7602cddcaee274d42213cd9365f6d1722dab79
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="configure-performance-monitoring"></a>성능 모니터링 구성

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
  
## <a name="bkmk_ConfigurePerfMon"></a>  
Adfs의 성능 federation 서버 및 federation 서버 프록시 컴퓨터를 모니터링 하는 데 도움이 되는 자체 전용된 성능 카운터 포함 되어 있습니다. 모니터링할 ADFS 서버 성능을 성능 모니터를 사용 하려면 데이터 수집기 새롭고 만들고 ADFS 카운터 보기를 추가 유용 합니다. 다음 절차에서는 성능 ADFS 모니터링 하 고 구성 하는 방법을 설명 합니다.  
  
#### <a name="to-configure-performance-monitoring-for-ad-fs-using-performance-monitor"></a>Adfs 성능 모니터를 사용 하 여 성능 모니터링 구성 하려면  
  
1.  에 **시작** 화면에서 입력 **성능 모니터**, ENTER 키를 누릅니다.  
  
2.  콘솔 트리에서 **수집기 데이터 집합**, right\ 클릭 **사용자 정의**를 가리킨 **새로**, 클릭 한 다음 **데이터 수집기 설정**합니다.  
  
    새 데이터 수집기 설정 만들기 마법사 나타납니다.  
  
3.  **새 데이터 컬렉터 집합 만들기**에 대 한 **이름** 새 데이터 컬렉터 집합에 대해 이름을 입력 \ ("ADFS 성능"와 같은 \)를 클릭 **\(Advanced\) 수동으로 만들**, 클릭 한 다음 **다음**합니다.  
  
4.  확인 포함할 데이터의 유형에 **데이터는 로그 만들** 을 선택한 다음 데이터 형식 옆의 확인란을 클릭 한 다음: **성능 카운터**, **이벤트 추적 데이터**, **시스템 구성 정보**합니다.  
  
5.  성능 카운터 확장 **ADFS** 에 **사용 가능한 카운터** 목록을 클릭 한 다음 선택 하 고 **추가**합니다.  
  
    ADFS 성능 카운터에서 표시 해야는 **카운터 추가** 목록입니다.  
  
6.  이벤트 추적 공급자를 추가 하 라는 메시지가 나타나면 클릭 **추가**선택 **광고 FS 이벤트** 및 **광고 FS 추적** 공급자 목록에서 합니다.  
  
7.  모니터를 레지스트리 키를 추가 하 라는 메시지가 나타나면 때 **다음**합니다.  
  
8.  기본 위치를 적용 수 있는 성능 데이터를 저장할 위치를 지정 메시지가 \ (**%systemdrive%\\PerfLogs\\Admin\\***< data\_collector\_set >*을 차례로 클릭 하 고 **다음**합니다.  
  
9. 데이터 컬렉터 집합을 만들려면 하는 메시지가 표시 되 면 **저장 하 고 닫기**을 차례로 클릭 하 고 **완료**합니다.  
  
    새 데이터 컬렉터 세트의 콘솔 트리에서에 표시 되 면는 **사용자 정의** 노드 합니다.  
  
10. 다음 단계를 사용 하 여 ADFS 성능 카운터에서 작동 하도록 합니다.  
  
    -   성능 카운터 광고 FS\ 관련 사용 모니터링 시작 right\ 클릭 데이터 수집기 설정는 추가 \ ("ADFS 성능"와 같은 \)를 클릭 한 다음 **시작**합니다.  
  
    -   성능을 확인 하 고 모니터링 결과 보고서를 만들려면 right\ 클릭 데이터 수집기 설정는 추가 \ ("ADFS 성능"와 같은 \)를 클릭 한 다음 **최신 보고서**합니다.  
  
    -   최신 보고서를 볼 수 있도록 캡처 성능 데이터를 종료, right\ 클릭 데이터 수집기 설정는 추가 \ ("ADFS 성능"와 같은 \)를 클릭 한 다음 **중지**합니다.  
  
    최신 보고서 추가 되 고 자동으로 번호 \(starting at 000001\) 아래에서 **Report\\User 정의***\\ < data\_collector\_set >* 노드의 콘솔 트리에서 합니다.  
  
## <a name="ad-fs-performance-counters"></a>광고 FS 성능 카운터  
다음 표에서 ADFS 성능 카운터 나열 하 고 모니터링 federation 서버 또는 federation 서버 프록시와 관련 된 작업에 사용 되는 방법을 설명 합니다.  
  
|카운터|설명|사용할 수 있습니다. 
|-----------|---------------|------------------- 
|토큰 요청|토큰 요청 SSOAuth 토큰 요청을 비롯 한 federation 서버에 전송으로 모니터링 합니다.|Federation 서버 
|토큰 Requests\ 초당|초당 SSOAuth 토큰 요청을 포함 하 여 federation 서버에 전송 토큰 요청으로 모니터링 합니다.|Federation 서버  
|Federation 메타 데이터 요청|들어오는 federation 메타 데이터 요청 federation 서버에 전송으로 모니터링 합니다.|Federation 서버  
|초당 federation Requests\ 메타 데이터|Federation 메타 데이터 초당 하 고 있는 요청 federation 서버에 전송 되어으로 모니터링 합니다.|Federation 서버  
|아티팩트 해상도 요청|Federation 메타 데이터 초당 하 고 있는 요청 federation 서버에 전송 되어으로 모니터링 합니다.|Federation 서버  
|아티팩트 해상도 Requests\ 초당|초당 아티팩트 해상도 끝점 요청을 처리 federation 서버에 전송 되어으로 모니터링 합니다.|Federation 서버  
|프록시 요청|들어오는 요청을 전송 federation 서버 프록시도 모니터링 합니다.|Federation 서버 프록시  
|프록시 Requests\ 초당|프록시 federation 서버에 전송 초당 들어오는 요청으로 모니터링 합니다.|Federation 서버 프록시  
|프록시 MEX 요청|프록시 federation 서버에 전송 하 고 있는 WS\ 메타 데이터 교환 \(MEX\) 요청으로 모니터링 합니다.|Federation 서버 프록시 
|프록시 MEX Requests\ 초당|초당 프록시 federation 서버에 전송 된 들어오는 MEX 요청으로 모니터링 합니다.|Federation 서버 프록시  
  

