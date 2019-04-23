---
title: SPN(서비스 사용자 이름) Kerberos
description: 네트워크 컨트롤러 관리 클라이언트와의 통신에 대 한 여러 인증 방법을 지원합니다. 사용할 수 Kerberos 기반 인증을 X509 인증서 기반 인증 합니다. 테스트 배포에 대 한 인증 안 함을 사용 하는 옵션이 있습니다.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: bc625de9-ee31-40a4-9ad2-7448bfbfb6e6
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 2459cfa8dfec3de4aa23da7aba192d6eeed7f8ec
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828974"
---
# <a name="kerberos-with-service-principal-name-spn"></a>SPN(서비스 사용자 이름) Kerberos

>적용 대상: Windows Server 2019

네트워크 컨트롤러 관리 클라이언트와의 통신에 대 한 여러 인증 방법을 지원합니다. 사용할 수 Kerberos 기반 인증을 X509 인증서 기반 인증 합니다. 테스트 배포에 대 한 인증 안 함을 사용 하는 옵션이 있습니다.

System Center Virtual Machine Manager Kerberos 기반 인증을 사용 합니다. Kerberos 기반 인증을 사용 하는 경우에 Active Directory에서 네트워크 컨트롤러에 대 한를 이름 SPN (서비스 사용자)를 구성 해야 합니다. SPN은 Kerberos 인증 서비스 로그인 계정을 사용 하 여 서비스 인스턴스 연결에 사용 되는 네트워크 컨트롤러 서비스 인스턴스에 대해 고유 식별자입니다. 자세한 내용은 참조 하세요. [서비스 사용자 이름](https://docs.microsoft.com/windows/desktop/ad/service-principal-names)합니다.

## <a name="configure-service-principal-names-spn"></a>서비스 주체 이름 (SPN) 구성

네트워크 컨트롤러는 자동으로 SPN을 구성합니다. 하기만 하면 등록 하 고 SPN을 수정 하는 네트워크 컨트롤러 컴퓨터에 대 한 권한을 제공 하는 것입니다.

1.  도메인 컨트롤러 컴퓨터에서 시작 **Active Directory Users and Computers**합니다.

2.  선택 **뷰 \> 고급**합니다.

3.  아래 **컴퓨터**, 네트워크 컨트롤러 컴퓨터 계정 중 하나를 찾아 마우스 오른쪽 단추로 클릭을 선택한 다음 **속성**합니다.

4.  선택 된 **Security** 탭을 클릭 **고급**합니다.

5.  목록에서 모든 네트워크 컨트롤러 컴퓨터 계정 또는 보안에는 모든 네트워크 컨트롤러 컴퓨터 계정을 나타나지 것 그룹, 클릭 **추가** 추가 합니다.

6.  각 네트워크 컨트롤러 컴퓨터 계정 또는 네트워크 컨트롤러 컴퓨터 계정을 포함 하는 하나의 보안 그룹의 경우:

    a.  계정 또는 그룹을 선택 하 고 클릭 **편집**합니다.

    b.  사용 권한 선택 **servicePrincipalName 쓰기의 유효성을 검사**합니다.

    d.  아래에서 아래로 스크롤하여 **속성** 선택:

       -  **ServicePrincipalName 읽기**

       -  **ServicePrincipalName 쓰기**

    e.  **확인** 을 두 번 클릭합니다.

7.  각 네트워크 컨트롤러 컴퓨터에 대 한 3 ~ 6 단계를 반복 합니다.

8.  **Active Directory 사용자 및 컴퓨터**를 닫습니다.

## <a name="failure-to-provide-permissions-for-spn-registrationmodification"></a>SPN 등록/수정에 대 한 사용 권한을 제공 하지 못함

에 **새로 만들기** REST 클라이언트 인증에 Kerberos를 선택 하 고 네트워크 컨트롤러 노드를 등록 하거나 SPN 수정에 대 한 권한을 부여 하지 하는 경우 Windows Server 2019 배포, 네트워크 컨트롤러에 대 한 REST 작업 실패 SDN 관리에서 사용자를 방지 합니다.

REST 클라이언트 인증에 대 한 Kerberos를 선택 하는 Windows Server 2016에서 Windows Server 2019를로 업그레이드에 대 한 REST 작업 수행 차단 되지, 기존 프로덕션 배포에 대 한 투명성을 보장 합니다. 

SPN 등록 되어 있지 않으면 REST 클라이언트 인증 인 NTLM을 사용는 안전성이 떨어집니다. 관리 채널에 중요 한 이벤트를 가져올 수도 **NetworkController Framework** SPN을 등록 하려면 네트워크 컨트롤러 노드에 사용 권한을 제공 하 라는 메시지가 이벤트 채널입니다. 권한을 제공한 후 네트워크 컨트롤러의 SPN을 자동으로 등록 하 고 모든 클라이언트 작업 Kerberos를 사용 합니다.


>[!TIP]
>일반적으로 IP 주소 또는 REST 기반 작업에 대 한 DNS 이름을 사용 하 여 네트워크 컨트롤러를 구성할 수 있습니다. 그러나 Kerberos를 구성한 경우 IP 주소를 네트워크 컨트롤러 REST 쿼리를 사용할 수 없습니다. 예를 들어 사용할 수 있습니다 \< https://networkcontroller.consotso.com\>를 사용할 수 없습니다 있지만 \< https://192.34.21.3\>합니다. 서비스 주체 이름 IP 주소가 사용 되는 경우 작동 하지 못합니다.
>
>Windows Server 2016에서 Kerberos 인증와 함께 REST 작업에 대 한 IP 주소를 사용한, NTLM 인증을 통해 실제 통신 것입니다. 이러한 배포에서는 Windows Server 2019로 업그레이드 하면 NTLM 기반 인증을 사용 하 여 계속 합니다. Kerberos 기반 인증을 이동 하려면 REST 작업에 대 한 네트워크 컨트롤러 DNS 이름을 사용 하며 네트워크 컨트롤러 노드 SPN 등록에 대 한 사용 권한을 제공 합니다.

---