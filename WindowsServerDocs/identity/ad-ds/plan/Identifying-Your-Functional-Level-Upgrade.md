---
ms.assetid: 231158d8-5e81-4630-b8d5-93fee16e0cd3
title: 기능 수준 업그레이드 식별
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 8aee6a5560edfae656582b3c2812ca69c6b90f57
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812044"
---
# <a name="identifying-your-functional-level-upgrade"></a>기능 수준 업그레이드 식별

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

도메인 및 포리스트 기능 수준을 올릴 수 있습니다, 전에 현재 환경을 평가 하 고 조직의 요구에 가장 잘 부합 기능 수준 요구 사항을 식별 해야 합니다. 포리스트의 각 도메인, 운영 체제 및 각 도메인 컨트롤러를 실행 하는 서비스 팩 및 업그레이드 도메인 하려고 하는 날짜에 있는 도메인 컨트롤러는 도메인을 식별 하 여 현재 환경을 평가합니다 컨트롤러입니다. 도메인 컨트롤러를 사용 중지 되었는지 확인 하려는 경우 사용자 환경에는 이렇게 하는 전체 영향을 이해 합니다.  
  
다음과 같은 경우에서는 이전 버전 Windows Server 운영 체제의 Windows Server 2008 또는 Windows Server 2008 R2 기능 수준으로 업그레이드 하지 못할 수 있습니다.  
  
-   하드웨어 부족  
  
-   Windows Server 2008 또는 Windows Server 2008 R2를 사용 하 여 호환 되지 않는 바이러스 백신 프로그램을 실행 하는 도메인 컨트롤러   
  
-   Windows Server 2008 또는 Windows Server 2008 R2를 실행 하지 않는 버전별 프로그램 사용   
  
-   최신 서비스 팩을 사용 하 여 프로그램을 업그레이드할 필요가  
  
이 정보를 문서화 완벽 하 게 기능 Windows Server 2008 또는 Windows Server 2008 R2 환경이 있는지 확인 하기 위해 수행 하는 단계를 식별할 수 있습니다.  
  
현재 환경을 평가, 후 조직에 적용 되는 기능 수준 업그레이드 식별 해야 합니다. 이러한 옵션을 사용할 수 있습니다.  
  
-   Windows Server 2008 또는 Windows Server 2008 R2에 Windows 2000 기본 모드 환경   
  
-   Windows Server 2008 또는 Windows Server 2008 R2에 Windows Server 2003 포리스트   
  
-   새 Windows Server 2008 포리스트  
  
-   새 Windows Server 2008 R2 포리스트  
  
## <a name="upgrading-functional-levels-in-a-native-windows-2000-active-directory-forest"></a>기본 Windows 2000 Active Directory 포리스트의 기능 수준을 업그레이드  
Windows 2000 네이티브 환경에서 Windows 2000 기반 도메인 컨트롤러가 으로만 구성 된 기능 수준을 다음 수준으로 기본적으로 설정 됩니다 하 고 수동으로 발생 될 때까지 이러한 수준에서 계속 합니다.  
  
-   Windows 2000 기본 도메인 기능 수준  
  
-   Windows 2000 포리스트 기능 수준  
  
Windows Server 2008 또는 Windows Server 2008 R2의 모든 포리스트 수준 및 도메인 수준 기능을 사용 하려면이 Windows 2000 환경을 Windows Server 2008 또는 Windows Server 2008 R2로 업그레이드 해야 합니다. 다음 방법 중 하나로이 업그레이드를 수행할 수 있습니다.  
  
-   새로 설치 된 Windows Server 2008 소개-기반 또는 Windows Server 2008 R2-포리스트의로 기반 도메인 컨트롤러 및 다음 Windows 2000을 실행 하는 모든 도메인 컨트롤러를 사용 중지 합니다.  
  
