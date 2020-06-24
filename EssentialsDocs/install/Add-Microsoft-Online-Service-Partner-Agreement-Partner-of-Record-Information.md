---
title: Microsoft 온라인 서비스 파트너 계약 공식 파트너 정보 추가
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 9bd191d6-ecc5-4230-a88e-f3fc281cb956
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 8b397a8fd2047c1a6fcaf5de2f5e1af167f1029f
ms.sourcegitcommit: 6d6a0225b1f83b71fcb494b94d666cd5e54c7566
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85267454"
---
# <a name="add-microsoft-online-service-partner-agreement-partner-of-record-information"></a>Microsoft 온라인 서비스 파트너 계약 공식 파트너 정보 추가

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_3rdLevelDomanNames"></a>   
 Office 365에 대 한 MOSPA (Microsoft 온라인 서비스 파트너 계약) 파트너인 경우 Office 365 통합 모듈을 통해 Windows Server Essentials에서 구독 요청이 발생 했을 때 올바르게 보정 되도록 하려면 POR (레코드 파트너) id가 포함 된 레지스트리 키를 만들어야 합니다. 다음 정보가 Office 365 등록 URL을 통해 서비스 공급자에게 전달됩니다.  
  
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
  
## <a name="see-also"></a>참고 항목  

 [이미지 만들기 및 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포를 위한 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)

