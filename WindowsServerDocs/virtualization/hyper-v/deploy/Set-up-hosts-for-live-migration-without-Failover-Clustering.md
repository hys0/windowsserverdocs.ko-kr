---
title: 장애 조치 클러스터링이 없는 실시간 마이그레이션에 대 한 호스트 설정
description: 클러스터 되지 않은 환경에서 실시간 마이그레이션을 설정 하는 방법에 대 한 지침을 제공 합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: b5e3c405-cb76-4ff2-8042-c2284448c435
author: kbdazure
ms.author: kathydav
ms.date: 9/30/2016
ms.openlocfilehash: 2c2f671bf59e95de2604c91944fab3d65f82410e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860886"
---
# <a name="set-up-hosts-for-live-migration-without-failover-clustering"></a>장애 조치 클러스터링이 없는 실시간 마이그레이션에 대 한 호스트 설정

>적용 대상: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

이 문서는 서로 마이그레이션을 실시간 수행 수 있도록 클러스터 아닌 호스트에 설정 하는 방법을 보여줍니다. Hyper-v를 설치할 때 실시간 마이그레이션 설정 하지 않은 경우 또는 설정을 변경 하려는 경우 다음이 지침을 사용 합니다. 클러스터 된 호스트를 설정 하려면 장애 조치 클러스터링에 대 한 도구를 사용 합니다.

## <a name="requirements-for-setting-up-live-migration"></a>실시간 마이그레이션 설정에 대 한 요구 사항

실시간 마이그레이션용 클러스터 되지 않은 호스트를 설정 하려면 다음이 필요 합니다.

-  다양 한 단계를 수행할 수 있는 권한이 있는 사용자 계정입니다. 제한 된 위임을 구성 하는 경우가 아니면이 요구 사항을 충족 하는 로컬 Hyper-v Administrators 그룹 또는 소스와 대상 컴퓨터에서 Administrators 그룹의 구성원 이어야 합니다. 도메인 관리자 그룹의 구성원은 제한 된 위임을 구성 하는 데 필요한입니다.

- 원본 및 대상 서버에 Windows Server 2016 또는 Windows Server 2012 r 2의 Hyper-v 역할이 설치 되어 있어야 합니다. 가상 컴퓨터가 버전 5 이상인 경우 Windows Server 2016 및 Windows Server 2012 r 2를 실행 하는 호스트 간에 실시간 마이그레이션을 수행할 수 있습니다. <br>버전 업그레이드 지침은 [windows 10 또는 Windows Server 2016에서 hyper-v의 가상 머신 버전 업그레이드](Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)를 참조 하세요. 설치 지침은 [Windows Server에 hyper-v 역할 설치](../get-started/Install-the-Hyper-V-role-on-Windows-Server.md)를 참조 하세요.

- 동일한 Active Directory 도메인에 속하거나 서로 신뢰 하는 도메인에 속해 있는 원본 및 대상 컴퓨터.
- 도구는 원본 또는 대상 서버에 설치 되어 있지 않으면 Windows Server 2016 또는 Windows 10을 실행 하는 컴퓨터에 설치 된 Hyper-v 관리 도구는 서버에서 도구를 실행 합니다.

## <a name="consider-options-for-authentication-and-networking"></a>인증 및 네트워킹에 대 한 옵션을 고려

다음을 설정 하려면 어떻게 하는 것이 좋습니다.

-  **인증**: 프로토콜에서 원본 및 대상 서버 간의 실시간 마이그레이션 트래픽을 인증 하는 데 사용 됩니다. 선택 하는 실시간 마이그레이션을 시작 하기 전에 원본 서버에 로그온 해야 하는지 여부를 결정 합니다.
   - Kerberos 사용 하면 서버에 로그인 할 필요가 있지만 설정 하도록 제한 된 위임이 필요 합니다. 자세한 내용은 아래를 참조 하십시오.
   - CredSSP 하면 제한 된 위임을 구성 하지 않아도 되지만 원본 서버에 로그인 할 필요 합니다. 원격 데스크톱 세션 또는 원격 Windows PowerShell 세션을 사용 하는 로컬 콘솔 세션을 통해이 수행할 수 있습니다.

      CredSPP 명확 하지 않을 수 있는 상황에 대 한 로그인 해야 합니다. 예를 들어 가상 컴퓨터를 TestServer02을 이동한 후에 가상 컴퓨터를 다시 TestServer01를 이동 하려면 TestServer01에 로그인 할 TestServer01에 가상 컴퓨터를 다시 이동 하기 전에 TestServer02에 로그인 할 필요 합니다. 이렇게 하지 않으면 인증 시도가 실패 하면 오류가 발생 하 고 다음 메시지가 표시 됩니다.

      "마이그레이션 원본에서 가상 컴퓨터 마이그레이션 작업이 실패 했습니다.
      호스트와의 연결을 설정 하지 못했습니다 *컴퓨터 이름*: 자격 증명이 없는 0x8009030E 보안 패키지에서 사용할 수 있습니다. "

