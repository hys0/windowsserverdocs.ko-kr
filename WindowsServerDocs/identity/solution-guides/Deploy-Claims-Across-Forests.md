---
ms.assetid: ceb9ce18-5a94-4166-9edd-2685b81fc15f
title: "숲 클레임 배포"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 7d78258d8f1db9889b6d2db8c497780940ed35a1
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="deploy-claims-across-forests"></a>숲 클레임 배포

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows Server 2012에서 클레임 형식은 관련 된 개체에 대 한 설정 됩니다. 클레임 형식은 숲 Active Directory에 따라 정의 됩니다. 보안 사용자 신뢰할 수 있는 숲 속의 리소스에 액세스 하는 보안 경계 통과 해야 할 수 있는 경우도 있습니다. Windows Server 2012에서 간 숲 클레임 변환 클레임은 인식 하 고 신뢰 하 고 신뢰할 수 있는 숲에서 사용할 수 있도록 숲을 탐색 하는 송신와 수신 청구 변환 수 있습니다. 클레임 변환에 대 한 실제 시나리오는 다음과 같습니다.  
  
-   숲 신뢰 하는으로 사용할 수 클레임 변환 권한이 상승 로부터 보호 받는 클레임 특정 값으로를 필터링 하 여.  
  
    신뢰 하는 숲 신뢰할 수 있는 숲 지원 하거나 클레임 실행 하지 않는 경우 출시 신뢰 경계를 통해 사용자에 대 한 주장도 실행할 수 있습니다.  
  
-   신뢰할 수 있는 숲 특정 클레임 유형 및을 신뢰 숲 속의 특정 한 값으로 클레임 하지 않으려면 청구 변환을 사용할 수 있습니다.  
  
-   다른 지도로 변환 클레임 신뢰 하 고 신뢰할 수 있는 숲 간에 유형 클레임을 사용할 수 있습니다. 이 generalize 클레임 유형, 클레임 값 또는 둘 다를 사용할 수 있습니다. 이 않고도 수집 클레임은 사용 하려면 먼저 숲 간에 데이터가 필요 합니다. 신뢰 하 고 신뢰할 수 있는 숲 간에 클레임이 IT 비용 줄일 수 있습니다.  
  
## <a name="claim-transformation-rules"></a>변환 규칙 주장  
두 부분으로 구성 변환 규칙 언어 구문 구분 단일 규칙:는 일련의 조건이 문 및 문제 문의 합니다. 각 조건 문의 두 가지 하위: 클레임 식별자와 상태입니다. 문제 문을 키워드, 구분을 및 문제 식을 포함 되어 있습니다. 조건 문으로 클레임 식별자 변수와 일치 입력된 클레임 나타내는으로 필요에 따라 시작 합니다. 식 상태를 확인합니다. 입력된 클레임 상태와 일치 하지 않는 경우 다음 변환 엔진 문제 문 무시 하 고 평가 변환 규칙에 대 한 다음 입력된 청구 합니다. 모든 조건이 입력된 클레임와 일치 하는 경우 문제 정책을 처리 합니다.  
  
클레임은 규칙 언어에 대 한 자세한 정보를 참조 하세요. [클레임 변환 규칙 언어](Claims-Transformation-Rules-Language.md)합니다.  
  
## <a name="linking-claim-transformation-policies-to-forests"></a>클레임은 변환 정책을 숲 연결  
클레임 변환 정책 설정에 포함 된 두 가지 구성 요소는: 주장 변환 정책 개체와 변환 링크를 클릭 합니다. 정책 개체를 숲 속의 구성 명명 컨텍스트에 거주 하 고 클레임에 대 한 지도 제작 정보를 포함 합니다. 링크를 신뢰 하는 지정 하 고 신뢰할 수 있는 숲 매핑에 적용 됩니다.  
  
숲 인지 신뢰 또는 신뢰할 수 있는 숲 변환 정책 개체 연결에 대 한 기본 이므로 이해 하는 합니다. 예를 들어 신뢰할 수 있는 숲 사용자 계정에 액세스 해야 하는 포함 된 숲이입니다. 신뢰 숲은 사용자에 대 한 액세스를 제공 하려는 리소스를 포함 하 여 숲입니다. 클레임 보안 액세스 해야 하는 사용자와 같은 방향으로 이동 합니다. 예를 들어 일 방향 신뢰 contoso.com 숲에서 adatum.com 숲을 경우 클레임 adatum.com에서 contoso.com adatum.com에서 사용자가 contoso.com 리소스에 액세스할 수 있는로 이동 합니다.  
  
기본적으로 신뢰할 수 있는 숲 모든 보내는 클레임을 통과 하 고 신뢰 숲 수신 하는 모든 들어오는 클레임 삭제 합니다.  
  
## <a name="in-this-scenario"></a>이 경우  
다음 지침을이 시나리오에 대해 사용할 수 있습니다.  
  
-   [숲 & #40; 데모 단계 & #41; 클레임 배포](Deploy-Claims-Across-Forests--Demonstration-Steps-.md)  
  
-   [클레임 변환 규칙 언어](Claims-Transformation-Rules-Language.md)  
  
## <a name="BKMK_NEW"></a>역할 및이 시나리오에 포함 된 기능  
다음 표에서 역할 및이 시나리오에 포함 된 기능을 나열 하 고 지 원하는 방식에 대해 설명 합니다.  
  
|역할/기능|이 시나리오를 지 원하는 방법을|  
|-----------------|---------------------------------|  
|Active Directory Domain Services|이 경우 두 가지 Active Directory 숲 양방향 보안으로 설정 해야 합니다. 두 숲 클레임 가지고합니다. 또한 리소스 있는 신뢰 숲 속의 중앙 액세스 정책을 설정 합니다.|  
|파일 및 저장소 서비스 역할|이 경우 데이터 분류 파일 서버에 리소스에 적용 됩니다. 사용자 액세스 권한을 부여 하려는 폴더에 있는 중앙 액세스 정책이 적용 됩니다. 변환, 후 클레임 사용자 폴더의 파일 서버에 적용 되는 중앙 액세스 정책에 따라 리소스에 대 한 액세스 권한을 부여 합니다.|  
  


