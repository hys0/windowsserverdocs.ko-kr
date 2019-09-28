---
title: OTP 인증을 통한 원격 액세스 구성
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82505b18-dd77-4dd1-aa27-b2962b8241ca
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c4340b59fd797d5d9d0e6270409b562128c0ccc1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404418"
---
# <a name="configure-remote-access-with-otp-authentication"></a>OTP 인증을 통한 원격 액세스 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

 Windows Server 2016 및 Windows Server 2012에서는 DirectAccess 및 RRAS (라우팅 및 원격 액세스 서비스) VPN을 단일 원격 액세스 역할로 결합 합니다. 이 개요에서는 단일 Windows Server 2016 또는 Windows Server 2012 원격 액세스 멀티 사이트 배포를 배포 하기 위해 필요한 구성 단계를 소개 합니다.  


- [1단계: 단일 서버 원격 액세스 배포 @ no__t-0을 구현 합니다. 단일 원격 액세스 서버를 설치 하 고 구성 합니다. 자세한 내용은 [고급 설정을 사용 하 여 단일 DirectAccess 서버 배포](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings)를 참조 하세요.

- [2단계: RADIUS 서버 @ no__t-0을 구성 합니다.

- [3단계: OTP @ no__t-0에 대 한 원격 액세스 서버를 구성 합니다.

- [4단계: OTP @ no__t-0을 사용 하 여 DirectAccess를 확인 합니다.
  


