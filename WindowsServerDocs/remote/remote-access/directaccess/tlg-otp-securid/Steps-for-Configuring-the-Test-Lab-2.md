---
title: 테스트 랩 구성 단계
description: 이 항목은 일부 테스트 랩 가이드-OTP 인증 및 Windows Server 2016 RSA SecurID를 사용한 DirectAccess 시연
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a40183c-afd1-43ca-b306-05745640a37d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0607506f2b6dd49284e6b377fb87da4f731eb94d
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283088"
---
# <a name="steps-for-configuring-the-test-lab"></a>테스트 랩 구성 단계

>적용 대상: Windows Server (반기 채널), Windows Server 2016

다음 단계는 원격 액세스 인프라 구성, 원격 액세스 서버 및 클라이언트를 구성 하 고 Homenet 및 인터넷 서브넷에서 DirectAccess 연결을 테스트 하는 방법을 설명 합니다.  
  
이 테스트 랩 가이드에서 다음 단계를 수행 하 여 원격 액세스 OTP 환경과 빌드합니다.  
  
-   [1단계: DirectAccess 구성을 완료할](assetId:///4dbf877f-02fb-439b-907a-f5b3f1d8afa6)합니다. 모든 단계를 완료 합니다 [테스트 랩 가이드: IPv4 및 IPv6을 사용 하 여 DirectAccess 단일 서버 설치 시연](https://go.microsoft.com/fwlink/p/?LinkId=237004)합니다.  
  
-   [2단계: APP1 구성](assetId:///c1bb590f-91d4-4ed5-bceb-b0e36eabd4ff)합니다. EDGE1 사용에 대 한 OTP 인증서 템플릿을 사용 하 여 APP1을 구성 합니다.  
  
-   [3단계: DC1 구성](assetId:///904a6edc-a771-45ed-9630-a34a680bb522)합니다. DC1에 정의 된 사용자 계정 이름 확인 합니다.  
  
-   [7단계: 설치 및 구성 RSA](assetId:///baa4c28c-add7-42e2-8afd-ccc7a559406a)합니다. 설치 및 RSA, RADIUS 및 OTP 서버를 구성 하 고 otp EDGE1를 구성 합니다.  
  
-   [11단계: EDGE1에서 OTP 상태를 확인](assetId:///3b397a4a-8478-47f2-a932-9e8e048c14ba)합니다. OTP의 상태를 원격 액세스 서버에서 정상 상태 인지 확인 합니다.  
  
-   [8단계: Homenet 서브넷에서 DirectAccess 연결을 테스트](assetId:///ba1652a6-0692-4add-91ca-34a84956ba14)합니다. NAT 장치 뒤에서 DirectAccess OTP 기능을 테스트 합니다.  
  
-   [10단계: 인터넷에서 DirectAccess 연결을 테스트](assetId:///321149eb-5f23-4a0b-b8fb-1244540126e9)합니다. 인터넷에서 DirectAccess 클라이언트 연결을 테스트 합니다.  
  
-   [12단계: 구성 스냅숏 만들기](assetId:///8a51ed3c-9c32-402f-85d1-617ce46845b4)합니다. 테스트 실습을 마친 후 나중에 추가 시나리오를 테스트할로 돌아갈 수 있도록 DirectAccess OTP 구성 작업의 스냅숏을 만듭니다.  
  


