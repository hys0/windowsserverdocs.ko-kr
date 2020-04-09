---
title: TPM에서 신뢰할 수 있는 증명을 사용 하 여 HGS 초기화
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: b8ceebe63a586ec95b502dfea12f99d174549448
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856616"
---
# <a name="initialize-hgs-using-tpm-trusted-attestation"></a>TPM에서 신뢰할 수 있는 증명을 사용 하 여 HGS 초기화

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

이러한 단계는 새 포리스트나 기존 요새 포리스트에서 HGS를 초기화 하는지에 따라 달라 집니다.

1. [새 포리스트에서 HGS 클러스터 초기화 (기본값)](guarded-fabric-initialize-hgs-tpm-mode-default.md)

   -또는-

   [기존 요새 포리스트에서 HGS 클러스터 초기화](guarded-fabric-initialize-hgs-tpm-mode-bastion.md)

2. [신뢰할 수 있는 TPM 루트 인증서 설치](guarded-fabric-install-trusted-tpm-root-certificates.md)   
3. [패브릭 DNS 구성](guarded-fabric-configuring-fabric-dns.md)

