---
ms.assetid: 5a1ae56b-adcb-447e-9e34-c0629d7cb241
title: "수동으로 서비스 계정을 Federation 서버 팜에 대 한 구성"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5b5a8d198f93772903ea9b0a2b4b01075799bf0f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="manually-configure-a-service-account-for-a-federation-server-farm"></a>수동으로 서비스 계정을 Federation 서버 팜에 대 한 구성

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Federation Services \(AD FS\) federation 서버 농장 환경을 구성할 하려는 경우 만들고 해야 Active Directory 도메인 서비스 \(AD DS\) 팜 있는에서 전용된 서비스 계정을 구성 합니다. 각 federation 서버에이 계정을 사용 하 여 농장 구성 합니다. Windows 통합 인증을 사용 하는 ADFS 농장의 federation 서버 인증을 회사 네트워크에서 컴퓨터 클라이언트를 허용 하려는 경우 조직에는 다음과 같은 작업을 완료 해야 합니다.  
  
> [!NOTE]  
> 한 번만 전체 federation 서버 그룹에 대 한이 절차의 작업을 수행 해야 합니다. 나중에 AD FS Federation 서버 구성 마법사를 사용 하 여 federation 서버를 만들 때 지정 해야이 동일한 계정에는 **서비스 계정** 팜 각 federation 서버에서 마법사 페이지 합니다.  
  
#### <a name="create-a-dedicated-service-account"></a>전용된 서비스 계정 만들기  
  
1.  신원 공급자 조직에 있는 Active Directory 숲 속의 전용된 user\/서비스 계정을 만듭니다. 이 계정은 Kerberos 인증 프로토콜 농장 시나리오에서 작업 하 고 각 federation 서버의 pass\ 쓰루 인증 허용 하는 데 필요한입니다. Federation 서버 팜 목적 으로만이 계정을 사용 합니다.  
  
2.  사용자 계정 속성 편집한는 **암호** 확인란을 선택 합니다. 이 작업을이 수행 도메인 암호 변경 요구 사항으로 인해 서비스 계정의이 함수가 중단 되지 않도록 수 있습니다.  
  
    > [!NOTE]  
    > 네트워크 서비스 계정을 사용 하 여이 전용된 계정에 대 한 액세스 Kerberos 티켓 다른 한 서버에서 하지 유효성 검사 결과 통해 Windows 통합 인증 시도할 때 임의 오류 발생 합니다.  
  
#### <a name="to-set-the-spn-of-the-service-account"></a>서비스 계정의 SPN 설정 하려면  
  
1.  AD FS AppPool의 응용 프로그램 풀 id user\/서비스의 도메인 계정을으로 실행 되 고 있으므로 Setspn.exe command\ 선 도구 된 도메인의 해당 계정에 대 한 서비스 사용자 이름 \(SPN\) 구성 해야 합니다. Setspn.exe는 Windows Server 2008 실행 하는 컴퓨터에서 기본적으로 설치 됩니다. User\/서비스 계정이 있는 같은 도메인에 가입 하는 컴퓨터에서 다음 명령을 실행 합니다.  
  
    ```  
    setspn -a host/<server name> <service account>  
    ```  
  
    예를 들어 모든 federation 서버가 Domain Name System \(DNS\) 호스트 이름 fs.fabrikam.com 아래 클러스터 되어 및 AD FS AppPool에 할당 된 서비스 계정 이름을 adfs2farm 라는 시나리오에서 다음과 같이 명령을 입력 한 다음 ENTER 키를:  
  
    ```  
    setspn -a host/fs.fabrikam.com adfs2farm  
    ```  
  
    이 계정에 대해 한 번만이 작업을 수행 해야 하는 합니다.  
  
2.  서비스 계정 FS AppPool 광고 id 변경 된 후이 새 계정에 대 한 읽기 AD FS AppPool 정책 데이터 읽을 수 있도록 허용 하려면 SQL Server 데이터베이스에 대 한 액세스를 제어 목록을 \(ACLs\) 설정 합니다.  
  

