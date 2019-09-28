---
title: 원격 데스크톱 서비스 - Multi-Factor Authentication
description: RDS에서 MFA를 사용하기 위한 계획 정보
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 833eafd0b762098b67b11e6e5f26f63e62057fd1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403849"
---
# <a name="remote-desktop-services---multi-factor-authentication"></a>원격 데스크톱 서비스 - Multi-Factor Authentication

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

Azure Directory에서 Multi-Factor Authentication을 사용하여 비즈니스 리소스에 대해 보안을 강화할 수 있습니다.

데스크톱 및 애플리케이션에 연결되는 최종 사용자의 경우 두 번째 인증 조치를 수행하여 원하는 리소스에 연결하므로 이미 사용 중인 환경과 비슷한 환경이 제공됩니다.
- RDP 파일에서 또는 원격 데스크톱 클라이언트 애플리케이션을 통해 데스크톱 또는 RemoteApp을 시작합니다.
- 안전한 원격 액세스를 위해 RD 게이트웨이에 연결할 경우 SMS 또는 모바일 애플리케이션 MFA 문제가 발생합니다.
- 올바르게 인증을 받고 해당 리소스에 연결합니다.

구성 프로세스에 대한 자세한 내용은 [NPS(네트워크 정책 서버) 확장 및 Azure AD를 사용하여 원격 데스크톱 게이트웨이 인프라 통합](https://docs.microsoft.com/azure/multi-factor-authentication/nps-extension-remote-desktop-gateway)을 참조하세요.
