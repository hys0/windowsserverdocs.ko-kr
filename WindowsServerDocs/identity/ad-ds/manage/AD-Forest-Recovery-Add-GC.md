---
title: "광고 숲 복구-GC 추가"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: 3749fd99737f61c55871f613b9feaa21090d3bae
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---adding-the-gc"></a>광고 숲 복구-GC 추가 

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

 다음 절차를 사용 하 여 드 DC에 추가 합니다.  
  
## <a name="to-add-the-global-catalog"></a>고 드 추가 하려면  
  
1.  클릭 **시작**, 가리킨 **모든 프로그램**, 가리킨 **관리 도구**을 차례로 클릭 하 고 **Active Directory 사이트 및 서비스**합니다.  
2.  콘솔 트리에서 확장는 **사이트** 컨테이너 및 대상 서버를 포함 하는 해당 사이트를 선택 합니다.  
3.  확장은 **서버** 컨테이너 드 추가할 DC에 대 한 서버 개체를 확장 합니다.  
4.  마우스 오른쪽 단추로 클릭 **NTDS 설정**을 차례로 클릭 하 고 **속성**합니다.  
5.  선택는 **드** 확인란을 선택 합니다.  
![GC 추가](media/AD-Forest-Recovery-Add-GC/addgc1.png)
  
## <a name="to-add-the-global-catalog-using-repadmin"></a>드 Repadmin를 사용 하 여 추가 하려면  
  
1.  관리자 명령 프롬프트를 열고 다음 명령을 입력 하 ENTER 키를 누릅니다.  
  
    ```  
    repadmin.exe /options DC_NAME +IS_GC  
    ```  
  
 다음은 드 루트 도메인에 있는 DC에 추가 하는 작업 속도를 향상 하는 방법:  
  
-   이 가장 좋습니다 루트 도메인에 있는 DC 루트 비 도메인에 복원 dc 복제 파트너 있어야 합니다. 그렇다면 확인 해당 정보 일관성 검사 (KCC)가 만든 **repsFrom** 원본 DC 및 파티션을 DC 루트에 대 한 합니다. 실행 하 여이 확인할 수 있는 **repadmin /showreps /v** 명령 합니다.  
  
-   없는 경우 없이 **repsFrom** 만든 개체, 구성 파티션에 대 한이 개체 발생 합니다. 이런 방법이으로 루트 도메인에 있는 DC 루트 비 도메인에 있는 Dc 삭제 된 확인할 수 있습니다. 다음 명령을 사용 하 여이 수행할 수 있습니다.  
  
    ```  
    repadmin /add ConfigurationNamingContext DestinationDomainController SourceDomainControllerCNAME  
    ```  
  
    ```  
    repadmin /options DSA -Disable_NTDSCONN_XLATE  
    ```  
  
     형식에 대 한는 *SourceDomainControllerCNAME* 는 다음과 같습니다.  
  
    ```  
  
    sourceDCGuid._msdcs.root domain  
    ```  
  
     예를 들어, contoso.com 도메인 구성 파티션 repadmin /add 명령을 수 있습니다.  
  
    ```  
    repadmin /add cn=configuration,DC=contoso,DC=com DC01 937ef930-7356-43c8-88dc-8baaaa781cf6._msdcs.dDSP17A22.contoso.com  
    ```  
  
-   하는 경우는 **repsFrom** 개체가 있는 경우 다음과 같은 DC 루트 비 도메인에 있는 루트 도메인에 있는 DC 동기화 하려고 합니다.  
  
    ```  
    Repadmin /sync DomainNamingContext DestinationDomainController SourceDomainControllerGUID  
    ```  
  
     여기서 *DestinationDomainController* 루트 도메인 dc 및 *SourceDomainController* 복원된 DC 루트 비 도메인에는 합니다.  
  
-   루트 도메인 DNS 서버에 대 한 소스 DC (CNAME) 별칭 리소스 레코드 있어야 합니다. 부모 DNS 영역 포함 되어 있는지 확인 (NS 이름 서버 () 및 리소스 레코드 호스트 (A)) 위임 리소스 레코드 올바른 Dc (백업에서 복원 된 Dc)에 대 한 자녀가 영역에서 합니다.  
  
-   DC 루트 도메인에 루트 비 도메인에 올바른 키 메일 센터 (KDC)는 연결 하는 있는지 확인 합니다. 명령 프롬프트이 테스트를 하려면 다음 명령을 입력 하 고 enter:  
  
    ```  
    nltest /dsgetdc:nonroot domain name /KDC /Force  
    ```  
## <a name="next-steps"></a>다음 단계

- [광고 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)  
