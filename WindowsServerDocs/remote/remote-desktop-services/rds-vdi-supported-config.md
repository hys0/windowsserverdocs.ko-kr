---
title: 원격 데스크톱 서비스 VDI에 대한 지원되는 Windows 10 보안 구성
description: Windows Server 2016에서 RDS를 사용하여 Windows 10 VDI에 대해 지원되는 구성 관련 정보를 제공합니다.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 10/27/2016
ms.topic: article
ms.assetid: 8f164f5d-a498-4f91-a12f-3e01d554f810
author: lizap
manager: dongill
ms.openlocfilehash: 914e6f4507e0fd997a31866b10e3c48e0cd4cbd7
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80857266"
---
# <a name="supported-windows-10-security-configurations-for-remote-desktop-services-vdi"></a>원격 데스크톱 서비스 VDI에 대한 지원되는 Windows 10 보안 구성

> 적용 대상: Windows Server 2016

Windows 10 및 Windows Server 2016은 운영 체제에 기본 제공되는 새로운 보호 계층을 제공하여 보안 위반에 대해 보다 강력히 보호하고, 악의적인 공격 차단을 지원하고, 가상 머신, 애플리케이션 및 데이터의 보안을 강화합니다.

> [!NOTE]
> [원격 데스크톱 서비스의 지원되는 구성 정보](rds-supported-config.md)를 검토해야 합니다.

다음 표에서는 이러한 새 기능 중에서 RDS를 사용하는 VDI 배포에서 지원되는 기능을 보여 줍니다.

|  VDI 컬렉션 유형               |  관리형 풀링됨 |  관리형 개인 |  비관리형 풀링됨                                     |  비관리형 개인                                    |
|-------------------------------------|------------------|--------------------|--------------------------------------------------------|--------------------------------------------------------|
| [Credential Guard](https://technet.microsoft.com/itpro/windows/keep-secure/credential-guard)                    | 예              | 예                | 예                                                    | 예                                                    |
| [Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)                        | 예              | 예                | 예                                                    | 예                                                    |
| [원격 Credential Guard](https://technet.microsoft.com/itpro/windows/keep-secure/remote-credential-guard)             | 아니요               | 아니요                 | 아니요                                                     | 아니요                                                     |
| [보호 및 암호화 지원 VM](../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md) | 아니요               | 아니요                 | 추가 구성을 사용하는 암호화 지원 VM | 추가 구성을 사용하는 암호화 지원 VM |

## <a name="remote-credential-guard"></a>원격 Credential Guard:

원격 Credential Guard는 대상 머신에 대한 직접 연결에서만 지원되며, 원격 데스크톱 연결 브로커 및 원격 데스크톱 게이트웨이를 통한 연결에서는 지원되지 않습니다.
> [!NOTE]
> 단일 인스턴스 환경에 연결 브로커가 있고 DNS 이름이 컴퓨터 이름과 일치하는 경우 원격 Credential Guard가 지원되지 않아도 사용할 수 있습니다.

## <a name="shielded-vms-and-encryption-supported-vms"></a>보호된 VM 및 암호화 지원 VM 

- 보호된 VM은 원격 데스크톱 서비스 VDI에서 지원되지 않습니다. 

암호화 지원 VM을 사용하는 경우:
- 원격 데스크톱 서비스 컬렉션 만들기 프로세스 외부에서 비관리형 컬렉션 및 프로비저닝 기술을 사용하여 가상 머신을 프로비저닝합니다. 
- 사용자 프로필 디스크는 차등 디스크에 의존하므로 지원되지 않습니다. 

