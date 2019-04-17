---
title: 웹 서버 WEB1 설치
description: 이 항목은 802.1 X 유선 및 무선 배포에 대 한 배포 서버 인증서 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f51c9e38-98bb-49c1-9d39-427d07021499
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e818eac49719b394a2c73cc125a2e7ba9ea80c82
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="install-the-web-server-web1"></a>웹 서버 WEB1 설치

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Windows Server 2016에는 웹 서버 (IIS) 역할 안정적으로 웹 사이트, 서비스 및 응용 프로그램을 호스트할 안전 하 고 관리 하기 쉬운, 모듈식 있으며 extensible 플랫폼을 제공 합니다. Iis 인터넷, 인트라넷과 또는 엑스트라넷 정보 사용자와 공유할 수 있습니다. IIS는 IIS, ASP.NET, FTP 서비스, PHP, 및 Windows WCF () 통합 하는 웹 통합된 플랫폼입니다.  

서버 인증서를 배포 웹 서버 인증 기관 (캐나다)에 대 한 인증서 해지 목록 CRL ()을 게시할 수 있는 위치를 제공 합니다. 를 게시 한 후 CRL는 네트워크의 모든 컴퓨터에 액세스할 수 있는 다른 컴퓨터에서 제시 인증서가 해지 하지 있는지 확인 하려면이 목록 인증 과정 사용할 수 있습니다.   

인증서가 해지으로 CRL 켜져 있는 경우 인증 노력 실패 하 고 신뢰 하는 더 이상 유효는 인증서 엔터티의에서 컴퓨터를 보호 합니다.  

웹 IIS () 역할을 설치 하기 전에 서버 이름 및 IP 주소 구성한 컴퓨터가 도메인에 가입한을 확인 합니다.  

## <a name="to-install-the-web-server-iis-server-role"></a>웹 IIS () 서버 역할을 설치 하려면  
이 절차를 완료 하려면의 회원 있어야는 **관리자** 그룹입니다.  

>[!NOTE]  
>Windows PowerShell를 사용 하 여이 절차를 수행 하려면 PowerShell 열고 다음 명령을 입력 하 고 enter 합니다.  
`Install-WindowsFeature Web-Server -IncludeManagementTools`  

1.  서버 관리자 클릭 **관리**을 차례로 클릭 하 고 **역할 추가 및 기능**합니다. 역할 추가 및 기능 마법사가 열립니다.  
2.  **시작 하기 전에**, 클릭 **다음**합니다.  

**노트**   
**시작 하기 전에** 역할 추가 및 기능 마법사 실행 이전에 있는 경우 선택한 역할 추가 및 기능 마법사의 페이지가 표시 되지 않으면 **이 페이지 기본적으로 건너뛰기** 당시에 있습니다.  

3.  에 **설치 유형을** 페이지, 클릭 **다음**합니다.  
4.  에 **서버 선택** 페이지, 클릭 **다음**합니다.  
5.  에 **서버 역할** 페이지를 **웹 IIS ()**을 차례로 클릭 하 고 **다음**합니다.  
6.  클릭 **다음** 웹 서버 설정, 기본 설정의 모든와 클릭 한 다음 수락한 될 때까지 **설치**합니다.  
7.  설치 된 모든, 성공 했음을 확인 하 고 클릭 한 다음 **닫기**합니다.
