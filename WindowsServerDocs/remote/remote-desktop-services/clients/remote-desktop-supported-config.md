---
title: 원격 데스크톱 클라이언트-지원 되는 구성
description: 원격 데스크톱 클라이언트를 사용 하 여 액세스할 수 있는 Pc를 설명 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb932dad-6f74-484f-8f7b-dd957b615d44
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d38008b6387385917ad21ce7e169b8ff3f4d18ba
ms.sourcegitcommit: 96e968bbe8dc50ebb1535ae1c8ce92fa73c83171
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "1978050"
---
# <a name="remote-desktop-client---supported-configuration"></a>원격 데스크톱 클라이언트-지원 되는 구성

## <a name="supported-pcs"></a>지원되는 PC
다음 Windows 운영 체제를 실행 하는 Pc에 연결할 수 있습니다.
- Windows10 Pro
- Windows 10 Enterprise
- Windows 8 Enterprise
- Windows 8 Professional
- Windows7 Professional
- Windows7 Enterprise
- Windows7 Ultimate
- Windows7 Ultimate
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- WindowsServer 2012 R2
- WindowsServer 2016
- Windows Multipoint 서버 2011
- Windows Multipoint Server 2012
- Windows Small Business Server 2008
- Windows Small Business Server 2011

다음 컴퓨터는 원격 데스크톱 게이트웨이 실행할 수 있습니다.

- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- WindowsServer 2012 R2
- WindowsServer 2016
- Windows Small Business Server 2011

다음 운영 체제 RD 웹 액세스 또는 RemoteApp 서버로 사용 될 수 있습니다.
- Windows Server 2008 R2
- Windows Server 2012
- WindowsServer 2012 R2
- WindowsServer 2016

## <a name="unsupported-windows-versions-and-editions"></a>지원 되지않는 Windows 버전 및 에디션

원격 데스크톱 클라이언트 이러한 Windows 버전 및 에디션에 연결 되지 않습니다.

- Windows7 Starter K
- Windows 7 홈
- Windows 8 홈
- Windows 8.1 홈
- Windows10 Home

설치 된 Windows 버전 중 하나를 포함 하는 컴퓨터에 액세스 하려는 경우에 RDP를 지 원하는 Windows 버전으로 업그레이드 하는 것이 좋습니다.

## <a name="rd-gateway-messaging-is-not-supported"></a>RD 게이트웨이 메시징 수 없습니다.
원격 데스크톱 클라이언트 RD 게이트웨이 메시징 지원 하지 않습니다. 원격 데스크톱 리소스 액세스 정책 (RD 랩) RD 게이트웨이 서버에 대 한 **RD 게이트웨이 메시징에 대 한 지원 사용 하는 컴퓨터만 허용** 지정 되지 않은 또는 연결할 수 있는지 확인 합니다.