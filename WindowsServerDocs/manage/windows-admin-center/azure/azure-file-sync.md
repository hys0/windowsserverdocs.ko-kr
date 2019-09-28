---
title: Azure File Sync를 사용 하 여 클라우드와 파일 서버 동기화
description: Azure File Sync를 사용 하 여 온-프레미스 파일 서버의 유연성, 성능 및 호환성을 유지 하면서 Azure에서 조직의 파일 공유를 중앙 집중화할 수 있습니다. Azure File Sync Windows Server를 선택적 클라우드 계층화 기능을 사용 하 여 Azure 파일 공유의 빠른 캐시로 변환 합니다.
ms.technology: manage
ms.topic: article
author: fauhse
ms.author: fauhse
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: fe0e3337962b7d9c2f025a9d4eba826f3349c1f9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357381"
---
# <a name="sync-your-file-server-with-the-cloud-by-using-azure-file-sync"></a>Azure File Sync를 사용 하 여 클라우드와 파일 서버 동기화

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Azure File Sync를 사용 하 여 온-프레미스 파일 서버의 유연성, 성능 및 호환성을 유지 하면서 Azure에서 조직의 파일 공유를 중앙 집중화할 수 있습니다. Azure File Sync Windows Server를 선택적 클라우드 계층화 기능을 사용 하 여 Azure 파일 공유의 빠른 캐시로 변환 합니다. SMB, NFS 및 FTPS를 비롯 하 여 로컬에서 데이터에 액세스 하기 위해 Windows Server에서 사용할 수 있는 모든 프로토콜을 사용할 수 있습니다.

파일이 클라우드와 동기화 된 후에는 여러 서버를 동일한 Azure 파일 공유에 연결 하 여 콘텐츠를 로컬로 동기화 및 캐시할 수 있습니다. 즉, 권한 (Acl)도 항상 전송 됩니다. Azure Files는 Azure 파일 공유의 차등 스냅숏을 생성할 수 있는 스냅숏 기능을 제공 합니다. 이러한 스냅숏은 손쉽게 검색 하 고 복원 하기 위해 SMB를 통해 읽기 전용 네트워크 드라이브로 탑재할 수 있습니다. 클라우드 계층화와 결합 되어 온-프레미스 파일 서버를 실행 하는 것이 더 쉬워졌습니다.

자세한 내용은 [Azure File Sync 배포 계획](https://aka.ms/afs)을 참조 하세요.