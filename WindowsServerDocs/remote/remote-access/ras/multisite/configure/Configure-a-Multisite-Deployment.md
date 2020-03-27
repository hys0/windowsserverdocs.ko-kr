---
title: 멀티 사이트 배포 구성
description: 이 항목은 Windows Server 2016에서 멀티 사이트 배포에서 여러 원격 액세스 서버 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb84920e-7cf5-4266-b071-d09e3d5e1f10
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 4a0229d5605271876f89e8e0ae75f8612e3f5762
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314012"
---
# <a name="configure-a-multisite-deployment"></a>멀티 사이트 배포 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

 Windows Server 2016에서는 DirectAccess와 RAS (원격 액세스 서비스) VPN이 단일 원격 액세스 역할로 결합 됩니다. 이 개요에서는 단일 Windows Server 2016 또는 Windows Server 2012 원격 액세스 멀티 사이트 배포를 배포 하기 위해 필요한 구성 단계를 소개 합니다.  
  
-   1 단계: [고급 설정을 사용 하 여 단일 DirectAccess 서버를 배포](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings)합니다. 단일 원격 액세스 서버를 설치 하 고 구성 합니다. 멀티 사이트 배포에서는 멀티 사이트 배포를 구성 하기 전에 단일 서버를 설치 해야 합니다.  
  
-   [2 단계: 멀티 사이트 인프라를 구성](Step-2-Configure-the-Multisite-Infrastructure.md)합니다. 멀티 사이트 배포의 경우 추가 Active Directory 사이트 및 도메인 컨트롤러를 구성 해야 합니다. 자동으로 구성 된 Gpo를 사용 하지 않는 경우 추가 보안 그룹 및 Gpo (그룹 정책 개체)도 필요 합니다.  
  
-   [3 단계: 멀티 사이트 배포 구성](Step-3-Configure-the-Multisite-Deployment.md)-추가 원격 액세스 서버에 원격 액세스 역할을 설치 하 고, 멀티 사이트 배포를 사용 하도록 설정 하 고, 추가 서버를 배포에 대 한 진입점으로 구성 합니다.  
  
-   [4 단계: 멀티 사이트 배포 확인](Step-4-Verify-the-Multisite-Deployment.md) 
  


