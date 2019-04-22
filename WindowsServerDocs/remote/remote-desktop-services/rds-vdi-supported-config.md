---
title: 원격 데스크톱 서비스 VDI에 대 한 지원 되는 Windows 10 보안 구성
description: Windows Server 2016에서 RDS 사용 하 여 Windows 10 VDI에 대 한 지원 되는 구성에 대 한 정보를 제공합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 10/27/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8f164f5d-a498-4f91-a12f-3e01d554f810
author: lizap
manager: dongill
ms.openlocfilehash: ff890150dcea30c425267dcaae9b1bdbc6d78b8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820084"
---
# <a name="supported-windows-10-security-configurations-for-remote-desktop-services-vdi"></a>원격 데스크톱 서비스 VDI에 대 한 지원 되는 Windows 10 보안 구성

> 적용 대상: Windows Server 2016

Windows 10 및 Windows Server 2016 새로운 더 보안 위반 으로부터 보호 악의적인 공격을 차단 하 고 virtual machines, 응용 프로그램 및 데이터의 보안을 강화 하려면 운영 체제에 기본 제공 보호 계층을 있습니다.

> [!NOTE]
> 검토 해야 합니다 [원격 데스크톱 서비스 구성 정보를 지원](rds-supported-config.md)합니다.

이러한 새 기능의 rds.를 사용 하 여 VDI 배포에서 지원 되는 다음 표에 정리 되어

|  VDI 컬렉션 형식               |  풀 관리 |  관리 되는 개인 |  관리 되지 않는 풀링된                                     |  관리 되지 않는 개인                                    |
|-------------------------------------|------------------|--------------------|--------------------------------------------------------|--------------------------------------------------------|
| [Credential Guard](https://technet.microsoft.com/itpro/windows/keep-secure/credential-guard)                    | 예              | 예                | 예                                                    | 예                                                    |
| [Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)                        | 예              | 예                | 예                                                    | 예                                                    |
| [원격 Credential Guard](https://technet.microsoft.com/itpro/windows/keep-secure/remote-credential-guard)             | 아니오               | 아니요                 | 아니요                                                     | 아니오                                                     |
| [보호 및 암호화 지원 Vm](../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md) | 아니오               | 아니오                 | 추가 구성을 사용 하 여 지원 되는 Vm 암호화 | 추가 구성을 사용 하 여 지원 되는 Vm 암호화 |

## <a name="remote-credential-guard"></a>원격 Credential Guard:

원격 Credential Guard 대상 컴퓨터에 직접 연결 하 고 원격 데스크톱 연결 브로커 및 원격 데스크톱 게이트웨이 통해을 하지에 지원 됩니다.
> [!NOTE]
> 단일 인스턴스 환경에서 연결 브로커 있고 DNS 이름은 컴퓨터 이름과 일치 하는 경우 있습니다 될 수 원격 Credential Guard 사용할 수 있지만 지원 되지 않습니다.

## <a name="shielded-vms-and-encryption-supported-vms"></a>보호 된 Vm 및 암호화 지원 Vm: 

- 보호 된 Vm VDI 원격 데스크톱 서비스에서에서 지원 되지 않습니다. 

암호화 지원 Vm을 활용 합니다.
- 가상 컴퓨터를 프로 비전 하는 관리 되지 않는 컬렉션 및 원격 데스크톱 서비스 컬렉션 만들기 프로세스가 외부 프로 비전 기술을 사용 합니다. 
- 사용자 프로필 디스크 차등 디스크에 의존 하므로 지원 되지 않습니다. 

