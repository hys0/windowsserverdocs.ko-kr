---
title: SPN(서비스 사용자 이름) Kerberos
description: 네트워크 컨트롤러는 관리 클라이언트와의 통신을 위한 여러 인증 방법을 지원 합니다. Kerberos 기반 인증, X509 인증서 기반 인증을 사용할 수 있습니다. 또한 테스트 배포에 대해 인증을 사용 하지 않는 옵션도 있습니다.
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: bc625de9-ee31-40a4-9ad2-7448bfbfb6e6
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/23/2018
ms.openlocfilehash: 12ad2b27d275c074e0d8baacccd864e8926f405f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854377"
---
# <a name="kerberos-with-service-principal-name-spn"></a>SPN(서비스 사용자 이름) Kerberos

>적용 대상: Windows Server 2019

네트워크 컨트롤러는 관리 클라이언트와의 통신을 위한 여러 인증 방법을 지원 합니다. Kerberos 기반 인증, X509 인증서 기반 인증을 사용할 수 있습니다. 또한 테스트 배포에 대해 인증을 사용 하지 않는 옵션도 있습니다.

System Center Virtual Machine Manager Kerberos 기반 인증을 사용 합니다. Kerberos 기반 인증을 사용 하는 경우 Active Directory에서 네트워크 컨트롤러에 대 한 SPN (서비스 사용자 이름)을 구성 해야 합니다. SPN은 Kerberos 인증에서 서비스 인스턴스를 서비스 로그인 계정과 연결 하는 데 사용 하는 네트워크 컨트롤러 서비스 인스턴스에 대 한 고유 식별자입니다. 자세한 내용은 [서비스 사용자 이름](https://docs.microsoft.com/windows/desktop/ad/service-principal-names)을 참조 하세요.

## <a name="configure-service-principal-names-spn"></a>SPN (서비스 사용자 이름) 구성

네트워크 컨트롤러에서 SPN을 자동으로 구성 합니다. 네트워크 컨트롤러 컴퓨터에서 SPN을 등록 하 고 수정할 수 있는 권한을 제공 하기만 하면 됩니다.

1.  도메인 컨트롤러 컴퓨터에서 **사용자 및 컴퓨터 Active Directory**를 시작 합니다.

2.  **보기 \> 고급**을 선택 합니다.

3.  **컴퓨터**에서 네트워크 컨트롤러 컴퓨터 계정 중 하나를 찾은 다음 마우스 오른쪽 단추를 클릭 하 고 **속성**을 선택 합니다.

4.  **보안** 탭을 선택 하 고 **고급**을 클릭 합니다.

5.  목록에서 모든 네트워크 컨트롤러 컴퓨터 계정 또는 모든 네트워크 컨트롤러 컴퓨터 계정을 포함 하는 보안 그룹이 나열 되지 않은 경우 **추가** 를 클릭 하 여 추가 합니다.

6.  각 네트워크 컨트롤러 컴퓨터 계정 또는 네트워크 컨트롤러 컴퓨터 계정을 포함 하는 단일 보안 그룹:

    a.  계정 또는 그룹을 선택 하 고 **편집**을 클릭 합니다.

    b.  사용 권한 아래에서 **Write ServicePrincipalName 유효성 검사**를 선택 합니다.

    .  아래로 스크롤하고 **속성** 아래에서 다음을 선택 합니다.

       -  **ServicePrincipalName 읽기**

       -  **ServicePrincipalName 쓰기**

    e.  **확인** 을 두 번 클릭합니다.

7.  각 네트워크 컨트롤러 컴퓨터에 대해 3-6 단계를 반복 합니다.

8.  **Active Directory 사용자 및 컴퓨터**를 닫습니다.

## <a name="failure-to-provide-permissions-for-spn-registrationmodification"></a>SPN 등록/수정에 대 한 사용 권한을 제공 하지 못했습니다.

**새** Windows Server 2019 배포에서 rest 클라이언트 인증에 Kerberos를 선택 하 고 네트워크 컨트롤러 노드에 SPN을 등록 하거나 수정할 수 있는 권한을 부여 하지 않으면 네트워크 컨트롤러의 REST 작업이 실패 하 여 SDN을 관리할 수 없게 됩니다.

Windows Server 2016에서 Windows Server 2019로 업그레이드 하는 경우 REST 클라이언트 인증을 위해 Kerberos를 선택 하면 REST 작업이 차단 되지 않고 기존 프로덕션 배포에 대 한 투명도를 보장 합니다. 

SPN이 등록 되어 있지 않으면 REST 클라이언트 인증에서 NTLM을 사용 합니다 .이는 보안 수준이 낮습니다. 또한 SPN을 등록 하기 위해 네트워크 컨트롤러 노드에 대 한 권한을 제공 하 라는 **NetworkController 프레임 워크** 이벤트 채널의 관리 채널에서 중요 한 이벤트를 받게 됩니다. 권한을 제공 하면 네트워크 컨트롤러에서 SPN을 자동으로 등록 하 고 모든 클라이언트 작업에서 Kerberos를 사용 합니다.


>[!TIP]
>일반적으로는 REST 기반 작업에 IP 주소 또는 DNS 이름을 사용 하도록 네트워크 컨트롤러를 구성할 수 있습니다. 그러나 Kerberos를 구성 하는 경우 네트워크 컨트롤러에 대 한 REST 쿼리의 IP 주소를 사용할 수 없습니다. 예를 들어 \<https://networkcontroller.consotso.com\>를 사용할 수 있지만 \<https://192.34.21.3\>는 사용할 수 없습니다. IP 주소가 사용 되는 경우 서비스 사용자 이름은 작동할 수 없습니다.
>
>Windows Server 2016에서 Kerberos 인증과 함께 REST 작업에 IP 주소를 사용 하는 경우 실제 통신은 NTLM 인증을 통해 수행 된 것입니다. 이러한 배포에서 Windows Server 2019로 업그레이드 한 후에는 NTLM 기반 인증을 계속 사용 합니다. Kerberos 기반 인증으로 이동 하려면 REST 작업에 네트워크 컨트롤러 DNS 이름을 사용 하 고 SPN을 등록할 네트워크 컨트롤러 노드에 대 한 권한을 제공 해야 합니다.

---