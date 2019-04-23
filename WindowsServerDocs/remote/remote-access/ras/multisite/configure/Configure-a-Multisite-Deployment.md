---
title: 멀티 사이트 배포 구성
description: 이 가이드의 일부인이 항목에서는 여러 원격 액세스 서버 배포 Windows Server 2016에서 멀티 사이트 배포에서 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb84920e-7cf5-4266-b071-d09e3d5e1f10
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b602855db271348ac48ee0a5691424a7321c7370
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849754"
---
# <a name="configure-a-multisite-deployment"></a>멀티 사이트 배포 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

 Windows Server 2016는 DirectAccess 및 원격 액세스 서비스 (RAS) VPN 단일 원격 액세스 역할로 결합합니다. 이 개요에서는 단일 Windows Server 2016 또는 Windows Server 2012 원격 액세스 멀티 사이트 배포를 배포 하는 데 필요한 구성 단계를 소개 합니다.  
  
-   1단계: [고급 설정 사용 하 여 단일 DirectAccess 서버 배포](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings)합니다. 설치 하 고 단일 원격 액세스 서버를 구성 합니다. 멀티 사이트 배포에 멀티 사이트 배포를 구성 하기 전에 단일 서버를 설치 해야 합니다.  
  
-   [2단계: 멀티 사이트 인프라 구성](Step-2-Configure-the-Multisite-Infrastructure.md)합니다. 멀티 사이트 배포에 대 한 추가 Active Directory 사이트 및 도메인 컨트롤러를 구성 해야 합니다. 추가 보안 그룹 및 그룹 정책 개체 (Gpo) 자동으로 구성 된 Gpo를 사용 하지 않는 경우 필요한 수 있습니다.  
  
-   [3 단계: 멀티 사이트 배포를 구성할](Step-3-Configure-the-Multisite-Deployment.md)-추가 원격 액세스 서버에서 원격 액세스 역할을 설치, 멀티 사이트 배포, 사용 및 배포에 대 한 진입점으로 추가 서버를 구성 합니다.  
  
-   [4 단계: 멀티 사이트 배포를 확인 합니다.](Step-4-Verify-the-Multisite-Deployment.md) 
  


