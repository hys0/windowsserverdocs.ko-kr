---
title: 디스크 보호를 사용하여 시스템 볼륨 보호
description: MultiPoint 서비스의 디스크 보호에 대 한 정보를 제공 합니다.
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18694665-ed65-4d84-8505-f460cf3df907
author: evaseydl
manager: scotman
ms.author: evas
ms.openlocfilehash: 27bcce68cfe5856e987f5ad93460abd12217c26b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389512"
---
# <a name="protecting-the-system-volume-with-disk-protection"></a>디스크 보호를 사용하여 시스템 볼륨 보호
MultiPoint 서비스는 컴퓨터가 시작 될 때마다 시스템 볼륨에 대 한 변경 내용을 즉시 지울 수 있는 옵션을 제공 합니다. 디스크 보호 기능을 사용 하도록 설정 하면 다음에 컴퓨터를 다시 시작할 때 구성 손상이 나 맬웨어 도입 등 드라이브에 대 한 모든 수정 내용이 취소 됩니다. 이것은 알려진 "양호" 또는 "골든" 소프트웨어 이미지가 매번 로드 되도록 하려는 관리자에 게 편리한 기능입니다. 예를 들어 야간 도중에 자동 업데이트 또는 소프트웨어 패치를 예약할 수 있습니다. 계획 고려 사항은 최종 사용자가 인터넷에서 소프트웨어를 설치 하는 등의 변경 작업을 수행할 수 있도록 할지 여부입니다. 이 기능을 사용 하도록 설정 하면 사용자가 파일을 저장할 수 있도록 하려면 파일 공유가 시스템 볼륨의 외부에 있어야 합니다.  
  
