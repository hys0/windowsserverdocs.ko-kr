---
title: 릴리스 정보-Windows Server 2019의 중요 한 문제
description: 충돌, 중단, 설치 실패 및 데이터 손실 방지 하기 위해 해결 방법이 필요한 중요 한 문제를 요약 합니다.
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
ms.sourcegitcommit: dbb4738fdac3b7911952ff11f1eaed9649d6567a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/07/2019
ms.locfileid: "9149893"
---
# 릴리스 정보-Windows Server 2019의 중요 한 문제

>적용 대상: WindowsServer 2019

이러한 릴리스 정보는 Windows Server의 가장 중요 한 문제를 요약&reg; 2019 운영 체제를 방지 하거나 문제를 해결 하는 방법을 포함 하 여 알려진 경우. 디자인 변경, 새로운 기능 및이 릴리스에서 수정에 대 한 정보를 [Windows Server 2019의 새로운 기능](whats-new-19.md) 및 해당 기능 팀의 공지를 참조 하세요. 달리 지정 하지 않는 한 각 보고 된 문제는 모든 버전 및 Windows Server 2019의 설치 옵션에 적용 됩니다.  

이 문서는 계속해서 업데이트됩니다. 해결 방법이 필요한 중요한 문제가 발견되면 그 내용이 추가되고 새로운 해결 방법 및 수정 사항이 제공됩니다.  
  
## 릴리스 정보
Windows Server 2019에 다음과 같은 알려진된 문제가 있습니다. 
<table border="1" rules="rows">
  <thead align="left" valign="middle">
    <tr>
      <th>제목</th>
      <th>설명</th>
    </tr>
  </thead>
  <tbody align="left" valign="middle">
    <tr>
      <td>서버 설치 하는 동안 설치 옵션 메뉴 독일 텍스트 잘림가</td>
      <td>데스크톱 경험 설치 옵션에 대 한 설명을 맨 끝에서 누락 된 및 잘못 된 문자를 갖습니다 "를 설치 하려는 운영 체제 선택" 이라는 운영 체제 선택 창에 독일 서버 미디어에서 설치할 때 문장의 합니다. 실제로 표시 될 전체 독일 텍스트 다음과 같습니다.  
      <br/>
      <p><i>Durch diese 옵션 wird 다 vollständige grafische Umgebung 본 Windows installiert, wodurch zusätzlicher Speicherplatz verbraucht wird 합니다. Sie kann hilfreich sein, wenn Sie 서 재 Windows 데스크톱 verwenden möchten 된 계열이 über eine 앱 verfügen, 다 grafische Umgebung benötigt die 합니다.</i> </p>
      <p>이 공용 가용성의 Windows Server 2019, Windows Server, 버전 1809 및 Microsoft Hyper-v Server 2019 출시 독일 미디어에만 영향을 줍니다.</p></td>
    </tr>
    <tr>
      <td>Windows Server, 버전 1809의 설치 하는 동안 잘못 된 Windows Server 브랜딩 이미지  </td>
      <td>Windows Server, 버전 1809에 대 한 설정 경험 중 일부 초기 화면 배경 이미지 "Windows Server 2019" 표시 됩니다.  로 Windows server, 버전 1709 및 1803이 간단 하 게 나타나야 "Windows Server".  제품의 어느 부분에서 다른 영향은 없습니다 되며 Windows Server 2019 제품에 영향이 없습니다.  Windows Server, 버전 1809, 볼륨 라이선스 서비스 센터에 액세스 하는 볼륨 라이선스 고객에만 사용할 수 있는 설치 시 문제가 이미지 제한 됩니다.  
      </td>
    </tr>
  </tbody>
</table>


### 저작권  
이 문서는 "있는 그대로" 제공됩니다. URL 및 다른 인터넷 웹 사이트 참조를 포함한 이 문서의 내용과 관점은 예고 없이 변경될 수 있습니다.  

이 문서는 귀하에게 Microsoft 제품의 지적 재산에 대한 어떠한 법적 권리도 제공하지 않습니다. 내부 참조용으로 이 문서의 사본을 만들 수 있습니다.  

&copy;2019 Microsoft Corporation입니다. All rights reserved.  

Microsoft, Active Directory, Hyper-V, Windows 및 Windows Server는 미국, 대한민국 및/또는 기타 국가에서의 Microsoft Corporation 등록 상표 또는 상표입니다.  

이 제품에는 부분적으로 Independent JPEG Group의 작업을 기반으로 하는 그래픽 필터 소프트웨어가 포함되어 있습니다.  


1.0  
