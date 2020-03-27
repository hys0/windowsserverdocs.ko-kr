---
author: eross-msft
ms.author: lizross
ms.date: 10/02/2018
ms.prod: windows-server
ms:topic: include
ms.openlocfilehash: f2065acb89af4bed4dc525453bb5a294a4e2c3ef
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316496"
---
동적을 사용 하는 경우 아웃 바운드 로드는 TCP 포트 및 IP 주소의 해시에 따라 분산 됩니다. 또한 동적 모드는 지정 된 아웃 바운드 흐름이 팀 멤버 간에 앞뒤로 이동할 수 있도록 실시간으로 부하의 균형을 조정 합니다. 반면에 인바운드 로드는 Hyper-v 포트와 동일한 방식으로 배포 됩니다. 간단히 말해서 동적 모드는 주소 해시와 Hyper-v 포트의 가장 적합 한 측면을 활용 하며 가장 높은 부하 분산 모드입니다. 

