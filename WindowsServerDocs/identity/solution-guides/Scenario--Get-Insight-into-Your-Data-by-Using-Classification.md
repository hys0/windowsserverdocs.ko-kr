---
ms.assetid: ad3f0480-99f7-428a-ab33-6d165a440840
title: "시나리오 Get 통찰력 분류를 사용 하 여 데이터"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 2e5248b5fd5e20b7436de9f796367c018d8ef16e
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="scenario-get-insight-into-your-data-by-using-classification"></a>시나리오: 분류를 사용 하 여 사용자의 데이터에 대 한 정보 가져오기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

데이터와 저장소 리소스에 의존 계속 대부분 조직에 대 한 중요의 증가 하 합니다. IT 관리자 과제가 점점 더 복잡 저장소 인프라 감독, 되도록 책임을 동시에 담당 하는 동안 해당 총 소유의 비용-적절 한 수준의 유지 됩니다. 도 볼륨 약 데이터의 사용 가능 여부는 리소스 저장소 관리 회사 정책이 적용 및 저장소 효율적인 활용도 및 위험을 완화 하 준수 수 있도록 소모 되는 방식을 파악에 대 한 이기도 합니다. 파일 분류 인프라 보다 효율적으로 사용자의 데이터를 관리할 수 있도록 분류 프로세스 자동화 하 여 사용자의 데이터에 대 한 정보를 제공 합니다. 다음 분류 방법 파일 분류 인프라를 사용할 수 있는: 수동 프로그래밍 방식으로, 및 자동 합니다. 이 항목에서는 자동 파일 분류에 집중합니다.  
  
## <a name="BKMK_OVER"></a>시나리오 설명  
파일 분류 인프라에 자동으로 파일을 검색 하 고 파일의 내용에 따라 분류 분류 규칙을 사용 합니다. 분류 속성 이러한 정의 파일 서버에서 조직에서 공유할 수 있도록 Active Directory에 중앙 집중식으로 정의 됩니다. 표준 문자열 또는 문자열로 패턴 (일반 식)와 일치 하는 파일을 검색 하는 분류 규칙 만들 수 있습니다. 파일에서 구성 된 분류 매개 발견 되 면 해당 파일에 분류 규칙 구성 된 대로 분류 됩니다. 분류 규칙의 몇 가지 예는 다음과 같습니다.  
  
-   업무에 큰 영향을 하는 것으로 "Contoso 기밀" 문자열을 포함 하는 모든 파일을 분류  
  
-   분류 개인 식별 정보를 가진 것으로 최소 10 사회 보장 번호가 포함 된 모든 파일  
  
파일을을 분류 되는 경우 사용할 수 있습니다 관리 작업 작업을 수행 하는 모든 파일에는 특정 방식으로 분류 됩니다. 파일 관리 작업에서 작업 파일을 만료 하 고 (와 같은 웹 서비스에 정보를 게시) 사용자 지정 작업을 실행 하 여 파일을와 관련 된 권리를 보호 포함 됩니다.  
  
찾을 수 계획에 자동으로 파일 분류 구성에 대 한 정보 [자동 파일 분류 계획](assetId:///e3c3bb4b-3034-42b7-b391-8ef5f5851955)합니다.  
  
자동으로 파일에서 분류 하는 방법에 대 한 단계를 찾을 수 [자동 파일 분류 배포 & #40; 데모 단계 & #41;](Deploy-Automatic-File-Classification--Demonstration-Steps-.md).  
  
## <a name="in-this-scenario"></a>이 경우  
이 시나리오는 동적 액세스 제어 시나리오의 일부입니다. 동적 액세스 제어 대 한 자세한 내용은 참조 하십시오.  
  
-   [동적 액세스 제어: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="BKMK_APP"></a>실용적인 응용 프로그램  
Windows Server 2012에서 파일 분류 인프라 비즈니스 데이터 소유자가 분류 쉽고 레이블을 데이터를 사용 하 여 동적 액세스 제어에 적용 됩니다. 분류 정보 중앙 액세스 정책에 저장 된 데이터 클래스 비즈니스에 중요 한에 대 한 액세스 정책을 정의 수 있습니다.  
  
## <a name="BKMK_NEW"></a>이 경우에 포함 된 기능  
다음 표에서이 시나리오에 포함 된 기능을 설명 하 고 지 원하는 방법을 설명 합니다.  
  
|기능|이 시나리오를 지 원하는 방법을|  
|-----------|---------------------------------|  
|[파일 서버 리소스 관리자 개요](https://technet.microsoft.com/library/hh831701.aspx)|파일 분류 인프라 파일 서버 리소스 관리자에 포함 된 기능입니다.|  
|[파일 및 저장소 서비스 개요](https://technet.microsoft.com/library/hh831487.aspx)|파일 서버 리소스 관리자 파일 서비스 거부에 포함 된 기능입니다.|  
  


