---
ms.assetid: c50ecc6a-9504-4b4a-816f-e762dcf3a95e
title: 페더레이션 서비스 프록시 역할 서비스 설치
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 1f66e863c28aea7c9214c8363328a103b0a92f06
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359574"
---
# <a name="install-the-federation-service-proxy-role-service"></a>페더레이션 서비스 프록시 역할 서비스 설치

필수 구성 요소 응용 프로그램 및 인증서를 사용 하 여 컴퓨터를 구성한 후에는 Active Directory Federation Services \(페더레이션 서비스 프록시 역할 서비스를 설치할 준비가 된 것입니다 AD FS\). 다음 절차를 사용 하 여 페더레이션 서비스 프록시 역할 서비스를 설치할 수 있습니다. 컴퓨터에 페더레이션 서비스 프록시 역할 서비스를 설치 하면 해당 컴퓨터가 페더레이션 서버 프록시가 됩니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-install-the-federation-service-proxy-role-service-using-the-server-manager"></a>서버 관리자를 사용 하 여 페더레이션 서비스 프록시 역할 서비스를 설치 하려면
  
1.  **시작** 화면에서**서버 관리자**를 입력 한 다음 enter 키를 누릅니다.  
  
2.  **관리**, **역할 및 기능 추가** 를 차례로 클릭 하 여 역할 및 기능 추가 마법사를 시작 합니다.  
  
3.  **시작하기 전** 페이지에서 **다음**을 클릭합니다.  
  
4.  **설치 유형 선택** 페이지에서 **역할\-기반 또는 기능\-기반 설치**를 클릭 하 고 **다음**을 클릭 합니다.  
  
5.  **대상 서버 선택** 페이지에서 **서버 풀에서 서버 선택**을 클릭 하 고 대상 컴퓨터가 강조 표시 되었는지 확인 한 후 **다음**을 클릭 합니다.  
  
6.  **서버 역할 선택** 페이지에서 **원격 액세스**를 클릭 하 고 다음을 클릭 합니다.  
  
    > [!NOTE]  
    > 추가 .NET Framework 또는 Windows Process Activation Service 기능을 설치 하 라는 메시지가 표시 되 면 **기능 추가** 를 클릭 하 여 설치 합니다.  
  
7. **역할 서비스 선택** 페이지에서 **페더레이션 서비스 프록시** 확인란을 선택 하 고 **다음**을 클릭 합니다.  

8. **설치 선택 확인** 페이지에서 정보를 확인한 후 **필요한 경우 자동으로 대상 서버 다시 시작** 확인란을 선택하고 **설치**를 클릭합니다.  
  
13. **설치 진행률** 페이지에서 모든 항목이 올바르게 설치되었는지 확인하고 **닫기**를 클릭합니다.  

### <a name="to-install-the-federation-service-proxy-role-service-using-powershell"></a>PowerShell을 사용 하 여 페더레이션 서비스 프록시 역할 서비스를 설치 하려면

1. Windows PowerShell을 엽니다 (관리자 권한으로 실행).

2. 다음 명령을 입력 하 고 **enter**키를 누릅니다.

        Install-WindowsFeature Web-Application-Proxy -IncludeManagementTools



  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)  
  
[검사 목록: 페더레이션 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

