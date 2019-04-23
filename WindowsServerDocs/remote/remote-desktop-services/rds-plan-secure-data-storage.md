---
title: 원격 데스크톱 서비스-보안 데이터 저장소
description: 안전 하 게 rds.의 사용자 프로필 디스크 (Upd)를 사용 하 여 데이터를 저장 하기 위한 계획 정보
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 37b7f68e-7c3a-4190-a52f-99ae96885fae
author: lizap
ms.author: elizapo
ms.date: 11/21/2016
manager: dongill
ms.openlocfilehash: 242d09e49141e9fb789a83421714366105730cc2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870594"
---
# <a name="remote-desktop-services---secure-data-storage-with-upds"></a>원격 데스크톱 서비스-Upd 사용 하 여 보안 데이터 저장소

>적용 대상: Windows Server (반기 채널), Windows Server 2016

Store 비즈니스 리소스, 사용자 개인 설정 데이터 및 설정을 안전 하 게 온-프레미스 또는 Azure입니다. RD 세션 호스트 AD 인증을 사용 및 개인 설정 된 환경에서 안전 하 게 필요한 리소스를 사용 하 여 사용자 역량을 강화 합니다. 

보장 사용자는 자신의 원격 리소스에 액세스, RDS 배포를 관리 하는 중요 한 측면은 끝점에 관계 없이 일관 된 환경이 있습니다. 사용자 프로필 디스크 (Upd)에 사용자 데이터, 사용자 지정 및 단일 컬렉션 내에서 사용자에 따라 응용 프로그램 설정을 허용 합니다. UPD는 사용자별, 경우에 로그인 할-UPD는 해당 세션의 기간에 대 한 로컬 드라이브 취급 사용자의 세션에 탑재 된 공유를 중앙에 저장 하는 컬렉션 별 VHD 파일입니다. 

사용자의 관점에서 UPD famililar 경험이-해당 문서를 저장할 폴더 (대가 로컬 드라이브)를 변경 하는 문서는 앱 설정, 일반적인 방법으로 하며 Windows 환경에 사용자 지정 합니다. 레지스트리 하이브를 포함 하 여이 모든 데이터는 UPD에 저장 하 고 중앙 네트워크 공유에 유지 합니다. 사용자가 적극적으로 데스크톱 또는 RemoteApp에 연결 하는 경우에 Upd 사용자에 게 제공 됩니다. 사용자의 전체 C:\Users 때문에 컬렉션 내에서 Upd만 로밍할 수 있습니다&#92;\<사용자 이름\> AppData\Local 등 디렉터리 UPD에 저장 됩니다.

사용할 수 있습니다 [PowerShell cmdlet](https://technet.microsoft.com/library/jj215443.aspx) 중앙 공유, 각 UPD의 크기와 폴더를 포함 하거나 UPD에 저장 된 사용자 프로필에서 제외 해야 경로를 지정 합니다. 으로 이동 하 여 서버 관리자를 통해 Upd를 설정할 수 있습니다. 또는 **원격 데스크톱 서비스 > 컬렉션 > 데스크톱 컬렉션 > 바탕 화면 컬렉션 속성 > 사용자 프로필 디스크**합니다. 사용 하도록 설정 하거나 해당 컬렉션의 특정 사용자가 아닌에 전체 컬렉션의 모든 사용자에 대 한 Upd를 비활성화할 있습니다 note 합니다. Upd 서버 컬렉션에 있는 전체 제어 권한이 있는 중앙 식 파일 공유에 저장 되어야 합니다. 

사용 하 여 Azure에 저장 하 여 Upd에 대 한 고가용성을 얻을 수 있습니다 [저장소 공간 다이렉트](rds-storage-spaces-direct-deployment.md)합니다. 