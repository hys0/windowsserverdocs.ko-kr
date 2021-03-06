---
ms.assetid: 67d8a8d7-2fbd-4ed7-bb41-75769f942024
title: 성능 모니터링 구성
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 94ff5a5e4ca16bdd1851a2997fdca1fd36741888
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854916"
---
# <a name="configure-performance-monitoring"></a>성능 모니터링 구성
  
## <a name="bkmk_ConfigurePerfMon"></a>  
AD FS에는 페더레이션 서버와 페더레이션 서버 프록시 컴퓨터의 성능을 모니터링 하는 데 도움이 되는 자체 전용 성능 카운터가 포함 되어 있습니다. 성능 모니터를 사용 하 여 AD FS 서버의 성능을 모니터링 하려면 새 데이터 수집기 집합을 만들고이 뷰에 AD FS 카운터를 추가 하는 것이 유용 합니다. 다음 절차에서는 AD FS에 대 한 성능 모니터링을 구성 하는 방법을 설명 합니다.  
  
#### <a name="to-configure-performance-monitoring-for-ad-fs-using-performance-monitor"></a>성능 모니터를 사용 하 여 AD FS에 대 한 성능 모니터링을 구성 하려면  
  
1. **시작** 화면에서 **성능 모니터**를 입력 한 다음 enter 키를 누릅니다.  
  
2. 콘솔 트리에서 **데이터 수집기 집합**을 확장 하 고\-마우스 오른쪽 단추로 **사용자 정의**를 클릭 한 다음 **새로 만들기**를 가리키고 **데이터 수집기 집합**을 클릭 합니다.  
  
   새 데이터 수집기 집합 만들기 마법사가 나타납니다.  
  
3. **새 데이터 수집기 집합 만들기**에서 **이름** 에 대해 새 데이터 수집기 \(집합의 이름 (예: "AD FS 성능\)")을 입력 하 고 **고급\)\(수동으로 만들기** 를 클릭 한 후 **다음**을 클릭 합니다.  
  
4. 포함할 데이터 형식에 대해 **데이터 로그 만들기** 가 선택 되어 있는지 확인 하 고 **성능 카운터**, **이벤트 추적 데이터**, **시스템 구성 정보**등의 데이터 형식에 대 한 확인란을 클릭 합니다.  
  
5. 성능 카운터의 경우 **사용 가능한 카운터** 목록에서 **AD FS** 을 확장 한 다음 **추가**를 클릭 합니다.  
  
   AD FS 성능 카운터가 **추가 된 카운터** 목록에 나타나야 합니다.  
  
6. 이벤트 추적 공급자를 추가 하 라는 메시지가 표시 되 면 **추가**를 클릭 하 고, **AD FS 이벤트** 를 선택 하 고, 공급자 목록에서 **추적을 AD FS** 합니다.  
  
7. 모니터링할 레지스트리 키를 추가 하 라는 메시지가 표시 되 면 **다음**을 클릭 합니다.  
  
8. 성능 데이터를 저장 하는 위치를 지정 하 라는 메시지가 표시 되 면 기본 위치 \( **% PerfLogs%\\\\관리\\** _< 데이터\_수집기_\_> 설정 하 고 **다음**을 클릭 합니다.  
  
9. 데이터 수집기 집합을 만들지 묻는 메시지가 표시 되 면 **저장 후 닫기**를 선택 하 고 **마침**을 클릭 합니다.  
  
    새 데이터 수집기 집합이 콘솔 트리의 **사용자 정의** 노드 아래에 나타납니다.  
  
10. 다음 단계를 사용 하 여 AD FS 성능 카운터를 사용할 수 있습니다.  
  
    -   AD FS\-관련 된 카운터를 사용 하 여 성능 모니터링을 시작 하려면 \(추가한 데이터 수집기 집합 (예: "AD FS 성능"\))을 마우스 오른쪽\-단추로 클릭 한 다음 **시작**을 클릭 합니다.  
  
    -   성능 모니터링 결과를 볼 보고서를 만들려면 "AD FS 성능"\)같이 \(추가한 데이터 수집기 집합을 마우스 오른쪽 단추로\-클릭 한 다음 **최신 보고서**를 클릭 합니다.  
  
    -   최신 보고서를 볼 수 있도록 성능 데이터 캡처를 종료 하려면\-\(추가한 데이터 수집기 집합을 마우스 오른쪽 단추로 클릭 하 고 (예: "AD FS 성능")\)클릭 한 다음 **중지**를 클릭 합니다.  
  
    최신 보고서가 자동 \(으로 추가 되 고 번호가 매겨집니다. **보고서\\사용자 정의** <em>\\< 데이터\_</em>\_\) 000001에서 시작 하 여 콘솔 트리의 > 노드를 설정 합니다.  
  
## <a name="ad-fs-performance-counters"></a>AD FS 성능 카운터  
다음 표에는 AD FS 성능 카운터가 나열 되어 있으며 페더레이션 서버 또는 페더레이션 서버 프록시와 관련 된 작업을 모니터링 하는 데 도움이 되는 방법이 설명 되어 있습니다.  
  
|카운터|설명|다음에서 사용할 수 있습니다. 
|-----------|---------------|------------------- 
|토큰 요청|SSOAuth 토큰 요청을 포함 하 여 페더레이션 서버로 보낸 토큰 요청 수를 모니터링 합니다.|페더레이션 서버 
|초당 토큰 요청\/|초당 SSOAuth 토큰 요청을 포함 하 여 페더레이션 서버로 보낸 토큰 요청 수를 모니터링 합니다.|페더레이션 서버  
|페더레이션 메타데이터 요청|페더레이션 서버로 전송 된 들어오는 페더레이션 메타 데이터 요청의 수를 모니터링 합니다.|페더레이션 서버  
|페더레이션 메타 데이터 요청\/초|페더레이션 서버에 전송 되는 초당 들어오는 페더레이션 메타 데이터 요청 수를 모니터링 합니다.|페더레이션 서버  
|아티팩트 확인 요청|페더레이션 서버에 전송 되는 초당 들어오는 페더레이션 메타 데이터 요청 수를 모니터링 합니다.|페더레이션 서버  
|아티팩트 확인 요청\/초|페더레이션 서버에 전송 되는 초당 아티팩트 확인 끝점에 대 한 요청 수를 모니터링 합니다.|페더레이션 서버  
|프록시 요청|페더레이션 서버 프록시로 전송 된 들어오는 요청의 수를 모니터링 합니다.|페더레이션 서버 프록시  
|프록시 요청\/초|페더레이션 서버 프록시에 전송 되는 초당 들어오는 요청 수를 모니터링 합니다.|페더레이션 서버 프록시  
|프록시 MEX 요청|페더레이션 서버 프록시로 전송 되는 MEX\) 요청 \(들어오는 WS\-Metadata Exchange의 수를 모니터링 합니다.|페더레이션 서버 프록시 
|프록시 MEX 요청\/초|페더레이션 서버 프록시에 전송 되는 초당 들어오는 MEX 요청 수를 모니터링 합니다.|페더레이션 서버 프록시  
  

