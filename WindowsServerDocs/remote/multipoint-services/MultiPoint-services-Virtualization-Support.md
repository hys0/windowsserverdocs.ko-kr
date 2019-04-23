---
title: MultiPoint 서비스 가상화 지원
description: Hyper-v를 사용 하 여 MultiPoint 서비스를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f0864b8-a087-4890-94ef-05efbd3c4241
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 06d518dcea154ac2bab49a7d0e83a90f96be6e44
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872524"
---
# <a name="multipoint-services-virtualization-support"></a>MultiPoint 서비스 가상화 지원
MultiPoint 서비스는 두 가지 방법으로 Hyper-v 역할을 지원합니다.  
  
-   Hyper-v를 실행 하는 서버에서 게스트 운영 체제로 multiPoint 서비스를 배포할 수 있습니다.  
  
-   MultiPoint 서비스 가상화 서버로 사용할 수 있습니다.   
  
가상 컴퓨터에서 MultiPoint 서비스를 실행 중인 운영 체제를 관리 하기 위한 Hyper-v 도구 사용을 제공 합니다. 이러한 도구에는 검사점 및 롤백 기능을 포함 하며이 통해 가상 컴퓨터를 가져오고 내보낼 수 있습니다. 대규모 설치를 위해 단일 실제 서버에 여러 MultiPoint 서비스 가상 컴퓨터를 실행 하 여 서버를 통합할 수 있습니다. 가능한 시나리오는 다음과 같습니다.  
  
-   단일 클래스 룸 또는 랩에 20 개가 넘는 실제 사용자 수 있습니다. MultiPoint 서비스를 실행 하는 여러 물리적 컴퓨터를 배포 하는 대신 단일 물리적 컴퓨터에서 여러 가상 컴퓨터를 배포할 수 있습니다.  
  
    > [!NOTE]  
    > 실제 또는 가상 다중 포인트 관리자 콘솔을 통해 여러 MultiPoint 서버를 관리할 수 있습니다.  
  
-   MultiPoint 서버는 동일한 물리적 컴퓨터의 다른 서버 인프라를 사용 하 여 가상 컴퓨터에서 실행 됩니다. 이 경우이 서버 인프라에는 도메인, 보안 및 네트워크에 대 한 데이터 중앙 집중화합니다. MultiPoint 서버에는 중앙에 집중 하는 데스크톱 및 원격 데스크톱 서비스를 제공 합니다.  
  
> [!NOTE]  
> 가상 컴퓨터에서 MultiPoint 서비스를 실행 하는 경우에 USB-이더넷 및 RDP 클라이언트 스테이션 지원 됩니다. 직접 비디오 및 USB 제로 클라이언트 연결 스테이션 지원 되지 않습니다.  
  
Hyper-v 역할에 대 한 자세한 내용은 참조 하세요. [Hyper-v](../../virtualization/hyper-v/hyper-v-on-windows-server.md)합니다.  