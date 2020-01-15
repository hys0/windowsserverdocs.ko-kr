---
title: 'SMB: 파일 및 프린터 공유 포트를 열어야 합니다.'
TOCTitle: 'SMB: File and printer sharing ports should be open'
ms.date: 07/02/2012
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 80cc75f983d4593e4ee98309d1fa39c024b7b379
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950291"
---
# <a name="smb-file-and-printer-sharing-ports-should-be-open"></a>SMB: 파일 및 프린터 공유 포트를 열어야 합니다.


업데이트: 2 월 2 일, 2011

적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012, Windows Server 2008 R2

*이 항목에서는 모범 사례 분석기 검색에서 식별 한 특정 문제를 해결 하기 위한 것입니다. 이 항목의 정보는 파일 서비스 모범 사례 분석기 실행 되 고이 항목에서 다루는 문제가 발생 한 컴퓨터에만 적용 해야 합니다. 모범 사례 및 검사에 대 한 자세한 내용은 [모범 사례 분석기](https://go.microsoft.com/fwlink/?linkid=122786%0d%0a)를 참조* 하세요.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>운영 체제</strong></p></td>
<td><p>Windows Server</p></td>
</tr>
<tr class="even">
<td><p><strong>제품/기능</strong></p></td>
<td><p>파일 서비스</p></td>
</tr>
<tr class="odd">
<td><p><strong>Severity</strong></p></td>
<td><p>오류</p></td>
</tr>
<tr class="even">
<td><p><strong>범주</strong></p></td>
<td><p>구성</p></td>
</tr>
</tbody>
</table>

## <a name="issue"></a>문제

> *파일 및 프린터 공유에 필요한 방화벽 포트가 열려 있지 않습니다 (포트 445 및 139).*

## <a name="impact"></a>영향

> *컴퓨터에서이 서버의 공유 폴더 및 기타 SMB (서버 메시지 블록) 기반 네트워크 서비스에 액세스할 수 없습니다.*

## <a name="resolution"></a>해상도

> *파일 및 프린터 공유를 사용 하도록 설정 하 여 컴퓨터의 방화벽을 통해 통신 합니다.*

이 절차를 완료하려면 최소한 **Administrators** 또는 이와 동등한 그룹 구성원 자격이 필요합니다.

## <a name="to-open-the-firewall-ports-to-enable-file-and-printer-sharing"></a>파일 및 프린터 공유를 사용 하도록 방화벽 포트를 열려면

1.  제어판을 열고 **시스템 및 보안**을 클릭 한 다음 **Windows 방화벽**을 클릭 합니다.

2.  왼쪽 창에서 **고급 설정**을 클릭 하 고 콘솔 트리에서 **인바운드 규칙**을 클릭 합니다.

3.  **인바운드 규칙**에서 **파일 및 프린터 공유 (NB 세션)** 및 **파일 및 프린터 공유 (SMB 인)** 규칙을 찾습니다.

4.  각 규칙을 마우스 오른쪽 단추로 클릭한 다음, **규칙 사용**을 클릭합니다.

## <a name="additional-references"></a>추가 참조

[공유 폴더 및 Windows 방화벽 이해](https://technet.microsoft.com/library/cc731402.aspx)(https://technet.microsoft.com/library/cc731402.aspx)

