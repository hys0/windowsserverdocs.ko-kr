---
ms.assetid: 231158d8-5e81-4630-b8d5-93fee16e0cd3
title: 기능 수준 업그레이드 식별
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 920f051ef188670f81233098ba38370900e015ae
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822356"
---
# <a name="identifying-your-functional-level-upgrade"></a>기능 수준 업그레이드 식별

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

도메인 및 포리스트 기능 수준을 올리려면 먼저 현재 환경을 평가 하 고 조직의 요구에 가장 잘 맞는 기능 수준 요구 사항을 확인 해야 합니다. 포리스트의 도메인, 각 도메인에 있는 도메인 컨트롤러, 각 도메인 컨트롤러가 실행 중인 운영 체제 및 서비스 팩, 도메인 컨트롤러를 업그레이드할 날짜를 식별 하 여 현재 환경을 평가 합니다. 도메인 컨트롤러의 사용을 중지 하려는 경우 환경에 적용 되는 모든 영향을 이해 해야 합니다.  
  
다음 상황에서는 windows server 운영 체제의 이전 버전을 Windows Server 2008 또는 Windows Server 2008 R2 기능 수준으로 업그레이드 하지 못할 수 있습니다.  
  
-   하드웨어 부족  
  
-   Windows Server 2008 또는 Windows Server 2008 r 2와 호환 되지 않는 바이러스 백신 프로그램을 실행 하는 도메인 컨트롤러   
  
-   Windows Server 2008 또는 Windows 2008 Server 2008 r 2에서 실행 되지 않는 버전별 프로그램 사용   
  
-   최신 Service Pack를 사용 하 여 프로그램을 업그레이드 해야 합니다.  
  
이 정보를 문서화 하면 완벽 하 게 작동 하는 Windows Server 2008 또는 Windows Server 2008 R2 환경을 유지 하기 위해 수행할 단계를 쉽게 파악할 수 있습니다.  
  
현재 환경을 평가한 후에는 조직에 적용 되는 기능 수준 업그레이드를 확인 해야 합니다. 다음 옵션을 사용할 수 있습니다.  
  
-   Windows 2000 기본 모드 환경-windows Server 2008 또는 Windows Server 2008 R2   
  
-   Windows server 2003 포리스트-windows server 2008 또는 Windows Server 2008 R2   
  
-   새 Windows Server 2008 포리스트  
  
-   새 Windows Server 2008 R2 포리스트  
  
## <a name="upgrading-functional-levels-in-a-native-windows-2000-active-directory-forest"></a>네이티브 Windows 2000 Active Directory 포리스트에서 기능 수준 업그레이드  
Windows 2000 기반 도메인 컨트롤러만으로 구성 된 Windows 2000 네이티브 환경에서는 기본적으로 기능 수준이 다음 수준으로 설정 되 고 수동으로 발생 시킬 때까지 이러한 수준으로 유지 됩니다.  
  
-   Windows 2000 기본 도메인 기능 수준  
  
-   Windows 2000 포리스트 기능 수준  
  
Windows Server 2008 또는 2008 Windows server 2008 r 2에서 모든 포리스트 수준 및 도메인 수준 기능을 사용 하려면 windows 2000 환경을 Windows Server 2008 또는 Windows Server 2008 r 2로 업그레이드 해야 합니다. 다음 방법 중 하나로이 업그레이드를 수행할 수 있습니다.  
  
-   포리스트에 새로 설치한 Windows Server 2008 기반 또는 Windows Server 2008 R2 기반 도메인 컨트롤러를 소개 하 고 Windows 2000를 실행 하는 모든 도메인 컨트롤러를 사용 중지 합니다.  
  
