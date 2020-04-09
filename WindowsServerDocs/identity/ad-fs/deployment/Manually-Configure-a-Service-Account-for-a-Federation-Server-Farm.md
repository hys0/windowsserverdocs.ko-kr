---
ms.assetid: 5a1ae56b-adcb-447e-9e34-c0629d7cb241
title: 페더레이션 서버 팜에 대해 수동으로 서비스 계정 구성
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c30215f5f8e39bb97452fccaaef8d1bb0469dc31
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855346"
---
# <a name="manually-configure-a-service-account-for-a-federation-server-farm"></a>페더레이션 서버 팜에 대해 수동으로 서비스 계정 구성

Active Directory Federation Services \(AD FS\)에서 페더레이션 서버 팜 환경을 구성 하려면 팜이 상주 하는 Active Directory Domain Services \(AD DS에서 전용 서비스 계정을 만들고 구성 해야 합니다.\) 그런 다음 이 계정을 사용하도록 팜의 각 페더레이션 서버를 구성합니다. 회사 네트워크의 클라이언트 컴퓨터가 Windows 통합 인증을 사용 하 여 AD FS 팜의 페더레이션 서버에 인증 하도록 허용 하려면 조직에서 다음 작업을 완료 해야 합니다.  

> [!IMPORTANT]
> AD FS 3.0 (Windows Server 2012 R2)에서 AD FS는 [그룹 관리 서비스 계정](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview) \(gMSA\)를 서비스 계정으로 사용할 수 있도록 지원 합니다.  이 옵션은 시간 경과에 따라 서비스 계정 암호를 관리할 필요가 없기 때문에 권장 되는 옵션입니다.  이 문서에서는 Windows Server 2008 R2 또는 이전 도메인 기능 수준 \(DFL\)를 실행 하는 도메인에서와 같이 기존 서비스 계정을 사용 하는 다른 사례에 대해 설명 합니다.

> [!NOTE]  
> 이 절차의 작업은 전체 페더레이션 서버 팜에 대해 한 번만 수행해야 합니다. 나중에 AD FS 페더레이션 서버 구성 마법사를 사용하여 페더레이션 서버를 만들 때 팜 내 각 페더레이션 서버의 **서비스 계정** 마법사 페이지에서 이 동일 계정을 지정해야 합니다.  
  
#### <a name="create-a-dedicated-service-account"></a>전용 서비스 계정 만들기  
  
1.  Id 공급자 조직에 있는 Active Directory 포리스트에 전용 사용자\/서비스 계정을 만듭니다. 이 계정은 Kerberos 인증 프로토콜이 팜 시나리오에서 작동 하 고 각 페더레이션 서버에서 인증을 통해\-를 통과 하도록 허용 하는 데 필요 합니다. 이 계정은 페더레이션 서버 팜의 용도로만 사용 합니다.  
  
2.  사용자 계정 속성을 편집하고 **암호 사용 기간 제한 없음** 확인란을 선택합니다. 이렇게 하면 도메인 암호 변경 요구 사항으로 인해 이 서비스 계정의 작동이 중단되는 일이 발생하지 않습니다.  
  
    > [!NOTE]  
    > Kerberos 티켓은 서버 간에 유효성을 검사하지 않으므로 이 전용 계정에 네트워크 서비스 계정을 사용하면 Windows 통합 인증을 통해 액세스할 때 임의 오류가 발생합니다.  
  
#### <a name="to-set-the-spn-of-the-service-account"></a>서비스 계정의 SPN을 설정하려면  
  
1.  AD FS AppPool의 응용 프로그램 풀 id는 도메인 사용자\/서비스 계정으로 실행 되므로 Setspn 명령\-줄 도구를 사용 하 여 도메인에서 해당 계정에 대 한 SPN\) 서비스 사용자 \(이름을 구성 해야 합니다. Setspn은 Windows Server 2008를 실행 하는 컴퓨터에 기본적으로 설치 됩니다. 사용자\/서비스 계정이 있는 동일한 도메인에 가입 된 컴퓨터에서 다음 명령을 실행 합니다.  
  
    ```  
    setspn -a host/<server name> <service account>  
    ```  
  
    예를 들어, DNS\) 호스트 이름 fs.fabrikam.com \(도메인 이름 시스템에서 모든 페더레이션 서버를 클러스터링 하 고 AD FS AppPool에 할당 된 서비스 계정 이름을 adfs2farm으로 지정로 지정한 경우 다음과 같이 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
    ```  
    setspn -a host/fs.fabrikam.com adfs2farm  
    ```  
  
    이 작업은 이 계정에 대해 한 번만 완료해야 합니다.  
  
2.  AD FS AppPool id를 서비스 계정으로 변경한 후에는 AD FS AppPool에서 정책 데이터를 읽을 수 있도록 SQL Server 데이터베이스에서 Acl\) Acl \(Acl을 설정 하 여이 새 계정에 대 한 읽기 액세스를 허용 합니다.  
  

