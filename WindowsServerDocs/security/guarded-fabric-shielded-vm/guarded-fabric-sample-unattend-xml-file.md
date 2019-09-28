---
title: OS 전문화 응답 파일 만들기
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 299aa38e-28d2-4cbe-af16-5b8c533eba1f
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 4920f9a90bd0190d390a9d35b3d265023d69efac
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386498"
---
# <a name="create-os-specialization-answer-file"></a>OS 전문화 응답 파일 만들기

>적용 대상: Windows server 2019, Windows Server (반기 채널), Windows Server 2016

보호 된 Vm 배포를 준비 하는 경우 운영 체제 특수화 응답 파일을 만들어야 할 수 있습니다. Windows에서이를 일반적으로 "unattend.xml" 파일 이라고 합니다. **ShieldingDataAnswerFile** Windows PowerShell 함수를 사용 하면이 작업을 수행할 수 있습니다. 그런 다음 System Center Virtual Machine Manager (또는 기타 패브릭 컨트롤러)를 사용 하 여 템플릿에서 보호 된 Vm을 만들 때 응답 파일을 사용할 수 있습니다.

보호 된 Vm의 무인 파일에 대 한 일반적인 지침은 [응답 파일 만들기](guarded-fabric-tenant-creates-shielding-data.md#create-an-answer-file)를 참조 하세요.
 
## <a name="downloading-the-new-shieldingdataanswerfile-function"></a>ShieldingDataAnswerFile 함수 다운로드

[PowerShell 갤러리](https://aka.ms/gftools)에서 **ShieldingDataAnswerFile** 함수를 가져올 수 있습니다. 컴퓨터가 인터넷에 연결 되어 있는 경우 다음 명령을 사용 하 여 PowerShell에서 설치할 수 있습니다.

```powershell
Install-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0
```

@No__t-0 출력을 추가 아티팩트와 함께 보호 데이터로 패키지 하 여 템플릿에서 보호 된 Vm을 만드는 데 사용할 수 있습니다.

다음 섹션에서는 다양 한 옵션을 포함 하는 `unattend.xml` 파일에 함수 매개 변수를 사용 하는 방법을 보여 줍니다.

- [기본 Windows 응답 파일](#basic-windows-answer-file)
- [도메인 가입을 사용 하는 Windows 응답 파일](#windows-answer-file-with-domain-join)
- [고정 IPv4 주소를 사용 하는 Windows 응답 파일](#windows-answer-file-with-static-ipv4-addresses)
- [사용자 지정 로캘을 사용 하는 Windows 응답 파일](#windows-answer-file-with-a-custom-locale)
- [기본 Linux 응답 파일](#basic-linux-answer-file)

## <a name="basic-windows-answer-file"></a>기본 Windows 응답 파일

다음 명령은 단순히 관리자 계정 암호와 호스트 이름을 설정 하는 Windows 응답 파일을 만듭니다.
VM 네트워크 어댑터는 DHCP를 사용 하 여 IP 주소를 가져오고 VM은 Active Directory 도메인에 가입 되지 않습니다.
관리자 자격 증명을 입력 하 라는 메시지가 표시 되 면 원하는 사용자 이름과 암호를 지정 합니다.
기본 제공 관리자 계정을 구성 하려는 경우 사용자 이름에 "관리자"를 사용 합니다.

```powershell
$adminCred = Get-Credential -Message "Local administrator account"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred
```

## <a name="windows-answer-file-with-domain-join"></a>도메인 가입을 사용 하는 Windows 응답 파일

다음 명령은 보호 된 VM을 Active Directory 도메인에 조인 하는 Windows 응답 파일을 만듭니다.
VM 네트워크 어댑터는 DHCP를 사용 하 여 IP 주소를 가져옵니다.

첫 번째 자격 증명 프롬프트에서 로컬 관리자 계정 정보를 요청 합니다.
기본 제공 관리자 계정을 구성 하려는 경우 사용자 이름에 "관리자"를 사용 합니다.

두 번째 자격 증명 프롬프트는 컴퓨터를 Active Directory 도메인에 가입 시킬 권한이 있는 자격 증명을 요청 합니다.

"-DomainName" 매개 변수의 값을 Active Directory 도메인의 FQDN으로 변경 해야 합니다.

```powershell
$adminCred = Get-Credential -Message "Local administrator account"
$domainCred = Get-Credential -Message "Domain join credentials"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred -DomainName 'my.contoso.com' -DomainJoinCredentials $domainCred
```
## <a name="windows-answer-file-with-static-ipv4-addresses"></a>고정 IPv4 주소를 사용 하는 Windows 응답 파일

다음 명령은 System Center Virtual Machine Manager와 같이 패브릭 관리자가 배포 시 제공 하는 고정 IP 주소를 사용 하는 Windows 응답 파일을 만듭니다.

Virtual Machine Manager는 IP 풀을 사용 하 여 고정 IP 주소에 세 가지 구성 요소를 제공 합니다. IPv4 주소, IPv6 주소, 게이트웨이 주소 및 DNS 주소입니다. 추가 필드를 포함 하거나 사용자 지정 네트워크 구성이 필요한 경우에는 스크립트에 의해 생성 된 응답 파일을 수동으로 편집 해야 합니다.

다음 스크린샷은 Virtual Machine Manager에서 구성할 수 있는 IP 풀을 보여 줍니다. 이러한 풀은 고정 IP를 사용 하려는 경우에 필요 합니다.

현재이 함수는 하나의 DNS 서버만 지원 합니다. DNS 설정은 다음과 같습니다.

![고정 IP 풀을 사용 하 여 DNS 서버 구성](../media/Guarded-Fabric-Shielded-VM/guarded-host-unattend-static-ip-address-pool-dns-settings.png)

고정 IP 주소 풀을 만드는 방법에 대 한 요약은 다음과 같습니다. 간단히 말해서 네트워크 경로, 게이트웨이 및 DNS 서버가 하나씩만 있어야 하 고, IP 주소를 지정 해야 합니다.

![고정 IP 풀 만들기 요약](../media/Guarded-Fabric-Shielded-VM/guarded-host-unattend-static-ip-address-pool-summary.png)

가상 컴퓨터에 대 한 네트워크 어댑터를 구성 해야 합니다. 다음 스크린샷은 해당 구성을 설정 하는 위치와 고정 IP로 전환 하는 방법을 보여 줍니다.

![고정 IP를 사용 하도록 하드웨어 구성](../media/Guarded-Fabric-Shielded-VM/guarded-host-unattend-static-ip-address-pool-network-adapter-settings.png)

그런 다음 `-StaticIPPool` 매개 변수를 사용 하 여 응답 파일에 고정 IP 요소를 포함할 수 있습니다. 응답 파일에서-0, `@NextHop-1-1@` 및 `@DNSAddr-1-1@` @no__t 매개 변수는 배포 시 Virtual Machine Manager에서 지정한 실제 값으로 대체 됩니다.

```powershell
$adminCred = Get-Credential -Message "Local administrator account"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred -StaticIPPool IPv4Address
```

## <a name="windows-answer-file-with-a-custom-locale"></a>사용자 지정 로캘을 사용 하는 Windows 응답 파일

다음 명령은 사용자 지정 로캘을 사용 하 여 Windows 응답 파일을 만듭니다.

관리자 자격 증명을 입력 하 라는 메시지가 표시 되 면 원하는 사용자 이름과 암호를 지정 합니다.
기본 제공 관리자 계정을 구성 하려는 경우 사용자 이름에 "관리자"를 사용 합니다.

```powershell
$adminCred = Get-Credential -Message "Local administrator account"
$domainCred = Get-Credential -Message "Domain join credentials"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred -Locale es-ES
```

## <a name="basic-linux-answer-file"></a>기본 Linux 응답 파일

Windows Server 버전 1709부터 보호 된 Vm에서 특정 Linux 게스트 Os를 실행할 수 있습니다.
System Center Virtual Machine Manager Linux 에이전트를 사용 하 여 이러한 Vm을 특수화 하는 경우 ShieldingDataAnswerFile cmdlet은 해당 Vm에 대해 호환 되는 응답 파일을 만들 수 있습니다.

Linux 응답 파일에는 일반적으로 루트 암호, 루트 SSH 키 및 선택적으로 고정 IP 풀 정보를 포함 합니다.
아래 스크립트를 실행 하기 전에 경로를 SSH 키의 공용 절반으로 바꿉니다.

```powershell
$rootPassword = Read-Host -Prompt "Root password" -AsSecureString

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -RootPassword $rootPassword -RootSshKey '~\.ssh\id_rsa.pub'
```

## <a name="see-also"></a>참조

- [보호된 VM 배포](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
