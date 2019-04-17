---
ms.assetid: 231158d8-5e81-4630-b8d5-93fee16e0cd3
title: "식별 수준 기능 업그레이드"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9527a186cb20c470e0b5644fff58f90786520f97
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="identifying-your-functional-level-upgrade"></a>식별 수준 기능 업그레이드

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

도메인 및 숲 기능 수준을 발생 시킬 수 전에 현재 환경 평가 하 고 가장 조직 요구를 충족 기능 수준 요구 사항 확인 해야 합니다. 각 도메인, 운영 체제 및 각 도메인 컨트롤러를 실행 하는 서비스 팩 및 도메인 컨트롤러 업그레이드 하려고 하는 날짜에 있는 도메인 컨트롤러 도메인 숲을 식별 하 여 현재 환경을 평가 합니다. 도메인 컨트롤러를 사용 중지, 하 않도록 하려는 경우 모든 있는 작업은 귀하의 환경에 영향을 이해 합니다.  
  
다음과 같은 경우 이전 버전의 Windows Server 운영 체제 기능 Windows Server 2008 또는 Windows Server 2008 R2 수준으로 업그레이드 되지 않을 수 있습니다.  
  
-   하드웨어 부족  
  
-   Windows Server 2008 또는 Windows Server 2008 r 2와 호환 되는 바이러스 백신 프로그램을 실행 하는 도메인 컨트롤러   
  
-   Windows Server 2008 또는 Windows Server 2008 R2에서 실행 되지 않는 버전의 프로그램의 사용   
  
-   프로그램은 최신 서비스 팩으로 업그레이드 하는 데 필요  
  
이 정보 문서화 완벽 하 게 작동 Windows Server 2008 또는 Windows Server 2008 R2 환경 있는지 확인 하기 위해 수행 하는 단계를 식별 수 있습니다.  
  
현재 사용자 환경의 평가 후 조직에 적용 되는 기능 수준 업그레이드를 확인 해야 합니다. 이러한 옵션을 사용할 수 있습니다.  
  
-   Windows 2000 전용 모드 환경에 Windows Server 2008 또는 Windows Server 2008 R2   
  
-   Windows Server 2008 또는 Windows Server 2008 R2 Windows Server 2003 숲   
  
-   새로운 Windows Server 2008 숲  
  
-   새로운 Windows Server 2008 R2 숲  
  
## <a name="upgrading-functional-levels-in-a-native-windows-2000-active-directory-forest"></a>기본 Windows 2000 Active Directory 숲 속의 기능 수준 업그레이드  
Windows 2000 기반 도메인 컨트롤러 이루어진 기본 Windows 2000 환경에 기능 수준 다음과 같은 수준을 기본적으로 설정 되어 고 될 때까지 이러한 수준 수동으로 올려:  
  
-   Windows 2000 기본 도메인 기능 수준  
  
-   Windows 2000 숲 기능 수준  
  
Windows Server 2008 또는 Windows Server 2008 R2 숲 수준과 도메인 수준 모든 기능을 사용 하려면 Windows Server 2008 또는 Windows Server 2008 r 2에이 Windows 2000 환경을 업그레이드 해야 합니다. 이 업그레이드는 다음 방법 중 하나에서 수행할 수 있습니다.  
  
-   새로 설치 된 Windows Server 2008 소개-기반 또는 Windows Server 2008 R2-도메인 컨트롤러에 숲을 기반으로 한 다음 Windows 2000 실행 도메인 컨트롤러를 모두 사용 중지 됩니다.  
  
