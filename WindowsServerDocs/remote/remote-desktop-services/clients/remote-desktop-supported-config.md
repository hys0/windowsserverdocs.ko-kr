---
title: 원격 데스크톱 클라이언트-지원 되는 구성
description: 원격 데스크톱 클라이언트를 사용하여 액세스할 수 있는 PC에 대해 알아보기
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
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "63748968"
---
# <a name="remote-desktop-client---supported-configuration"></a>원격 데스크톱 클라이언트-지원 되는 구성

## <a name="supported-pcs"></a>지원되는 PC
다음 Windows 운영 체제를 실행 하는 Pc에 연결할 수 있습니다.
- Windows 10 Pro
- Windows 10 Enterprise
- Windows 8 Enterprise
- Windows 8 Professional
- Windows 7 Professional
- Windows 7 Enterprise
- Windows 7 Ultimate
- Windows 7 Ultimate
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows Multipoint Server 2011
- Windows Multipoint Server 2012
- Windows Small Business Server 2008
- Windows Small Business Server 2011

다음 컴퓨터는 원격 데스크톱 게이트웨이 실행할 수 있습니다.

- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows Small Business Server 2011

다음 운영 체제 RD 웹 액세스 또는 RemoteApp 서버 역할도 할 수 있습니다.
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016

## <a name="unsupported-windows-versions-and-editions"></a>지원 되지 않는 Windows 버전 및 에디션

원격 데스크톱 클라이언트 이러한 Windows 버전 및 버전에 연결 하지 않습니다.

- Windows 7 Starter
- Windows 7 홈
- Windows 8 Home
- Windows 8.1 Home
- Windows 10 Home

설치 된 Windows 버전 중 하나에 있는 컴퓨터에 액세스 하려는 경우에 RDP를 지 원하는 Windows 버전으로 업그레이드 하는 것이 좋습니다.

## <a name="rd-gateway-messaging-is-not-supported"></a>RD 게이트웨이 메시징 수 없습니다.
원격 데스크톱 클라이언트는 RD 게이트웨이 메시징을 지원 하지 않습니다. 원격 데스크톱 리소스 액세스 정책 (RD RAP) RD 게이트웨이 서버에 대 한 지정 하지 않는 확인 **RD 게이트웨이 메시징에 대 한 지원 사용 하는 컴퓨터만 허용** 또는 연결할 수 없습니다.