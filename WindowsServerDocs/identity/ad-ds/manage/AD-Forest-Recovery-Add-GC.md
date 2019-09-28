---
title: AD 포리스트 복구-GC 추가
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: f82033dd042847c7c735423c25756b936b137230
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369343"
---
# <a name="ad-forest-recovery---adding-the-gc"></a>AD 포리스트 복구-GC 추가

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

글로벌 카탈로그를 DC에 추가 하려면 다음 절차를 따르십시오.  
  
## <a name="to-add-the-global-catalog"></a>글로벌 카탈로그를 추가 하려면  
  
1. **시작**을 클릭 하 고 **모든 프로그램**, **관리 도구**를 차례로 가리킨 다음 **Active Directory 사이트 및 서비스**를 클릭 합니다.  
2. 콘솔 트리에서 **사이트** 컨테이너를 확장 하 고 대상 서버가 포함 된 적절 한 사이트를 선택 합니다.  
3. **서버** 컨테이너를 확장 한 다음 글로벌 카탈로그를 추가할 DC의 서버 개체를 확장 합니다.  
4. **NTDS 설정**을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.  
5. **글로벌 카탈로그** 확인란을 선택 합니다.  
![ Add GC @ no__t-1

## <a name="to-add-the-global-catalog-using-repadmin"></a>Repadmin을 사용 하 여 글로벌 카탈로그를 추가 하려면  

- 관리자 권한 명령 프롬프트를 열고 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  

   ```  
   repadmin.exe /options DC_NAME +IS_GC  
   ```  

다음은 루트 도메인의 DC에 글로벌 카탈로그를 추가 하는 프로세스의 속도를 높이는 방법입니다.  

- 이상적으로 루트 도메인의 DC는 루트가 아닌 도메인에 있는 복원 된 Dc의 복제 파트너 여야 합니다. 그렇다면 지식 일관성 검사기 (KCC)가 루트 DC의 원본 DC 및 파티션에 대해 해당 **repsFrom** 개체를 만들었는지 확인 합니다. **Repadmin/showreps/v** 명령을 실행 하 여이를 확인할 수 있습니다. 

- **RepsFrom** 개체가 생성 되지 않은 경우 구성 파티션에 대해이 개체를 만듭니다. 이러한 방식으로 루트 도메인의 DC는 루트가 아닌 도메인의 dc가 삭제 되었는지 확인할 수 있습니다. 다음 명령을 사용 하 여이 작업을 수행할 수 있습니다.  

   ```
   repadmin /add ConfigurationNamingContext DestinationDomainController SourceDomainControllerCNAME  
   ```

   ```
   repadmin /options DSA -Disable_NTDSCONN_XLATE  
   ```

   *SourceDomainControllerCNAME* 형식은 다음과 같습니다.  

   ```
  
   sourceDCGuid._msdcs.root domain  
   ```

   예를 들어 contoso.com 도메인의 구성 파티션에 대 한 repadmin/add 명령은 다음과 같을 수 있습니다.  

   ```
   repadmin /add cn=configuration,DC=contoso,DC=com DC01 937ef930-7356-43c8-88dc-8baaaa781cf6._msdcs.dDSP17A22.contoso.com  
   ```

- **RepsFrom** 개체가 있는 경우 다음과 같이 루트 도메인의 dc를 루트가 아닌 도메인의 dc와 동기화 해 봅니다.  

   ```
   Repadmin /sync DomainNamingContext DestinationDomainController SourceDomainControllerGUID  
   ```

   여기서 *DestinationDomainController* 은 루트 도메인의 dc이 고 *SourceDomainController* 는 루트 도메인에 있는 복원 된 dc입니다. 

- 루트 도메인 DNS 서버에는 원본 DC에 대 한 별칭 (CNAME) 리소스 레코드가 있어야 합니다. 부모 DNS 영역에 자식 영역에서 올바른 Dc (백업에서 복원 된 Dc)에 대 한 위임 리소스 레코드 (NS (이름 서버) 및 호스트 (A) 리소스 레코드)가 포함 되어 있는지 확인 합니다. 
- 루트 도메인의 DC가 루트가 아닌 도메인의 올바른 키 배포 센터 (KDC)에 연결 하 고 있는지 확인 합니다. 이를 테스트 하려면 명령 프롬프트에서 다음 명령을 입력 한 후 ENTER 키를 누릅니다.  

   ```
   nltest /dsgetdc:nonroot domain name /KDC /Force  
   ```

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)  
