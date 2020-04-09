---
title: 관리자가 신뢰할 수 있는 증명을 사용 하 여 HGS 초기화
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: b7c0b88071a28953ddda8abb57a805ef119511e0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856676"
---
# <a name="initialize-hgs-using-admin-trusted-attestation"></a>관리자가 신뢰할 수 있는 증명을 사용 하 여 HGS 초기화

>적용 대상: Windows Server(반기 채널), Windows Server 2016

>[!IMPORTANT]
>관리자가 신뢰할 수 있는 증명 (AD 모드)은 Windows Server 2019부터 사용 되지 않습니다. TPM 증명을 사용할 수 없는 환경의 경우 [호스트 키 증명](guarded-fabric-initialize-hgs-key-mode.md)을 구성 합니다. 호스트 키 증명은 AD 모드와 비슷한 보증을 제공 하 고 설정 하는 것이 더 간단 합니다. 


이러한 단계는 새 포리스트나 기존 요새 포리스트에서 HGS를 초기화 하는지에 따라 달라 집니다.

1. [새 포리스트에서 HGS 클러스터 초기화 (기본값)](guarded-fabric-initialize-hgs-ad-mode-default.md)

   -또는-

   [기존 요새 포리스트에서 HGS 클러스터 초기화](guarded-fabric-initialize-hgs-ad-mode-bastion.md)

2. [패브릭 도메인에서 DNS 전달 구성](guarded-fabric-configuring-fabric-dns.md)

3. [HGS 도메인에서 DNS 전달 및 단방향 트러스트 구성](guarded-fabric-configure-dns-forwarding-and-trust.md)