-   **성능**: 않는 것이 합리적 성능 옵션을 구성 하 시겠습니까? 이러한 옵션 수 네트워크 및 CPU 사용량을 줄일 뿐 실시간 마이그레이션 속도 더 빠르게 확인 하십시오. 요구 사항 및 인프라를와 고려 결정 하려면 서로 다른 구성을 테스트 합니다. 옵션 2 단계 후에 설명 되어 있습니다.

-  **기본 설정 네트워크**:는 사용 가능한 모든 네트워크를 통해 실시간 마이그레이션 트래픽을 허용 하거나 특정 네트워크로 트래픽을 격리할? 보안을 유지하는 가장 좋은 방법으로 실시간 마이그레이션 트래픽은 네트워크를 통해 전송될 때 암호화되지 않으므로 트래픽을 신뢰할 수 있는 프라이빗 네트워크로 격리하는 것이 좋습니다. 네트워크 격리는 물리적으로 떨어진 네트워크나 VLAN 등의 또 다른 신뢰할 수 있는 네트워킹 기술을 통해 구현할 수 있습니다.

## <a name="step-1-configure-constrained-delegation-optional"></a><a name="BKMK_Step1"></a>1 단계: 제한 된 위임 구성 (선택 사항)
실시간 마이그레이션 트래픽을 인증에 Kerberos를 사용 하 여 했으면 Domain Administrators 그룹의 구성원 인 계정을 사용 하는 제한 된 위임을 구성 합니다.

### <a name="use-the-users-and-computers-snap-in-to-configure-constrained-delegation"></a>사용자 및 컴퓨터 스냅인을 사용 하 여 제한 된 위임 구성

1.  Active Directory 사용자 및 컴퓨터 스냅인을 엽니다. (선택 하지 않은 경우 서버 관리자에서 서버를 선택, 클릭 **도구** >> **Active Directory 사용자 및 컴퓨터**).

2.  탐색 창에서 **Active Directory 사용자 및 컴퓨터**, 도메인을 선택 하 고 두 번 클릭 하 여 **컴퓨터** 폴더입니다.

3.  **컴퓨터** 폴더를 원본 서버의 컴퓨터 계정을 마우스 오른쪽 단추로 클릭 **속성**합니다.

4.  **속성**, 클릭 하 고 **위임** 탭 합니다.

5.  위임 탭에서 **지정한 서비스에 대 한 위임용 으로만이 컴퓨터 트러스트** 를 선택한 다음 **모든 인증 프로토콜 사용**을 선택 합니다.

6.  **추가**를 클릭합니다.

7.  **서비스 추가**, 를 클릭 하 여 **사용자 또는 컴퓨터**합니다.

8.  **사용자 또는 컴퓨터 선택**, 대상 서버의 이름을 입력 합니다. 클릭 **이름 확인** 를 확인 한 다음 클릭 **확인**합니다.

9. **서비스 추가**, 사용 가능한 서비스 목록에서 다음을 수행 하 고 클릭, **확인**:

    -   가상 컴퓨터 저장소를 이동하려면 **cifs**를 선택합니다. 이동 하려는 가상 컴퓨터와 함께 스토리지도 가상 컴퓨터의 스토리지만 이동 하려는 경우 처럼이 소프트웨어가 필요 합니다. 서버가 Hyper-V용 SMB 스토리지를 사용하도록 구성된 경우 이미 이 선택 사항이 선택되어 있습니다.

    -   가상 컴퓨터를 이동하려면 **Microsoft 가상 시스템 마이그레이션 서비스**를 선택합니다.

10. 속성 대화 상자의 **위임** 탭에서, 이전 단계에서 선택한 서비스가 위임된 자격 증명을 제공할 수 있는 대상 컴퓨터에 대한 서비스로 나열되어 있는지 확인합니다. **확인**을 클릭합니다.

11. **Computers** 폴더에서 대상 서버의 컴퓨터 계정을 선택하고 프로세스를 반복합니다. **사용자 또는 컴퓨터 선택** 대화 상자에서 원본 서버의 이름을 지정해야 합니다.

둘 중 발생 한 후 구성 변경 내용을 적용 합니다.

  -  Hyper-v를 실행 하는 서버에 로그인 하는 도메인 컨트롤러에 변경 내용이 복제 됩니다.
  -  도메인 컨트롤러에서 새 Kerberos 티켓을 발급 합니다.

## <a name="step-2-set-up-the-source-and-destination-computers-for-live-migration"></a><a name="BKMK_Step2"></a>2 단계: 실시간 마이그레이션을 위한 원본 및 대상 컴퓨터 설정
이 단계에서는 인증 및 네트워킹에 대 한 옵션을 선택 합니다. 보안 모범 사례로, 위에서 설명한 대로 실시간 마이그레이션 트래픽에 사용할 특정 네트워크를 선택 하는 것이 좋습니다. 또한이 단계는 성능 옵션을 선택 하는 방법을 보여줍니다.

### <a name="use-hyper-v-manager-to-set-up-the-source-and-destination-computers-for-live-migration"></a>Hyper-v 관리자를 사용 하 여 실시간 마이그레이션 위한 원본 및 대상 컴퓨터를 설정 하려면

