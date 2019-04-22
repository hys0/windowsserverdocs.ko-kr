---
title: HGS 관리자 신뢰할 수 있는 증명을 사용 하 여 초기화
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 664404cb72981e162bca016df14847e684d987c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821834"
---
# <a name="initialize-hgs-using-admin-trusted-attestation"></a>HGS 관리자 신뢰할 수 있는 증명을 사용 하 여 초기화

>적용 대상: Windows Server (반기 채널), Windows Server 2016

>[!IMPORTANT]
>관리자-신뢰할 수 있는 증명 (AD 모드)는 Windows Server 2019로 시작 하는 사용 되지 않습니다. TPM 증명 수 없는 환경에 대 한 구성 [호스트 키 증명](guarded-fabric-initialize-hgs-key-mode.md)합니다. 호스트 키 증명 AD 모드에 유사한 보증을 제공 하며 간단 하 게 설정 합니다. 


이러한 단계는 새 포리스트 또는 기존 배스 천 포리스트는 HGS를 초기화 하는 여부에 따라 달라 집니다.

1. [(기본값)를 새 포리스트의 HGS 클러스터를 초기화 합니다.](guarded-fabric-initialize-hgs-ad-mode-default.md)

   -또는-

   [기존 배스 천 포리스트의 HGS 클러스터를 초기화 합니다.](guarded-fabric-initialize-hgs-ad-mode-bastion.md)

2. [Fabric 도메인에서 DNS 전달 구성](guarded-fabric-configuring-fabric-dns.md)

3. [DNS 전달 및 HGS 도메인에서 단방향 트러스트를 구성 합니다.](guarded-fabric-configure-dns-forwarding-and-trust.md)



