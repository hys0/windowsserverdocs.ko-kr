---
title: 사용자 계정 컨트롤 개요
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: bdc9f4dc4b8e19d62288f12a4f2b4e8c86b93b68
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403321"
---
# <a name="user-account-control-overview"></a>사용자 계정 컨트롤 개요
UAC\) \(사용자 계정 컨트롤은 Microsoft의 전반적인 보안 비전의 기본 구성 요소입니다.  UAC를 사용하면 악성 프로그램의 영향을 줄일 수 있습니다.

## <a name="BKMK_OVER"></a>기능 설명
UAC를 사용하면 모든 사용자가 표준 사용자 계정을 사용하여 자신의 컴퓨터에 로그온할 수 있습니다. 표준 사용자 토큰을 사용하여 시작된 프로세스는 표준 사용자에게 부여된 액세스 권한을 사용하여 작업을 수행할 수 있습니다. 예를 들어 Windows 탐색기는 표준 사용자 수준 권한을 자동으로 상속합니다. 또한 Windows 탐색기를 사용 하 여 실행 되는 모든 프로그램은 예를 들어 응용 프로그램 바로\) 가기를 두 번 클릭 하 여 표준 사용자 권한 집합을 사용 하 여 실행 하는 등의 방법으로\-\(. 운영 체제 자체에 포함 된 응용 프로그램을 비롯 한 많은 응용 프로그램은 이러한 방식으로 제대로 작동 하도록 설계 되었습니다.

특히 보안 설정을 염두에 둔 특별히 설계 되지 않은 다른 응용 프로그램의 경우 성공적으로 실행 하려면 추가 권한이 필요할 수 있습니다. 이러한 종류의 프로그램을 레거시 응용 프로그램 이라고 합니다. 또한 새 소프트웨어를 설치 하 고 Windows 방화벽과 같은 프로그램의 구성을 변경 하는 등의 작업을 수행 하려면 표준 사용자 계정에 사용할 수 있는 것 보다 많은 권한이 필요 합니다.

표준 사용자 권한 이상의 응용 프로그램을 실행 해야 하는 경우 UAC는 토큰에 추가 사용자 그룹을 복원할 수 있습니다. 이를 통해 사용자는 컴퓨터 또는 장치에 시스템 수준 변경을 수행 하는 프로그램을 명시적으로 제어할 수 있습니다.

## <a name="BKMK_APP"></a>실용적인 응용 프로그램
UAC의 관리자 승인 모드를 사용 하면 관리자의 지식 없이 악성 프로그램의 자동 설치를 방지할 수 있습니다. 또한 실수로 인 한 시스템\-광범위 한 변경을 방지할 수 있습니다. 마지막으로, 관리자가 적극적으로 동의하거나 각 관리 프로세스에 대해 자격 증명을 제공해야 하는 더 높은 수준의 규정 준수를 적용하는 데 사용할 수 있습니다.



