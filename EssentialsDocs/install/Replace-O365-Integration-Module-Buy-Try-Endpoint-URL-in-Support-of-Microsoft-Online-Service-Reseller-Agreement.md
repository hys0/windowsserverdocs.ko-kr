---
title: Microsoft 온라인 서비스 재판매인 계약을 지원하기 위해 O365 통합 모듈 구입-평가판 끝점 URL 바꾸기
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9860a6b9-baea-4bf0-9a9f-6f1a288f996e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 11e18d7d61edb0a618fb71791f77c4df84c9d708
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311541"
---
# <a name="replace-o365-integration-module-buy-try-endpoint-url-in-support-of-microsoft-online-service-reseller-agreement"></a>Microsoft 온라인 서비스 재판매인 계약을 지원하기 위해 O365 통합 모듈 구입-평가판 끝점 URL 바꾸기

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_O365"></a>   
 Microsoft 온라인 서비스 재판매인 계약 (MOSRA) 파트너인 경우 포털을 통해 고객 등록 트랜잭션이 처리 되도록 하려면 Windows Server Essentials Office 365 통합 모듈에서 사용 되는 끝점 Url을 바꾸어야 합니다.  
  
 통합 모듈에서는 다음 4개의 엔드포인트 URL을 사용합니다.  
  
1.  Office 365 Enterprise 정기 가입 구입 엔드포인트입니다.  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   유형 = REG-SZ  
  
    -   키 이름 = MOSRASTDBUY  
  
    -   값 = *xxxxx*, 여기서 xxxxx는 기업 정기 가입 구입 URL입니다. 예: 값 = http://syndicatepartner.office365.com/enterprisebuy.html  
  
2.  Office 365 Enterprise 정기 가입 평가판 엔드포인트입니다.  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   유형 = REG-SZ  
  
    -   키 이름 = MOSRASTDTRY  
  
    -   값 = *xxxxx*, 여기서 xxxxx는 기업 정기 가입 구입 URL입니다. 예: 값 = http://syndicatepartner.office365.com/enterprisetry.html  
  
3.  Office 365 Small Business Premium subscription 구매 끝점입니다.  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   유형 = REG-SZ  
  
    -   키 이름 = MOSRALITEBUY  
  
    -   값 = *xxxxx*, 여기서 xxxxx는 기업 정기 가입 구입 URL입니다. 예: 값 = http://syndicatepartner.office365.com/smallbizbuy.html  
  
4.  Office 365 Small Business Premium 정기 가입 평가판 끝점입니다.  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   유형 = REG-SZ  
  
    -   키 이름 = MOSRALITETRY  
  
    -   값 = *xxxxx*, 여기서 xxxxx는 기업 정기 가입 구입 URL입니다. 예: 값 = http://syndicatepartner.office365.com/smallbiztry.html  
  
#### <a name="to-add-an-endpoint-url-key-to-the-registry"></a>레지스트리에 엔드포인트 URL 키를 추가하려면  
  
1.  참조 컴퓨터에서 **시작**을 클릭하고 **regedit**를 입력한 다음 Enter 키를 누릅니다.  
  
2.  왼쪽 창에서 **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft**, **Windows Server**, **MSO**를 차례로 확장합니다.  
  
3.  MSO가 없으면 **Windows Server**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **키**를 클릭하고 키 이름으로 **MSO**를 입력합니다.  
  
4.  MSO를 마우스 오른쪽 단추로 클릭한 다음 **문자열 값**을 클릭합니다. 문자열 이름으로 다음 엔드포인트 문자열 이름 중 하나를 입력합니다.  
  
    -   MOSRASTDBUY  
  
    -   MOSRASTDTRY  
  
    -   MOSRALITEBUY  
  
    -   MOSRALITETRY  
  
5.  오른쪽 창에서 새 문자열을 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다.  
  
6.  **값 데이터** 입력란에 새 엔드포인트 URL을 입력한 다음 **확인**을 클릭합니다.  
  
7.  4단계에 나열된 각 문자열 이름에 대해 4-6단계를 반복합니다.  
  
## <a name="see-also"></a>관련 항목  

 [이미지  만들기 및 사용자 지정](Creating-and-Customizing-the-Image.md)  
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포할 이미지를 준비 하는 중](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md) [이미지 만들기 및 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](../install/Additional-Customizations.md)   
 [배포할 이미지를 준비 하는 중](../install/Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](../install/Testing-the-Customer-Experience.md)

