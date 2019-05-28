---
ms.assetid: cf32926a-2083-408b-a264-2cad179ed18a
title: 그룹 정책을 사용 하 여 클라이언트 컴퓨터에 인증서 배포
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 11cdd9c75ca588ebeac9387e6512fee439621bf8
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192163"
---
# <a name="distribute-certificates-to-client-computers-by-using-group-policy"></a>그룹 정책을 사용 하 여 클라이언트 컴퓨터에 인증서 배포


다음 절차를 사용 하 여 적절 한 Secure Sockets Layer를 밀어 넣는 데 \(SSL\) 인증서 \(해당 하는 연결 된 신뢰할 수 있는 루트 인증서 또는\) 계정 페더레이션 서버에 대 한 리소스 페더레이션 서버 및 그룹 정책을 사용 하 여 계정 파트너 포리스트의 각 클라이언트 컴퓨터에 웹 서버입니다.  
  
멤버 자격이 **Domain Admins** 또는 **Enterprise Admins**, 또는 Active Directory Domain Services에서 그와 동등한 \(AD DS\) 이 절차를 완료 하려면 최소한 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/? LinkId\=83477\)합니다.   
  
### <a name="to-distribute-certificates-to-client-computers-by-using-group-policy"></a>그룹 정책을 사용 하 여 클라이언트 컴퓨터에 인증서를 배포 하려면  
  
1.  계정 파트너 조직의 포리스트의 도메인 컨트롤러에서를 시작 합니다 **그룹 정책 관리** 맞춤\-에서 합니다.  
  
2.  기존 그룹 정책 개체를 찾습니다 \(GPO\) 하거나 인증서 설정을 포함 하 여 새 GPO를 만듭니다. GPO는 도메인, 사이트 또는 조직 구성 단위와 연결 되었는지 확인 하십시오 \(OU\) 적절 한 사용자 및 컴퓨터 계정의 위치입니다.  
  
3.  오른쪽\-GPO를 클릭 한 다음 클릭 **편집**합니다.  
  
4.  콘솔 트리에서 엽니다 **컴퓨터 구성\\정책을\\Windows 설정\\보안 설정\\공개 키 정책**그렇죠\- 클릭**신뢰할 수 있는 루트 인증 기관**를 클릭 하 고 **가져오기**합니다.  
  
5.  에 **인증서 가져오기 마법사 시작** 페이지에서 클릭 **다음**합니다.  
  
6.  에 **가져올 파일** 페이지에서 적절 한 인증서 파일의 경로를 입력 \(예를 들어 \\ \\fs1\\c$\\fs1.cer\)를 클릭 하 고 **다음**합니다.  
  
7.  에 **인증서 저장소** 페이지에서 클릭 **모든 인증서를 다음 저장소에 저장**를 클릭 하 고 **다음**합니다.  
  
8.  에 **인증서 가져오기 마법사 완료** 페이지에서 제공한 정보가 정확한 지 확인 한 다음 클릭 **마침**합니다.  
  
9. 각 팜에 페더레이션 서버에 대 한 추가 인증서를 추가할 2-6 단계를 반복 합니다.  