-   Windows Server 2003을 실행 하는 도메인 컨트롤러에 Windows 2000 숲에서 실행 중인 모든 기존 도메인 컨트롤러의 현재 위치에서 업그레이드를 수행 합니다. 그런 다음 Windows Server 2008 또는 Windows Server 2008 R2 도메인 컨트롤러 제자리에 업그레이드를 수행 합니다. 자세한 내용은 참조 [Windows Server 2008 광고 DS 도메인 \[LH\에 Active Directory 도메인 업그레이드]](assetId:///9c91be5f-df14-40b2-b176-2b1852a51e61)합니다.  
  
    > [!IMPORTANT]  
    >  Windows Server 2008 R2 x64 기반 운영 체제입니다. 서버 x64 기반 버전의 Windows Server 2003을 실행 중인 경우 Windows Server 2008 r 2에이 컴퓨터의 운영 체제의 전체 업그레이드 성공적으로 수행할 수 있습니다. 서버 x86 기반 버전의 Windows Server 2003을 실행 중인 경우 Windows Server 2008 r 2에이 컴퓨터를 업그레이드할 수 없습니다.  
  
Windows Server 2008 또는 Windows Server 2008 r 2에 전체 Windows 2000 숲 업그레이드 하지 않고도 Windows Server 2008 또는 Windows Server 2008 R2 도메인 수준 기능을 사용 하려면 올리기만 Windows Server 2008 또는 Windows Server 2008 R2.  
  
> [!NOTE]  
> 도메인 기능 수준을, 발생 하기 전에 해당 도메인에 있는 모든 Windows 2000 기반 도메인 컨트롤러 Windows Server 2008 또는 Windows Server 2008 R2로 업그레이드 해야 합니다.  
  
Windows Server 2008 또는 Windows Server 2008 R2 실행 하는 도메인 컨트롤러 관련 있는 숲 속의 모든 Windows 2000 기반 도메인 컨트롤러를 교체한 후 Windows Server 2008 또는 Windows Server 2008 R2 숲 기능 수준을 발생 시킬 수 있습니다. 자동으로 수행 하는 숲 속의 모든 Windows Server 2008 또는 Windows Server 2008 R2 기본 이상 영문으로 설정 된 도메인의 기능 수준을 발생 합니다.  
  
숲 및 도메인 기능 수준 향상에 대 한 자세한 내용은 하 고 해당 작업을 수행 하는 절차 참조 [배포 하는 Windows Server 2008 숲 루트 도메인 \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)합니다.  
  
## <a name="upgrading-functional-levels-in-a-windows-server-2003-active-directory-forest"></a>Windows Server 2003에 대 한 Active Directory 숲 속의 기능 수준 업그레이드  
Windows Server 2003 환경의 Windows Server 2003 기반 도메인 컨트롤러에만으로 구성 된에서 기능 수준은 다음과 같은 수준을 기본적으로 설정 하 고 될 때까지 이러한 수준 수동으로 발생 합니다.  
  
-   Windows 2000 기본 도메인 기능 수준  
  
-   Windows 2000 숲 기능 수준  
  
Windows Server 2008 또는 Windows Server 2008 R2 숲 수준과 도메인 수준 모든 기능을 사용 하려면이 Windows Server 2003 환경의 Windows Server 2008 또는 Windows Server 2008 R2로 업그레이드 해야 합니다. 이 업그레이드는 다음 방법 중 하나에서 수행할 수 있습니다.  
  
-   새로 설치 된 Windows Server 2008 소개-기반 또는 Windows Server 2008 R2-기반 도메인 컨트롤러에 숲, 다음 Windows Server 2003을 실행 하는 모든 도메인 컨트롤러를 사용 중지 또는 Windows Server 2008 또는 Windows Server 2008 R2로 업그레이드 합니다.  
  
-   실행 중인 Windows Server 2008 또는 Windows Server 2008 R2 도메인 컨트롤러에 Windows Server 2003을 실행 하는 모든 기존 도메인 컨트롤러의 현재 위치에서 업그레이드를 수행 합니다. 자세한 내용은 참조 [Windows Server 2008 광고 DS 도메인 \[LH\에 Active Directory 도메인 업그레이드]](assetId:///9c91be5f-df14-40b2-b176-2b1852a51e61)합니다.  
  
> [!IMPORTANT]  
>  Windows Server 2008 R2 x64 기반 운영 체제입니다. 서버 x64 기반 버전의 Windows Server 2003을 실행 중인 경우 Windows Server 2008 r 2에이 컴퓨터의 운영 체제의 전체 업그레이드 성공적으로 수행할 수 있습니다. 서버 x86 기반 버전의 Windows Server 2003을 실행 중인 경우 Windows Server 2008 R2 실행이 컴퓨터를 업그레이드할 수 없습니다.  
  
Windows Server 2008 또는 Windows Server 2008 r 2에 전체 Windows Server 2003 숲 업그레이드 하지 않고도 Windows Server 2008 또는 Windows Server 2008 R2 도메인 수준 기능을 사용 하려면 올리기만 Windows Server 2008 또는 Windows Server 2008 R2.  
  
> [!NOTE]  
> 도메인 기능 수준을, 발생 하기 전에 해당 도메인에 있는 모든 Windows Server 2003 기반 도메인 컨트롤러 Windows Server 2008 또는 Windows Server 2008 R2로 업그레이드 해야 합니다.  
  
Windows Server 2008 또는 Windows Server 2008 r 2에는 숲 속의 모든 Windows Server 2003 기반 도메인 컨트롤러를 업그레이드 한 후 Windows Server 2008 또는 Windows Server 2008 R2 숲 기능 수준을 발생 시킬 수 있습니다. 자동으로 수행 하는 숲 속의 모든 Windows Server 2008 또는 Windows Server 2008 R2 Windows Server 2003로 설정 되어 있는 도메인의 기능 수준을 발생 합니다.  
  
숲 및 도메인 기능 수준 향상에 대 한 자세한 내용은 하 고 해당 작업을 수행 하는 절차 참조 [배포 하는 Windows Server 2008 숲 루트 도메인 \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)합니다.  
  
## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-forest"></a>새로운 Windows Server 2008 숲 속의 기능 수준 업그레이드  
새로운 Windows Server 2008 숲 속의 첫 번째 도메인 컨트롤러를 설치할 때 기능 수준 다음과 같은 수준을 기본적으로 설정 되어 하 고 될 때까지 이러한 수준 수동으로 발생 합니다.  
  
-   Windows 2000 기본 도메인 기능 수준  
  
-   Windows 2000 숲 기능 수준  
  
Windows 2000 또는 Windows Server 2003 기반 도메인 컨트롤러에 새로운 Windows Server 2008 숲에 추가 하는 옵션을 제공 하도록 이러한 기본 수준에서 기능 수준은 설정 합니다. 숲 루트 도메인을 만든 후 Windows Server 2008 숲에 추가 하는 각 도메인 도메인 기능 수준이 설정은 Windows 2000 기본 합니다. 그러나 Windows Server 2008 실행 하면 새로운 Windows Server 2008 환경에서 모든 도메인 컨트롤러 하려는 경우 숲 기능 수준 및 도메인 기능 수준으로 설정에 숲 속의 첫 번째 도메인 컨트롤러를 설치한 경우 Windows Server 2008 합니다. 이 시간을 절약 하 고 숲 수준과 도메인 수준의에서 모든 기능에 Windows Server 2008 수 있습니다.  
  
> [!IMPORTANT]  
> Windows Server 2008 기능에서 숲 작동 수준 하 고 Windows Server 2003 기반 구성원 서버의 Active Directory 설치를 시도 또는 Windows 2000 기반 회원 서버를 설치가 실패 합니다.  
  
숲 및 도메인 기능 수준 향상에 대 한 자세한 내용은 하 고 해당 작업을 수행 하는 절차 참조 [배포 하는 Windows Server 2008 숲 루트 도메인 \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)합니다.  
  
## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-r2-forest"></a>새로운 Windows Server 2008 R2 숲 속의 기능 수준 업그레이드  
새로운 Windows Server 2008 R2 숲 속의 첫 번째 도메인 컨트롤러를 설치할 때 기능 수준 다음과 같은 수준을 기본적으로 설정 되어 하 고 될 때까지 이러한 수준 수동으로 발생 합니다.  
  
-   Windows Server 2003 도메인 기능 수준  
  
-   Windows Server 2003 숲 기능 수준  
  
기능 수준 Windows Server 2003 기반 도메인 컨트롤러에 새로운 Windows Server 2008 R2 숲에 추가 하는 옵션을 제공 하도록 이러한 기본 수준으로 설정 됩니다. 숲 루트 도메인을 만든 후 도메인 기능 수준 Windows Server 2008 R2 숲에 추가 하는 각 도메인에 대 한 Windows Server 2003으로 설정 됩니다. 그러나 Windows Server 2008 R2 실행 하면 새로운 Windows Server 2008 R2 환경에서 모든 도메인 컨트롤러 하려는 경우 설정 숲 기능 수준 및 도메인 기능 수준 하 여 숲 속의 첫 번째 도메인 컨트롤러를 설치한 경우 Windows Server 2008 R2. 이 시간을 절약할 수 Windows Server 2008 r 2의 모든 숲 수준과 도메인 수준 기능을 사용할 수 있습니다.  
  
> [!IMPORTANT]  
> 숲 Windows Server 2008 R2 기능 수준에서 작동 하 고 Windows Server 2008 Active Directory 설치를 시도 하는 경우-기반 또는 Windows Server 2003 기반 구성원 서버, Windows 2000 기반 멤버 서버의 설치에 실패 하거나 합니다.  
  
숲 및 도메인 기능 수준 향상에 대 한 자세한 내용은 하 고 해당 작업을 수행 하는 절차 참조 [배포 하는 Windows Server 2008 숲 루트 도메인 \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)합니다.  
  
> [!NOTE]  
> Windows Server 2008 ADMT v3.1 설치 해야 하지만 개체 하나 이상의 Windows Server 2008 R2 도메인 컨트롤러에서 호스트 하는 도메인 하 게 마이그레이션하 ADMT v3.1을 사용할 수 있습니다. 자세한 내용은 참조 [976659 문서](https://go.microsoft.com/fwlink/?LinkId=180398) 에 Microsoft 기술 자료 (https://go.microsoft.com/fwlink/?LinkId=180398).  
  


