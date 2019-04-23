---
ms.assetid: 5a1ae56b-adcb-447e-9e34-c0629d7cb241
title: 페더레이션 서버 팜에 대해 수동으로 서비스 계정 구성
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 7d215c80c03236df9479aff8046981741dfc83e2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838154"
---
# <a name="manually-configure-a-service-account-for-a-federation-server-farm"></a>페더레이션 서버 팜에 대해 수동으로 서비스 계정 구성

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Federation Services에서 페더레이션 서버 팜 환경을 구성 하려면 \(AD FS\)를 만들고 Active Directory Domain Services에서 전용된 서비스 계정을 구성 해야 \(AD DS\) 팜에서 상주 합니다. 그런 다음 이 계정을 사용하도록 팜의 각 페더레이션 서버를 구성합니다. Windows 통합 인증을 사용 하 여 AD FS 팜에 페더레이션 서버에 인증 하려면 회사 네트워크에서 클라이언트 컴퓨터를 허용 하려는 경우 조직에서 다음 작업을 완료 해야 합니다.  

> [!IMPORTANT]
> AD FS 3.0 (Windows Server 2012 R2), AD FS 지원의 사용을 [그룹 관리 서비스 계정](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview) \(gMSA\) 서비스 계정으로 합니다.  시간이 지남에 따라 서비스 계정 암호를 관리할 필요가 없으므로 이것이 권장된 옵션입니다.  이 문서에서는 여전히 실행 하는 Windows Server 2008 R2 또는 이전 도메인 기능 수준은 도메인에서와 같은 기존 서비스 계정을 사용에 대 한 대체 사례의 \(DFL\)합니다.

> [!NOTE]  
> 이 절차의 작업은 전체 페더레이션 서버 팜에 대해 한 번만 수행해야 합니다. 나중에 AD FS 페더레이션 서버 구성 마법사를 사용 하 여 페더레이션 서버를 만들 때 지정 해야이 동일한 계정에는 **서비스 계정** 팜의 각 페더레이션 서버에서 마법사 페이지입니다.  
  
#### <a name="create-a-dedicated-service-account"></a>전용 서비스 계정 만들기  
  
1.  전용된 사용자를 만드는\/서비스 계정 id 공급자 조직에 있는 Active Directory 포리스트에 있습니다. 이 계정은 Kerberos 인증 프로토콜이 팜 시나리오에서 작동 하 고 통과 허용 하려면 반드시\-각 페더레이션 서버의 인증을 통해. 페더레이션 서버 팜의 목적에이 계정을 사용 합니다.  
  
2.  사용자 계정 속성을 편집하고 **암호 사용 기간 제한 없음** 확인란을 선택합니다. 이 작업은 도메인 암호 변경 요구 사항으로 인해 이 서비스 계정의 작동이 중단되지 않도록 해줍니다.  
  
    > [!NOTE]  
    > Kerberos 티켓은 서버 간에 유효성을 검사하지 않으므로 이 전용 계정에 네트워크 서비스 계정을 사용하면 Windows 통합 인증을 통해 액세스할 때 임의 오류가 발생합니다.  
  
#### <a name="to-set-the-spn-of-the-service-account"></a>서비스 계정의 SPN을 설정하려면  
  
1.  AD FS AppPool에 대 한 응용 프로그램 풀 id에 도메인 사용자로 실행 되 고 있어서\/서비스 계정, 서비스 주체 이름을 구성한 \(SPN\) Setspn.exe명령사용하여도메인에서해당계정에대한\-명령줄 도구입니다. Setspn.exe는 Windows Server 2008을 실행 하는 컴퓨터에서 기본적으로 설치 됩니다. 동일한 도메인에 가입 된 컴퓨터에서 다음 명령을 실행 여기서 사용자\/상주 하는 서비스 계정:  
  
    ```  
    setspn -a host/<server name> <service account>  
    ```  
  
    에 모든 페더레이션 서버는 아래에 클러스터 Domain Name System 시나리오의 예를 들어 \(DNS\) 호스트 이름 fs.fabrikam.com 및 AD FS AppPool에 할당 되는 서비스 계정 이름이 adfs2farm 라는 명령을 입력 합니다. 같이 다음 ENTER를 누릅니다.  
  
    ```  
    setspn -a host/fs.fabrikam.com adfs2farm  
    ```  
  
    이 작업은 이 계정에 대해 한 번만 완료해야 합니다.  
  
2.  AD FS AppPool id는 서비스 계정에 변경 되 면 액세스 제어 목록 설정 \(Acl\) AD FS AppPool에서 정책 데이터를 읽을 수 있도록이 새 계정에 대 한 읽기 권한을 허용 하려면 SQL Server 데이터베이스에 있습니다.  
  