-   Windows Server 2003을 실행 하는 도메인 컨트롤러를 포리스트에 Windows 2000을 실행 하는 모든 기존 도메인 컨트롤러의 현재 위치 업그레이드를 수행 합니다. 그런 다음 Windows Server 2008 또는 Windows Server 2008 R2에 해당 도메인 컨트롤러의 현재 위치 업그레이드를 수행 합니다. 자세한 내용은 [Windows Server 2008 AD DS 도메인에 Active Directory 도메인 업그레이드 \[LH\]](assetId:///9c91be5f-df14-40b2-b176-2b1852a51e61)합니다.  
  
    > [!IMPORTANT]  
    >  Windows Server 2008 R2 x64 기반 운영 체제는입니다. 서버를 x64 기반 버전의 Windows Server 2003을 실행 하는 경우이 컴퓨터의 Windows Server 2008 R2 운영 체제의 현재 위치 업그레이드를 성공적으로 수행할 수 있습니다. 서버는 x86 기반 버전의 Windows Server 2003을 실행 하는 경우에 Windows Server 2008 R2로이 컴퓨터를 업그레이드할 수 없습니다.  
  
Windows Server 2008 또는 Windows Server 2008 R2로 전체 Windows 2000 포리스트를 업그레이드 하지 않고 Windows Server 2008 또는 Windows Server 2008 R2 도메인 수준 기능을 사용 하려면만 도메인 기능 수준 올리기 Windows Server 2008 또는 Windows Server 2008 R2입니다.  
  
> [!NOTE]  
> 도메인 기능 수준을 올리면 전에 도메인에 있는 모든 Windows 2000 기반 도메인 컨트롤러가 Windows Server 2008 또는 Windows Server 2008 R2를 업그레이드 해야 합니다.  
  
Windows Server 2008 또는 Windows Server 2008 R2를 실행 하는 도메인 컨트롤러를 사용 하 여 포리스트에 있는 모든 Windows 2000 기반 도메인 컨트롤러를 바꾼 후 Windows Server 2008 또는 Windows Server 2008 R2 포리스트 기능 수준을 발생 시킬 수 있습니다. 자동으로 수행 Windows Server 2008 또는 Windows Server 2008 R2 이상 기본 Windows 2000으로 설정 되는 포리스트의 모든 도메인 기능 수준을 발생 시킵니다.  
  
포리스트 및 도메인 기능 수준 올리기 하는 방법에 대 한 자세한 내용은 이러한 작업을 수행 하는 절차를 참조 하세요 [Windows Server 2008 포리스트 루트 도메인 배포 \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)합니다.  
  
## <a name="upgrading-functional-levels-in-a-windows-server-2003-active-directory-forest"></a>Windows Server 2003 Active Directory 포리스트의 기능 수준을 업그레이드  
Windows Server 2003 기반 도메인 컨트롤러에만 구성 된 Windows Server 2003 환경에서 기능 수준을 다음 수준으로 기본적으로 설정 됩니다 하 고 수동으로 발생 될 때까지 이러한 수준에서 계속 합니다.  
  
-   Windows 2000 기본 도메인 기능 수준  
  
-   Windows 2000 포리스트 기능 수준  
  
Windows Server 2008 또는 Windows Server 2008 R2의 모든 포리스트 수준 및 도메인 수준 기능을 사용 하려면이 Windows Server 2003 환경을 Windows Server 2008 또는 Windows Server 2008 R2로 업그레이드 해야 합니다. 다음 방법 중 하나로이 업그레이드를 수행할 수 있습니다.  
  
-   새로 설치 된 Windows Server 2008 소개-기반 또는 Windows Server 2008 R2-기반 도메인 컨트롤러를 포리스트에 다음 Windows Server 2003을 실행 하는 모든 도메인 컨트롤러를 사용 중지 하거나 Windows Server 2008 또는 Windows Server 2008 R2로 업그레이드 합니다.  
  
-   Windows Server 2008 또는 Windows Server 2008 R2를 실행 하는 도메인 컨트롤러에 Windows Server 2003을 실행 하는 모든 기존 도메인 컨트롤러의 현재 위치 업그레이드를 수행 합니다. 자세한 내용은 [Windows Server 2008 AD DS 도메인에 Active Directory 도메인 업그레이드 \[LH\]](assetId:///9c91be5f-df14-40b2-b176-2b1852a51e61)합니다.  
  
> [!IMPORTANT]  
>  Windows Server 2008 R2 x64 기반 운영 체제는입니다. 서버를 x64 기반 버전의 Windows Server 2003을 실행 하는 경우이 컴퓨터의 Windows Server 2008 R2 운영 체제의 현재 위치 업그레이드를 성공적으로 수행할 수 있습니다. 서버는 x86 기반 버전의 Windows Server 2003을 실행 하는 경우에 Windows Server 2008 R2를 실행 하려면이 컴퓨터를 업그레이드할 수 없습니다.  
  
Windows Server 2008 또는 Windows Server 2008 R2로 전체 Windows Server 2003 포리스트를 업그레이드 하지 않고 모든 Windows Server 2008 또는 Windows Server 2008 R2 도메인 수준 기능을 사용 하려면만 도메인 기능 수준을 Windows Server 2008 또는 Windows S를 발생 시킵니다. 2008 R2 서버입니다.  
  
> [!NOTE]  
> 도메인 기능 수준을 올리면 전에 도메인에 있는 모든 Windows Server 2003 기반 도메인 컨트롤러가 Windows Server 2008 또는 Windows Server 2008 R2를 업그레이드 해야 합니다.  
  
포리스트에 있는 모든 Windows Server 2003 기반 도메인 컨트롤러가 Windows Server 2008 또는 Windows Server 2008 R2로 업그레이드 한 후 Windows Server 2008 또는 Windows Server 2008 R2 포리스트 기능 수준을 발생 시킬 수 있습니다. 자동으로 수행 Windows Server 2008 또는 Windows Server 2008 R2에 Windows Server 2003으로 설정 되는 포리스트의 모든 도메인 기능 수준을 발생 시킵니다.  
  
포리스트 및 도메인 기능 수준 올리기 하는 방법에 대 한 자세한 내용은 이러한 작업을 수행 하는 절차를 참조 하세요 [Windows Server 2008 포리스트 루트 도메인 배포 \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)합니다.  
  
## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-forest"></a>새 Windows Server 2008 포리스트 기능 수준 업그레이드  
새 Windows Server 2008 포리스트의 첫 번째 도메인 컨트롤러를 설치할 때 기능 수준은 기본적으로 다음 수준으로 설정 됩니다 및 수동으로 발생 될 때까지 이러한 수준에서 계속 합니다.  
  
-   Windows 2000 기본 도메인 기능 수준  
  
-   Windows 2000 포리스트 기능 수준  
  
기능 수준에 새 Windows Server 2008 포리스트를 Windows 2000 또는 Windows Server 2003 기반 도메인 컨트롤러를 추가 하는 옵션을 제공 하려면 이러한 기본 수준에서 설정 됩니다. 포리스트 루트 도메인을 만든 후 도메인 기능 수준이 Windows Server 2008 포리스트를 추가 하는 각 도메인에 대 한 설정은 Windows 2000 네이티브 합니다. 그러나 Windows Server 2008을 실행 하려면 새 Windows Server 2008 환경의 모든 도메인 컨트롤러를 하려는 경우 설정 포리스트 기능 수준이 되었다가 도메인 기능 수준을 Windows Server 2008에 fores에서 첫 번째 도메인 컨트롤러를 설치할 때 t입니다. 이렇게 시간을 저장 하 고 Windows Server 2008의 모든 포리스트 수준 및 도메인 수준 기능을 사용할 수 있습니다.  
  
> [!IMPORTANT]  
> 포리스트 기능 Windows Server 2008에서 작동 하는 경우 수준 멤버 Windows Server 2003 기반 서버에서 Active Directory 설치를 시도 하거나 Windows 2000 기반 멤버 서버에 설치 실패 합니다.  
  
포리스트 및 도메인 기능 수준 올리기 하는 방법에 대 한 자세한 내용은 이러한 작업을 수행 하는 절차를 참조 하세요 [Windows Server 2008 포리스트 루트 도메인 배포 \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)합니다.  
  
## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-r2-forest"></a>새 Windows Server 2008 R2 포리스트 기능 수준 업그레이드  
새 Windows Server 2008 R2 포리스트의 첫 번째 도메인 컨트롤러를 설치할 때 기능 수준은 기본적으로 다음 수준으로 설정 됩니다 하 고 수동으로 발생 될 때까지 이러한 수준에서 계속 합니다.  
  
-   Windows Server 2003 도메인 기능 수준  
  
-   Windows Server 2003 포리스트 기능 수준  
  
기능 수준에 새 Windows Server 2008 R2 포리스트를 Windows Server 2003 기반 도메인 컨트롤러를 추가 하는 옵션을 제공 하려면 이러한 기본 수준에서 설정 됩니다. 포리스트 루트 도메인을 만든 후 Windows Server 2003 도메인 기능 수준이 Windows Server 2008 R2 포리스트를 추가 하는 각 도메인에 대해 설정 됩니다. 그러나 Windows Server 2008 R2를 실행 하려면 새 Windows Server 2008 R2 환경에서 모든 도메인 컨트롤러를 원하는 경우로 포리스트 기능 수준 및 다음 도메인 기능 수준을 Windows Server 2008 R2를 설치한 경우 첫 번째 도메인 컨트롤러 yo 포리스트입니다. 이렇게 시간을 저장 하 고 Windows Server 2008 R2의 모든 포리스트 수준 및 도메인 수준 기능을 사용 하도록 설정 합니다.  
  
> [!IMPORTANT]  
> 포리스트의 Windows Server 2008 R2 기능 수준에서 작동 및 Windows Server 2008에서 Active Directory를 설치 하려는 경우-기반 또는 Windows Server 2003 기반 멤버 서버에 Windows 2000 기반 멤버 서버에서 설치에 실패 합니다.  
  
포리스트 및 도메인 기능 수준 올리기 하는 방법에 대 한 자세한 내용은 이러한 작업을 수행 하는 절차를 참조 하세요 [Windows Server 2008 포리스트 루트 도메인 배포 \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)합니다.  
  
> [!NOTE]  
> ADMT v3.1 Windows Server 2008에 설치 해야 하지만 하나 이상의 Windows Server 2008 R2 도메인 컨트롤러에서 호스트 되는 도메인에 개체를 마이그레이션할 ADMT v3.1를 사용할 수 있습니다. 자세한 내용은 [976659 문서](https://go.microsoft.com/fwlink/?LinkId=180398) Microsoft 기술 자료 (https://go.microsoft.com/fwlink/?LinkId=180398)합니다.  
  


