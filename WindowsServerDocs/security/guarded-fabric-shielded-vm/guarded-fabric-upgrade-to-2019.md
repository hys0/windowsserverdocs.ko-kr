---
title: Windows Server 2019로 보호된 패브릭 업그레이드
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 11/21/2018
ms.openlocfilehash: 50e35939031a74173fb031cf963af97bf8bb6dba
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856356"
---
# <a name="upgrade-a-guarded-fabric-to-windows-server-2019"></a>Windows Server 2019로 보호된 패브릭 업그레이드

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

이 문서에서는 Windows Server 2016, Windows Server 버전 1709 또는 Windows Server 버전 1803에서 windows server 2019로 기존의 보호 된 패브릭을 업그레이드 하는 데 필요한 단계를 설명 합니다.

## <a name="whats-new-in-windows-server-2019"></a>Windows Server 2019의 새로운 기능

Windows Server 2019에서 보호 된 패브릭을 실행 하는 경우 다음과 같은 여러 가지 새로운 기능을 활용할 수 있습니다.

**호스트 키 증명** 은 최신 증명 모드 이며, hyper-v 호스트에 tpm 증명에 사용할 수 있는 tpm 2.0 장치가 없을 때 보호 된 vm을 쉽게 실행할 수 있도록 설계 되었습니다. 호스트 키 증명은 키 쌍을 사용 하 여 HGS로 호스트를 인증 하 고, 호스트에서 Active Directory 도메인에 가입 해야 하는 요구 사항을 제거 하 고, HGS와 회사 포리스트 간에 AD 트러스트를 제거 하 고, 열려 있는 방화벽 포트의 수를 줄여 줍니다. 호스트 키 증명은 Windows Server 2019에서 더 이상 사용 되지 않는 Active Directory 증명을 대체 합니다.

**V2 증명 버전** -나중에 호스트 키 증명 및 새로운 기능을 지원 하기 위해 HGS로 버전 관리를 도입 했습니다. Windows Server 2019에 HGS를 새로 설치 하면 v2 증명을 사용 하는 서버가 생성 됩니다. 즉, Windows server 2019 호스트에 대 한 호스트 키 증명을 지원 하 고 Windows Server 2016의 v1 호스트를 계속 지원할 수 있습니다. 2019로의 현재 위치 업그레이드는 수동으로 v2를 사용 하도록 설정할 때까지 v1 버전으로 유지 됩니다. 이제 대부분의 cmdlet에는 레거시 또는 최신 증명 정책을 사용 하려는 경우 지정할 수 있는-HgsVersion 매개 변수가 있습니다.

**Linux 차폐 vm에 대 한 지원** -Windows Server 2019를 실행 하는 hyper-v 호스트는 Linux 차폐 vm을 실행할 수 있습니다. Linux 차폐 Vm은 Windows Server 버전 1709 이후 출시 되었지만 Windows Server 2019은이를 지원 하기 위한 첫 장기 서비스 채널 릴리스입니다.

**지점 개선 사항** -hyper-v 호스트의 오프 라인 보호 된 vm 및 대체 구성에 대 한 지원을 통해 지점에서 보호 된 vm을 보다 쉽게 실행할 수 있습니다.

**TPM 호스트 바인딩** -보호 된 VM이 생성 된 첫 번째 호스트 에서만 실행 되도록 하는 가장 안전한 워크 로드의 경우, 이제는 호스트의 TPM을 사용 하 여 VM을 해당 호스트에 바인딩할 수 있습니다. 이는 호스트 간에 마이그레이션해야 하는 일반 데이터 센터 작업 보다는 권한 있는 액세스 워크스테이션과 지점에 가장 적합 합니다.

## <a name="compatibility-matrix"></a>호환성 매트릭스

보호 된 패브릭을 Windows Server 2019로 업그레이드 하기 전에 다음 호환성 매트릭스를 검토 하 여 구성이 지원 되는지 확인 합니다.

|  | WS2016 HGS | WS2019 HGS|
|---|---|---|
|**WS2016 Hyper-v 호스트** | 지원함 | 지원 됨<sup>1</sup>|
|**WS2019 Hyper-v 호스트** | 지원 되지 않는<sup>2</sup> | 지원함|

<sup>1</sup> windows server 2016 호스트는 v1 증명 프로토콜을 사용 하 여 windows SERVER 2019 HGS 서버에 대해서만 증명할 수 있습니다. 호스트 키 증명을 비롯 한 v2 증명 프로토콜에서 독점적으로 사용할 수 있는 새로운 기능은 Windows Server 2016 호스트에서 지원 되지 않습니다.

<sup>2</sup> MICROSOFT에서는 TPM 증명을 사용 하는 windows server 2019 호스트가 windows SERVER 2016 HGS 서버에 대해 성공적으로 증명 수 없도록 하는 문제를 알고 있습니다. 이러한 제한 사항은 Windows Server 2016에 대 한 향후 업데이트에서 해결 될 예정입니다.

## <a name="upgrade-hgs-to-windows-server-2019"></a>Windows Server 2019에 대 한 HGS 업그레이드

Hyper-v 호스트를 업그레이드 하기 전에 windows server 2016 또는 2019를 실행 하는 모든 호스트가 성공적으로 증명을 계속 증명할 수 있도록 하려면 먼저 HGS 클러스터를 Windows Server 2019로 업그레이드 하는 것이 좋습니다.