1.  Hyper-V 관리자를 엽니다. (서버 관리자에서 클릭 **도구** >>**Hyper-v 관리자**.)

2.  탐색 창에서 서버 중 하나를 선택 합니다. (이 나열 되어 있지 않으면 단추로 **Hyper-v 관리자**, 클릭 **서버에 연결**, 서버 이름을 입력 하 고 클릭 **확인**합니다. 서버를 더 추가 반복 합니다.)

3.  에 **작업** 창에서 클릭 **Hyper-v 설정** >>**실시간 마이그레이션**합니다.

4.  **실시간 마이그레이션** 창에서 **들어오고 나가는 실시간 마이그레이션 사용**을 선택합니다.

5.  아래에서 **동시 실시간 마이그레이션**, 2의 기본값을 사용 하지 않으려는 경우 다른 숫자를 지정 합니다.

6.  특정 네트워크 연결을 사용하여 실시간 마이그레이션 트래픽을 수용하려는 경우 **들어오는 실시간 마이그레이션** 아래에서 **추가**를 클릭하여 IP 주소 정보를 입력합니다. 그렇지 않은 경우, **사용 가능한 모든 네트워크를 실시간 마이그레이션에 사용**을 클릭합니다. **확인**을 클릭합니다.

7.  Kerberos 및 성능 옵션을 선택 하려면 확장 **실시간 마이그레이션** 선택한 다음 **고급 기능**합니다.

    - 아래에서 제한 된 위임을 구성 하는 경우 **인증 프로토콜**, 선택, **Kerberos**합니다.
    - 아래에서 **성능 옵션**, 세부 정보를 검토 하 고 환경에 적합 한 경우 다른 옵션을 선택 합니다.

8. **확인**을 클릭합니다.

9. Hyper-v 관리자에서 다른 서버를 선택 하 고 단계를 반복 합니다.

### <a name="use-windows-powershell-to-set-up-the-source-and-destination-computers-for-live-migration"></a>Windows PowerShell을 사용 하 여 실시간 마이그레이션 위한 원본 및 대상 컴퓨터를 설정 하려면

클러스터 되지 않은 호스트에서 실시간 마이그레이션을 구성 하는 데 사용할 수 있는 세 가지 cmdlet: [Enable-vmmigration](https://technet.microsoft.com/library/hh848544.aspx), [Set-vmmigrationnetwork](https://technet.microsoft.com/library/hh848467.aspx), 및 [Set-vmhost](https://technet.microsoft.com/library/hh848524.aspx)합니다. 이 예제에서는 세 가지 모두를 사용 하 여 하 고 다음 작업을 수행 합니다.
  - 로컬 호스트에서 실시간 마이그레이션을 구성합니다
  - 특정 네트워크 에서만 들어오는 마이그레이션 트래픽을 허용합니다
  - 인증 프로토콜로 Kerberos를 선택합니다.

각 행은 별개의 명령을 나타냅니다.

```PowerShell
PS C:\> Enable-VMMigration

PS C:\> Set-VMMigrationNetwork 192.168.10.1

PS C:\> Set-VMHost -VirtualMachineMigrationAuthenticationType Kerberos
```

또한 Set-vmhost 성능 옵션 (및 다른 많은 호스트 설정)를 선택할 수 있습니다. 예를 들어 SMB 선택 상태로 두려면 CredSSP의 기본값으로 설정 하는 인증 프로토콜를 입력 합니다.

```PowerShell
PS C:\> Set-VMHost -VirtualMachineMigrationPerformanceOption SMB
```

이 표에서 성능 옵션이 작동 하는 방법을 설명 합니다.

|옵션|설명|
|----------|---------------|
    |TCP/IP|TCP/IP 연결을 통해 대상 서버에 가상 컴퓨터의 메모리를 복사합니다.|
    |압축|TCP/IP 연결을 통해 대상 서버로 복사 하기 전에 가상 컴퓨터의 메모리 내용이 압축 합니다. **참고:** 이것이 **기본** 설정 합니다.|
    |SMB|SMB 3.0 연결을 통해 대상 서버에 가상 컴퓨터의 메모리를 복사합니다.<p>-원본 및 대상 서버에서 네트워크 어댑터는 원격 직접 메모리 액세스 (RDMA) 기능이 사용 하도록 설정 하는 경우 SMB 다이렉트가 사용 됩니다.<br />-SMB 다중 채널은 자동으로 감지 하 고 적절 한 SMB 다중 채널 구성이 식별 된 다중 연결 사용 합니다.<p>자세한 내용은 [SMB 다이렉트를 사용한 파일 서버의 성능 향상](https://technet.microsoft.com/library/jj134210(WS.11).aspx)을 참조하십시오.|

 ## <a name="next-steps"></a>다음 단계

 호스트를 설정 하면 실시간 마이그레이션을 수행 준비가 된 것입니다. 자세한 내용은 [장애 조치 클러스터링이 없는 실시간 마이그레이션을 사용 하 여 가상 컴퓨터를 이동 하려면](../manage/Use-live-migration-without-Failover-Clustering-to-move-a-virtual-machine.md)합니다.
