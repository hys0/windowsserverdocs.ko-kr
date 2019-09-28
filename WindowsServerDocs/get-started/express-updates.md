---
title: 2018년 11월 업데이트를 위한 Windows Server 2016용 Express 업데이트
description: Windows Server 2016의 Express 업데이트에 대한 정보를 제공합니다.
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.openlocfilehash: e97be57a344a36be7d14d11e23b7af7049d2118a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71391527"
---
# <a name="express-updates-for-windows-server-2016-re-enabled-for-november-2018-update"></a>2018년 11월 업데이트를 위한 Windows Server 2016용 Express 업데이트

> 작성자: Joel Frauenheim
> 
> 적용 대상: Windows Server 2016

2018년 11월 13일 화요일 업데이트부터 Windows는 Windows Server 2016용 Express 업데이트를 다시 게시할 예정입니다. Windows Server 2016용 Express 업데이트는 업데이트가 제대로 설치되지 못하도록 하는 심각한 문제가 발생한 2017년 중반 이후부터 중지되었습니다. 2017년 11월에 이 문제가 해결되었지만 업데이트 팀은 대부분의 고객이 서버 환경에 2017년 11월 14일 업데이트([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953))를 설치하지만 이 문제의 영향을 받지 않도록 하기 위해 Express 패키지를 조심스럽게 게시하는 방안을 채택했습니다.

WSUS 및 SCCM(System Center Configuration Manager)의 시스템 관리자는 2018년 11월에 Windows Server 2016 업데이트의 패키지 2개, 즉 전체 업데이트와 Express 업데이트가 다시 제공될 것임을 알고 있어야 합니다. 서버 환경을 위해 Express를 사용하려는 시스템 관리자는 디바이스에 2017년 11월 14일 이후 전체 업데이트([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953))를 받아 Express 업데이트가 올바르게 설치되도록 해야 합니다. 2017년 11월 14일 업데이트([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) 이후로 업데이트되지 않은 디바이스에서 Express 업데이트를 시도하는 경우 대역폭 및 CPU 리소스를 소비하면서 반복되는 오류가 무한 루프로 표시됩니다.  이러한 상태에 대한 수정 방법은 시스템 관리자가 Express 업데이트의 푸시를 중지하고 최신 전체 업데이트를 푸시하여 실패 루프를 중지하도록 하는 것입니다.

2018년 11월 13일 Express 업데이트를 사용하는 경우 관리 시스템과 Windows Server 2016 엔드포인트 사이에서 패키지 크기가 즉시 감소합니다.  