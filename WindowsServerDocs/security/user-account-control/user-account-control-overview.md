---
title: 사용자 계정 컨트롤 개요
description: Windows Server 보안
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887674"
---
# <a name="user-account-control-overview"></a>사용자 계정 컨트롤 개요
사용자 계정 컨트롤 \(UAC\) Microsoft의 전체적인 보안 비전의 기본 구성 요소입니다.  UAC를 사용하면 악성 프로그램의 영향을 줄일 수 있습니다.

## <a name="BKMK_OVER"></a>기능 설명
UAC를 사용하면 모든 사용자가 표준 사용자 계정을 사용하여 자신의 컴퓨터에 로그온할 수 있습니다. 표준 사용자 토큰을 사용하여 시작된 프로세스는 표준 사용자에게 부여된 액세스 권한을 사용하여 작업을 수행할 수 있습니다. 예를 들어 Windows 탐색기는 표준 사용자 수준 권한을 자동으로 상속합니다. 또한 Windows 탐색기를 사용 하 여 실행 되는 모든 프로그램 \(double에서 예를 들어\-응용 프로그램 바로 가기를 클릭 하\) 사용자 권한의 표준 집합을 사용 하 여 실행할 수도 있습니다. 운영 체제 자체와 함께 제공 되는 대부분의 응용 프로그램은이 방식으로 제대로 작동 하도록 설계 되었습니다.

특히 보안 설정에 따라, 특히 설계 되지 않았습니다 하는 다른 응용 프로그램에는 종종 성공적으로 실행 하려면 추가 권한이 필요 합니다. 이러한 종류의 프로그램은 레거시 응용 프로그램 이라고 합니다. 또한 새 소프트웨어를 설치 하 고 Windows 방화벽과 같은 프로그램에 대 한 구성 변경 등의 작업에는 표준 사용자 계정에 사용할 수 있는 것 보다 더 많은 권한이 필요 합니다.

때 여러 표준 사용자 권한으로 실행 되도록 응용 프로그램 요구 사항, UAC 토큰에 추가 사용자 그룹을 복원할 수 있습니다. 이 사용자를에 게 변경 하는 시스템 수준 자신의 컴퓨터 또는 장치 프로그램의 명시적으로 제어할 수 있습니다.

## <a name="BKMK_APP"></a>실제 응용 프로그램
UAC에서 관리자 승인 모드는 악의적인 프로그램 관리자의 지식 없이 자동으로 설치 하지 못하도록 합니다. 또한 부주의 한 시스템에서 보호할 수\-와이드 변경 합니다. 마지막으로, 관리자가 적극적으로 동의하거나 각 관리 프로세스에 대해 자격 증명을 제공해야 하는 더 높은 수준의 규정 준수를 적용하는 데 사용할 수 있습니다.



