---
ms.assetid: e1f2ce2d-b24f-4ccd-8add-9e69419fc6c1
title: "기본 웹 서버 인증 인증서 가져오기"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 7bc890c744de5cd86d4e8b0418e75512518f656c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="import-a-server-authentication-certificate-to-the-default-web-site"></a>기본 웹 서버 인증 인증서 가져오기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

인증 기관에서 서버 인증 인증서 확인 한 후 \(CA\)를 수동으로 설치 해야 인증서 해당 federation 서버 또는 federation 서버 프록시 서버 발전소의 각에 대 한 기본 웹 사이트에서 합니다.  
  
웹 서버에 대 한 적절 한 웹 사이트 또는 연결 된 응용 프로그램이 있는 가상 디렉터리 서버 인증 인증서를 수동으로 설치 해야 합니다.  
  
농장을 설정 하는 경우 사용할 동일 하 게이 절차를 수행 해야-동일한 설정을 사용 하 여 등 각 사용자 농장의 서버에 있습니다.  
  
> [!NOTE]  
> snap\ AD FS 관리 서버 인증 인증서 federation 서버에 대 한 서비스 통신 인증서도 참조합니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-import-a-server-authentication-certificate-to-the-default-web-site"></a>서버 인증 인증서를 기본 웹 사이트를 가져오려면  
  
1.  에 **시작** 화면에서 입력**인터넷 정보 서비스 \(IIS\) 관리자**, ENTER 키를 누릅니다.  
  
2.  콘솔 트리에서 클릭 **ComputerName**합니다.  
  
3.  가운데 창에서 double\ 클릭 **서버 인증서**합니다.  
  
4.  에 **작업** 창 클릭 **가져오기**합니다.  
  
5.  에 **인증서 가져오기** 대화 상자를 클릭는 **...** 단추입니다.  
  
6.  Pfx 인증서 파일의 위치를 강조 표시 하 고 클릭 한 다음 **열기**합니다.  
  
7.  인증서에 대 한 암호를 입력 한 다음 **확인**합니다.  
  
## <a name="additional-references"></a>추가 참조  
[Federation 서버 설정 검사:](Checklist--Setting-Up-a-Federation-Server.md)  
  
[검사 목록: Federation 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Federation 서버의 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)  
  
[인증서 Federation 서버 프록시 요구 사항](https://technet.microsoft.com/library/dd807054.aspx)  
   
  

