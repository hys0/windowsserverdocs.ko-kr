---
title: "사용자 계정 컨트롤 개요"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tpm
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b7a39cd-fc10-4408-befd-4b2c45806732
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 90ce72cb3d1850563d16a12d09a6872d107c0690
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="user-account-control-overview"></a>사용자 계정 컨트롤 개요
사용자 계정 컨트롤 \(UAC\) Microsoft의 전체 보안 비전 기본 구성 요소입니다.  UAC는 악성 프로그램의 영향을 줄일 수 있습니다.

## <a name="BKMK_OVER"></a>기능 설명
UAC 모든 사용자를 표준 사용자 계정을 사용 하 여 자신의 컴퓨터에 로그온 할 수 있습니다. 표준 사용자 토큰을 사용 하 여 실행 하는 프로세스 표준 사용자에 게 부여 액세스 권한을 사용 하 여 작업을 수행할 수 있습니다. 예를 들어, Windows 탐색기를 자동으로 표준 사용자 수준 권한을 상속합니다. 모든 프로그램 Windows 탐색기를 사용 하 여 실행 되는 또한 \ (double\ 클릭 하 여 예를 들어, 응용 프로그램 shortcut\) 사용자의 사용 권한 표준 집합으로 실행할 수도 있습니다. 많은 응용 프로그램을 비롯 하 여 운영 체제와 함께 제공 되는 이런 방법으로 제대로 작동 하도록 설계 되었습니다.

특히 보안 설정에 따라, 디자인 되지 않았습니다 하는 기타 응용 프로그램의 성공적으로 실행 하려면 추가 권한을 해야 합니다. 이러한 종류의 프로그램은 레거시 응용 프로그램 이라고 합니다. 또한 새로운 소프트웨어 설치 및 프로그램 등 Windows 방화벽을 구성을 변경 하는 등의 작업 표준 사용자 계정을를 제공할 수 있는 것 보다 더 많은 권한이 필요 합니다.

때 표준 개 이상의 사용자 권한으로 실행 하는 응용 프로그램 요구 UAC 토큰 추가 사용자 그룹 복원할 수 있습니다. 이렇게 하면 사용자에 게 변경 하는 시스템 수준 컴퓨터나 디바이스 프로그램의 명시적인 제어할 수 있습니다.

## <a name="BKMK_APP"></a>실용적인 응용 프로그램
UAC의 승인 모드 관리자의 관리자 인 모르게 자동으로 설치 악성 프로그램 방지할 수 있습니다. 또한 실수로 system\ 전체 변경 로부터 보호할 수 있습니다. 마지막으로, 높은 수준의 있는 관리자 해야 적극적으로 동의 하거나 제공 자격 증명 각 관리 프로세스에 대 한 준수를 적용 하기 위해 사용할 수 있습니다.



