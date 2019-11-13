---
title: DirectAccess를 배포하기 위한 필수 조건
description: 이 항목에서는 Windows Server 2016의 DirectAccess 배포에 대 한 필수 구성 요소를 제공 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57c7e039-42ef-4909-867a-b5f669c9e74e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6e04dbf1576277493ec849c8de82aeab51e97649
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388807"
---
# <a name="prerequisites-for-deploying-directaccess"></a>DirectAccess를 배포하기 위한 필수 조건

>적용 대상: Windows Server(반기 채널), Windows Server 2016

다음 표에서는 구성 마법사를 사용 하 여 DirectAccess를 배포 하는 데 필요한 필수 구성 요소를 나열 합니다.  
  
|||  
|-|-|  
|시나리오|필수 구성 요소|  
|[시작 마법사를 사용 하 여 단일 DirectAccess 서버 배포](../../remote-access/directaccess/single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)|-모든 프로필에서 Windows 방화벽을 사용 하도록 설정 해야 합니다.<br /><br />-Windows 10&reg;를 실행 하는 클라이언트에만 지원 됨 <br />              Windows&reg; 8 및 Windows&reg; 8.1 Enterprise.<br /><br />-공개 키 인프라가 필요 하지 않습니다.<br /><br />-2 단계 인증 배포에 지원 되지 않습니다. 인증에 도메인 자격 증명이 필요합니다.<br /><br />-현재 도메인의 모든 모바일 컴퓨터에 DirectAccess를 자동으로 배포 합니다.<br /><br />-인터넷에 대 한 트래픽은 DirectAccess를 통해 이동 하지 않습니다. 강제 터널 구성이 지원되지 않습니다.<br /><br />-DirectAccess 서버가 네트워크 위치 서버입니다.<br /><br />-NAP (네트워크 액세스 보호)는 지원 되지 않습니다.<br /><br />-DirectAccess 관리 콘솔 또는 Windows PowerShell cmdlet 이외의 기능을 사용 하 여 정책을 변경 하는 것은 지원 되지 않습니다.<br /><br />-멀티 사이트 구성의 경우 현재 또는 향후에는 먼저 [고급 설정을 사용 하 여 단일 DirectAccess 서버 배포](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)의 지침을 따릅니다.|  
|[고급 설정을 사용하여 단일 DirectAccess 서버 배포](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)|-공개 키 인프라를 배포 해야 합니다.<br />    자세한 내용은 [테스트 랩 가이드 미니 모듈: Windows Server 2012에 대 한 기본 PKI](https://social.technet.microsoft.com/wiki/contents/articles/7862.test-lab-guide-mini-module-basic-pki-for-windows-server-2012.aspx)를 참조 하세요.<br /><br />-모든 프로필에서 Windows 방화벽을 사용 하도록 설정 해야 합니다.<br /><br />다음 서버 운영 체제는 DirectAccess를 지원 합니다.<br /><br />-모든 버전의 Windows Server 2016을 DirectAccess 클라이언트 또는 DirectAccess 서버로 배포할 수 있습니다.<br />-모든 버전의 Windows Server 2012 r 2를 DirectAccess 클라이언트 또는 DirectAccess 서버로 배포할 수 있습니다.<br />-모든 버전의 Windows Server 2012을 DirectAccess 클라이언트 또는 DirectAccess 서버로 배포할 수 있습니다.<br />-모든 버전의 Windows Server 2008 r 2를 DirectAccess 클라이언트 또는 DirectAccess 서버로 배포할 수 있습니다.<br /><br />다음 클라이언트 운영 체제는 DirectAccess를 지원 합니다.<br /><br />-Windows 10&reg; Enterprise<br />-Windows 10&reg; Enterprise 2015 장기 서비스 분기 (LTSB)<br />-Windows&reg; 8 및 8.1 Enterprise<br />-Windows&reg; 7 Ultimate<br />-Windows&reg; 7 Enterprise<br /><br />-인증 강제 터널 구성은 KerbProxy 인증에서 지원 되지 않습니다.<br /><br />-DirectAccess 관리 콘솔 또는 Windows PowerShell cmdlet 이외의 기능을 사용 하 여 정책을 변경 하는 것은 지원 되지 않습니다.<br /><br />-다른 서버에서 NAT64/DNS64와 IPHTTPS 서버 역할을 분리 하는 것은 지원 되지 않습니다.|  
  


