---
title: Windows Server 2019로 보호된 패브릭 업그레이드
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 11/21/2018
ms.openlocfilehash: 274bdf027947ffb6fe807d4acd0a3b2174c20e28
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867454"
---
# <a name="upgrade-a-guarded-fabric-to-windows-server-2019"></a>Windows Server 2019로 보호된 패브릭 업그레이드

> 적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

이 문서는 기존 보호 된 패브릭 Windows Server 2016, Windows Server 버전 1709 또는 Windows Server를 Windows Server 2019 버전 1803에서에서 업그레이드 하는 데 필요한 단계를 설명 합니다.

## <a name="whats-new-in-windows-server-2019"></a>Windows Server 2019의 새로운 기능

Windows Server 2019에서 보호 된 패브릭을 실행할 때 몇 가지 새로운 기능을 수행할 수 있습니다.

**키 증명 호스트** 쉽게 Hyper-v 호스트에 TPM 증명에 대 한 TPM 2.0 장치 사용할 수 없는 경우 보호 된 Vm을 실행할 수 있도록 설계 당사의 최신 증명 모드입니다. 호스트 키 증명 hgs에서 Active Directory 도메인에 조인할 수는 호스트에 대 한 요구 사항을 제거 HGS와 회사 포리스트 간에 AD 트러스트를 제거 하 고 방화벽 포트가 열려의 수를 줄이면 호스트 인증 키 쌍을 사용 합니다. 호스트 키 증명을 Windows Server 2019 되지 않는 Active Directory 증명을으로 바꿉니다.

**V2 증명 버전** -나중에 호스트 키 증명 및 새로운 기능을 지원 하도록 HGS 버전 관리 도입 했습니다. Windows Server 2019에서 HGS 새로 설치할 수 있습니다 Windows Server 2019 호스트에 대 한 호스트 키 증명을 지원 하 고 여전히 v1 호스트를 Windows Server 2016에서 지원 즉 v2 증명을 사용 하 여 서버에서 발생 합니다. 2019에 전체 업그레이드는 v2 수동으로 활성화할 때까지 버전 v1에서 유지 됩니다. 대부분의 cmdlet에는 이제 레거시 또는 최신 증명 정책을 사용 하려는 경우 지정할 수 있는-HgsVersion 매개 변수입니다.

**보호 된 Vm Linux에 대 한 지원을** -Windows Server 2019를 실행 하는 Hyper-v 호스트 수 실행 보호 된 Linux Vm입니다. 보호 된 Linux Vm Windows Server 버전 1709부터 제공 된, Windows Server 2019 릴리스입니다 첫 번째 장기 용어 서비스 채널 지원 합니다.

**분기 office 향상** -Hyper-v 호스트에서 오프 라인 보호 된 Vm 및 대체 (fallback) 구성에 대 한 지원을 통해 지점의 보호 된 Vm을 실행 하기 쉽도록 했습니다.

**TPM 호스트 바인딩** -호스트의 TPM을 사용 하 여 해당 호스트 VM 바인딩할 수 하려는 워크 로드를 생성 하지만 다른 있던 첫 번째 호스트에만 실행 되도록 보호 된 VM을 보호 하는 가장에 대 한 합니다. 이 호스트 간에 마이그레이션해야 하는 일반 데이터 센터 작업 보다는 권한 있는 액세스 워크스테이션 지점에 대 한 가장 사용 됩니다.

## <a name="compatibility-matrix"></a>호환성 매트릭스

Windows Server 2019로 보호 된 패브릭에 업그레이드 하기 전에 구성에 지원 되는 경우를 확인 하려면 다음 호환성 매트릭스를 검토 합니다.

|  | WS2016 HGS | WS2019 HGS|
|---|---|---|
|**WS2016 Hyper-v 호스트** | 지원됨 | 지원 되는<sup>1</sup>|
|**WS2019 Hyper-v 호스트** | 지원 되지 않는<sup>2</sup> | 지원됨|

<sup>1</sup> Windows Server 2016 호스트는 v1 증명 프로토콜을 사용 하 여 Windows Server 2019 HGS 서버에 대해만 증명할 수 있습니다. 호스트 키 증명을 포함 하 여 v2 증명 프로토콜을 단독으로 사용할 수 있는 새로운 기능 Windows Server 2016 호스트에 대 한 지원 되지 않습니다.

<sup>2</sup> Microsoft는 Windows Server 2016 HGS 서버에 대해 성공적으로 입증에서 TPM 증명을 사용 하 여 Windows Server 2019 호스트 방지 문제를 확인 합니다. 이 제한은 Windows Server 2016에 대 한 향후 업데이트에서 해결 될 예정입니다.

## <a name="upgrade-hgs-to-windows-server-2019"></a>HGS 2019 Windows 서버로 업그레이드

모든 호스트에 Windows Server 2016 또는 2019, 실행 되는지에 수에 계속을 성공적으로 입증 하기 위해 Hyper-v 호스트를 업그레이드 하기 전에 Windows Server 2019로 HGS 클러스터를 업그레이드 하는 것이 좋습니다.

HGS 클러스터 업그레이드를 일시적으로 하나의 클러스터에서 노드 제거는 한 번에 업그레이드 하는 동안 해야 합니다. 이 위해 Hyper-v 호스트에서 요청에 응답 하도록 클러스터의 용량 줄이고 테 넌 트에 대 한 느린 응답 시간 또는 서비스 중단이 발생할 수 있습니다. HGS 서버를 업그레이드 하기 전에 고 증명 키 해제 요청을 처리 하기에 충분 한 용량이 있는지 확인 합니다.

