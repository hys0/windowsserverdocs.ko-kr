---
title: 분기 Office 고려 사항
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.openlocfilehash: d93c37227af1eb62368fbcd4ec5d6a48374b45ff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877064"
---
# <a name="branch-office-considerations"></a>지점 고려 사항

> 적용 대상: Windows Server 2019, Windows Server (반기 채널) 

이 문서에서는 Hyper-v 호스트 HGS에 대 한 연결 제한 시간이 있을 수 있는 실행 지점에서 보호 된 가상 컴퓨터 및 기타 원격 시나리오에 대 한 모범 사례를 설명 합니다.

## <a name="fallback-configuration"></a>대체 (fallback) 구성

Windows Server 버전 1709부터 구성할 수 있습니다 추가 집합이 호스트 보호자 서비스 Url 사용에 대 한 Hyper-v 호스트에서 때 주 HGS가 응답 하지 않습니다.
이 로컬 서버 종료 된 경우 회사 데이터 센터의 HGS로 대체 하는 기능을 사용 하 여 성능 향상을 위해 기본 서버로 사용 되는 로컬 HGS 클러스터를 실행할 수 있습니다.

대체 (fallback) 옵션을 사용 하려면 두 HGS 서버를 설정 해야 합니다. Windows Server 2019를 실행할 수 있습니다 또는 Windows Server 2016 및 중 하나에 동일 하거나 다른 클러스터의 일부 여야 합니다. 이들이 서로 다른 클러스터, 운영 방침 증명 정책을 확인 하는 두 서버 간에 동기화를 설정 하려고 합니다. 모두 올바르게 보호 된 Vm을 실행 하 고 보호 된 Vm을 시작 하는 데 필요한 키 자료를 Hyper-v 호스트를 승인할 수 되도록 해야 합니다. 공유 암호화 및 서명 인증서를 두 클러스터의 쌍 또는 별도 인증서를 사용 하 고 구성 하도록 선택할 수 있습니다 HGS 차폐 VM 실딩 데이터에서 모두 보호자 (암호화/서명 인증서 쌍) 권한을 부여 하려면 파일입니다.

그런 다음 Windows Server 버전 1709 또는 Windows Server 2019 하기 위해 Hyper-v 호스트를 업그레이드 하 고 명령을 실행 합니다.
```powershell
# Replace https://hgs.primary.com and https://hgs.backup.com with your own domain names and protocols
Set-HgsClientConfiguration -KeyProtectionServerUrl 'https://hgs.primary.com/KeyProtection' -AttestationServerUrl 'https://hgs.primary.com/Attestation' -FallbackKeyProtectionServerUrl 'https://hgs.backup.com/KeyProtection' -FallbackAttestationServerUrl 'https://hgs.backup.com/Attestation'
```

대체 (fallback) 서버를 구성 취소를 모두 대체 매개 변수를 생략 하면 됩니다.
```powershell
Set-HgsClientConfiguration -KeyProtectionServerUrl 'https://hgs.primary.com/KeyProtection' -AttestationServerUrl 'https://hgs.primary.com/Attestation'
```

Hyper-v 호스트가 기본 및 대체 (fallback) 서버를 사용 하 여 증명을 전달 하는 데 사용할 순서로 증명 정보 모두 HGS 클러스터를 사용 하 여 최신 상태 인지 확인 해야 합니다.
또한 가상 컴퓨터의 TPM을 암호 해독에 사용 된 인증서를 HGS 클러스터 모두에서 사용할 수 있도록 해야 합니다.
다른 인증서를 사용 하 여 각 HGS를 구성 하 고 둘 다를 신뢰 하도록 VM을 구성 하거나 HGS 클러스터 모두에 인증서 집합을 공유를 추가할 수 있습니다.

HGS 대체 Url을 사용 하 여 지점에 구성 하는 방법에 대 한 자세한 내용은 블로그 게시물을 참조 하세요 [향상 된 Windows Server 버전 1709에서에서 보호 된 Vm에 대 한 분기 office 지원](https://blogs.technet.microsoft.com/datacentersecurity/2017/11/15/improved-branch-office-support-for-shielded-vms-in-windows-server-version-1709/)합니다.


## <a name="offline-mode"></a>오프 라인 모드

오프 라인 모드를 켜려면 HGS에 연결할 수 없는 경우 Hyper-v 호스트의 보안 구성이 변경 되지 않았는지 하기만 보호 된 VM 수 있습니다.
오프 라인 모드에서 Hyper-v 호스트에서 VM TPM 키 보호기의 특수 버전을 캐시 하 여 작동 합니다.
키 보호기 (가상화 기반 보안 id 키를 사용 하 여) 하는 호스트의 현재 보안 구성에 암호화 됩니다.
호스트를 HGS와 통신할 수 없는 경우 해당 보안 구성을 변경 되지 않은 보호 된 VM을 시작 하려면 캐시 키 보호기를 사용할 수 없게 됩니다.
시스템에서 보안 설정을 변경 하는 새 코드 무결성 정책 적용 등 보안 부팅 사용 안 함, 캐시 키 보호기가 무효화 됩니다. 시간과 호스트 보호 된 Vm 다시 시작 하기 오프 라인를 하기 전에 HGS 증명 해야 합니다.

호스트 보호자 서비스 클러스터 및 Hyper-v 호스트에 대해 오프 라인 모드에 17609 또는 최신 Windows Server Insider Preview 빌드에 필요합니다.
이 기본적으로 해제 되어 있는 HGS에서 정책에 의해 제어 됩니다.
오프 라인 모드에 대 한 지원을 사용 하려면 HGS 노드에서 다음 명령을 실행 합니다.

```powershell
Set-HgsKeyProtectionConfiguration -AllowKeyMaterialCaching:$true
```

캐시 가능한 키 보호기가 각 보호 된 VM에 고유 하므로 완전히 (없습니다 다시 시작)를 종료 한 후을 얻기 위해 캐시할 키 보호기를 HGS에이 설정을 사용 하는 보호 된 Vm을 시작 해야 합니다.
보호 된 VM의 Windows Server 이전 버전을 실행 하는 Hyper-v 호스트를 마이그레이션합니다 또는 HGS의 이전 버전에서 새로운 키 보호기를 가져옵니다 하는 경우 오프 라인 모드에서 자체 시작할 수 없습니다 있지만 계속 HGS에 대 한 액세스 사용 가능한 경우 온라인 모드로 실행할 수 있습니다. 수 있습니다.
