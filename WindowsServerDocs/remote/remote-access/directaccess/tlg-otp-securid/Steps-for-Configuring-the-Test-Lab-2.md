---
title: 테스트 랩 구성 단계
description: 이 항목은 테스트 랩 가이드-OTP 인증을 사용 하는 DirectAccess 시연 및 Windows Server 2016에 대 한 RSA SecurID의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a40183c-afd1-43ca-b306-05745640a37d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ef5ce37983b8565fab8287eeaae7423be0c269f6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404730"
---
# <a name="steps-for-configuring-the-test-lab"></a>테스트 랩 구성 단계

>적용 대상: Windows Server(반기 채널), Windows Server 2016

다음 단계에서는 원격 액세스 인프라를 구성 하 고, 원격 액세스 서버 및 클라이언트를 구성 하 고, Ho Et 및 인터넷 서브넷에서 DirectAccess 연결을 테스트 하는 방법을 설명 합니다.  
  
이 테스트 랩 가이드에서는 다음 단계를 수행 하 여 OTP 환경에서 원격 액세스를 작성 합니다.  
  
-   [1 단계: DirectAccess 구성 완료](assetId:///4dbf877f-02fb-439b-907a-f5b3f1d8afa6) [테스트 랩 가이드: IPv4 및 IPv6 혼합을 사용 하 여 DirectAccess 단일 서버 설정 시연](https://go.microsoft.com/fwlink/p/?LinkId=237004)의 모든 단계를 완료 합니다.  
  
-   [2 단계: APP1 구성](assetId:///c1bb590f-91d4-4ed5-bceb-b0e36eabd4ff) EDGE1에서 사용할 OTP 인증서 템플릿을 사용 하 여 APP1를 구성 합니다.  
  
-   [3 단계: DC1 구성](assetId:///904a6edc-a771-45ed-9630-a34a680bb522) DC1에 정의 된 사용자 계정 이름을 확인 합니다.  
  
-   [7 단계: RSA를 설치 하 고 구성](assetId:///baa4c28c-add7-42e2-8afd-ccc7a559406a)합니다. RSA, RADIUS 및 OTP 서버를 설치 및 구성 하 고 OTP에 대해 EDGE1를 구성 합니다.  
  
-   [11 단계: EDGE1에서 OTP 상태를 확인](assetId:///3b397a4a-8478-47f2-a932-9e8e048c14ba)합니다. 원격 액세스 서버에서 OTP의 상태가 정상 인지 확인 합니다.  
  
-   [8 단계: Ho et 서브넷에서 DirectAccess 연결을 테스트](assetId:///ba1652a6-0692-4add-91ca-34a84956ba14)합니다. NAT 장치 뒤에서 DirectAccess OTP 기능을 테스트 합니다.  
  
-   [10 단계: 인터넷에서 DirectAccess 연결을 테스트](assetId:///321149eb-5f23-4a0b-b8fb-1244540126e9)합니다. 인터넷에서 DirectAccess 클라이언트 연결을 테스트 합니다.  
  
-   [12 단계: 구성 스냅숏 만들기](assetId:///8a51ed3c-9c32-402f-85d1-617ce46845b4) 테스트 랩을 완료 한 후에는 나중에 추가 시나리오를 테스트할 수 있도록 OTP 구성을 사용 하 여 작동 하는 DirectAccess의 스냅숏을 만듭니다.  
  


