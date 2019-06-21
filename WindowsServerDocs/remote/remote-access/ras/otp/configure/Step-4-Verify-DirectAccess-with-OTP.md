---
title: 4 단계 DirectAccess OTP 사용 하 여 확인
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed49a0a3-1c45-42e5-8f13-cad20c1c1d68
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1ce9fe1327cfad6409d66981e6baadc133fb92a6
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282404"
---
# <a name="step-4-verify-directaccess-with-otp"></a>4 단계 DirectAccess OTP 사용 하 여 확인

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 OTP 배포에 DirectAccess를 올바르게 구성 되었는지 확인 하는 방법을 설명 합니다.
  
### <a name="to-verify-otp-health-on-the-remote-access-server"></a>원격 액세스 서버의 OTP 상태를 확인 하려면

1. 열기 원격 액세스 서버에는 **원격 액세스 관리** 콘솔.  

2. 아래 **원격 액세스 서버** OTP 지원에 대해 구성 된 원격 액세스 서버를 클릭 합니다.  

3. 클릭 **작업 상태**합니다.  

4. OTP의 상태를 녹색 아이콘을 표시 하는 작업을 확인 합니다.  
  
    > [!NOTE]  
    > 상태 상태 업데이트 간격 HKLM\SYSTEM\CCS\Services\Ramgmtsvc\parameters\HealthRefreshTimeout 레지스트리 키에서 값을 합한 값의 최대 수와 **서버 작업에 대 한 시간 간격** 에 설정 된는 원격 액세스 구성 합니다.  
  
### <a name="to-verify-access-to-internal-resources-using-otp-authentication"></a>OTP 인증을 사용 하 여 내부 리소스에 대 한 액세스를 확인 하려면  
  
1.  회사 네트워크에 DirectAccess 클라이언트 컴퓨터를 연결 및 실행 **gpupdate /force** 그룹 정책을 가져오려면 명령 프롬프트에서.  
  
2.  클라이언트 컴퓨터는 회사 네트워크에서 분리, 외부 네트워크에 연결 및 내부 리소스에 액세스 하려고 합니다. 내부 리소스에 액세스할 수 없어야 합니다.  
  
3.  소프트웨어 토큰의 경우 공급 업체 지침을 사용 하 여 OTP 클라이언트 토큰을 액세스 하 고 현재 토큰 코드를 확인 합니다. 하드웨어 토큰을 사용 하면 인증에 대 한 공급 업체 지침을 따릅니다.  
  
4.  알림 영역에서 **네트워크 연결** 아이콘을 클릭하여 DA 미디어 관리자에 액세스합니다.  
  
5.  클릭 합니다 **DirectAccess 연결**, 클릭 **계속**합니다.  
  
6.  이전에 설명한 토큰 코드를 입력 하 고 클릭 **확인**합니다. 인증 완료 될 때까지 기다립니다. DirectAccess 작업 공간 연결 상태를 이제 됩니다 **Connected**합니다.  
  
7.  내부 리소스에 액세스 하려고 시도 합니다. 모든 회사 리소스에 액세스할 수 있어야 합니다.  
  


