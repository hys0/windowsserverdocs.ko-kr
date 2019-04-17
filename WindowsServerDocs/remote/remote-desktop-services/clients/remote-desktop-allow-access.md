---
title: 원격 데스크톱-PC에 대 한 액세스를 허용 합니다.
description: 원격 PC에 액세스 하기 위한 옵션에 알아보기
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0f1557ed-53f7-4333-b023-c8e0f4b58bf4
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d3c85c1c765583eb26cef60ecd245708e0e02772
ms.sourcegitcommit: d3f73936160505a40633ad8dd5931ac5fe3eccdb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297222"
---
# 원격 데스크톱-PC에 대 한 액세스를 허용 합니다.

>적용 대상: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

원격 데스크톱을 사용 하 여 연결 하 고 [Microsoft 원격 데스크톱 클라이언트](remote-desktop-clients.md) (Windows, iOS, Android 및 macOS에 대 한 사용 가능)를 사용 하 여 원격 장치에서 PC를 제어할 수 있습니다. PC에 원격 연결을 허용 하는 경우 PC에 연결한 경우 책상에 앉아 있는 것 처럼 모든 앱, 파일 및 네트워크 리소스에 액세스할 수 있는 다른 장치를 사용할 수 있습니다.  

> [!NOTE]
> 원격 데스크톱을 사용 하 여 Windows 10 Pro 및 엔터프라이즈, Windows 8.1 및 Windows Server 2008 보다 최신 엔터프라이즈 및 Pro, Windows 7 Professional, Enterprise 및 Ultimate, 및 Windows Server 버전 8에 연결할 수 있습니다. (예: Windows 10 Home) Home 버전을 실행 중인 컴퓨터에 연결할 수 없습니다. 

연결할 원격 PC에는 컴퓨터를 켜야 합니다, 네트워크 연결 있어야, 원격 데스크톱을 사용 해야 합니다 (인터넷을 통해 될 수 있음)에서 원격 컴퓨터에 대 한 네트워크 액세스 있어야 하며 연결할 권한이 있어야 합니다. 연결 사용 권한을 사용자 목록에서 여야 합니다. 연결을 시작 하기 전에 것에 연결 하는 컴퓨터의 이름을 조회 하 고 방화벽을 통해 원격 데스크톱 연결 허용 되어 있는지 확인 하는 것이 좋습니다.

## 원격 데스크톱을 사용 하는 방법

원격 장치에서 PC에 액세스할 수 있도록 하는 가장 간단한 방법은 설정에서 원격 데스크톱 옵션을 사용 합니다. 이 기능이 추가 되었습니까? 다운로드할 수 있는 별도 Windows 10 Fall Creator update (1709)에서 앱을 사용할 수 있는 이기도 하므로 이전 버전의 Windows에 대 한 유사한 기능을 제공 하는 합니다. 하지만이 방법은 덜 기능 및 유효성 검사를 제공 원격 데스크톱을 사용 하는 레거시 방법은 사용할 수도 있습니다.

### Windows 10 Fall Creator Update (1709) 이상

몇 가지 간단한 단계를 사용 하 여 원격 액세스를 위해 PC를 구성할 수 있습니다.
1. 장치에서 **시작** 왼쪽에서 **설정** 아이콘을 클릭 하 고 선택한 연결 하려고 합니다.
2. [**원격 데스크톱**](ms-settings:remotedesktop) 항목 앞에 오는 **시스템** 그룹을 선택 합니다.
3. 슬라이더를 사용 하 여 원격 데스크톱을 사용 하도록 설정 합니다.
4. 또한 항시 대기 하 고 연결을 검색 PC를 유지 하는 것이 좋습니다. 사용 하도록 **설정 표시** 를 클릭 합니다.
5. 필요에 따라 클릭 **이 PC에 원격으로 액세스할 수 있는 사용자를 선택**하 여 원격으로 연결할 수 있는 사용자를 추가 합니다.
   1. 관리자 그룹의 구성원에는 자동으로 액세스할을 수 있습니다.
6. **이 PC에 연결 하는 방법**에서이 PC의 이름을 기록해 둡니다. 클라이언트를 구성 하려면이 호출 해야 합니다.

### Windows 7 및 Windows 10의 초기 버전

원격 액세스를 위해 PC를 구성 하려면 다운로드 하 고 [Microsoft 원격 데스크톱 도우미](https://www.microsoft.com/download/details.aspx?id=50042)실행 합니다. 이 도우미 원격 액세스를 사용 하도록 시스템 설정을 업데이트, 컴퓨터 연결을 위한 활성 상태일 때 하 고 방화벽 원격 데스크톱 연결을 허용 하는지 확인 합니다. 

### 모든 버전의 Windows (레거시 메서드)

레거시 시스템 속성을 사용 하 여 원격 데스크톱을 사용 하려면 [원격 데스크톱 연결을 사용 하 여 다른 컴퓨터에 연결](https://windows.microsoft.com/windows/remote-desktop-connection-faq)하려면 지침을 따릅니다.

## 원격 데스크톱을 사용 해야 하나요?

물리적으로 바로 앞 때 PC에 액세스 하려는 경우에 원격 데스크톱 사용 필요가 없습니다. 로컬 네트워크에 표시 되는 PC에 대 한 포트를 열고 원격 데스크톱을 사용 합니다. 집 같은 신뢰할 수 있는 네트워크에서 원격 데스크톱에만 사용 해야 합니다. 또한 하지 않으려면 액세스 긴밀 하 게 제어 된 모든 PC에서 원격 데스크톱을 사용 합니다.

사용 하도록 설정 하면 원격 데스크톱에 대 한 액세스 권한을 부여 하는 관리자 그룹에 사용자 추가 사용자 뿐만 아니라 선택 하는, 자신의 계정을 컴퓨터에서 원격으로 액세스 하는 기능 명심 하세요.

강력한 암호를 사용 하 여 PC에 액세스할 수 있는 모든 계정 구성 되어 있는지 확인 해야 합니다.

## 네트워크 수준 인증을 사용 하 여만 연결을 허용 하는 이유 
 
PC에 액세스할 수 있는 사람을 제한 하려는 경우에 사용 하 여 NLA 네트워크 수준 인증 () 액세스를 허용 하도록 선택 합니다. 이 옵션을 활성화 하면 사용자가 PC에 연결 하기 전에 네트워크에 인증 해야 합니다. NLA를 사용 하 여 원격 데스크톱을 실행 하는 컴퓨터 에서만에서 연결 허용 악의적인 사용자와 소프트웨어에서 컴퓨터를 보호 하는 데 도움이 되는 더욱 안전한 인증 방법입니다. NLA 및 원격 데스크톱에 대 한 자세한 내용은 [RDS 연결에 대 한 구성 NLA](https://technet.microsoft.com/library/cc732713(v=ws.11).aspx)확인 합니다. 

해당 네트워크 외부에서 홈 네트워크의 원격 PC에 연결 하,이 옵션을 선택 하지 마십시오.
