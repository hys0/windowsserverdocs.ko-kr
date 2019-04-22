---
title: AD 포리스트 복구-GC를 추가 합니다.
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: 156a4a64d9c3bb8261bd603b72ae11b81ff1d152
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825634"
---
# <a name="ad-forest-recovery---adding-the-gc"></a>AD 포리스트 복구-GC를 추가 합니다.

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

글로벌 카탈로그 DC를 추가 하려면 다음 절차를 따르십시오.  
  
## <a name="to-add-the-global-catalog"></a>글로벌 카탈로그를 추가 하려면  
  
1. 클릭 **시작**, 가리킨 **모든 프로그램**를 가리킨 **관리 도구**를 클릭 하 고 **Active Directory 사이트 및 서비스**.  
2. 콘솔 트리에서 확장 된 **사이트** 컨테이너 및 대상 서버를 포함 하는 적절 한 사이트를 선택 합니다.  
3. 확장을 **서버** 컨테이너는 글로벌 카탈로그를 추가 하려는 DC에 대 한 서버 개체를 차례로 확장 합니다.  
4. 마우스 오른쪽 단추로 클릭 **NTDS 설정**를 클릭 하 고 **속성**합니다.  
5. 선택 된 **글로벌 카탈로그** 확인란 합니다.  
![GC를 추가 합니다.](media/AD-Forest-Recovery-Add-GC/addgc1.png)

## <a name="to-add-the-global-catalog-using-repadmin"></a>Repadmin을 사용 하 여 글로벌 카탈로그를 추가 하려면  

- 관리자 권한 명령 프롬프트를 열고, 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  

   ```  
   repadmin.exe /options DC_NAME +IS_GC  
   ```  

다음은 루트 도메인의 dc는 글로벌 카탈로그를 추가 하는 과정을 가속화 하는 방법입니다.  

- 이상적으로 루트 도메인의 DC 복제 파트너 복원 된 Dc의 루트가 아닌 도메인에 있어야 합니다. 그렇다면 지식 일관성 검사기 (KCC)가 해당 만들어졌는지 확인 **repsFrom** 루트 DC에서에서 파티션을 확인 하 고 원본 DC에 대 한 개체입니다. 실행 하 여이 확인할 수 있습니다 합니다 **repadmin /showreps /v** 명령입니다. 

- 없는 경우 없습니다 **repsFrom** 개체 생성, 구성 파티션에 대해이 개체를 만듭니다. 이러한 방식으로 루트 도메인의 DC 루트가 아닌 도메인의 Dc 삭제 된 확인할 수 있습니다. 다음 명령을 사용 하 여이 수행할 수 있습니다.  

   ```
   repadmin /add ConfigurationNamingContext DestinationDomainController SourceDomainControllerCNAME  
   ```

   ```
   repadmin /options DSA -Disable_NTDSCONN_XLATE  
   ```

   형식은 합니다 *SourceDomainControllerCNAME* 는:  

   ```
  
   sourceDCGuid._msdcs.root domain  
   ```

   Repadmin 예를 들어 contoso.com 도메인의 구성 파티션 수에 대 한 명령을 추가 합니다.  

   ```
   repadmin /add cn=configuration,DC=contoso,DC=com DC01 937ef930-7356-43c8-88dc-8baaaa781cf6._msdcs.dDSP17A22.contoso.com  
   ```

- 경우는 **repsFrom** 개체가, 다음과 같은 루트 도메인에 루트가 아닌 도메인의 DC는 DC를 동기화 하려고 합니다.  

   ```
   Repadmin /sync DomainNamingContext DestinationDomainController SourceDomainControllerGUID  
   ```

   여기서 *DestinationDomainController* 루트 도메인의 dc와 *SourceDomainController* 루트가 아닌 도메인에 복원 된 dc입니다. 

- 루트 도메인의 DNS 서버를 원본 DC에 대 한 별칭 (CNAME) 리소스 레코드가 있어야 합니다. 부모 DNS 영역에 위임 리소스 레코드 (NS (이름 서버) 및 호스트 (A) 리소스 레코드) 올바른 Dc (백업에서 복원 된 Dc)에 대 한 자식 영역에서 확인 합니다. 
- 루트 도메인의 DC 루트가 아닌 도메인에 올바른 키 배포 센터 (KDC)를 연결 하 고 있는지 확인 합니다. 이 명령 프롬프트에서 테스트 하려면 다음 명령을 입력 하 고 ENTER를 누릅니다.  

   ```
   nltest /dsgetdc:nonroot domain name /KDC /Force  
   ```

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)  
