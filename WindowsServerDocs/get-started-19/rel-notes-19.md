---
title: 릴리스 정보-Windows Server 2019의 중요 한 문제
description: 충돌, 중단, 설치 오류 및 데이터 손실을 방지 하려면 해결 방법이 필요한 중요 한 문제 요약
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 134aab85-664f-4d55-87ef-9e5fd098371f
author: coreyp-at-msft
ms.author: coreyp
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: d5d84bb1cd204a5419271cc3668343f8ac9c9a54
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824524"
---
# <a name="release-notes---important-issues-in-windows-server-2019"></a>릴리스 정보-Windows Server 2019의 중요 한 문제

>적용 대상: Windows Server 2019

이러한 릴리스 정보는 Windows Server에서 가장 중요 한 문제 요약&reg; 2019 운영 체제에 알려진 경우 방지 하거나 문제를 해결 하는 방법을 포함 합니다. 디자인별 변경 내용, 새 기능 및이 릴리스에서 수정 하는 방법에 대 한 내용은 [What's New in Windows Server 2019](whats-new-19.md) 및 특정 기능 팀의에서 공지 합니다. 달리 지정 하지 않으면 보고 된 각 문제는 모든 버전 및 Windows Server 2019의 설치 옵션에 적용 됩니다.  

이 문서는 계속해서 업데이트됩니다. 해결 방법이 필요한 중요한 문제가 발견되면 그 내용이 추가되고 새로운 해결 방법 및 수정 사항이 제공됩니다.  
  
## <a name="release-notes"></a>릴리스 정보
Windows Server 2019에 다음과 같은 알려진된 문제가 있습니다. 
<table border="1" rules="rows">
  <thead align="left" valign="middle">
    <tr>
      <th>Title</th>
      <th>설명</th>
    </tr>
  </thead>
  <tbody align="left" valign="middle">
    <tr>
      <td>서버 설치 중 설치 옵션 메뉴 독일어 텍스트가 잘렸습니다 합니다.</td>
      <td>데스크톱 환경 설치 옵션에 대 한 설명을 누락 및 잘못 된 문자를 맨 끝에는 "를 설치 하려는 운영 체제 선택" 이라는 운영 체제 선택 창에 독일어 server 미디어에서 설치 프로그램을 실행 하는 경우 문장입니다. 표시 될 전체 독일어 텍스트가 다음과 같습니다.  
      <br/>
      <p><i>Durch diese 옵션 wird 주사위 vollständige grafische Umgebung von Windows installiert, wodurch zusätzlicher Speicherplatz verbraucht wird 합니다. Sie kann hilfreich sein, Sie den Windows Desktop verwenden möchten 만들게 über eine 앱 verfügen, 주사위 주사위 grafische Umgebung benötigt wenn 합니다.</i> </p>
      <p>이 공용 가용성의 Windows Server 2019, Windows Server, 1809, 버전 및 Microsoft Hyper-v Server 2019 때 해제 독일어 미디어에만 영향을 줍니다.</p></td>
    </tr>
    <tr>
      <td>Windows Server 버전 1809 설치 하는 동안 잘못 된 Windows Server 브랜드 이미지  </td>
      <td>Windows server, 버전, 1809 설치 경험 중 일부 초기 화면에 배경 이미지에 "Windows Server를 2019" 보여 줍니다.  로 Windows Server 버전 1709 및 1803를 사용 하 여이 단순히 "Windows Server"입니다.  어디서 나 다른 제품에서 다른 영향은 없습니다 되며 Windows Server 2019 제품에 영향을 주지 않습니다.  문제는 설치 Windows Server 버전 1809, 볼륨 라이선스 서비스 센터에 액세스 하는 볼륨 라이선스 고객 에게만 제공 하는 동안이 이미지 제한 됩니다.  
      </td>
    </tr>
  </tbody>
</table>


### <a name="copyright"></a>저작권  
이 문서는 "있는 그대로" 제공됩니다. URL 및 기타 인터넷 웹 사이트 참조를 포함하여 이 설명서의 내용 및 의견은 예고 없이 변경될 수 있습니다.  

이 설명서는 Microsoft 제품의 지적 재산에 대한 법적 권한을 제공하지 않습니다. 이 설명서는 내부 참조용으로만 복사 및 사용할 수 있습니다.  

&copy; 2019 Microsoft Corporation. All rights reserved.  

Microsoft, Active Directory, Hyper-V, Windows 및 Windows Server는 미국, 대한민국 및/또는 기타 국가에서의 Microsoft Corporation 등록 상표 또는 상표입니다.  

이 제품에는 부분적으로 Independent JPEG Group의 작업을 기반으로 하는 그래픽 필터 소프트웨어가 포함되어 있습니다.  


1.0  
