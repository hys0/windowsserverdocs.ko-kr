---
title: AD 포리스트 복구-정리
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: c4e800f380cf75022c03e21b91f3b6f71cf79708
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369236"
---
# <a name="ad-forest-recovery---cleanup"></a>AD 포리스트 복구-정리

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

 필요에 따라 다음 복구 후 단계를 수행 합니다.  
  
- 전체 포리스트를 복구한 후에는 각 Dc에서 기본 설정 및 대체 DNS 서버 구성을 포함 하 여 원래 DNS 구성으로 되돌릴 수 있습니다. 오작동 이전에 DNS 서버가 구성 된 후에는 이전 이름 확인 기능이 복원 됩니다. 복구 되지 않은 Dc에 대 한 DNS 레코드를 삭제 합니다.  
- 복구 되지 않은 모든 Dc에 대해 WINS (Windows Internet Name Service) 레코드를 삭제 합니다.  
- 작업 마스터 역할을 도메인 이나 포리스트의 다른 Dc로 전송 하 고 실패 전 구성에 따라 글로벌 카탈로그 서버를 더 추가할 수 있습니다.  
- 전체 포리스트가 이전 상태로 복원 되기 때문에 추가 된 모든 개체 (예: 사용자 및 컴퓨터)와이 시점 이후에 기존 개체에 적용 된 모든 업데이트 (예: 암호 변경)는 손실 됩니다. 따라서 이러한 누락 된 개체를 다시 만들고 누락 된 업데이트를 적절 하 게 다시 적용 해야 합니다.  
- 외부 트러스트 관계가 백업에서 자동으로 복원 되지 않으므로 외부 도메인 및 포리스트와 나가는 트러스트를 복원 해야 할 수도 있습니다.

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)  
