---
Title: 'SMB: 파일 및 프린터 공유 포트가 열려 있어야'
TOCTitle: 'SMB: File and printer sharing ports should be open'
ms.date: 07/02/2012
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: fae579347a43dfa361206e65032b1f3da512ec4a
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284371"
---
# <a name="smb-file-and-printer-sharing-ports-should-be-open"></a>SMB: 파일 및 프린터 공유 포트가 열려 있어야


업데이트됨: 2011 년 2 월 2 일

적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012, Windows Server 2008 R2

*이 항목은 모범 사례 분석기 검사에서 식별 한 특정 문제를 해결 하는 데 사용 됩니다. 이 항목의 정보는 파일 서비스 모범 사례 분석기에 대해 실행 했 고이 항목에서 다루는 문제가 발생 하는 컴퓨터에만 적용 해야 합니다. 모범 사례 및 검사 하는 방법에 대 한 자세한 내용은 참조 하십시오* [Best Practices Analyzer](http://go.microsoft.com/fwlink/?linkid=122786%0d%0a)합니다.


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
<td><p>Error</p></td>
</tr>
<tr class="even">
<td><p><strong>범주</strong></p></td>
<td><p>Configuration</p></td>
</tr>
</tbody>
</table>

## <a name="issue"></a>문제점

> *파일 및 프린터 공유에 대 한 필요한 방화벽 포트 (포트 139 및 445) 열입니다.*

## <a name="impact"></a>영향

> *컴퓨터는 공유 폴더 및이 서버에서 다른 SMB 서버 메시지 블록 기반 네트워크 서비스에 액세스할 수 없습니다.*

## <a name="resolution"></a>해결 방법

> *파일 및 프린터 공유 컴퓨터의 방화벽을 통해 통신을 사용 하도록 설정 합니다.*

이 절차를 완료하려면 최소한 **Administrators** 또는 이와 동등한 그룹 구성원 자격이 필요합니다.

## <a name="to-open-the-firewall-ports-to-enable-file-and-printer-sharing"></a>파일 및 프린터 공유를 사용 하도록 설정 하려면 방화벽 포트를 열려면

1.  제어판을 열고 **시스템 및 보안**를 클릭 하 고 **Windows 방화벽**합니다.

2.  왼쪽된 창에서 클릭 **고급 설정**, 콘솔 트리에서 클릭 **인바운드 규칙**합니다.

3.  아래 **인바운드 규칙**, 규칙을 찾을 **파일 및 프린터 공유 (NB-세션-In)** 하 고 **파일 및 프린터 공유 (Smb-in)** 합니다.

4.  각 규칙에 대 한 규칙을 마우스 오른쪽 단추로 클릭 하 고 클릭 **규칙 사용**합니다.

## <a name="additional-references"></a>추가 참조

[이해를 공유 폴더 및 Windows 방화벽](https://technet.microsoft.com/library/cc731402.aspx)(https://technet.microsoft.com/library/cc731402.aspx)

