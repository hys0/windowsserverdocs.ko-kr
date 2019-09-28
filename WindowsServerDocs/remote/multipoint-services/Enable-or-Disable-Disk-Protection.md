---
title: 디스크 보호 사용 또는 사용 안 함
description: MultiPoint 서비스에서 디스크 보호를 사용 하는 방법 알아보기
ms.custom: na
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 00aba4c4-0244-4b39-8c85-c46fd96e1d6a
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: ad5f12a3901a3faf3559abae76e0ba924dce2eb9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389754"
---
# <a name="enable-or-disable-disk-protection"></a>디스크 보호 사용 또는 사용 안 함
디스크 보호 기능을 사용하면 시스템을 다시 시작할 때마다 MultiPoint 서비스 시스템을 지정된 상태로 다시 설정할 수 있습니다. 사용자는 디스크 보호를 사용하여 MultiPoint 서비스 시스템을 일시적으로 변경할 수 있습니다. 일시적인 변경이므로 서버가 다시 시작될 때 해당 변경 내용은 취소됩니다. 서버를 다시 시작할 때 삭제 되는 변경 사항의 예는 사용자 프로필 개인 설정, 파일 저장, 설정 변경 또는 응용 프로그램 설치를 포함 합니다.  
  
## <a name="enable-disk-protection"></a>디스크 보호를 사용 하도록 설정  
  
1.  다중 포인트 관리자에서 **홈** 탭을 클릭 한 다음 *컴퓨터 이름* **작업**에서 **디스크 보호 사용**을 클릭 합니다.  
  
2.  정보를 검토한 후 **확인**을 클릭합니다.  
  
시스템이 다시 시작된 이후에 설치된 새 응용 프로그램을 비롯하여 시스템에 대한 변경 내용은 다음번에 다시 시작될 때 취소됩니다.  
  
## <a name="disable-disk-protection"></a>디스크 보호 사용 안 함  
  
1.  다중 포인트 관리자에서 **홈** 탭을 클릭 한 다음 *컴퓨터 이름* **작업**에서 **디스크 보호 사용 안 함**을 클릭 합니다.  
  
2.  정보를 검토한 후 **확인**을 클릭합니다.  
  
시스템이 다시 시작된 이후에 서버에 설치된 응용 프로그램을 비롯하여 시스템에 대한 모든 변경 내용이 영구적으로 적용되며 다음번에 시스템이 다시 시작될 때 취소되지 않습니다.  
  
