---
title: 인증 기관 설치
description: 이 항목은 서버 배포 인증서 802.1 X 유선 및 무선 배포 가이드의 일부
manager: brianlic
ms.topic: article
ms.assetid: 4acdc3ad-078e-45cc-b54c-e9456e0c90f5
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 84e4b2fe0b59820b9e51229335f3539bcbeeec90
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860744"
---
# <a name="install-the-certification-authority"></a>인증 기관 설치

>적용 대상: Windows Server (반기 채널), Windows Server 2016

네트워크 정책 (NPS 서버), 라우팅 및 원격 액세스 서비스 (RRAS) 또는 둘 모두를 실행 하는 서버에 서버 인증서를 등록할 수 있도록 Active Directory 인증서 서비스 (AD CS)를 설치 하려면이 절차를 사용할 수 있습니다.  
  
> [!IMPORTANT]  
> -   Active Directory 인증서 서비스를 설치 하기 전에 컴퓨터의 이름, 정적 IP 주소를 가진 컴퓨터를 구성 하며 컴퓨터를 도메인에 가입 있습니다. 이러한 작업을 수행 하는 방법에 대 한 자세한 내용은 Windows Server 2016 참조 [핵심 네트워크 가이드](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide)합니다.  
> -   이 절차를 수행 하려면 AD CS를 설치 하는 컴퓨터를 Active Directory 도메인 서비스 (AD DS) 설치 되어 있는 도메인에 가입 해야 합니다.  
  
둘 다의 구성원은 **Enterprise Admins** 및 루트 도메인의 **Domain Admins** 그룹은이 절차를 완료 하려면 최소한 합니다.  
  
> [!NOTE]  
> Windows PowerShell을 사용 하 여이 절차를 수행 하려면 Windows PowerShell 및 열고 다음 명령을 입력 한 다음 ENTER 키를 누릅니다.   
>   
> `Add-WindowsFeature Adcs-Cert-Authority -IncludeManagementTools`  
>   
> AD CS를 설치한 후 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
>   
> `Install-AdcsCertificationAuthority -CAType EnterpriseRootCA`  
  
### <a name="to-install-active-directory-certificate-services"></a>Active Directory 인증서 서비스를 설치 하려면  

>[!TIP]
>참조를 Active Directory 인증서 서비스를 설치 하려면 Windows PowerShell을 사용 하려는 경우 [Install-adcscertificationauthority](https://docs.microsoft.com/powershell/module/adcsdeployment/install-adcscertificationauthority?view=win10-ps) cmdlet 및 선택적 매개 변수입니다.
  
1.  Enterprise Admins 그룹 및 루트 도메인의 Domain Admins 그룹의 구성원으로 로그온 합니다.  
  
2.  서버 관리자에서 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다. 역할 및 기능 추가 마법사가 열립니다.  
  
3.  **시작하기 전**에서 **다음**을 클릭합니다.  
  
    > [!NOTE]  
    > 이전에 역할 및 기능 추가 마법사를 실행할 때 **항상 이 페이지 건너뛰기**를 선택한 경우에는 역할 및 기능 추가 마법사의 **시작하기 전** 페이지가 표시되지 않습니다.  
  
4.  **설치 유형 선택**에서 **역할 기반 또는 기능 기반 설치**가 선택되어 있는지 확인하고 **다음**을 클릭합니다.  
  
5.  **대상 서버 선택**에서 **서버 풀에서 서버 선택**이 선택되어 있는지 확인합니다. **서버 풀**에서 로컬 컴퓨터가 선택되어 있는지 확인합니다. **다음**을 클릭합니다.  
  
6.  **서버 역할 선택**,  **역할**, 선택, **Active Directory 인증서 서비스**합니다. 필수 기능을 추가 하는 메시지가 나타나면 클릭 **기능 추가**, 를 클릭 하 고 **다음**합니다.  
  
7.  **기능 선택**, 클릭 **다음**합니다.  
  
8.  **Active Directory 인증서 서비스**, 에서 제공 된 정보를 읽고 클릭 **다음**합니다.  
  
9. **설치 선택 확인**, 클릭 **설치**합니다. 설치 과정에서 마법사를 닫지 마십시오. 설치가 완료 되 면 클릭 **대상 서버에서 Active Directory 인증서 서비스 구성**합니다. AD CS 구성 마법사가 열립니다. 자격 증명 정보를 읽고 필요한 경우 Enterprise Admins 그룹의 구성원 인 계정의 자격 증명을 제공 합니다. **다음**을 클릭합니다.  
  
10. **역할 서비스**, 클릭 **인증 기관**, 를 클릭 하 고 **다음**합니다.  
  
11. 에 **설치 유형** 페이지에서 **엔터프라이즈 CA** 을 선택한 다음 클릭 **다음**합니다.  
  
12. 에 **CA의 유형을 지정** 페이지에서 **루트 CA** 을 선택한 다음 클릭 **다음**합니다.  
  
13. 에 **개인 키의 형식을 지정** 페이지에서 **새 개인 키를 만들** 을 선택한 다음 클릭 **다음**합니다.  
  
14. 에 **CA에 대 한 암호화** 페이지, CSP에 대 한 기본 설정을 유지 (**RSA #Microsoft Software Key Storage Provider**) 및 해시 알고리즘 (**SHA2**), 최상의 결정 배포에 대 한 키 문자 길이입니다. 최적의 보안;을 제공 하는 큰 키 문자 길이 그러나 서버 성능에 영향을 줄 수 하며 레거시 응용 프로그램과 호환 되지 않을 수 있습니다. 2048의 기본 설정을 유지 하는 것이 좋습니다. **다음**을 클릭합니다.  
  
15. 에 **CA 이름** 페이지, CA에 대 한 일반적인 제안 된 이름을 그대로 사용 하거나 요구 사항에 따라 이름을 변경 합니다. 사용자가 있는지 확인 특정 AD CS를 설치한 후 CA 이름을 변경할 수 없으므로 CA 이름 명명 규칙 및 용도와 호환 됩니다. **다음**을 클릭합니다.  
  
16. 에 **유효 기간** 페이지 **유효 기간을 지정**, 번호를 입력 하 고 시간 값 (예: 년, 월, 주, 또는 일)을 선택 합니다. 근무 연수가 5 년의 기본 설정은 사용 하는 것이 좋습니다. **다음**을 클릭합니다.  
  
17. 에 **CA 데이터베이스** 페이지 **데이터베이스 위치를 지정**, 인증서 데이터베이스 및 인증서 데이터베이스 로그에 대 한 폴더 위치를 지정 합니다. 기본 위치 이외의 위치를 지정 하는 경우 폴더는 권한이 없는 사용자 또는 컴퓨터 CA 데이터베이스 및 로그 파일에 액세스 하지 못하도록 하는 액세스 제어 목록 (Acl)로 보호 되는 확인 합니다. **다음**을 클릭합니다.  
  
18. **확인**, 클릭 **구성** 선택 사항을 적용 한 다음 클릭 **닫기**합니다.  
  


