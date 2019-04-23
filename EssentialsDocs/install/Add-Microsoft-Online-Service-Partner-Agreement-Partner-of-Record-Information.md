---
title: Microsoft 온라인 서비스 파트너 계약 공식 파트너 정보 추가
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833044"
---
# <a name="add-microsoft-online-service-partner-agreement-partner-of-record-information"></a>Microsoft 온라인 서비스 파트너 계약 공식 파트너 정보 추가

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_3rdLevelDomanNames"></a>   
 Office 365에 대 한 Microsoft 온라인 서비스 파트너 계약 (MOSPA) 파트너 라면 올바르게 구독 요청은 Office 365 Integration Module을 통해 Windows Server Essentials에서 시작 하는 경우 보정 됩니다 확인 하려면 만들기를 사용자 레코드의 파트너 식별 (POR ID)를 포함 하는 레지스트리 키입니다. 다음 정보가 Office 365 등록 URL을 통해 서비스 공급자에게 전달됩니다.  
  
-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO  
  
-   형식 = 문자열 값  
  
-   키 이름 = Partner  
  
-   값 = xxxxx, 여기서 xxxxx는 POR ID  
  
#### <a name="to-add-the-por-id-key-to-the-registry"></a>POR ID 키를 레지스트리에 추가하려면  
  
1.  참조 컴퓨터에서 **시작**을 클릭하고 **regedit**를 입력한 다음 Enter 키를 누릅니다.  
  
2.  왼쪽 창에서 **HKEY_LOCAL_MACHINE**, **소프트웨어**, **Microsoft**, **Windows Server**를 차례로 확장합니다.  
  
3.  **Windows Server**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **키**를 클릭합니다.  
  
4.  키 이름에 **MSO**를 입력합니다.  
  
5.  방금 만든 키를 마우스 오른쪽 단추로 클릭한 다음 **문자열 값**을 클릭합니다.  
  
6.  문자열 이름에 **Partner**를 입력한 다음 Enter 키를 누릅니다.  
  
7.  오른쪽 창에서 새 **Partner** 문자열을 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다.  
  
8.  **값 데이터** 입력란에 POR ID를 입력하고 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  

 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)

 [만들기 및 이미지를 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](../install/Additional-Customizations.md)   
 [배포용 이미지 준비](../install/Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](../install/Testing-the-Customer-Experience.md)

