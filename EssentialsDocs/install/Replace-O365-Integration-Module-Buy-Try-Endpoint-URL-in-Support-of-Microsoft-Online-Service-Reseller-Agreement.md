---
title: "Microsoft 온라인 서비스 재판매인 계약 지원 하기 위해 O365 통합 모듈 구입 Try 끝점 URL 바꾸기"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9860a6b9-baea-4bf0-9a9f-6f1a288f996e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: b690cedd2f692cc6d11af6e05dd0cd4b4ea5a1d6
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="replace-o365-integration-module-buy-try-endpoint-url-in-support-of-microsoft-online-service-reseller-agreement"></a>Microsoft 온라인 서비스 재판매인 계약 지원 하기 위해 O365 통합 모듈 구입 Try 끝점 URL 바꾸기

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

##  <a name="BKMK_O365"></a>   
 포털을 통해 고객 등록 거래를 처리 하기 위해 Microsoft 온라인 서비스 재판매인 계약 (MOSRA) 파트너는 Windows Server Essentials Office 365 통합 모듈에서 사용 되는 endpoint Url 교체 해야 합니다.  
  
 통합 모듈 다음 네 가지 endpoint Url을 사용합니다.  
  
1.  Office 365 엔터프라이즈 구독 구매 끝점 합니다.  
  
    -   Server\MSO\  
  
    -   입력 등록이 SZ =  
  
    -   키 이름 MOSRASTDBUY =  
  
    -   값 = *xxxxx*, 여기서 xxxxx 엔터프라이즈 구독 구매 URL이 합니다. 예를 들어, 가치 http://syndicatepartner.office365.com/enterprisebuy.html =  
  
2.  Office 365 엔터프라이즈 구독 평가판 끝점 합니다.  
  
    -   Server\MSO\  
  
    -   입력 등록이 SZ =  
  
    -   키 이름 MOSRASTDTRY =  
  
    -   값 = *xxxxx*, 여기서 xxxxx 엔터프라이즈 구독 구매 URL이 합니다. 예를 들어, 가치 http://syndicatepartner.office365.com/enterprisetry.html =  
  
3.  Office 365 소규모 기업 Premium 구독 구매 끝점 합니다.  
  
    -   Server\MSO\  
  
    -   입력 등록이 SZ =  
  
    -   키 이름 MOSRALITEBUY =  
  
    -   값 = *xxxxx*, 여기서 xxxxx 엔터프라이즈 구독 구매 URL이 합니다. 예를 들어, 가치 http://syndicatepartner.office365.com/smallbizbuy.html =  
  
4.  Office 365 소규모 기업 Premium 구독 평가판 끝점 합니다.  
  
    -   Server\MSO\  
  
    -   입력 등록이 SZ =  
  
    -   키 이름 MOSRALITETRY =  
  
    -   값 = *xxxxx*, 여기서 xxxxx 엔터프라이즈 구독 구매 URL이 합니다. 예를 들어, 가치 http://syndicatepartner.office365.com/smallbiztry.html =  
  
#### <a name="to-add-an-endpoint-url-key-to-the-registry"></a>Endpoint URL 키 레지스트리를 추가 하려면  
  
1.  참조 컴퓨터에서 클릭 **시작**, 입력 **regedit**, ENTER 키를 누릅니다.  
  
2.  왼쪽된 창에서 확장 **HKEY_LOCAL_MACHINE**, 확장 **소프트웨어**, 확장 **Microsoft**, 확장 **Windows Server**를 확장 한 다음 **MSO**합니다.  
  
3.  MSO가 없는 경우 마우스 오른쪽 단추로 클릭 **Windows Server**를 가리킨 **새로**, 클릭 **키**, 한 다음 입력 **MSO** 키의 이름에 대 한 합니다.  
  
4.  MSO를 마우스 오른쪽 단추로 클릭 한 다음 한 **문자열 값**합니다. 하나는 문자열의 이름에 대 한 다음 끝점 문자열 이름을 입력 합니다.  
  
    -   MOSRASTDBUY  
  
    -   MOSRASTDTRY  
  
    -   MOSRALITEBUY  
  
    -   MOSRALITETRY  
  
5.  새 문자열 오른쪽 창에서 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **수정**합니다.  
  
6.  에 새로운 사용자 끝점 URL 입력는 **값 데이터** 텍스트 상자와 클릭 한 다음 **확인**합니다.  
  
7.  4 단계에 나열 된 각 문자열 이름에 대해 4 6 단계를 반복 합니다.  
  
## <a name="see-also"></a>참조 하십시오  

 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트](Testing-the-Customer-Experience.md) [만들기 및 이미지를 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](../install/Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](../install/Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](../install/Testing-the-Customer-Experience.md)

