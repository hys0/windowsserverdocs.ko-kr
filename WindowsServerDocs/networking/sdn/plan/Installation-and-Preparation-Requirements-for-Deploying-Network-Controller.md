---
title: 설치 및 네트워크 컨트롤러 배포 하기 위한 준비 요구 사항
description: 네트워크 컨트롤러 배포 데이터 센터 준비 하려면이 항목을 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 7f899e62-6e5b-4fca-9a59-130d4766ee2f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c50a2167a894871ea76fb96523c19531100648ce
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="installation-and-preparation-requirements-for-deploying-network-controller"></a>설치 및 네트워크 컨트롤러 배포 하기 위한 준비 요구 사항

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

네트워크 컨트롤러 배포 데이터 센터 준비 하려면이 항목을 사용할 수 있습니다.  
  
> [!NOTE]  
> 이 항목에서는 뿐만 아니라 다음 네트워크 컨트롤러 설명서를 사용할 수 있습니다.  
> 
> - [네트워크 컨트롤러](../technologies/network-controller/Network-Controller.md)
> - [네트워크 컨트롤러 높은 공급 일](../technologies/network-controller/network-controller-high-availability.md)
> - [네트워크 컨트롤러를 사용 하 여 Windows PowerShell 배포](../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)  
> - [네트워크 컨트롤러 서버 역할 서버 관리자를 사용 하 여 설치](../technologies/network-controller/Install-the-Network-Controller-server-role-using-Server-Manager.md)  

다음은 설치, 소프트웨어 및 기타 요구 사항 및 준비 단계 네트워크 컨트롤러 배포 하기 전에 위해 수행 해야 합니다.

## <a name="installation-requirements"></a>설치 요구 사항

다음은 네트워크 컨트롤러용 설치 요구 합니다.

- Windows Server 2016 배포를 위해 네트워크 컨트롤러 하나 이상의 컴퓨터, 하나 이상의 Vm 또는 Vm 컴퓨터의 조합으로 나만의에 배포할 수 있습니다. 모든 Vm 및 네트워크 컨트롤러 노드로 계획 컴퓨터 Windows Server 2016 Datacenter edition을 실행 해야 합니다.

## <a name="software-requirements"></a>소프트웨어 요구 사항

네트워크 컨트롤러 배포 컴퓨터 또는 네트워크 컨트롤러용 관리 클라이언트 역할을 역할을 네트워크 컨트롤러 및 한 컴퓨터 Vm 또는 VM 하나 이상의 필요 합니다. 이러한 컴퓨터 또는 Vm 다음 운영 체제를 실행 해야 합니다.  

- 컴퓨터 또는 VM (가상 컴퓨터) 있는 네트워크 컨트롤러 설치한 Windows Server 2016 Datacenter edition을 실행 해야 합니다.  
  
- Windows 8, Windows 8.1 또는 Windows 10 관리 클라이언트 컴퓨터 또는 네트워크 컨트롤러용는 VM 실행 해야 합니다.  
  
## <a name="additional-requirements"></a>추가 요구 사항

다음 추가 해야 할 단계가 네트워크 컨트롤러 배포 하기 전에 합니다.
  
### <a name="configure-security-groups"></a>보안 그룹 구성
  
컴퓨터 또는 네트워크 컨트롤러 및 관리 클라이언트 Vm 인 도메인에 가입한 경우 다음과 같은 보안 그룹 Kerberos 인증에 대 한 구성 합니다.

