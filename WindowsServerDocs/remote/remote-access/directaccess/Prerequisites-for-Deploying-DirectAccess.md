---
title: DirectAccess를 배포하기 위한 필수 조건
description: 이 항목에서는 Windows Server 2016의 DirectAccess 배포에 대 한 필수 구성 요소를 제공합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57c7e039-42ef-4909-867a-b5f669c9e74e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 09c21facd1a0242b1edbd0436e90c8ebd79f0e2d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824174"
---
# <a name="prerequisites-for-deploying-directaccess"></a>DirectAccess를 배포하기 위한 필수 조건

>적용 대상: Windows Server (반기 채널), Windows Server 2016

다음 표에서 구성 마법사를 사용 하 여 DirectAccess를 배포 하는 데 필요한 필수 구성 요소를 나열 합니다.  
  
|||  
|-|-|  
|시나리오|사전 요구 사항|  
|[시작된 마법사를 사용 하 여 단일 DirectAccess 서버 배포](../../remote-access/directaccess/single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)|-Windows 방화벽이 모든 프로필에서 사용 해야 합니다.<br /><br />-Windows 10을 실행 하는 클라이언트에 대 한 지원만&reg;, <br />              Windows&reg; 8 및 Windows&reg; 8.1 Enterprise입니다.<br /><br />-공개 키 인프라 필요 하지 않습니다.<br /><br />-2 단계 인증을 배포 하기 위한 지원 되지 않습니다. 인증에 도메인 자격 증명이 필요합니다.<br /><br />현재 도메인의 모든 모바일 컴퓨터에 DirectAccess를 자동으로 배포합니다.<br /><br />트래픽이 인터넷에 DirectAccess를 통해 이동 하지 않습니다. 강제 터널 구성이 지원되지 않습니다.<br /><br />-DirectAccess 서버가 네트워크 위치 서버가입니다.<br /><br />-네트워크 액세스 보호 (NAP) 지원 되지 않습니다.<br /><br />-DirectAccess 관리 콘솔 또는 Windows PowerShell cmdlet 이외의 기능을 사용 하 여 정책을 변경 하는 것은 지원 되지 않습니다.<br /><br />-멀티 사이트 구성에 대 한 지금 또는 나중에 먼저의 지침을 따르세요 [고급 설정을 사용 하 여 단일 DirectAccess 서버 배포](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)합니다.|  
|[고급 설정 사용 하 여 단일 DirectAccess 서버 배포](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)|-공개 키 인프라를 배포 되어야 합니다.<br />    자세한 내용은 참조 하세요. [테스트 랩 가이드 미니 모듈: Windows Server 2012에 대 한 기본 PKI](https://social.technet.microsoft.com/wiki/contents/articles/7862.test-lab-guide-mini-module-basic-pki-for-windows-server-2012.aspx)합니다.<br /><br />-Windows 방화벽이 모든 프로필에서 사용할 수 있어야 합니다.<br /><br />다음 서버 운영 체제에서 DirectAccess를 지원 합니다.<br /><br />-DirectAccess 클라이언트 또는 DirectAccess 서버를 Windows Server 2016의 모든 버전을 배포할 수 있습니다.<br />-모든 버전 Windows Server 2012 R2의 DirectAccess 클라이언트 또는 DirectAccess 서버를 배포할 수 있습니다.<br />-모든 버전 Windows Server 2012의 DirectAccess 클라이언트 또는 DirectAccess 서버를 배포할 수 있습니다.<br />-모든 버전 Windows Server 2008 R2의 DirectAccess 클라이언트 또는 DirectAccess 서버를 배포할 수 있습니다.<br /><br />다음 클라이언트 운영 체제에서 DirectAccess를 지원 합니다.<br /><br />-   Windows 10&reg; Enterprise<br />-Windows 10&reg; Enterprise 2015 장기 라는 용어를 LTSB (분기) 서비스<br />-Windows&reg; 8 및 8.1 Enterprise<br />-Windows&reg; 7 Ultimate<br />-   Windows&reg; 7 Enterprise<br /><br />-KerbProxy 인증 강제 터널 구성이 지원 되지 않습니다.<br /><br />-DirectAccess 관리 콘솔 또는 Windows PowerShell cmdlet 이외의 기능을 사용 하 여 정책을 변경 하는 것은 지원 되지 않습니다.<br /><br />-NAT64/DNS64와 IPHTTPS 서버 역할이 다른 서버에서 분리 하는 것은 지원 되지 않습니다.|  
  


