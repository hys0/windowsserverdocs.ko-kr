---
title: CAL(클라이언트 액세스 라이선스)로 RDS 배포 라이선싱
description: 원격 데스크톱 서비스의 클라이언트 라이선싱 개요입니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5be6546b-df16-4475-bcba-aa75aabef3e3
author: lizap
ms.author: elizapo
ms.date: 02/12/2020
manager: dongill
ms.openlocfilehash: 391f9e7569abd3c3496bfcc9b52d3ddf8abdebbb
ms.sourcegitcommit: 5797a2e67211651070404a5893f5c0a91c63e960
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2020
ms.locfileid: "77173424"
---
# <a name="license-your-rds-deployment-with-client-access-licenses-cals"></a>CAL(클라이언트 액세스 라이선스)로 RDS 배포 라이선싱

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

원격 데스크톱 세션 호스트에 연결하는 각 사용자 및 디바이스는 CAL(클라이언트 액세스 라이선스)이 필요합니다. RD 라이선싱을 사용하여 RDS CAL을 설치, 발급 및 추적합니다.  

사용자 또는 디바이스가 RD 세션 호스트 서버에 연결하는 경우 RD 세션 호스트 서버는 RDS CAL이 필요한지를 결정합니다. 그런 후에 RD 세션 호스트 서버는 원격 데스크톱 라이선스 서버에서 RDS CAL을 요청합니다. 라이선스 서버에서 적절한 RDS CAL을 사용할 수 있는 경우 RDS CAL이 클라이언트로 발급되고, 클라이언트는 데스크톱 RD 세션 호스트 서버에 연결하고, 다시 이 서버에서 사용하려는 데스크톱 또는 앱에 연결할 수 있습니다.

라이선스 서버가 필요하지 않은 라이선스 유예 기간이 있지만 유예 기간이 끝난 후 클라이언트가 RD 세션 호스트 서버에 로그온하려면 라이선스 서버에서 발급한 유효한 RDS CAL이 있어야 합니다.

클라이언트 액세스 라이선싱이 원격 데스크톱 서비스에서 작동하는 방식을 알아보고 라이선스를 배포 및 관리하려면 다음 정보를 사용하세요.

