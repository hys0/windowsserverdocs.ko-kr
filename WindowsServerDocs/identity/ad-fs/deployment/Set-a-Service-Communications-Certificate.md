---
ms.assetid: 638c89bd-87e6-484b-9d2e-8ae2a74227e5
title: "서비스 통신 인증서 설정"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 0d630372d82cf1519da82397a9c90d6a28903ed0
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="set-a-service-communications-certificate"></a>서비스 통신 인증서 설정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Federation 서버 Active Directory Federation Services \(AD FS\)의 웹 서비스 트래픽 또는 federation 서버 프록시 웹 하는 클라이언트와 안전한 주소 \(SSL\) 통신에 대 한 보안 서비스 통신 인증서를 사용 합니다. 인터넷 정보 서비스 \(IIS\) SSL 인증서도 federation 서버를 사용 하 여 동일한 인증서입니다.  
  
서비스 통신 인증서에 snap\ AD FS 관리를 변경 하려면 다음 절차에 사용할 수 있습니다.  
  
> [!NOTE]  
> snap\ AD FS 관리 서버 인증 인증서 federation 서버에 대 한 서비스 통신 인증서도 참조합니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) \ (http:///\/ go.microsoft.com\/fwlink\/있나요? LinkId\ 83477\ =).   
  
### <a name="to-set-a-service-communications-certificate"></a>서비스 통신 인증서를 설정 하려면  
  
1.  에 **시작** 화면에서 입력**AD FS 관리**, ENTER 키를 누릅니다.  
  
2.  콘솔 트리에서 double\ 클릭 **서비스**을 차례로 클릭 하 고 **인증서**합니다.  
  
3.  에 **작업** 창 클릭는 **서비스 통신 인증서 설정** 링크입니다.  
  
4.  에 **서비스 통신 인증서를 선택** 대화 상자에 설정 된 서비스 통신 인증서 인증서 파일을 선택한 다음 원하는 인증서 파일을 찾아 **열기**합니다.  
  
## <a name="additional-references"></a>추가 참조  
[Federation 서버 설정 검사:](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Federation 서버의 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)  
  