-   포리스트에서 Windows 2000를 실행 하는 기존의 모든 도메인 컨트롤러를 Windows Server 2003를 실행 하는 도메인 컨트롤러로 전체 업그레이드를 수행 합니다. 그런 다음 Windows Server 2008 또는 Windows Server 2008 r 2로 해당 도메인 컨트롤러의 전체 업그레이드를 수행 합니다. 자세한 내용은 [Active Directory 도메인을 Windows Server 2008 AD DS 도메인으로 업그레이드 \[LH\]](assetId:///9c91be5f-df14-40b2-b176-2b1852a51e61)를 참조 하세요.  
  
    > [!IMPORTANT]  
    >  Windows Server 2008 R2은 x64 기반 운영 체제입니다. 서버에서 Windows Server 2003의 x64 기반 버전을 실행 하는 경우이 컴퓨터의 운영 체제를 Windows Server 2008 r 2로 전체 업그레이드를 성공적으로 수행할 수 있습니다. 서버에서 x86 기반 버전의 Windows Server 2003를 실행 하는 경우이 컴퓨터를 Windows Server 2008 r 2로 업그레이드할 수 없습니다.  
  
전체 Windows 2000 포리스트를 Windows Server 2008 또는 Windows server 2008 r 2로 업그레이드 하지 않고 Windows Server 2008 또는 Windows Server 2008 R2 도메인 수준 기능을 사용 하려면 Windows Server 2008 또는 Windows Server 2008 r 2로 도메인 기능 수준만 올립니다.  
  
> [!NOTE]  
> 도메인 기능 수준을 올리기 전에 해당 도메인의 모든 Windows 2000 기반 도메인 컨트롤러를 Windows Server 2008 또는 Windows Server 2008 r 2로 업그레이드 해야 합니다.  
  
포리스트의 모든 Windows 2000 기반 도메인 컨트롤러를 Windows Server 2008 또는 Windows Server 2008 r 2를 실행 하는 도메인 컨트롤러로 바꾸면 포리스트 기능 수준을 Windows Server 2008 또는 Windows Server 2008 r 2로 올릴 수 있습니다. 이렇게 하면 windows 2000 기본 이상으로 설정 된 포리스트에 있는 모든 도메인의 기능 수준이 Windows Server 2008 또는 Windows Server 2008 r 2로 자동으로 발생 합니다.  
  
포리스트와 도메인 기능 수준을 올리는 방법 및 해당 작업을 수행 하는 절차에 대 한 자세한 내용은 [Windows Server 2008 포리스트 루트 도메인 배포 \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)를 참조 하세요.  
  
## <a name="upgrading-functional-levels-in-a-windows-server-2003-active-directory-forest"></a>Windows Server 2003 Active Directory 포리스트에서 기능 수준 업그레이드  
Windows Server 2003 기반 도메인 컨트롤러만 구성 된 Windows Server 2003 환경에서는 기능 수준이 기본적으로 다음 수준으로 설정 되 고 수동으로 발생 시킬 때까지 이러한 수준으로 유지 됩니다.  
  
-   Windows 2000 기본 도메인 기능 수준  
  
-   Windows 2000 포리스트 기능 수준  
  
Windows Server 2008 또는 2008 Windows server 2008 r 2에서 모든 포리스트 수준 및 도메인 수준 기능을 사용 하려면 windows server 2003 환경을 Windows server 2008 또는 Windows Server 2008 r 2로 업그레이드 해야 합니다. 다음 방법 중 하나로이 업그레이드를 수행할 수 있습니다.  
  
-   포리스트에 새로 설치한 Windows Server 2008 기반 또는 Windows Server 2008 R2 기반 도메인 컨트롤러를 소개 하 고 Windows Server 2003를 실행 하는 모든 도메인 컨트롤러를 사용 중지 하거나 windows server 2008 또는 Windows Server 2008 r 2로 업그레이드 합니다.  
  
-   Windows server 2003를 실행 하는 기존의 모든 도메인 컨트롤러에 대해 Windows server 2008 또는 Windows Server 2008 r 2를 실행 하는 도메인 컨트롤러로 전체 업그레이드를 수행 합니다. 자세한 내용은 [Active Directory 도메인을 Windows Server 2008 AD DS 도메인으로 업그레이드 \[LH\]](assetId:///9c91be5f-df14-40b2-b176-2b1852a51e61)를 참조 하세요.  
  
> [!IMPORTANT]  
>  Windows Server 2008 R2은 x64 기반 운영 체제입니다. 서버에서 Windows Server 2003의 x64 기반 버전을 실행 하는 경우이 컴퓨터의 운영 체제를 Windows Server 2008 r 2로 전체 업그레이드를 성공적으로 수행할 수 있습니다. 서버에서 x86 기반 Windows Server 2003 버전을 실행 하는 경우이 컴퓨터를 업그레이드 하 여 Windows Server 2008 r 2를 실행할 수 없습니다.  
  
전체 Windows Server 2003 포리스트를 Windows Server 2008 또는 Windows server 2008 r 2로 업그레이드 하지 않고 모든 Windows Server 2008 또는 Windows Server 2008 R2 도메인 수준 기능을 사용 하려면 Windows Server 2008 또는 Windows Server 2008 r 2로 도메인 기능 수준만 올립니다.  
  
> [!NOTE]  
> 도메인 기능 수준을 올리기 전에 해당 도메인의 모든 Windows Server 2003 기반 도메인 컨트롤러를 Windows server 2008 또는 Windows Server 2008 r 2로 업그레이드 해야 합니다.  
  
포리스트의 모든 Windows Server 2003 기반 도메인 컨트롤러를 Windows server 2008 또는 Windows server 2008 r 2로 업그레이드 한 후에는 포리스트 기능 수준을 Windows Server 2008 또는 Windows Server 2008 r 2로 올릴 수 있습니다. 이렇게 하면 Windows server 2003로 설정 된 포리스트에 있는 모든 도메인의 기능 수준이 windows server 2008 또는 Windows Server 2008 r 2로 자동으로 발생 합니다.  
  
포리스트와 도메인 기능 수준을 올리는 방법 및 해당 작업을 수행 하는 절차에 대 한 자세한 내용은 [Windows Server 2008 포리스트 루트 도메인 배포 \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)를 참조 하세요.  
  
## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-forest"></a>새 Windows Server 2008 포리스트에서 기능 수준 업그레이드  
새 Windows Server 2008 포리스트에 첫 번째 도메인 컨트롤러를 설치 하면 기본적으로 기능 수준이 다음 수준으로 설정 되 고 수동으로 발생 시킬 때까지 이러한 수준으로 유지 됩니다.  
  
-   Windows 2000 기본 도메인 기능 수준  
  
-   Windows 2000 포리스트 기능 수준  
  
기능 수준은 이러한 기본 수준에서 설정 되어 새 Windows Server 2008 포리스트에 Windows 2000 또는 Windows Server 2003 기반 도메인 컨트롤러를 추가 하는 옵션을 제공 합니다. 포리스트 루트 도메인을 만든 후 Windows Server 2008 포리스트에 추가 하는 각 도메인의 도메인 기능 수준이 Windows 2000 native로 설정 됩니다. 그러나 새 Windows Server 2008 환경에 있는 모든 도메인 컨트롤러가 Windows Server 2008를 실행 하도록 하려면 포리스트의 첫 번째 도메인 컨트롤러를 설치할 때 포리스트 기능 수준 및 도메인 기능 수준을 Windows Server 2008로 설정 합니다. 이렇게 하면 시간이 절약 되 고 Windows Server 2008의 모든 포리스트 수준 및 도메인 수준 기능을 사용할 수 있습니다.  
  
> [!IMPORTANT]  
> 포리스트가 Windows Server 2008 기능 수준에서 작동 하 고 Windows Server 2003 기반 구성원 서버 또는 Windows 2000 기반 구성원 서버에 Active Directory를 설치 하려고 하면 설치가 실패 합니다.  
  
포리스트와 도메인 기능 수준을 올리는 방법 및 해당 작업을 수행 하는 절차에 대 한 자세한 내용은 [Windows Server 2008 포리스트 루트 도메인 배포 \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)를 참조 하세요.  
  
## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-r2-forest"></a>새 Windows Server 2008 R2 포리스트에서 기능 수준 업그레이드  
새 Windows Server 2008 R2 포리스트에 첫 번째 도메인 컨트롤러를 설치 하는 경우 기본적으로 기능 수준이 다음 수준으로 설정 되 고 수동으로 발생 시킬 때까지 이러한 수준으로 유지 됩니다.  
  
-   Windows Server 2003 도메인 기능 수준  
  
-   Windows Server 2003 포리스트 기능 수준  
  
기능 수준은 이러한 기본 수준에서 설정 되어 Windows Server 2003 기반 도메인 컨트롤러를 새 Windows Server 2008 R2 포리스트에 추가 하는 옵션을 제공 합니다. 포리스트 루트 도메인을 만든 후 Windows Server 2008 R2 포리스트에 추가 하는 각 도메인의 도메인 기능 수준이 Windows Server 2003로 설정 됩니다. 그러나 새 Windows Server 2008 R2 환경의 모든 도메인 컨트롤러에서 Windows Server 2008 r 2를 실행 하려면 포리스트의 첫 번째 도메인 컨트롤러를 설치할 때 포리스트 기능 수준 및 도메인 기능 수준을 Windows Server 2008 r 2로 설정 합니다. 이렇게 하면 시간이 절약 되 고 Windows Server 2008 r 2에서 모든 포리스트 수준 및 도메인 수준 기능을 사용할 수 있습니다.  
  
> [!IMPORTANT]  
> 포리스트가 Windows Server 2008 R2 기능 수준에서 작동 하 고 Windows Server 2008 기반 또는 Windows Server 2003 기반 구성원 서버 또는 Windows 2000 기반 구성원 서버에 Active Directory를 설치 하려고 하면 설치가 실패 합니다.  
  
포리스트와 도메인 기능 수준을 올리는 방법 및 해당 작업을 수행 하는 절차에 대 한 자세한 내용은 [Windows Server 2008 포리스트 루트 도메인 배포 \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1)를 참조 하세요.  
  
> [!NOTE]  
> Windows Server 2008에 ADMT v 3.1을 설치 해야 하지만 ADMT v 3.1을 사용 하 여 하나 이상의 Windows Server 2008 R2 도메인 컨트롤러에서 호스팅되는 도메인으로 개체를 마이그레이션할 수 있습니다. 자세한 내용은 Microsoft 기술 자료 [문서 976659](https://go.microsoft.com/fwlink/?LinkId=180398) (https://go.microsoft.com/fwlink/?LinkId=180398)를 참조 하세요.  
  


