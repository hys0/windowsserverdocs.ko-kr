---
title: 클라이언트 액세스 라이선스 (Cal)를 사용 하 여 RDS 배포 라이선스
description: 원격 데스크톱 서비스의 라이선스 클라이언트의 개요입니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5be6546b-df16-4475-bcba-aa75aabef3e3
author: lizap
ms.author: elizapo
ms.date: 09/20/2018
manager: dongill
ms.openlocfilehash: 6648a52bb4d09725935a2197d6ce6fa6d8cc74a8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853444"
---
# <a name="license-your-rds-deployment-with-client-access-licenses-cals"></a>클라이언트 액세스 라이선스 (Cal)를 사용 하 여 RDS 배포 라이선스

>적용 대상: Windows Server (반기 채널), Windows Server 2016

원격 데스크톱 세션 호스트에 연결 된 장치와 각 사용자는 클라이언트 액세스 라이선스 (CAL) 해야 합니다. 설치 및 발급 하 고 RDS Cal 추적에 RD 라이선싱을 사용 합니다.  

사용자 또는 장치에 RD 세션 호스트 서버에 연결 하는 경우 RD 세션 호스트 서버는 RDS CAL 필요한 경우를 결정 합니다. RD 세션 호스트 서버는 원격 데스크톱 라이선스 서버에서 RDS CAL을 요청합니다. 적절 한 RDS CAL 라이선스 서버에서 사용 가능한 경우 RDS CAL을 클라이언트에 발급 된와 클라이언트 데스크톱 또는 사용 하려는 앱을 여기에서 RD 세션 호스트 서버에 연결할 수 있습니다.

없음 라이선스 서버가 필요 합니다, 유예 기간이 끝나면 클라이언트 라이선스 서버에서 발급 한 유효한 RDS CAL 있어야 후 라이선스 유예 기간이 있지만 RD 세션 호스트 서버에 로그온 할 수 있습니다.

원격 데스크톱 서비스의 클라이언트 액세스 라이선스 작동 방식에 대해 자세히 알아보려면 및 배포 하 고 라이선스를 관리 하려면 다음 정보를 사용 합니다.

- [Cal 모델 이해](#understanding-the-cals-model)
- [라이선스 서버 활성화](rds-activate-license-server.md)
- [라이선스 서버에서 RDS Cal 설치](rds-install-cals.md)
- [배포에 사용 된 Cal 추적](rds-track-cals.md)

## <a name="understanding-the-cals-model"></a>Cal 모델 이해

Cal에는 다음과 같은 두 종류가 있습니다.

- RDS 장치 단위 Cal
- RDS 사용자 단위 Cal

다음 표에서 두 가지 유형의 Cal 간의 차이점을 설명합니다.

| 장치당                                                     | 사용자 당                                                                         |
|----------------------------------------------------------------|----------------------------------------------------------------------------------|
| Cal 각 장치에 물리적으로 할당 됩니다.                   | Cal은 Active Directory에서 사용자에 게 할당 됩니다.                                 |
| Cal은 라이선스 서버에서 추적 됩니다.                        | Cal은 라이선스 서버에서 추적 됩니다.                                          |
| Active Directory 구성원 자격에 관계 없이 Cal은 추적할 수 있습니다. | 작업 그룹 내에서 Cal은 추적할 수 없습니다.                                       |
| 최대 20%의 Cal 해지할 수 있습니다.                              | Cal을 해지할 수는 없습니다.                                                      |
| 임시 Cal 52 – 89 일간 유효 합니다.                       | 임시 Cal이 제공 되지 않습니다.                                                |
| Cal 초과 할당 될 수 없습니다.                                  | Cal (원격 데스크톱 라이선스 계약의 위반)에서 초과 할당 될 수 있습니다. |

장치 모델을 사용 하면 임시 라이선스 RD 세션 호스트에 연결 하는 장치를 처음으로 발급 됩니다. 두 번째 장치 연결, 라이선스 서버 활성화 되 고 사용할 수 있는 Cal을 라이선스 서버 문제는 영구 RDS 장치 단위 CAL 가지 합니다.

사용자별 모델을 사용 하는 경우 라이선스 적용 되지 않습니다 및 각 사용자에 라이선스를 여러 장치에서에서 RD 세션 호스트에 연결할 권한이 부여 됩니다. 라이선스 서버를 사용할 수 있는 CAL 풀 또는 Over-Used CAL 풀에서 라이선스를 발급합니다. 유효한 라이선스가 모든 사용자 및 Over-Used Cal 0 되도록 사용자의 책임-원격 데스크톱 서비스의 사용 조건에 위반 하 고 그렇지 않으면입니다.

원격 데스크톱 서비스의 사용 조건 준수을 보장 하려면 RDS 사용자 단위 Cal의 수를 추적 조직에서 사용 하 고는 충분 한 사용자 단위 Cal 모든 사용자에 대 한 라이선스 서버에 설치 되어 있는지 확인 하십시오.

추적 하 고 RDS 사용자 단위 Cal에 대 한 보고서를 생성 하려면 원격 데스크톱 라이선스 관리자를 사용할 수 있습니다.

## <a name="note-about-cal-versions"></a>CAL 버전에 대 한 note

사용자 또는 장치에서 사용 하는 CAL 사용자나 장치에 연결 하는 Windows 서버의 버전이 일치 해야 합니다. 오래 된 Cal을 사용 하 여 최신 Windows Server 버전에 액세스할 수 없습니다. 하지만 최신 Cal을 사용 하 여 이전 버전의 Windows Server에 액세스할 수 있습니다.

다음 표에서 RD 세션 호스트 및 RD 가상화 호스트에 호환 되는 Cal을 보여 줍니다.

|                  |2008 R2 및 이전 CAL|2012 CAL|2016 CAL|2019 CAL|
|---------------------------------|--------|--------|--------|--------|
| **2008, 2008 R2 라이선스 서버**| 예    | 아니오     | 아니요     | 아니오     |
| **2012 라이선스 서버**         | 예    | 예    | 아니오     | 아니요     |
| **2012 R2 라이선스 서버**      | 예    | 예    | 아니오     | 아니오     |
| **2016 라이선스 서버**         | 예    | 예    | 예    | 아니요     |
| **2019 라이선스 서버**         | 예    | 예    | 예    | 예    |

RDS 라이선스 서버는 원격 데스크톱 서비스의 모든 이전 버전 및 원격 데스크톱 서비스의 현재 버전에서 라이선스를 호스트할 수 있습니다. 예를 들어, Windows Server 2012 R2 RDS 라이선스 서버를 Windows Server 2012 R2까지 라이선스 호스팅할 수 있습니다 하는 동안 Windows Server 2016 RDS 라이선스 서버에서 RDS의 모든 이전 버전에서 라이선스를 호스트할 수 있습니다.
