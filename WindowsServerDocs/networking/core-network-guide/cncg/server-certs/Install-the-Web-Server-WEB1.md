---
title: 웹 서버 WEB1 설치
description: 이 항목은 서버 배포 인증서 802.1 X 유선 및 무선 배포 가이드의 일부
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: f51c9e38-98bb-49c1-9d39-427d07021499
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8871b2b82b30bca5b4efd62a31b52e8dbd7284a9
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318280"
---
# <a name="install-the-web-server-web1"></a>웹 서버 WEB1 설치

>적용 대상: Windows Server(반기 채널), Windows Server 2016

Windows Server 2016에서 웹 서버 (IIS) 역할 웹 사이트, 서비스 및 애플리케이션을 안정적으로 호스팅하기 위한 안전, 관리 하기 쉬운, 모듈식 하 고 확장 가능한 플랫폼을 제공 합니다. Iis에서 인터넷, 인트라넷 또는 엑스트라넷 사용자와 정보를 공유할 수 있습니다. IIS는 IIS, ASP.NET, FTP 서비스, PHP 및 Windows Communication Foundation (WCF)를 통합 하는 통합형된 웹 플랫폼.  

서버 인증서를 배포 하면 웹 서버 인증 기관 (CA)에 대해 인증서 해지 목록 (CRL)을 게시할 수 있는 위치를 제공 합니다. 를 게시 한 후 CRL을 네트워크에 있는 모든 컴퓨터에 액세스할 수 있으므로 인증 프로세스 중에이 목록을 사용 하 여 다른 컴퓨터에서 표시 되는 인증서는 해지 되지 않았는지 확인할 수 있습니다.   

인증서 취소 CRL에 포함 된 경우 인증 노력 실패 하 고는 더 이상 유효 인증서가 있는 엔터티를 신뢰 하에서 컴퓨터를 보호 합니다.  

웹 서버 (IIS) 역할을 설치 하기 전에 서버 이름 및 IP 주소 구성 하 고 컴퓨터를 도메인에 가입 시킨를 확인 합니다.  

## <a name="to-install-the-web-server-iis-server-role"></a>웹 서버 (IIS) 서버 역할을 설치 하려면  
이 절차를 완료하려면 **Administrators** 그룹의 구성원이어야 합니다.  

>[!NOTE]  
>Windows PowerShell을 사용 하 여이 절차를 수행 하려면 PowerShell을 열고 하 고 다음 명령을 입력 한 다음 ENTER 키를 누릅니다.  
`Install-WindowsFeature Web-Server -IncludeManagementTools`  

1.  서버 관리자에서 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다. 역할 및 기능 추가 마법사가 열립니다.  
2.  **시작하기 전**에서 **다음**을 클릭합니다.  

**참고**   
**시작 하기 전에** 역할 및 추가 기능 마법사의 페이지에는 역할 및 추가 기능 마법사를 이전에 실행 하 고 선택한 경우 표시 되지 않습니다 **기본적으로이 페이지 건너뛰기** 당시에 있습니다.  

3. **설치 유형** 페이지에서 **다음**을 클릭합니다.  
4. 에 **서버 선택** 페이지에서 클릭 **다음**합니다.  
5. 에 **서버 역할** 페이지에서 **웹 서버 (IIS)** , 를 클릭 하 고 **다음**합니다.  
6. 기본 웹 서버 설정이 모두 적용될 때까지 **다음**을 클릭한 후 **설치**를 클릭합니다.  
7. 모든 설치가 완료되었는지 확인한 다음 **닫기**를 클릭합니다.
