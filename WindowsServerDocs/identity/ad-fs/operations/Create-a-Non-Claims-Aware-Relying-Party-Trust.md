---
ms.assetid: 7b7ae389-5032-44f7-9c0a-94398c3e4d88
title: "비 클레임 인식 신뢰 파티 신뢰를 만들기"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f46675ff4c471af743fd8782c1e3036e7c546256
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-non-claims-aware-relying-party-trust"></a>클레임을 인식 의존 파티 신뢰 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

AD FS 관리 snap\에서, non\ claims\-인식 파티 신뢰 의존 federation 서비스 간의 단일 web\ 기반 응용 프로그램이 claims\ 인식 하지 않는 웹 응용 프로그램 프록시 통해 액세스 하 고 신뢰를 표시 하기 위해 만든 개체 됩니다.  
  
Non\ claims\ 인식 신뢰 파티 신뢰 신뢰 파티 신뢰를 통해 웹 응용 프로그램 프록시 액세스할 때 식별자, 이름, 및 인증과 규칙 구성 된 신뢰 파티 신뢰가입니다. 청구 자제는 이러한 web\ 기반 응용 프로그램이 즉, 이러한 통합 Windows Authentication\ 기반 응용 프로그램을 할 수 있습니다 인증 규칙이 적용 외부 웹 응용 프로그램 프록시 통해 회사 네트워크에 대 한 액세스 되 면 클레임 기준 액세스 하는 합니다.  
  
Snap\에서 AD FS 관리를 사용 하 여는 새로운 non\ claims\ 인식 신뢰 파티 신뢰를 추가 하려면 다음 절차를 수행 합니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
##<a name="to-create-a-non-claims-aware-relying-party-trust-manually"></a>수동으로 비 클레임 인식 의존 파티 신뢰를 만들려면 
1. 서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  아래에서 **작업**, 클릭 **의존 파티 신뢰 추가**합니다.  
![당사자에](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  에 **시작** 페이지에서 선택 **인식 비 클레임** 클릭 **시작**합니다.  
![당사자에](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon1.PNG) 
  
4.  에 **표시 이름 지정** 페이지에서에 이름을 입력 **표시 이름**, **노트** 이 신뢰 파티 보안에 대 한 설명을 입력 한 다음 **다음**합니다.  
![당사자에](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon2.PNG)

5. 에 **구성 식별자** 페이지이 당사자에 대 한 식별자 하나 또는 여러 개의 지정를 클릭 **추가** 목록에 추가를 클릭 한 다음 **다음**합니다.  
![당사자에](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon3.PNG)

6.  에 **액세스 제어 정책 선택** 정책을 선택 하 고 클릭 **다음**합니다.  액세스 제어 정책에 대 한 자세한 내용은 참조 [adfs에서 액세스 제어 정책을](Access-Control-Policies-in-AD-FS.md)합니다. 
![당사자에](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon4.PNG)

7. 에 **추가 보안 준비가** 페이지를 설정을 검토 하 고, 클릭 한 다음 **다음** 당사자에 저장 하려면 정보를 신뢰 합니다.  
   ![당사자에](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon5.PNG) 

8. 에 **완료** 페이지, 클릭 **닫기**합니다. 이 작업은 자동으로 표시는 **편집 클레임 규칙** 대화 상자가 합니다.  
![당사자에](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon6.PNG)  
  
## <a name="see-also"></a>참조 하십시오  
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md) 
