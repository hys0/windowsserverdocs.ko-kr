---
title: TPM 신뢰할 수 있는 증명을 사용 하 여 HGS를 초기화 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 672054462437b615236dfc4f00c8b20c946f11a7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882334"
---
# <a name="initialize-hgs-using-tpm-trusted-attestation"></a>TPM 신뢰할 수 있는 증명을 사용 하 여 HGS를 초기화 합니다.

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

이러한 단계는 새 포리스트 또는 기존 배스 천 포리스트는 HGS를 초기화 하는 여부에 따라 달라 집니다.

1. [(기본값)를 새 포리스트의 HGS 클러스터를 초기화 합니다.](guarded-fabric-initialize-hgs-tpm-mode-default.md)

   -또는-

   [기존 배스 천 포리스트의 HGS 클러스터를 초기화 합니다.](guarded-fabric-initialize-hgs-tpm-mode-bastion.md)

2. [신뢰할 수 있는 TPM 루트 인증서를 설치 합니다.](guarded-fabric-install-trusted-tpm-root-certificates.md)   
3. [패브릭을 DNS 구성](guarded-fabric-configuring-fabric-dns.md)

