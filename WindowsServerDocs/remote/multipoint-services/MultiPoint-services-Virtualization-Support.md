---
title: MultiPoint 서비스 가상화 지원
description: Hyper-v에서 MultiPoint 서비스를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f0864b8-a087-4890-94ef-05efbd3c4241
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 7b94b4a4015e58402a62cf74f9abbb3eb2333f26
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71395190"
---
# <a name="multipoint-services-virtualization-support"></a>MultiPoint 서비스 가상화 지원
MultiPoint 서비스는 두 가지 방법으로 Hyper-v 역할을 지원 합니다.  
  
-   MultiPoint 서비스는 Hyper-v를 실행 하는 서버에 게스트 운영 체제로 배포할 수 있습니다.  
  
-   MultiPoint 서비스는 가상화 서버로 사용할 수 있습니다.   
  
가상 머신에서 MultiPoint 서비스를 실행 하면 Hyper-v 도구를 사용 하 여 운영 체제를 관리할 수 있습니다. 이러한 도구에는 검사점 및 롤백 기능이 포함 되며,이를 통해 가상 컴퓨터를 내보내고 가져올 수 있습니다. 대규모 설치의 경우 단일 물리적 서버에서 다중 MultiPoint 서비스 가상 컴퓨터를 실행 하 여 서버를 통합할 수 있습니다. 가능한 시나리오는 다음과 같습니다.  
  
-   단일 교실 또는 랩에서는 20 명 이상의 사용자가 있습니다. MultiPoint 서비스를 실행 하는 여러 물리적 컴퓨터를 배포 하는 대신 단일 물리적 컴퓨터에 여러 가상 컴퓨터를 배포할 수 있습니다.  
  
    > [!NOTE]  
    > 단일 MultiPoint 관리자 콘솔을 통해 실제 또는 가상의 다중 포인트 서버를 관리할 수 있습니다.  
  
-   MultiPoint 서버가 동일한 물리적 컴퓨터의 다른 서버 인프라를 사용 하는 가상 컴퓨터에서 실행 되 고 있습니다. 이 경우이 서버 인프라는 네트워크에 대 한 도메인, 보안 및 데이터를 중앙 집중화 합니다. MultiPoint server는 원격 데스크톱 서비스을 제공 하 고 데스크톱을 중앙 집중화 합니다.  
  
> [!NOTE]  
> 가상 머신에서 MultiPoint 서비스를 실행 하는 경우 USB over 이더넷 및 RDP 클라이언트 스테이션이 지원 됩니다. 직접 비디오 및 USB 제로 클라이언트 연결 스테이션은 지원 되지 않습니다.  
  
Hyper-v 역할에 대 한 자세한 내용은 [hyper-v](../../virtualization/hyper-v/hyper-v-on-windows-server.md)를 참조 하세요.  