HGS 클러스터를 업그레이드 하는 경우 업그레이드 하는 동안 클러스터에서 한 노드를 일시적으로 제거 해야 합니다. 이렇게 하면 클러스터의 용량이 부족 하 여 Hyper-v 호스트의 요청에 응답 하 고, 테 넌 트에 대 한 응답 시간이 느리거나 서비스 중단이 발생할 수 있습니다. HGS 서버를 업그레이드 하기 전에 증명 및 키 릴리스 요청을 처리할 수 있는 충분 한 용량이 있는지 확인 합니다.

HGS 클러스터를 업그레이드 하려면 클러스터의 각 노드에서 한 번에 하나의 노드만 다음 단계를 수행 합니다.

1.  관리자 권한 PowerShell 프롬프트에서 `Clear-HgsServer`를 실행 하 여 클러스터에서 HGS 서버를 제거 합니다. 이 cmdlet은 장애 조치 (failover) 클러스터에서 HGS 복제 저장소, HGS 웹 사이트 및 노드를 제거 합니다.
2.  HGS 서버가 도메인 컨트롤러 (기본 구성) 인 경우 OS 업그레이드를 위해 도메인을 준비 하려면 업그레이드 되는 첫 번째 노드에서 `adprep /forestprep` 및 `adprep /domainprep`를 실행 해야 합니다. 자세한 내용은 [Active Directory Domain Services 업그레이드 설명서](https://docs.microsoft.com/windows-server/identity/ad-ds/deploy/upgrade-domain-controllers#supported-in-place-upgrade-paths) 를 참조 하세요.
3.  Windows Server 2019로 [전체 업그레이드](../../get-started-19/install-upgrade-migrate-19.md) 를 수행 합니다.
4.  [HgsServer](guarded-fabric-configure-additional-hgs-nodes.md) 를 실행 하 여 노드를 클러스터에 다시 가입 시킵니다.

모든 노드가 Windows Server 2019로 업그레이드 된 후에는 선택적으로 HGS 버전을 v2로 업그레이드 하 여 호스트 키 증명 등의 새로운 기능을 지원할 수 있습니다.

```powershell
Set-HgsServerVersion  v2
```

## <a name="upgrade-hyper-v-hosts-to-windows-server-2019"></a>Hyper-v 호스트를 Windows Server 2019로 업그레이드

Hyper-v 호스트를 Windows Server 2019로 업그레이드 하기 전에 HGS 클러스터가 이미 Windows Server 2019로 업그레이드 되었으며 Hyper-v 서버에서 모든 Vm을 이동 했는지 확인 합니다.

1.  서버에서 Windows Defender 응용 프로그램 제어 코드 무결성 정책 (항상 TPM 증명을 사용 하는 경우)을 사용 하는 경우, 서버 업그레이드를 시도 하기 전에 정책이 감사 모드 또는 사용 안 함으로 설정 되어 있는지 확인 합니다. [WDAC 정책을 사용 하지 않도록 설정 하는 방법 알아보기](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/disable-windows-defender-application-control-policies)
2.  [Windows server 업그레이드 콘텐츠의](../../upgrade/upgrade-overview.md) 지침에 따라 호스트를 windows server 2019로 업그레이드 합니다. Hyper-v 호스트가 장애 조치 (Failover) 클러스터의 일부인 경우 [클러스터 운영 체제 롤링 업그레이드](../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md)를 사용 하는 것이 좋습니다.
3.  업그레이드 전에 활성화 한 경우 Windows Defender 응용 프로그램 제어 정책을 [테스트 하 고 다시 사용 하도록 설정](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/audit-windows-defender-application-control-policies) 합니다.
4.  `Get-HgsClientConfiguration`를 실행 하 여 **Ishostguarded = True**인지 확인 합니다. 즉, 호스트가 HGS 서버와 증명을 성공적으로 전달 하 고 있음을 의미 합니다.
5.  TPM 증명을 사용 하는 경우 증명을 전달 하기 위해 업그레이드 후 [tpm 기준 또는 코드 무결성 정책을 다시 캡처해야](guarded-fabric-add-host-information-for-tpm-trusted-attestation.md) 할 수 있습니다.
6.  호스트에서 보호 된 Vm 실행을 다시 시작 합니다.

## <a name="switch-to-host-key-attestation"></a>호스트 키 증명으로 전환

현재 Active Directory 기반 증명을 실행 중이 고 호스트 키 증명으로 업그레이드 하려는 경우 다음 단계를 수행 합니다. Active Directory 기반 증명은 Windows Server 2019에서 더 이상 사용 되지 않으며 이후 릴리스에서 제거 될 수 있습니다.

1.  다음 명령을 실행 하 여 HGS 서버가 v2 증명 모드에서 작동 하는지 확인 합니다. 기존 v1 호스트는 HGS 서버가 v2로 업그레이드 된 경우에도 계속 증명 합니다.

    ```powershell
    Set-HgsServerVersion v2
    ```

2.  각 Hyper-v 호스트에서 [호스트 키를 생성](guarded-fabric-create-host-key.md) 하 고 HGS에 등록 합니다. HGS는 계속 Active Directory 모드에서 작동 하기 때문에 새 호스트 키가 즉시 적용 되지 않는 경고를 받게 됩니다. 모든 호스트가 호스트 키를 정상적으로 증명할 수 있을 때까지 호스트 키 모드로 변경 하지 않기 때문에 의도적인 것입니다.

3.  호스트 키가 모든 호스트에 등록 되 면 호스트 키 증명 모드를 사용 하도록 HGS를 구성할 수 있습니다.

    ```powershell
    Set-HgsServer -TrustHostKey
    ```

    호스트 키 모드에서 문제가 발생 하 여 Active Directory 기반 증명으로 다시 되돌려야 하는 경우 HGS에서 다음 명령을 실행 합니다.

    ```powershell
    Set-HgsServer -TrustActiveDirectory
    ```