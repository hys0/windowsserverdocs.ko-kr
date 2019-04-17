---
ms.assetid: c50ecc6a-9504-4b4a-816f-e762dcf3a95e
title: "설치 Federation 서비스 프록시 역할 서비스"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: aea1ef335604aa18f0b1a1c22ef13f6fee1601b3
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="install-the-federation-service-proxy-role-service"></a>설치 Federation 서비스 프록시 역할 서비스

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

필수 응용 프로그램 및 인증서도 컴퓨터를 구성 Active Directory Federation Services \(AD FS\)의 Federation 서비스 프록시 역할 서비스 설치할 준비가 되었습니다. 다음 절차 설치 Federation 서비스 프록시 역할 서비스를 사용할 수 있습니다. Federation 서비스 프록시 역할 서비스를 컴퓨터에 설치 하면 컴퓨터 해당 federation 프록시 서버 됩니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-install-the-federation-service-proxy-role-service"></a>Federation 서비스 프록시 역할 서비스를 설치 하려면  
  
1.  에 **시작** 화면에서 입력**서버 관리자**, ENTER 키를 누릅니다.  
  
2.  클릭 **관리**을 차례로 클릭 하 고 **역할 추가 및 기능** 역할 추가 및 기능 마법사를 시작 합니다.  
  
3.  에 **시작 하기 전에** 페이지, 클릭 **다음**합니다.  
  
4.  에 **설치 유형을 선택** 페이지, 클릭 **Role\ 또는 Feature\ 기반 설치**를 클릭 하 고 **다음**합니다.  
  
5.  에 **선택 대상 서버** 페이지, 클릭 **서버 풀에서 서버를 선택**, 대상 컴퓨터를 강조 표시 하 고 클릭 한 다음 확인 **다음**합니다.  
  
6.  에 **서버 역할 선택** 페이지, 클릭 **Active Directory Federation Services**, 다음을 클릭 합니다.  
  
    > [!NOTE]  
    > .NET Framework 또는 Windows 프로세스 정품 인증 서비스에 대 한 추가 기능 설치 하 라는 메시지가 나타나면 클릭 **기능 추가** 설치할 수 있습니다.  
  
7.  에 **기능 선택** 페이지에서 기능을 설정 하 고 클릭 한 다음 확인 **다음**합니다.  
  
8.  에 **Active Directory Federation 서비스 \(AD FS\)** 페이지, 클릭 **다음**합니다.  
  
9. 에 **역할 서비스를 선택** 페이지 선택는 **Federation 서비스 프록시** 확인란을 선택한 다음 클릭 **다음**합니다.  
  
10. 에 **웹 서버 역할 \(IIS\)** 페이지, 클릭 **다음**합니다.  
  
11. 에 **역할 서비스 선택** 페이지, 클릭 **다음**합니다.  
  
12. 정보를 확인 한 후는 **설치 선택을 확인** 페이지를 선택 하 고는 **필요한 경우 자동으로 목적지 서버를 다시 시작** 확인란을 선택한 다음 클릭 **설치**합니다.  
  
13. 에 **설치 진행률** 페이지 모든 올바르게 설치 되었는지 확인 한 다음 클릭 **닫기**합니다.  
  
## <a name="additional-references"></a>추가 참조  
[Federation 서버 설정 검사:](Checklist--Setting-Up-a-Federation-Server.md)  
  
[검사 목록: Federation 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

