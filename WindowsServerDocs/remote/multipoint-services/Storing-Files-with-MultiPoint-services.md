---
title: MultiPoint 서비스를 사용하여 파일 저장
description: MultiPoint 서비스에서 파일 저장소에 대 한 자세한 정보
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c9eb0461-3846-4ddc-97ff-de10f03f30cf
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: bf31f5c582cffb5b38cff8cb15fcfdb4b3f76386
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389303"
---
# <a name="storing-files-with-multipoint-services"></a>MultiPoint 서비스를 사용하여 파일 저장
MultiPoint 서비스는 다음과 같은 방법으로 사용자 파일을 저장 하도록 지원 합니다.  
  
-   **하드 디스크 드라이브의 운영 체제 파티션에 있습니다.** 기본적으로 MultiPoint 서비스는 운영 체제를 사용 하 여 하드 디스크 드라이브에 사용자 파일을 저장 합니다.  
  
-   **하드 디스크 드라이브의 별도 파티션에 있습니다.** MultiPoint 서비스 시스템을 처음으로 설정 하는 경우 하드 디스크 드라이브를 *분할할* 수 있습니다. 즉, 별도 드라이브인 것 처럼 작동 하도록 드라이브의 섹션을 구성할 수 있습니다. 이렇게 하면 사용자 파일에 영향을 주지 않고 운영 체제를 더 쉽게 복원 하거나 업그레이드할 수 있습니다. 자세한 내용은 Windows Server 기술 라이브러리에서 [파티션 또는 논리 드라이브 만들기](https://go.microsoft.com/fwlink/?LinkId=182618) 를 참조 하세요.  
  
-   **추가 내부 또는 외부 하드 디스크 드라이브** 데이터를 저장 하 고 백업 하기 위해 MultiPoint 서비스에 추가 내부 또는 외부 하드 디스크 드라이브를 연결할 수 있습니다.  
  
-   **공유 네트워크 폴더에 있습니다.** 모든 스테이션에서 사용자 파일을 사용할 수 있도록 하려면 네트워크에서 공유 폴더를 만들 수 있습니다. 이 경우 MultiPoint 서비스를 실행 하는 컴퓨터 외에 다른 컴퓨터 또는 서버가 필요 합니다. 사용할 수 있는 파일 서버가 있는 경우 파일을 저장 하는 데 권장 되는 방법입니다.  
  
    파일 서버를 사용할 수 없는 MultiPoint 서비스를 실행 하는 컴퓨터 2-3 대의 소규모 시스템의 경우 multipoint 서비스 컴퓨터 중 하나가 모든 MultiPoint 서비스 컴퓨터의 파일 서버 역할을 할 수 있습니다. 그런 다음 파일 서버 역할을 하는 MultiPoint 서비스에서 모든 사용자에 대 한 사용자 계정을 만듭니다.  
  