HGS 클러스터를 업그레이드 하려면 번에 하나의 노드 클러스터의 각 노드에서 다음 단계를 수행 합니다.

1.  HGS 서버를 실행 하 여 클러스터에서 제거 `Clear-HgsServer` 관리자 권한 PowerShell 프롬프트에서. 이 cmdlet에는 장애 조치 클러스터에서 HGS 복제 된 저장소, HGS 웹 사이트 및 노드 제거 됩니다.
2.  HGS 서버 도메인 컨트롤러 (기본 구성) 인 경우 실행 해야 합니다 `adprep /forestprep` 고 `adprep /domainprep` OS 업그레이드 도메인을 준비 하려면 업그레이드 되 고 첫 번째 노드에서 합니다. 참조를 [Active Directory Domain Services 업그레이드 설명서](https://docs.microsoft.com/windows-server/identity/ad-ds/deploy/upgrade-domain-controllers#supported-in-place-upgrade-paths) 자세한 내용은 합니다.
3.  수행을 [전체 업그레이드](../../get-started-19/install-upgrade-migrate-19.md) Windows Server 2019에 있습니다.
4.  실행 [Initialize HgsServer](guarded-fabric-configure-additional-hgs-nodes.md) 노드를 클러스터에 다시 가입 합니다.

모든 노드가 Windows Server 2019에 업그레이드 된 후 호스트 키 증명 같은 새 기능을 지원 하도록 v2를 필요에 따라 HGS 버전을 업그레이드할 수 있습니다.

```powershell
Set-HgsServerVersion  v2
```

## <a name="upgrade-hyper-v-hosts-to-windows-server-2019"></a>Windows Server 2019에 Hyper-v 호스트를 업그레이드 합니다.

Windows Server 2019 하기 위해 Hyper-v 호스트를 업그레이드 하기 전에 HGS 클러스터는 Windows Server 2019 이미 업그레이드 되 고 모든 Vm에서 Hyper-v 서버를 이동 했으므로 있는지 확인 합니다.

1.  Windows Defender 응용 프로그램 제어 코드 무결성 정책 서버의 (항상 경우 TPM 증명을 사용 하는 경우)를 사용 하는 경우 확인 정책이 감사 모드에는 서버를 업그레이드 하기 전에 사용 하지 않도록 설정 합니다. [WDAC 정책을 사용 하지 않도록 설정 하는 방법 알아보기](https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-defender-application-control/disable-windows-defender-application-control-policies)
2.  지침에 따라 합니다 [Windows Server 업그레이드 센터](http://aka.ms/upgradecenter) Windows Server 2019에 호스트를 업그레이드 합니다. Hyper-v 호스트 장애 조치 클러스터의 일부 이면 사용해를 [클러스터 운영 체제 롤링 업그레이드](../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md)합니다.
3.  [테스트 하 고 다시 사용 하도록 설정](https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-defender-application-control/audit-windows-defender-application-control-policies) 업그레이드 하기 전에 사용 하도록 설정 하나를 설치한 경우 Windows Defender 응용 프로그램 제어 정책.
4.  실행 `Get-HgsClientConfiguration` 경우 검사할 **IsHostGuarded = True**, 즉 호스트는 HGS 서버를 사용 하 여 증명 전달 성공적으로 합니다.
5.  TPM 증명을 사용 하는 경우 해야 [TPM 기준 또는 코드 무결성 정책을 다시 캡처하여](guarded-fabric-add-host-information-for-tpm-trusted-attestation.md) 증명을 전달 하려면 업그레이드 후 합니다.
6.  실행 시작 보호 된 Vm 호스트에서 다시!

## <a name="switch-to-host-key-attestation"></a>키 증명을 호스트 하는 스위치

Active Directory 기반 증명 현재 실행 중인 호스트 키 증명으로 업그레이드할 경우 다음 단계를 수행 합니다. 참고는 Active Directory 기반 증명 Windows Server 2019에 않으며 이후 릴리스에서 제거 될 수 있습니다.

1.  다음 명령을 실행 하 여 HGS 서버 v2 증명 모드에서 작동 하는지 확인 합니다. 기존 v1 호스트는 HGS 서버 v2로 업그레이드 하는 경우에 증명 계속 합니다.

    ```powershell
    Set-HgsServerVersion v2
    ```

2.  [호스트 키를 생성할](guarded-fabric-create-host-key.md) 각 Hyper-v 호스트 및 HGS에 등록 합니다. HGS Active Directory 모드로 작동, 때문에 새 호스트 키를 즉시 적용 되지 않았는지 경고를 받게 됩니다. 호스트 키를 사용 하 여 성공적으로 증명할 수 모든 호스트 될 때까지 호스트 키 모드를 변경 하지 않으려는 경우이 의도적입니다.

3.  모든 호스트에 대 한 호스트 키, 등록 되 면 호스트 키 증명 모드를 사용 하도록 HGS를 구성할 수 있습니다.

    ```powershell
    Set-HgsServer -TrustHostKey
    ```

    호스트 키 모드를 사용 하 여 문제를 실행 하 고 Active Directory 기반 증명으로 다시 되돌려야 HGS에서 다음 명령을 실행 합니다.

    ```powershell
    Set-HgsServer -TrustActiveDirectory
    ```