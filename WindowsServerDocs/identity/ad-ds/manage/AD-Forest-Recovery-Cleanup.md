---
title: AD 포리스트 복구-정리
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: fa7193cc800eac0fee6425a66bd5cd82d8c822c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868964"
---
# <a name="ad-forest-recovery---cleanup"></a>AD 포리스트 복구-정리

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

 필요에 따라 다음 복구 후 단계를 수행 합니다.  
  
- 전체 포리스트에 복구한 후에 Dc의 각 기본 및 대체 DNS 서버 구성을 포함 하 여 원래 DNS 구성으로 되돌릴 수 있습니다. DNS 서버는 오작동 되기 전의 구성한 후 해당 이전 이름 확인 기능 복원 됩니다. 복구 되지 않았습니다 하는 Dc에 대 한 DNS 레코드를 삭제 합니다.  
- 복구 하지 못한 모든 Dc에 대 한 Windows 인터넷 이름 서비스 WINS () 레코드를 삭제 합니다.  
- 도메인 이나 포리스트에서 다른 도메인 컨트롤러로 작업 마스터 역할을 전송 하 고 실패 하기 전에 구성에 따라 더 많은 글로벌 카탈로그 서버를 추가할 수 있습니다.  
- 전체 포리스트에 이전 상태로 복원 되 면 때문에 추가 된 모든 개체 (예: 사용자 및 컴퓨터) 및 (예: 암호 변경)이이 시점 이후에 기존 개체에 대 한 모든 업데이트가 손실 됩니다. 따라서 누락 된 개체를 다시 만드는 하 고 적절 하 게 누락 된 업데이트를 다시 적용 해야 합니다.  
- 백업에서 이러한 외부 트러스트 관계를 자동으로 복원 되지 않습니다 때문에 외부 도메인 및 포리스트를 사용 하 여 보내는 트러스트를 복원 하려면 할 수도 있습니다.

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)  
