---
title: 원격 데스크톱 서비스-Multi-factor Authentication
description: Rds.를 사용 하 여 MFA를 사용 하는 것에 대 한 계획 정보
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 09ea784e-5644-417a-a3d9-bdbcebc313f9
author: lizap
ms.author: elizapo
ms.date: 09/07/2016
manager: dongill
ms.openlocfilehash: 50cbabf377e5b01c44360d776b9ff999826303c6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814874"
---
# <a name="remote-desktop-services---multi-factor-authentication"></a>원격 데스크톱 서비스-Multi-factor Authentication

>적용 대상: Windows Server (반기 채널), Windows Server 2016

비즈니스 리소스의 높은 수준의 보안 보호를 적용 하려면 Multi-factor Authentication을 사용 하 여 Active Directory의 기능을 활용 합니다.

데스크톱 및 응용 프로그램에 연결 하면 최종 사용자에 대 한 환경은 어떤 이미 과연 원하는 리소스에 연결할 두 번째 인증 측정값을 수행할 때와 비슷합니다.
- 데스크톱 또는 원격 데스크톱 클라이언트 응용 프로그램을 통해 또는 RDP 파일에서 RemoteApp 시작
- 안전한 원격 액세스에 대 한 RD 게이트웨이 연결할 때는 SMS 또는 모바일 응용 프로그램 MFA 챌린지를 수신
- 올바르게 인증 하 고 해당 리소스에 연결 하기!

구성 프로세스에 대 한 자세한 내용은 체크 아웃 [네트워크 정책 (NPS 서버) 확장 및 Azure AD를 사용 하 여 원격 데스크톱 게이트웨이 인프라 통합 ](https://docs.microsoft.com/azure/multi-factor-authentication/nps-extension-remote-desktop-gateway)합니다.
