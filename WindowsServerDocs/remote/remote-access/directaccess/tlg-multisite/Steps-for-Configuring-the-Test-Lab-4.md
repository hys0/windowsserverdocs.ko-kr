---
title: 테스트 랩 구성 단계
description: 이 항목에서는 테스트 랩 가이드의 일부인-DirectAccess 멀티 사이트 배포에 대 한 Windows Server 2016를 보여 줍니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc7205b4-a822-4038-ab67-ec0a870737f2
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a3d01dd8002e28fb127ac6b1b4cea25c58953521
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281389"
---
# <a name="steps-for-configuring-the-test-lab"></a>테스트 랩 구성 단계

>적용 대상: Windows Server (반기 채널), Windows Server 2016

다음 단계는 원격 액세스 인프라 구성, 원격 액세스 서버 및 클라이언트 구성, 인터넷 및 Homenet 서브넷에서 DirectAccess 연결을 테스트 하는 방법을 설명 합니다.  
  
이 테스트 랩 가이드에서 다음 단계를 수행 하 여 멀티 사이트 원격 액세스 배포를 빌드합니다.  
  
-   [1단계: 기본 구성을 완료](assetId:///9eb4a9ba-9118-4ea3-8963-e643ec81c3ed)합니다. 모든 단계를 완료 합니다 [테스트 랩 가이드: IPv4 및 IPv6을 사용 하 여 DirectAccess 단일 서버 설치 시연](https://go.microsoft.com/fwlink/p/?LinkId=237004)합니다.  
  
-   [2단계: 설치 및 구성 ROUTER1](assetId:///e4b1a298-d5b0-410e-970b-c5358a9378f9)합니다. ROUTER1 라우팅 및 전달을 Corpnet 및 2 Corpnet 서브넷 간에 기능을 제공 합니다.  
  
-   [3단계: 설치 하 고 CLIENT2 구성](assetId:///6cbee1b5-f6f6-443f-8fa9-31cc5c05a0ee)합니다. CLIENT2는 보여 주기 위해 사용 되는 Windows 7 클라이언트 컴퓨터는 이전 버전과 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 원격 액세스 배포의 호환성.  
  
-   [4단계: APP1 구성](assetId:///a0ee655e-c01e-4bf3-a7b3-064e9614f810)합니다. ROUTER1를 사용 하 여 기본 게이트웨이 및 2-DC1 대체 DNS 서버로 APP1을 구성 합니다.  
  
-   [5단계: DC1 구성](assetId:///205ca795-93ce-4e53-aa6b-b44c87f0e14a)합니다. 추가 Active Directory 사이트 및 Windows 7 클라이언트 컴퓨터에 대 한 추가 보안 그룹을 사용 하 여 DC1을 구성 합니다.  
  
-   [6단계: 설치 및 구성 2-DC1](assetId:///16752f61-edbf-4ff4-9d7a-e2077b66a127)합니다. 멀티 사이트 배포에서 두 개 이상의 도메인 및 사이트 수 있습니다. 2-DC1 도메인 컨트롤러 및 corp2.corp.contoso.com 도메인에 대 한 DNS 서비스를 제공합니다.  
  
-   [7단계: 설치 및 구성 2-APP1](assetId:///7d04b54e-590a-4d33-9766-415789859f29)합니다. 2-APP1에는 2 Corpnet 네트워크에서 웹 및 파일 서버입니다.  
  
-   [8단계: INET1 구성](assetId:///8ecc0b63-8626-4939-8d26-3d51d051d231)합니다. INET1이 테스트 랩 가이드에서 인터넷을 시뮬레이션합니다. 2-EDGE1의 공용 IP 주소로 확인 하는 DNS 항목을 구성 해야 합니다.  
  
-   [9단계: EDGE1 구성](assetId:///562744dc-30f6-42fa-bd5f-60a013b2179e)합니다. 2-회사 네트워크 DNS 서버 및 EDGE1에 라우팅을 구성 합니다.  
  
-   [10단계: 설치 및 구성 2 EDGE1](assetId:///1938c4f3-ca96-475d-9f2e-6bea3b7a4130)합니다. 두 가지 원격 액세스 서버를 멀티 사이트 배포에 필요 합니다. 2-EDGE1 두 번째 도메인에 대 한 원격 액세스 서비스를 제공합니다.  
  
-   [11단계: 멀티 사이트 배포 구성](assetId:///537e4b68-043f-49c9-94d8-15ce8c4b18e2)합니다. 모두 원격 액세스 서버를 구성한 후 멀티 사이트 배포를 구성할 수 있습니다.  
  
-   [12단계: DirectAccess 연결을 테스트](assetId:///aa293b5d-4b6f-4004-95f3-0ab54804b15c)합니다. EDGE1 및 2 EDGE1를 통해 인터넷 서브넷에서 모두 클라이언트 컴퓨터에서 DirectAccess 연결을 테스트 합니다.  
  
-   [13단계: NAT 장치 뒤에서 DirectAccess 연결을 테스트](assetId:///41f8195b-00a1-4991-9db8-3703514dbe0c)합니다. NAT 장치 뒤에서 DirectAccess 연결을 테스트 합니다.  
  
-   [14단계: 구성 스냅숏 만들기](assetId:///7b56d5c9-c334-463e-9e29-d652ca110d84)합니다. 테스트 실습을 마친 후 나중에 추가 시나리오를 테스트할로 돌아갈 수 있도록 원격 액세스 멀티 사이트 배포 작업의 스냅숏을 만듭니다.  
  


