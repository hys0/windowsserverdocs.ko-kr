---
title: 테스트 랩 구성 단계
description: 이 항목은 테스트 랩 가이드-Windows Server 2016에 대 한 DirectAccess 멀티 사이트 배포 시연의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc7205b4-a822-4038-ab67-ec0a870737f2
ms.author: pashort
author: shortpatti
ms.openlocfilehash: dd8b8864dff98e51bf55aad9307523df4a0c30bf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404699"
---
# <a name="steps-for-configuring-the-test-lab"></a>테스트 랩 구성 단계

>적용 대상: Windows Server(반기 채널), Windows Server 2016

다음 단계에서는 원격 액세스 인프라를 구성 하 고, 원격 액세스 서버 및 클라이언트를 구성 하 고, 인터넷 및 Ho Et 서브넷에서 DirectAccess 연결을 테스트 하는 방법을 설명 합니다.  
  
이 테스트 랩 가이드에서는 다음 단계를 수행 하 여 멀티 사이트 원격 액세스 배포를 구축 합니다.  
  
-   [1단계: 기본 구성 @ no__t-0을 완료 합니다. @No__t-0 테스트 랩 가이드의 모든 단계를 완료 합니다. IPv4 및 IPv6 @ no__t를 혼합 하 여 DirectAccess 단일 서버 설치를 시연 합니다.  
  
-   [2단계: ROUTER1 @ no__t-0을 설치 하 고 구성 합니다. ROUTER1은 Corpnet 및 Corpnet 서브넷 간의 라우팅 및 전달 기능을 제공 합니다.  
  
-   [3단계: CLIENT2 @ no__t-0을 설치 하 고 구성 합니다. CLIENT2는 windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 원격 액세스 배포의 이전 버전과의 호환성을 보여 주는 데 사용 되는 Windows 7 클라이언트 컴퓨터입니다.  
  
-   [4단계: APP1 @ no__t-0을 구성 합니다. APP1를 기본 게이트웨이로 사용 하 고 2-d c 2를 대체 DNS 서버로 구성 합니다.  
  
-   [5단계: DC1 @ no__t-0을 구성 합니다. 추가 Active Directory 사이트와 Windows 7 클라이언트 컴퓨터에 대 한 추가 보안 그룹을 사용 하 여 DC1을 구성 합니다.  
  
-   [6단계: 2-DC1 @ no__t-0을 설치 하 고 구성 합니다. 멀티 사이트 배포에는 두 개 이상의 도메인 및 사이트가 있습니다. 2-DC1은 corp2.corp.contoso.com 도메인에 대 한 도메인 컨트롤러 및 DNS 서비스를 제공 합니다.  
  
-   [7단계: APP1 @ no__t-0을 설치 하 고 구성 합니다. 2-APP1는 2 Corpnet 네트워크의 웹 및 파일 서버입니다.  
  
-   [8단계: INET1 @ no__t-0을 구성 합니다. INET1는이 테스트 랩 가이드에서 인터넷을 시뮬레이트합니다. 2-EDGE1의 공용 IP 주소로 확인 되는 DNS 항목을 구성 해야 합니다.  
  
-   [9단계: EDGE1 @ no__t-0을 구성 합니다. EDGE1에서 2-Corpnet DNS 서버 및 라우팅을 구성 합니다.  
  
-   [10단계: EDGE1 @ no__t-0을 설치 하 고 구성 합니다. 멀티 사이트 배포에는 두 개의 원격 액세스 서버가 필요 합니다. 2-EDGE1는 두 번째 도메인에 대 한 원격 액세스 서비스를 제공 합니다.  
  
-   [11단계: 멀티 사이트 배포 @ no__t-0을 구성 합니다. 원격 액세스 서버를 모두 구성한 후에는 멀티 사이트 배포를 구성할 수 있습니다.  
  
-   [12단계: DirectAccess 연결 테스트 @ no__t-0. EDGE1 및 2 EDGE1를 통해 인터넷 서브넷의 클라이언트 컴퓨터에서 DirectAccess 연결을 테스트 합니다.  
  
-   [13단계: NAT 장치 뒤에서 DirectAccess 연결을 테스트 @ no__t-0. NAT 장치 뒤에서 DirectAccess 연결을 테스트 합니다.  
  
-   [14단계: 구성의 스냅숏 @ no__t-0 테스트 랩을 완료 한 후 나중에 다시 돌아가서 추가 시나리오를 테스트할 수 있도록 작동 하는 원격 액세스 멀티 사이트 배포의 스냅숏을 만듭니다.  
  


