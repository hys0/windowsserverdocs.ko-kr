---
title: 멀티 사이트 배포 계획
description: 이 가이드의 일부인이 항목에서는 여러 원격 액세스 서버 배포 Windows Server 2016에서 멀티 사이트 배포에서 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8387eabe-7363-4367-b5b1-03c67baa2933
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ba813fc5da53e9635e9ef1363f1a559a29419312
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282598"
---
# <a name="plan-a-multisite-deployment"></a>멀티 사이트 배포 계획

>적용 대상: Windows Server (반기 채널), Windows Server 2016

 Windows Server 2016, Windows Server 2012 DirectAccess 및 라우팅 및 원격 액세스 서비스 (RRAS) VPN 단일 원격 액세스 역할로 결합합니다. 이 개요에서는 멀티 사이트 구성에서 Windows Server 2016 또는 Windows Server 2012 원격 액세스를 배포 하는 데 필요한 계획 단계를 소개 합니다.  
  
1.  [고급 설정 사용 하 여 단일 DirectAccess 서버 배포](https://technet.microsoft.com/library/hh831436(v=ws.11).aspx)합니다. 이 단계는 단일 서버를 배포 하는 데 필요한 인프라에 대 한 계획이 포함 됩니다. 네트워크 및 서버 설정, 인증서 요구 사항, DNS 설정, 네트워크 위치 서버 배포, DirectAccess 관리 서버, Active Directory 설정 및 그룹 정책 개체 (Gpo)에 대 한 계획이 포함 됩니다.  
  
2.  [2 단계 계획 멀티 사이트 인프라](Step-2-Plan-the-Multisite-Infrastructure.md)합니다. 이 단계는 Active Directory 및 GPO 계획 및 DNS 구성을 포함 합니다.  
  
3.  [3 단계 계획 멀티 사이트 배포](Step-3-Plan-the-Multisite-Deployment.md)합니다. 이 단계는 계획 인증서 설정, 네트워크 위치 서버 구성, 클라이언트 항목 지점 설정, IPv6 접두사 설정 및 필요에 따라 전역 부하 분산 설정 포함 됩니다.  
  
> [!NOTE]  
> 원격 액세스 고급 배포를 위한 계획 관련 결정 사항을 기록 합니다. 배포 단계를 완료하는 데 참여하는 모든 사람은 이 기록을 작업 보조 자료로 활용할 수 있습니다.  
  
이러한 계획 단계를 완료 한 후 [멀티 사이트 배포를 구성](../configure/Configure-a-Multisite-Deployment.md)합니다.  
  