- [CAL(클라이언트 액세스 라이선스)로 RDS 배포 라이선싱](#license-your-rds-deployment-with-client-access-licenses-cals)
  - [RDS CAL 모델 이해](#understanding-the-rds-cal-model)
  - [RDS CAL 버전 호환성](#rds-cal-version-compatibility)

## <a name="understanding-the-rds-cal-model"></a>RDS CAL 모델 이해

RDS CAL에는 다음 두 가지 유형이 있습니다.

- RDS 디바이스 단위 CAL
- RDS 사용자 단위 CAL

다음 표에서는 이러한 두 가지 유형의 CAL 간 차이점을 설명합니다.

| 디바이스 단위                                                     | 사용자 단위                                                                         |
|----------------------------------------------------------------|----------------------------------------------------------------------------------|
| RDS CAL이 각 디바이스에 물리적으로 할당됩니다.                   | RDS CAL이 Active Directory의 사용자에게 할당됩니다.                                 |
| RDS CAL이 라이선스 서버에 의해 추적됩니다.                        | RDS CAL이 라이선스 서버에 의해 추적됩니다.                                          |
| Active Directory 멤버 자격에 관계 없이 RDS CAL을 추적할 수 있습니다. | 작업 그룹 내에서 RDS CAL을 추적할 수 없습니다.                                       |
| 최대 20%의 RDS CAL을 해지할 수 있습니다.                              | RDS CAL을 해지할 수 없습니다.                                                      |
| 임시 RDS CAL은 52–89일 동안 유효합니다.                       | 임시 RDS CAL을 사용할 수 없습니다.                                                |
| RDS CAL을 초과 할당할 수 없습니다.                                  | RDS CAL을 초과 할당할 수 있습니다(원격 데스크톱 사용권 계약을 위반하여). |

디바이스 단위 모델을 사용할 경우 디바이스가 RD 세션 호스트에 처음 연결할 때 임시 라이선스가 발급됩니다. 디바이스가 두 번째로 연결할 때는 라이선스 서버가 활성화되어 있고 사용 가능한 RDS CAL이 있으면, 라이선스 서버가 영구 RDS 디바이스 단위 CAL을 발급합니다.

사용자 단위 모델을 사용할 경우 라이선스는 적용되지 않으며 각 사용자에게 제한없는 수의 디바이스에서 RD 세션 호스트에 연결하기 위한 라이선스가 부여됩니다. 라이선스 서버는 사용 가능한 RDS CAL 풀 또는 과사용된 RDS CAL 풀에서 라이선스를 발급합니다. 모든 사용자에게 유효한 라이선스가 있고 과사용된 CAL이 없는지 확인하는 것은 사용자의 책임입니다. 그렇지 않으면 원격 데스크톱 서비스 사용 조건을 위반하게 됩니다.

원격 데스크톱 서비스 사용 조건을 준수하는지 확인하려면 조직에서 사용되는 RDS 사용자 단위 CAL의 수를 추적하고, 모든 사용자를 위해 라이선스 서버에 충분한 RDS 사용자 단위 CAL이 설치되어 있는지 확인하세요.

원격 데스크톱 라이선스 관리자를 사용하여 RDS 사용자 단위 CAL을 추적하고 관련 보고서를 생성할 수 있습니다.

## <a name="rds-cal-version-compatibility"></a>RDS CAL 버전 호환성

사용자 또는 디바이스의 CAL은 사용자나 디바이스가 연결하는 Windows 서버 버전과 호환되어야 합니다. 이전 버전의 RDS CAL을 사용하여 이후 버전의 Windows Server에 액세스할 수는 없지만 이후 버전의 RDS CAL을 사용하여 이전 버전의 Windows Server에 액세스할 수 있습니다. 예를 들어 Windows Server 2016 RD 세션 호스트에 연결하려면 RDS 2016 CAL 이상이 필요하고 Windows Server 2012 R2 RD 세션 호스트에 연결하려면 RDS 2012 CAL 이상이 필요합니다.

다음 표는 서로 호환되는 RDS CAL 및 RD 세션 호스트 버전을 보여줍니다.

|                  | RDS 2008 R2 및 이전 CAL | RDS 2012 CAL | RDS 2016 CAL | RDS 2019 CAL |
|---------------------------------|--------|--------|--------|--------|
| **2008, 2008 R2 세션 호스트** | 예    | 예    | 예    | 예     |
| **2012 세션 호스트**         | 아니요     | 예    | 예    | 예    |
| **2012 R2 세션 호스트**      | 아니요     | 예    | 예    | 예    |
| **2016 세션 호스트**         | 아니요     | 아니요     | 예    | 예    |
| **2019 세션 호스트**         | 아니요     | 아니요     | 아니요     | 예    |

호환되는 RD 라이선스 서버에 RDS CAL을 설치해야 합니다. RDS 라이선스 서버는 모든 이전 버전의 원격 데스크톱 서비스와 현재 버전의 원격 데스크톱 서비스의 라이선스를 호스트할 수 있습니다. 예를 들어, Windows Server 2012 R2 RDS 라이선스 서버는 모든 이전 버전의 라이선스를 호스트할 수 있지만, Windows Server 2016 RDS 라이선스 서버는 Windows Server 2012 R2까지만 라이선스를 호스트할 수 있습니다.

다음 표는 서로 호환되는 RDS CAL 및 라이선스 서버 버전을 보여줍니다.

|                  | RDS 2008 R2 및 이전 CAL | RDS 2012 CAL | RDS 2016 CAL | RDS 2019 CAL |
|---------------------------------|--------|--------|--------|--------|
| **2008, 2008 R2 라이선스 서버** | 예    | 아니요   | 아니요   | 아니요    |
| **2012 라이선스 서버**         | 예     | 예    | 아니요   | 아니요    |
| **2012 R2 라이선스 서버**      | 예     | 예    | 아니요   | 아니요    |
| **2016 라이선스 서버**         | 예     | 예    | 예   | 아니요    |
| **2019 라이선스 서버**         | 예     | 예    | 예  | 예   |
