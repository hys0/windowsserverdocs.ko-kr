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


다음 절차를 사용 하 여 계정 페더레이션 서버, 리소스 페더레이션 서버에 대해 신뢰할 수 있는 루트 @ no__t-3에 연결 된 해당 하는 SSL(Secure Sockets Layer) \(SSL @ no__t-1 인증서 \( 또는 해당 하는 인증서를 아래로 푸시할 수 있습니다. 그룹 정책를 사용 하 여 계정 파트너 포리스트의 각 클라이언트 컴퓨터에 웹 서버를 추가할 수 있습니다.  
  
이 절차를 완료 하려면 최소한 **Domain admins** 또는 **Enterprise admins**의 구성원 이거나이에 해당 하는 Active Directory Domain Services \(ad DS @ no__t-3이 필요 합니다.  [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) \(에서 적절 한 계정 및 그룹 구성원 자격 사용에 대 한 자세한 내용은\/http\/: go.microsoft.com fwlink?를 참조 하세요.\/\/ LinkId\=83477\).   
  
### <a name="to-distribute-certificates-to-client-computers-by-using-group-policy"></a>그룹 정책를 사용 하 여 클라이언트 컴퓨터에 인증서를 배포 하려면  
  
1.  계정 파트너 조직의 포리스트에 있는 도메인 컨트롤러에서 **그룹 정책 Management** snap @ no__t-1in을 시작 합니다.  
  
2.  기존 그룹 정책 개체 \(GPO @ no__t-1을 찾거나 인증서 설정을 포함 하는 새 GPO를 만듭니다. GPO가 도메인, 사이트 또는 조직 구성 @no__t 단위에 연결 되어 있는지 확인 합니다.-0OU @ no__t-1 (적절 한 사용자 및 컴퓨터 계정)  
  
3.  마우스 오른쪽 단추로 @ no__t-GPO를 클릭 한 다음 **편집**을 클릭 합니다.  
  
4.  콘솔 트리에서 **컴퓨터 구성 @ no__t-1 정책 @ no__t-2Windows 설정 @ no__t-3 보안 설정 @ no__t-4Public 키 정책**, 오른쪽 @ no__t-5 클릭 **신뢰할 수 있는 루트 인증 기관**을 차례로 클릭 한 다음 가져오기를 클릭 합니다..  
  
5.  에 **인증서 가져오기 마법사 시작** 페이지에서 클릭 **다음**합니다.  
  
6.  **가져올 파일** 페이지에서 적절 한 인증서 @no__t 파일의 경로를 입력 합니다. 1for 예, \\ @ no__t-3fs1 @ no__t-4c $ @no__t -5fs1.cer @ no__t-6을 입력 한 후 **다음**을 클릭 합니다.  
  
7.  **인증서 저장소** 페이지에서 **모든 인증서를 다음 저장소에**저장을 클릭 한 후 **다음**을 클릭 합니다.  
  
8.  **인증서 가져오기 마법사 완료** 페이지에서 입력 한 정보가 정확한 지 확인 한 다음 **마침**을 클릭 합니다.  
  
9. 2 ~ 6 단계를 반복 하 여 팜의 각 페더레이션 서버에 대 한 인증서를 추가 합니다.  
