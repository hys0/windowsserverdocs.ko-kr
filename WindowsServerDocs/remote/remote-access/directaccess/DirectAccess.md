---
title: DirectAccess
description: Windows Server 2016의 DirectAccess에 대 한 간략 한 개요를 보려면이 항목을 사용할 수 있습니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6b71d18e-1939-4fc0-bb42-29e0e5ffc8da
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d07e4ab62c7362d8d58f68380d8d9abb8e7a7f2c
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310820"
---
# <a name="directaccess"></a>DirectAccess

>적용 대상: Windows Server(반기 채널), Windows Server 2016

Directaccess를 지 원하는 서버 및 클라이언트 운영 체제와 Windows Server 2016에 대 한 추가 DirectAccess 설명서 링크를 비롯 하 여 DirectAccess에 대 한 간략 한 개요를 보려면이 항목을 사용할 수 있습니다.  
  
> [!NOTE]  
> 이 항목 외에도 다음과 같은 DirectAccess 설명서를 사용할 수 있습니다.  
>   
> -   [Windows Server의 DirectAccess 배포 경로](DirectAccess-Deployment-Paths-in-Windows-Server.md)  
> -   [DirectAccess를 배포하기 위한 필수 조건](Prerequisites-for-Deploying-DirectAccess.md)  
> -   [DirectAccess에서 지원되지 않는 구성](DirectAccess-Unsupported-Configurations.md)  
> -   [DirectAccess 테스트 랩 가이드](DirectAccess-Test-Lab-Guides.md)  
> -   [DirectAccess 알려진 문제](DirectAccess-Known-Issues.md)  
> -   [DirectAccess 용량 계획](DirectAccess-Capacity-Planning.md) 
> -   [DirectAccess 오프 라인 도메인 가입](DirectAccess-Offline-Domain-Join.md)  
> -   [DirectAccess 문제 해결](Troubleshooting-DirectAccess.md)  
> -   [시작 마법사를 사용 하 여 단일 DirectAccess 서버 배포](single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)  
> -   [고급 설정을 사용하여 단일 DirectAccess 서버 배포](single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)  
> -   [기존 원격 액세스(VPN) 배포에 DirectAccess 추가](add-to-existing-vpn/Add-DirectAccess-to-an-Existing-Remote-Access-VPN-Deployment.md)  
  
DirectAccess를 사용 하면 기존 VPN (가상 사설망)을 연결할 필요 없이 원격 사용자가 조직 네트워크 리소스에 연결할 수 있습니다. DirectAccess 연결을 사용 하는 경우 원격 클라이언트 컴퓨터는 항상 조직에 연결 되며, 원격 사용자가 연결을 시작 하 고 중지할 필요 없이 VPN 연결에 필요 합니다. 또한 IT 관리자가 DirectAccess 클라이언트 컴퓨터를 실행 하 고 인터넷에 연결할 때마다 관리할 수 있습니다.

>[!IMPORTANT]
>Microsoft Azure에서 VM\) \(가상 컴퓨터에 원격 액세스를 배포 하지 마십시오. Microsoft Azure에서 원격 액세스를 사용 하는 것은 지원 되지 않습니다. Azure VM에서 원격 액세스를 사용 하 여 Windows server 2016 또는 이전 버전의 Windows Server에서 VPN, DirectAccess 또는 기타 원격 액세스 기능을 배포할 수 없습니다. 자세한 내용은 [Microsoft Azure 가상 컴퓨터에 대 한 Microsoft 서버 소프트웨어 지원](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)을 참조 하세요.
  
DirectAccess는 DirectAccess에 대 한 운영 체제 지원을 포함 하는 도메인에 가입 된 클라이언트만 지원 합니다.  
  
다음 서버 운영 체제는 DirectAccess를 지원 합니다.  
  
-   모든 버전의 Windows Server 2016을 DirectAccess 클라이언트 또는 DirectAccess 서버로 배포할 수 있습니다.  
  
-   모든 버전의 Windows Server 2012 r 2를 DirectAccess 클라이언트 또는 DirectAccess 서버로 배포할 수 있습니다.  
  
-   모든 버전의 Windows Server 2012을 DirectAccess 클라이언트 또는 DirectAccess 서버로 배포할 수 있습니다.  
  
-   모든 버전의 Windows Server 2008 r 2를 DirectAccess 클라이언트 또는 DirectAccess 서버로 배포할 수 있습니다.  
  
다음 클라이언트 운영 체제는 DirectAccess를 지원 합니다.  
  
-   Windows 10 Enterprise  
  
-   Windows 10 Enterprise 2015 장기 서비스 분기 (LTSB)  
  
-   Windows 8 및 8.1 Enterprise  
  
-   Windows 7 Ultimate  
  
-   Windows 7 Enterprise
