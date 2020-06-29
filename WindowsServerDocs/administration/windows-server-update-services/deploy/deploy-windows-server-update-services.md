---
title: Windows Server Update Services 배포
description: WSUS(Windows Server Update Service) 항목 - 수행할 4단계에 대한 링크가 포함된 배포 프로세스 개요
ms.prod: windows-server
ms.technology: manage-wsus
ms.topic: get-started-article
ms.assetid: 2708f6b2-4252-4b8f-9b7e-84c9b4222075
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b9cc96badad864a0d76ef6295c604ff22ca4455f
ms.sourcegitcommit: fb808a6fc851a3e5c47e6a7654366145d2f19554
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84740616"
---
# <a name="deploy-windows-server-update-services"></a>Windows Server Update Services 배포

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

WSUS(Windows Server Update Services)를 사용하면 정보 기술 관리자가 최신 Microsoft 제품 업데이트를 배포할 수 있습니다. WSUS는 업데이트를 관리 및 분산하는 데 설치할 수 있는 Windows Server 서버 역할입니다. WSUS 서버는 조직 내 다른 WSUS 서버의 업데이트 원본이 될 수 있습니다. 업데이트 원본으로 사용되는 WSUS 서버를 업스트림 서버라고 합니다.  

WSUS 구현에서 사용 가능한 업데이트 정보를 얻으려면 네트워크에 있는 하나 이상의 WSUS 서버가 Microsoft 업데이트에 연결되어 있어야 합니다. 여기에서 확인할 수 있습니다 네트워크 보안 및 구성에 따라 다른 서버의 수 직접 Microsoft 업데이트에 연결 합니다.  

이 가이드는 계획 및 Windows Server Update Service 배포에 대 한 개념 정보를 제공 합니다.  

-   [WSUS 배포 계획](../plan/plan-your-wsus-deployment.md)  

-   [1단계: WSUS 서버 역할 설치](1-install-the-wsus-server-role.md)  

-   [2단계: WSUS 구성](2-configure-wsus.md)  

-   [3단계: WSUS에서 업데이트 승인 및 배포](3-approve-and-deploy-updates-in-wsus.md)  

-   [4단계: 자동 업데이트를 위한 그룹 정책 설정 구성](4-configure-group-policy-settings-for-automatic-updates.md)  
