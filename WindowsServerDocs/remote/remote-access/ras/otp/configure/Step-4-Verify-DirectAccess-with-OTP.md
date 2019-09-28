---
title: 4 단계 OTP를 사용 하 여 DirectAccess 확인
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed49a0a3-1c45-42e5-8f13-cad20c1c1d68
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 83ea3c4e4feefacde3e1ed7be6b605d8c0e644a3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366966"
---
# <a name="step-4-verify-directaccess-with-otp"></a>4 단계 OTP를 사용 하 여 DirectAccess 확인

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 OTP 배포를 사용 하 여 DirectAccess를 올바르게 구성 했는지 확인 하는 방법에 대해 설명 합니다.
  
### <a name="to-verify-otp-health-on-the-remote-access-server"></a>원격 액세스 서버에서 OTP 상태를 확인 하려면

1. 원격 액세스 서버에서 **원격 액세스 관리** 콘솔을 엽니다.  

2. **원격 액세스 서버** 에서 OTP 지원을 위해 구성 된 원격 액세스 서버를 클릭 합니다.  

3. **작업 상태**를 클릭 합니다.  

4. OTP 상태에 녹색 아이콘이 표시 되 고 작동 하는지 확인 합니다.  
  
    > [!NOTE]  
    > 상태 업데이트 간격은 HKLM\SYSTEM\CCS\Services\Ramgmtsvc\parameters\HealthRefreshTimeout 레지스트리 키의 값 합계 및 원격 액세스에 설정 된 **서버 작업에 대 한 시간 간격** 의 최대값입니다. 구성.  
  
### <a name="to-verify-access-to-internal-resources-using-otp-authentication"></a>OTP 인증을 사용 하 여 내부 리소스에 대 한 액세스를 확인 하려면  
  
1.  회사 네트워크에 DirectAccess 클라이언트 컴퓨터를 연결 하 고 명령 프롬프트에서 **gpupdate/force** 를 실행 하 여 그룹 정책을 가져옵니다.  
  
2.  회사 네트워크에서 클라이언트 컴퓨터의 연결을 끊은 다음 외부 네트워크에 연결 하 고 내부 리소스에 액세스를 시도 합니다. 내부 리소스에 대 한 액세스 권한이 없어야 합니다.  
  
3.  소프트웨어 토큰의 경우 공급 업체 지침에 따라 OTP 클라이언트 토큰에 액세스 하 고 현재 토큰 코드를 확인 합니다. 하드웨어 토큰을 사용 하는 경우 인증에 대 한 공급 업체 지침을 따릅니다.  
  
4.  알림 영역에서 **네트워크 연결** 아이콘을 클릭하여 DA 미디어 관리자에 액세스합니다.  
  
5.  **DirectAccess 연결**을 클릭 하 고 **계속**을 클릭 합니다.  
  
6.  앞에서 설명한 토큰 코드를 입력 하 고 **확인**을 클릭 합니다. 인증이 완료 될 때까지 기다립니다. 이제 DirectAccess 작업 공간 연결 상태가 **연결**됨으로 나타납니다.  
  
7.  내부 리소스에 액세스를 시도 합니다. 모든 회사 리소스에 액세스할 수 있어야 합니다.  
  


