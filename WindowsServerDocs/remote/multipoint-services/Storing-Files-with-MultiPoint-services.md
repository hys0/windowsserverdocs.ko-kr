---
title: MultiPoint 서비스를 사용하여 파일 저장
description: MultiPoint 서비스에서 파일 저장소에 대해 알아보기
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c9eb0461-3846-4ddc-97ff-de10f03f30cf
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: b432ca793b156997761f9fadab7340c394e3b553
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817344"
---
# <a name="storing-files-with-multipoint-services"></a>MultiPoint 서비스를 사용하여 파일 저장
MultiPoint 서비스는 다음과 같은 방법으로 사용자 파일 저장을 지원합니다.  
  
-   **하드 디스크 드라이브의 운영 체제 파티션에 합니다.** 기본적으로 MultiPoint 서비스는 운영 체제를 사용 하 여 하드 디스크 드라이브에 사용자 파일을 저장합니다.  
  
-   **하드 디스크 드라이브의 개별 파티션에 합니다.** MultiPoint 서비스 시스템을 처음으로 설치 되 면 수행할 수 있습니다 *파티션* 하드 디스크 드라이브입니다. 즉, 별도 드라이브 것 처럼 작동 하는 드라이브의 섹션을 구성할 수 있습니다. 이 쉽게 복원 하거나 사용자 파일에 영향을 주지 않고 운영 체제를 업그레이드 합니다. 자세한 내용은 [파티션을 만들거나 논리 드라이브](https://go.microsoft.com/fwlink/?LinkId=182618) Windows Server 기술 라이브러리에서.  
  
-   **추가 내부 또는 외부 하드 디스크 드라이브에 있습니다.** MultiPoint 서비스를 저장 하 고 데이터를 백업에 대 한 추가 내부 또는 외부 하드 디스크 드라이브를 연결할 수 있습니다.  
  
-   **공유 네트워크 폴더.** 사용자 파일을 사용 하려면 모든 스테이션에서 네트워크 공유 폴더를 만들 수 있습니다. MultiPoint 서비스를 실행 하는 컴퓨터 외에도 다른 서버나 컴퓨터 필요 합니다. 이것이 파일 서버를 사용할 수 있는 경우 파일을 저장 하기 위한 권장된 방법입니다.  
  
    사용할 수 없는 파일 서버를 사용 하 여 MultiPoint 서비스를 실행 하는 2 ~ 3 컴퓨터의 시스템의 작은 경우 MultiPoint 서비스 컴퓨터 중 하나는 MultiPoint 서비스 컴퓨터의 모든 파일 서버와 작동할 수 있습니다. 그런 다음 모든 사용자에 대 한 사용자 계정을 파일 서버 역할을 하는 MultiPoint 서비스에서 만듭니다.  
  
