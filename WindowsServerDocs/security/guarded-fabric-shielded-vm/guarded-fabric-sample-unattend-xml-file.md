---
title: OS 전문화 응답 파일 만들기
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 299aa38e-28d2-4cbe-af16-5b8c533eba1f
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 5717fcc9e1732b6273620e633c140c6df58ec8b7
ms.sourcegitcommit: 29ad32b9dea298a7fe81dcc33d2a42d383018e82
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65624648"
---
# <a name="create-os-specialization-answer-file"></a>OS 전문화 응답 파일 만들기

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

보호 된 Vm을 배포 하려면 준비, 운영 체제 특수화 응답 파일을 만들려고 해야 합니다. Windows에서이 일반적으로 라고 "unattend.xml" 파일입니다. 합니다 **-New-shieldingdataanswerfile** Windows PowerShell 함수를 사용 하면이 작업을 수행 합니다. System Center Virtual Machine Manager (또는 다른 패브릭 컨트롤러)를 사용 하 여 템플릿에서 보호 된 Vm 응답 파일을 만들 때 사용할 수 있습니다.

보호 된 Vm에 대 한 무인 파일에 대 한 일반적인 지침을 참조 하세요 [응답 파일을 만들고](guarded-fabric-tenant-creates-shielding-data.md#create-an-answer-file)합니다.
 
## <a name="downloading-the-new-shieldingdataanswerfile-function"></a>다운로드-New-shieldingdataanswerfile 함수

가져올 수 있습니다는 **-New-shieldingdataanswerfile** 에서 작동 합니다 [PowerShell 갤러리](https://aka.ms/gftools)합니다. 컴퓨터가 인터넷에 연결 하는 경우 다음 명령을 사용 하 여 PowerShell에서 설치할 수 있습니다.

```powershell
Install-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0
```

`unattend.xml` 템플릿에서 보호 된 Vm을 만들려면 사용할 수 있도록 추가 아티팩트와 함께 실딩 데이터를 출력을 패키징할 수 있습니다.

다음 섹션에 대 한 함수 매개 변수를 사용 하는 방법을 보여 줍니다는 `unattend.xml` 다양 한 옵션을 포함 하는 파일:

- [기본 Windows 응답 파일](#basic-windows-answer-file)
- [Windows는 도메인 가입을 사용 하 여 파일 응답](#windows-answer-file-with-domain-join)
- [고정 IPv4 주소를 사용 하 여 Windows 응답 파일](#windows-answer-file-with-static-ipv4-addresses)
- [사용자 지정 로캘 사용 하 여 Windows 응답 파일](#windows-answer-file-with-a-custom-locale)
- [기본 Linux 응답 파일](#basic-linux-answer-file)

## <a name="basic-windows-answer-file"></a>기본 Windows 응답 파일

다음 명령은 단순히 호스트 이름을 확인 하 고 관리자 계정 암호를 설정 하는 Windows 응답 파일을 만듭니다.
VM 네트워크 어댑터를 사용 하 여 DHCP IP 주소를 얻는 하 고 VM을 Active Directory 도메인에 가입 되지 않습니다.
관리자 자격 증명 입력 대화 상자가 나타나면 원하는 사용자 이름과 암호를 지정 합니다.
내장 된 Administrator 계정을 구성 하려는 경우에 사용자 이름에 대 한 "관리자"를 사용 합니다.

```powershell
$adminCred = Get-Credential -Message "Local administrator account"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred
```

## <a name="windows-answer-file-with-domain-join"></a>Windows는 도메인 가입을 사용 하 여 파일 응답

다음 명령은 Active Directory 도메인에 보호 된 VM을 조인 하는 Windows 응답 파일을 만듭니다.
VM 네트워크 어댑터 IP 주소를 가져올 DHCP를 사용 합니다.

첫 번째 자격 증명 프롬프트 로컬 관리자 계정 정보를 묻는 메시지가 나타납니다.
내장 된 Administrator 계정을 구성 하려는 경우에 사용자 이름에 대 한 "관리자"를 사용 합니다.

두 번째 자격 증명 프롬프트를 Active Directory 도메인에 컴퓨터를 가입 시킬 권한이 있는 자격 증명을 묻습니다.

값을 변경 해야 합니다 "-DomainName" Active Directory 도메인의 FQDN으로 매개 변수입니다.

```powershell
$adminCred = Get-Credential -Message "Local administrator account"
$domainCred = Get-Credential -Message "Domain join credentials"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred -DomainName 'my.contoso.com' -DomainJoinCredentials $domainCred
```
## <a name="windows-answer-file-with-static-ipv4-addresses"></a>고정 IPv4 주소를 사용 하 여 Windows 응답 파일

다음 명령은 System Center Virtual Machine Manager 같은 패브릭 관리자가 배포 시에 제공 하는 고정 IP 주소를 사용 하는 Windows 응답 파일을 만듭니다.

Virtual Machine Manager IP 풀을 사용 하 여 고정 IP 주소에는 세 가지 구성 요소를 제공 합니다. IPv4 주소, IPv6 주소, 게이트웨이 주소 및 DNS 주소입니다. 추가 필드를 포함 하거나 사용자 지정 네트워크 구성이 필요를 하려는 경우 스크립트에서 생성 된 응답 파일을 수동으로 편집 해야 합니다.

다음 스크린샷에서 Virtual Machine Manager 구성할 수 있는 IP 풀을 보여 줍니다. 이러한 풀은 고정 IP를 사용 하려는 경우에 필요 합니다.

현재 함수에는 DNS 서버가 하나만 지원합니다. DNS 설정 모양을 다음과 같습니다.

![고정 IP 풀을 사용 하 여 DNS 서버 구성](../media/Guarded-Fabric-Shielded-VM/guarded-host-unattend-static-ip-address-pool-dns-settings.png)

고정 IP 주소 풀을 만들기 위한 요약 모양을 다음과 같습니다. 즉, 하나의 네트워크 경로, 하나의 게이트웨이 및 DNS 서버만-있어야 하며 사용자의 IP 주소를 지정 해야 합니다.

![고정 IP 풀 만들기 요약](../media/Guarded-Fabric-Shielded-VM/guarded-host-unattend-static-ip-address-pool-summary.png)

가상 머신에 대 한 네트워크 어댑터를 구성 해야 합니다. 다음 스크린 샷에서 해당 구성을 설정 하는 위치 및 고정 IP를 전환 하는 방법을 보여 줍니다.

![고정 IP를 사용 하는 하드웨어 구성](../media/Guarded-Fabric-Shielded-VM/guarded-host-unattend-static-ip-address-pool-network-adapter-settings.png)

그런 다음 사용할 수 있습니다는 `-StaticIPPool` 매개 변수를 응답 파일에 정적 IP 요소를 포함 합니다. 매개 변수 `@IPAddr-1@`, `@NextHop-1-1@`, 및 `@DNSAddr-1-1@` 답에서 파일 다음 바뀝니다 Virtual Machine Manager 배포 시에 지정한 값은 실제 값입니다.

```powershell
$adminCred = Get-Credential -Message "Local administrator account"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred -StaticIPPool IPv4Address
```

## <a name="windows-answer-file-with-a-custom-locale"></a>사용자 지정 로캘 사용 하 여 Windows 응답 파일

다음 명령은 사용자 지정 로캘을 사용 하 여 Windows 응답 파일을 만듭니다.

관리자 자격 증명 입력 대화 상자가 나타나면 원하는 사용자 이름과 암호를 지정 합니다.
내장 된 Administrator 계정을 구성 하려는 경우에 사용자 이름에 대 한 "관리자"를 사용 합니다.

```powershell
$adminCred = Get-Credential -Message "Local administrator account"
$domainCred = Get-Credential -Message "Domain join credentials"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred -Locale es-ES
```

## <a name="basic-linux-answer-file"></a>기본 Linux 응답 파일

Windows Server 버전 1709 부터는 보호 된 Vm의 특정 Linux 게스트 Os를 실행할 수 있습니다.
System Center Virtual Machine Manager Linux 에이전트를 해당 Vm을 특수화를 사용 하는 경우-New-shieldingdataanswerfile cmdlet에 대 한 호환 응답 파일을 만들 수 있습니다.

Linux 응답 파일에서 일반적으로 루트 암호, 루트 SSH 키 및 필요에 따라 고정 IP 풀 정보를 포함 됩니다.
아래 스크립트를 실행 하기 전에 SSH 키의 공개 키 부분에 대 한 경로 대체 합니다.

```powershell
$rootPassword = Read-Host -Prompt "Root password" -AsSecureString

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -RootPassword $rootPassword -RootSshKey '~\.ssh\id_rsa.pub'
```

## <a name="see-also"></a>참조

- [보호된 VM 배포](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
