---
ms.assetid: cf32926a-2083-408b-a264-2cad179ed18a
title: 그룹 정책를 사용 하 여 클라이언트 컴퓨터에 인증서 배포
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 1d9692bc099174f15b77e792087f4c7055bf85d1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359617"
---
# <a name="distribute-certificates-to-client-computers-by-using-group-policy"></a>그룹 정책를 사용 하 여 클라이언트 컴퓨터에 인증서 배포


다음 절차에 따라\)를 사용 하 여 계정 파트너 포리스트의 각 클라이언트 컴퓨터에 계정 페더레이션 서버, 리소스 페더레이션 서버 및 웹 서버에 대 한 신뢰할 수 있는 루트 그룹 정책에 연결 된 SSL\) 인증서 \(또는 이와 동등한 인증서 \(SSL 인증서를 SSL(Secure Sockets Layer) 수 있습니다.  
  
이 절차를 완료 하려면 최소한 **Domain admins** 또는 **Enterprise admins**그룹의 구성원 이거나이에 해당 하는 Active Directory Domain Services \(AD DS\) 해야 합니다.  [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) 에서 적절 한 계정 및 그룹 구성원 자격 사용에 대 한 세부 정보를 검토 \(http:\/\/go.microsoft.com\/fwlink\/? LinkId\=83477\).   
  
### <a name="to-distribute-certificates-to-client-computers-by-using-group-policy"></a>그룹 정책를 사용 하 여 클라이언트 컴퓨터에 인증서를 배포 하려면  
  
1.  계정 파트너 조직의 포리스트에 있는 도메인 컨트롤러에서 **그룹 정책 관리** 스냅인\-를 시작 합니다.  
  
2.  GPO\) 기존 그룹 정책 \(개체를 찾거나 인증서 설정을 포함 하는 새 GPO를 만듭니다. GPO가 적절 한 사용자 및 컴퓨터 계정이 상주 하는 도메인, 사이트 또는 조직 구성 단위 \(OU\)와 연결 되어 있는지 확인 합니다.  
  
3.  GPO\-마우스 오른쪽 단추로 클릭 한 다음 **편집**을 클릭 합니다.  
  
4.  콘솔 트리에서 **컴퓨터 구성\\정책\\Windows 설정\\보안 설정\\공개 키 정책**을 열고 **신뢰할 수 있는 루트 인증 기관**을 마우스 오른쪽\-단추로 클릭 한 다음 **가져오기**를 클릭 합니다.  
  
5.  에 **인증서 가져오기 마법사 시작** 페이지에서 클릭 **다음**합니다.  
  
6.  **가져올 파일** 페이지에서 적절 한 인증서 파일의 경로 \((예: \\\\fs1\\c $\\fs1)를 입력 하 고 **다음**을 클릭 합니다.\)  
  
7.  **인증서 저장소** 페이지에서 **모든 인증서를 다음 저장소에**저장을 클릭 한 후 **다음**을 클릭 합니다.  
  
8.  **인증서 가져오기 마법사 완료** 페이지에서 입력 한 정보가 정확한 지 확인 한 다음 **마침**을 클릭 합니다.  
  
9. 2 ~ 6 단계를 반복 하 여 팜의 각 페더레이션 서버에 대 한 인증서를 추가 합니다.  
