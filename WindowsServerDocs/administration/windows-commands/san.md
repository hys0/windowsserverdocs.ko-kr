---
title: San
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d57c2df1-eb82-4b81-b8cd-e30564c6a929
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a999254507de2d90494c1acfb906d4bcf26168aa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872504"
---
# <a name="san"></a>San

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

표시 하거나 운영 체제에 대 한 저장소 영역 네트워크 (san) 정책을 가져오거나 설정 합니다.
> [!NOTE]
> 이 명령은 Windows 7과 Windows Server 2008 r 2에 적용 됩니다.

## <a name="syntax"></a>구문
```
san [policy={onlineAll | offlineAll | offlineShared}] [noerr]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|정책 = {onlineAll &#124; offlineAll &#124; offlineShared}]|현재 부팅 된 된 운영 체제에 대 한 san 정책을 설정합니다. San 정책을 새로 검색 된 디스크를 온라인 또는 오프 라인 상태로 유지 됩니다 여부 및가 읽기/쓰기 또는 읽기 전용으로 유지 여부를 결정 합니다. 디스크를 오프 라인 상태 이면 디스크 레이아웃을 읽을 수 있지만 플러그 앤 플레이 통해 볼륨 장치가 표시 됩니다. 즉, 파일 시스템이 없습니다 디스크에 탑재 될 수 있습니다. 디스크가 온라인 상태 이면 하나 이상의 볼륨 장치는 디스크에 대 한 설치 됩니다. 다음은 각 매개 변수에 대해 설명 합니다.<br /><br />-   **onlineAll**. 새로 검색 된 모든 디스크 상태가 되며 온라인 읽기/쓰기를 지정 합니다. **중요:**     지정 **onlineAll** 디스크를 공유 하는 서버의 데이터 손상이 발생할 수 있습니다. 따라서 서버는 클러스터의 일부가 아니라면 디스크 서버 간에 공유 되 면이 정책을 설정 해야 합니다.<br />-   **offlineAll**. 새로 검색 된 모든 디스크가 시동 디스크는 오프 라인 상태가 됩니다 점을 제외 하 고 지정 기본적으로 andread 전용입니다.<br />-   **offlineShared**. (예: SCSI 및 iSCSI) 공유 버스에 존재 하지 않는 디스크가 온라인 검색 및 읽기 / 쓰기를 수행 합니다. 모든 새로 지정 합니다. 오프 라인 남아 있는 디스크는 기본적으로 읽기 전용으로 설정 됩니다.<br /><br />자세한 내용은 [VDS_san_POLICY 열거형](https://go.microsoft.com/fwlink/?LinkId=203815) (https://go.microsoft.com/fwlink/?LinkId=203815)합니다.|
|noerr|스크립팅에 사용 합니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|
## <a name="remarks"></a>설명
-   이 명령은 매개 변수 없이 지정 되 면 현재 san 정책이 표시 됩니다.
## <a name="BKMK_Examples"></a>예제
현재 정책을 보려면 다음을 입력 합니다.
```
san
```
오프 라인 및 기본적으로 읽기 전용 시동 디스크를 제외 하 고 새로 검색 된 모든 디스크를 하려면 다음을 입력 합니다.
```
san policy=offlineAll
```
## <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)
