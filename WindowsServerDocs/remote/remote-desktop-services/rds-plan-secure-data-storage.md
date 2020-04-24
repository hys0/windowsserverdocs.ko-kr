---
title: 원격 데스크톱 서비스 - 데이터 스토리지 보안
description: RDS에서 UPD(사용자 프로파일 디스크)를 사용하여 데이터를 안전하게 저장하기 위한 계획 정보
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: 37b7f68e-7c3a-4190-a52f-99ae96885fae
author: lizap
ms.author: elizapo
ms.date: 11/21/2016
manager: dongill
ms.openlocfilehash: 934aab380f9e58f4fe9567921623279a1893af4b
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80860296"
---
# <a name="remote-desktop-services---secure-data-storage-with-upds"></a>원격 데스크톱 서비스 - UPD를 사용한 데이터 스토리지 보안

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

온-프레미스 또는 Azure에서 비즈니스 리소스, 사용자 개인 설정 데이터 및 설정을 안전하게 저장합니다. RD 세션 호스트는 AD 인증을 사용하며 사용자에게 개인 설정된 환경에서 필요한 리소스를 안전하게 사용할 수 있는 권한을 부여합니다. 

사용자가 원격 리소스에 액세스하는 엔드포인트에 관계없이 사용자가 일관된 경험을 갖도록 하는 것은 RDS 배포 관리에서 중요한 측면입니다. UPD(사용자 프로파일 디스크)를 사용하면 사용자 데이터, 사용자 지정 및 애플리케이션 설정이 단일 컬렉션 내에서 사용자를 팔로우할 수 있습니다. UPD는 사용자당, 컬렉션당 VHD 파일로 로그인 시 사용자 세션에 탑재된 중앙 공유에 저장됩니다. UPD는 해당 세션 동안 로컬 드라이브로 처리됩니다. 

사용자의 관점에서 UPD는 문서를 문서 폴더(로컬 드라이브로 보이는 것)에 저장하고, 평소처럼 앱 설정을 변경하며, Windows 환경을 사용자 지정하는 등 유사한 경험을 제공합니다. 레지스트리 하이브를 포함한 이 모든 데이터는 UPD에 저장되며 중앙 네트워크 공유로 유지됩니다. UPD는 사용자가 데스크톱 또는 RemoteApp에 연결되어 있을 때만 사용할 수 있습니다. 사용자의 전체 `C:\Users\<username\>` 디렉터리(AppData\Local 포함)가 UPD에 저장되어 있으므로 UPD는 컬렉션 내에서만 로밍할 수 있습니다.

[PowerShell cmdlet](https://technet.microsoft.com/library/jj215443.aspx)을 사용하여 중앙 공유에 대한 경로, 각 UPD의 크기 및 UPD에 저장된 사용자 프로필에서 포함하거나 제외할 폴더를 지정할 수 있습니다. 또는 **원격 데스크톱 서비스** > **컬렉션** > **데스크톱 컬렉션** > **데스크톱 컬렉션 속성** > **사용자 프로필 디스크**로 이동하여 서버 관리자를 통해 UPD를 사용하도록 설정할 수 있습니다. 해당 컬렉션의 특정 사용자가 아닌 전체 컬렉션의 모든 사용자에 대해 UPD를 사용하거나 사용하지 않도록 설정합니다. UPD는 컬렉션의 서버가 전체 제어 권한을 갖는 중앙 파일 공유에 저장되어야 합니다. 

[스토리지 공간 다이렉트](rds-storage-spaces-direct-deployment.md)를 사용하여 Azure에 저장하면 UPD에 대한 고가용성을 달성할 수 있습니다. 