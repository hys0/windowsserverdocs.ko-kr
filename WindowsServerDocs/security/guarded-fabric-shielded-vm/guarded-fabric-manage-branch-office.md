---
title: 지점 고려 사항
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.openlocfilehash: 5a07553e6662fd79230d566ba2049c5e8997f4d6
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322505"
---
# <a name="branch-office-considerations"></a>지점 고려 사항

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), 

이 문서에서는 지점에서 보호 된 가상 컴퓨터를 실행 하기 위한 모범 사례 및 Hyper-v 호스트가 HGS에 대해 제한 된 연결을 사용 하는 기간을 가질 수 있는 기타 원격 시나리오를 설명 합니다.

## <a name="fallback-configuration"></a>대체 구성

Windows Server 버전 1709부터 기본 HGS가 응답 하지 않을 때 사용할 Hyper-v 호스트에서 호스트 보호자 서비스 Url의 추가 집합을 구성할 수 있습니다.
이렇게 하면 로컬 서버가 다운 된 경우 회사 데이터 센터의 HGS로 대체 하는 기능을 통해 기본 서버로 사용 되는 로컬 HGS 클러스터를 실행할 수 있습니다.

대체 (fallback) 옵션을 사용 하려면 두 개의 HGS 서버를 설정 해야 합니다. Windows Server 2019 또는 Windows Server 2016를 실행 하 고 동일한 클러스터 또는 다른 클러스터의 일부가 될 수 있습니다. 서로 다른 클러스터 인 경우 두 서버 간에 증명 정책이 동기화 되도록 운영 관행을 설정 하는 것이 좋습니다. 둘 다 Hyper-v 호스트에 보호 된 Vm을 실행 하는 데 필요한 권한을 올바르게 부여 하 고 보호 된 Vm을 시작 하는 데 필요한 주요 자료를 제공할 수 있어야 합니다. 두 클러스터 간에 공유 암호화 및 서명 인증서의 쌍을 갖도록 선택 하거나, 별도의 인증서를 사용 하 고, 보호 데이터 파일에서 보호자 (암호화/서명 인증서 쌍)를 둘 다 인증 하도록 HGS 차폐 VM을 구성할 수 있습니다.

그런 다음 Hyper-v 호스트를 Windows Server 버전 1709 또는 Windows Server 2019로 업그레이드 하 고 다음 명령을 실행 합니다.
```powershell
# Replace https://hgs.primary.com and https://hgs.backup.com with your own domain names and protocols
Set-HgsClientConfiguration -KeyProtectionServerUrl 'https://hgs.primary.com/KeyProtection' -AttestationServerUrl 'https://hgs.primary.com/Attestation' -FallbackKeyProtectionServerUrl 'https://hgs.backup.com/KeyProtection' -FallbackAttestationServerUrl 'https://hgs.backup.com/Attestation'
```

대체 (fallback) 서버 구성을 취소 하려면 대체 (fallback) 매개 변수를 모두 생략 하면 됩니다.
```powershell
Set-HgsClientConfiguration -KeyProtectionServerUrl 'https://hgs.primary.com/KeyProtection' -AttestationServerUrl 'https://hgs.primary.com/Attestation'
```

Hyper-v 호스트에서 주 서버와 대체 서버 모두에 증명을 전달 하려면 두 HGS 클러스터를 모두 사용 하 여 증명 정보가 최신 상태 인지 확인 해야 합니다.
또한 가상 컴퓨터의 TPM 암호를 해독 하는 데 사용 되는 인증서를 두 HGS 클러스터에서 모두 사용할 수 있어야 합니다.
서로 다른 인증서를 사용 하 여 각 HGS를 구성 하 고 둘 다를 신뢰 하도록 VM을 구성 하거나 두 HGS 클러스터에 공유 인증서 집합을 추가할 수 있습니다.

대체 Url을 사용 하 여 지점에서 HGS를 구성 하는 방법에 대 한 자세한 내용은 블로그 게시물 [Windows Server의 보호 된 vm에 대 한 지점 지원 개선, 버전 1709](https://blogs.technet.microsoft.com/datacentersecurity/2017/11/15/improved-branch-office-support-for-shielded-vms-in-windows-server-version-1709/)을 참조 하세요.


## <a name="offline-mode"></a>오프 라인 모드

오프 라인 모드에서는 Hyper-v 호스트의 보안 구성이 변경 되지 않은 한 HGS에 도달할 수 없는 경우 보호 된 VM을 켤 수 있습니다.
오프 라인 모드는 Hyper-v 호스트에서 VM TPM 키 보호기의 특수 버전을 캐시 하는 방식으로 작동 합니다.
키 보호기는 가상화 기반 보안 id 키를 사용 하 여 호스트의 현재 보안 구성으로 암호화 됩니다.
호스트가 HGS와 통신할 수 없고 해당 보안 구성이 변경 되지 않은 경우 캐시 된 키 보호기를 사용 하 여 보호 된 VM을 시작할 수 있습니다.
새 코드 무결성 정책 적용 또는 보안 부팅을 사용 하지 않도록 설정 하는 등 시스템에서 보안 설정이 변경 되 면 캐시 된 키 보호기가 무효화 되 고, 보호 된 Vm을 다시 오프 라인으로 시작 하기 전에 HGS를 사용 하 여 호스트를 증명 해야 합니다.

오프 라인 모드를 사용 하려면 호스트 보호자 서비스 클러스터와 Hyper-v 호스트 모두에 Windows Server Insider preview 빌드 17609 이상이 필요 합니다.
이는 기본적으로 사용 하지 않도록 설정 된 HGS의 정책에 의해 제어 됩니다.
오프 라인 모드에 대 한 지원을 사용 하도록 설정 하려면 HGS 노드에서 다음 명령을 실행 합니다.

```powershell
Set-HgsKeyProtectionConfiguration -AllowKeyMaterialCaching:$true
```

캐시할 수 있는 키 보호기는 보호 된 각 VM 마다 고유 하므로,이 설정이 HGS에서 사용 하도록 설정 된 후에는 (다시 시작 하지 않음) 완전히 종료 하 고 보호 된 키 보호기를 얻기 위해 보호 된 Vm을 시작 해야 합니다.
보호 된 VM이 이전 버전의 Windows Server를 실행 하는 Hyper-v 호스트로 마이그레이션하거나 이전 버전의 HGS에서 새 키 보호기를 가져오는 경우 오프 라인 모드에서 자동으로 시작 될 수 없지만, HGS에 대 한 액세스를 사용할 수 있는 경우 온라인 모드에서 계속 실행할 수 있습니다. 되지.