- 보안 그룹 만들고이 모든 네트워크 컨트롤러 구성할 수 있는 권한이 있는 사용자를 추가 합니다. 예를 들어 라는 그룹을 만들고 **네트워크 컨트롤러 관리자**합니다. 모든이 그룹에 추가 하는 사용자의 회원 해야는 **도메인 사용자** Active Directory 사용자와 컴퓨터의 그룹입니다.  
  
    > [!NOTE]  
    > 그룹 Active Directory 사용자와 컴퓨터의 만드는 방법에 대 한 자세한 내용은 참조 [새 그룹을 만들려면](https://technet.microsoft.com/en-us/library/cc783256(v=ws.10).aspx)합니다.  

- 보안 그룹 만들고이 모든 구성 하 고 네트워크 컨트롤러를 사용 하 여 네트워크를 관리할 수 있는 권한이 있는 사용자를 추가 합니다.  예를 들어 라는 새로운 그룹을 만들고 **네트워크 컨트롤러 사용자**합니다. 모든 새 그룹에 추가 하는 사용자의 회원 해야는 **도메인 사용자** Active Directory 사용자와 컴퓨터의 그룹입니다. 모든 구성 네트워크 컨트롤러 및 관리 표시 상태 전송 \(REST\)를 사용 하 여 수행 됩니다.

### <a name="configure-log-file-locations-if-needed"></a>필요한 경우 로그 파일 위치 구성

네트워크 컨트롤러 디버그 로그 또는 원격 파일 공유 하는 네트워크 컨트롤러 컴퓨터 또는 VM에서에 저장할 수 있습니다. 로그 원격 파일 공유에서 저장 하려는 경우 공유 네트워크 컨트롤러에서 액세스할 수 있는지 확인 합니다.

### <a name="configure-dynamic-dns-registration-for-network-controller"></a>네트워크 컨트롤러에 대 한 동적 DNS 등록 구성
  
네트워크 컨트롤러 클러스터 노드가 같은 서브넷 또는 다른 서브넷에 배포할 수 있습니다. 

>[!NOTE]
>네트워크 컨트롤러 노드 같은 서브넷에 인 경우 네트워크 컨트롤러용 동적 DNS 등록 구성 하는 경우 네트워크 컨트롤러 나머지 IP 주소를 제공 해야 합니다. 다른 서브넷 노드 인 때 동적 DNS 등록 구성 네트워크 컨트롤러 나머지 DNS 이름을 제공 해야 합니다.

네트워크 컨트롤러 노드가 다른 서브넷의 경우 다음과 같은 추가 DNS 구성을 수행 해야 합니다.

- 네트워크 컨트롤러 DNS 이름을 배포 프로세스 동안 만들기

- DNS 서버에서 DNS 컨트롤러 DNS 네트워크 이름에 대 한 업데이트를 구성

- 네트워크 컨트롤러 노드로 DNS 동적 업데이트를 제한

다음 절차 DNS 동적 업데이트를 구성 하 고 네트워크 컨트롤러 이름 레코드의 동적 업데이트 제한에 사용할 수 있습니다.

> [!NOTE]
> 회원 **도메인 관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.
  
#### <a name="to-allow-dns-dynamic-updates-for-a-zone"></a>영역에 대 한 동적 업데이트 DNS 허용 하려면

1. DNS 관리자를 엽니다.

2. 콘솔 트리에서 해당 영역을 마우스 오른쪽 단추로 클릭 한 다음 **속성**합니다. 표준 시간대의 **속성** 대화 상자를 엽니다.

3. 에 **일반** 탭, 영역 종류 하나 인지 확인 **기본** 또는 **Active Directory 통합**합니다.

4. **동적 업데이트**, 되어 있는지 확인 **만 보안** 을 선택 합니다. 선택 하지 않은 경우 변경 하는 가치에 **동적 업데이트** 에 **만 보안**을 차례로 클릭 하 고 **확인**합니다.

#### <a name="to-configure-dns-zone-security-permissions-for-network-controller-nodes"></a>네트워크 컨트롤러 노드 영역 보안 권한을 DNS 구성 하려면

1.  DNS 관리자를 엽니다.

2.  콘솔 트리에서 해당 영역을 마우스 오른쪽 단추로 클릭 한 다음 **속성**합니다. 표준 시간대의 **속성** 대화 상자를 엽니다.

3.  클릭 하 고 **보안** 탭을 클릭 한 다음 **고급**합니다. **고급 보안 설정을** 대화 상자를 엽니다.

4. **고급 보안 설정을**, 클릭 **추가**합니다. **권한 항목** 대화 상자를 엽니다.
  
5. 클릭 **주체 선택**합니다. **사용자, 컴퓨터, 계정 서비스, 또는 그룹 선택** 대화 상자를 엽니다.

6. 에 **사용자, 컴퓨터, 계정 서비스, 또는 그룹 선택** 대화 상자를 클릭 **개체 유형**합니다. **개체 유형** 대화 상자를 엽니다. 

7. **개체 유형**선택 **컴퓨터**을 차례로 클릭 하 고 **확인**합니다.

8. 에 **사용자, 컴퓨터, 계정 서비스, 또는 그룹 선택** 대화 상자를 배포에서 네트워크 컨트롤러 노드 중 하나 NetBIOS 이름을 입력 하 고 클릭 한 다음 **확인**합니다.

9. **권한 항목**, 값을 확인 하는 **종류** 는 **허용**, 값 **에 적용 됩니다** 는 **이 개체와 하위 모든 개체**합니다.
  
10. 사용 권한에서 선택 **모든 속성 쓰기** 및 **삭제**을 차례로 클릭 하 고 **확인**합니다.

11. 단계를 반복 **5** 통해 **10** 모든 컴퓨터 및 네트워크 컨트롤러 클러스터의 Vm 합니다.

자세한 내용은 참조 [소프트웨어 정의 네트워크 Infrastructure 계획](https://technet.microsoft.com/windows-server-docs/networking/sdn/plan/plan-a-software-defined-network-infrastructure)합니다.
