---
title: "Microsoft 온라인 서비스 파트너 계약 기록 파트너 정보 추가"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9bd191d6-ecc5-4230-a88e-f3fc281cb956
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 39ce43228cd7392bcc86de4a410c52676ce15047
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="add-microsoft-online-service-partner-agreement-partner-of-record-information"></a>Microsoft 온라인 서비스 파트너 계약 기록 파트너 정보 추가

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

##  <a name="BKMK_3rdLevelDomanNames"></a>   
 Office 365에 대 한 Microsoft 온라인 서비스 파트너 계약 (MOSPA) 파트너 인 경우 구독 요청은 Office 365 통합 모듈을 통해 Windows Server Essentials에서 생성 된 때 보정 잘못 되어 있는지 확인 하려면 기록 파트너 식별 (POR ID)에 포함 된 레지스트리 키를 만들려면 합니다. 다음 정보를 읽고 Office 365 등록 Url 서비스 공급자에 게 전달 됩니다.  
  
-   Server\MSO  
  
-   타이핑 = 문자열 값  
  
-   키 이름 파트너 =  
  
-   값 xxxxx POR ID가 xxxxx =  
  
#### <a name="to-add-the-por-id-key-to-the-registry"></a>POR ID 키 레지스트리를 추가 하려면  
  
1.  참조 컴퓨터에서 클릭 **시작**, 입력 **regedit**, ENTER 키를 누릅니다.  
  
2.  왼쪽된 창에서 확장 **HKEY_LOCAL_MACHINE**, 확장 **소프트웨어**, 확장 **Microsoft**를 확장 한 다음 **Windows Server**합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **Windows Server**를 가리킨 **새로**을 차례로 클릭 하 고 **키**합니다.  
  
4.  입력 **MSO** 키의 이름입니다.  
  
5.  키 방금 만든 마우스 단추로 클릭 한 다음 **문자열 값**합니다.  
  
6.  입력 **파트너** 이름을 문자열을 하 고 ENTER 키를 누릅니다.  
  
7.  새을 마우스 오른쪽 단추로 클릭 **파트너** 오른쪽 창에는 문자열와 클릭 한 다음 **수정**합니다.  
  
8.  입력에 POR ID는 **값 데이터** 텍스트 상자와 클릭 한 다음 **확인**합니다.  
  
## <a name="see-also"></a>참조 하십시오  

 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)

 [만들기 및 이미지를 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](../install/Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](../install/Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](../install/Testing-the-Customer-Experience.md)

