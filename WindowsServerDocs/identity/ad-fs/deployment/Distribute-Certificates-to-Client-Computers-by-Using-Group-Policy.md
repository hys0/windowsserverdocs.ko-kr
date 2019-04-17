---
ms.assetid: cf32926a-2083-408b-a264-2cad179ed18a
title: "그룹 정책을 사용 하 여 컴퓨터에 인증서를 배포"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: d3a7e05e4d16565b17b69de254e353df749bbc3a
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="distribute-certificates-to-client-computers-by-using-group-policy"></a>그룹 정책을 사용 하 여 컴퓨터에 인증서를 배포

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


다음 절차를 사용 하 여 적절 한 주소 \(SSL\) 인증서 아래로 밀어 \ (해당 하는 인증서 나 신뢰할 수 있는 root\ 체인은) 계정 federation 서버, 리소스 federation 서버 및 그룹 정책을 사용 하 여 계정 파트너 숲 속의 각 클라이언트 컴퓨터 웹 서버에 대 한 합니다.  
  
회원 **도메인 관리자** 또는 **엔터프라이즈 관리자**, Active Directory 도메인 서비스에 해당 하는 \(AD DS\)는 최소가이 절차를 수행 하는 데 필요한 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) \ (http:///\/ go.microsoft.com\/fwlink\/있나요? LinkId\ 83477\ =).   
  
### <a name="to-distribute-certificates-to-client-computers-by-using-group-policy"></a>그룹 정책을 사용 하 여 컴퓨터에 인증서 배포할  
  
1.  계정 파트너 회사의 숲 속의 도메인 컨트롤러에서 시작의 **그룹 정책 관리** snap\에 있습니다.  
  
2.  기존 그룹 정책 개체 \(GPO\) 찾거나 만들기 인증서 설정이 포함 됩니다. GPO 도메인 사이트나 조직을와 연결 되어 있는지 확인 \(OU\) 적절 한 컴퓨터 및 사용자 계정이 있는 합니다.  
  
3.  Right\ GPO 클릭 하 고 다음 클릭 **편집**합니다.  
  
4.  콘솔 트리에서 열고 **컴퓨터 Configuration\\Policies\\Windows Settings\\Security Settings\\Public 키 정책**, right\ 클릭 **신뢰할 수 있는 인증 기관**을 차례로 클릭 하 고 **가져오기**합니다.  
  
5.  에 **인증서 가져오기 마법사** 페이지, 클릭 **다음**합니다.  
  
6.  에 **가져올 파일** 페이지에서 해당 인증서 파일 경로를 입력 \ (예: \\\fs1\\c$\\fs1.cer\)를 클릭 한 다음 **다음**합니다.  
  
7.  에 **인증서 스토어** 페이지, 클릭 **모든 인증서 다음 스토어에 저장**을 차례로 클릭 하 고 **다음**합니다.  
  
8.  에 **인증서 마법사를 완료** 페이지 정확 하 게, 사용자가 제공 하는 정보 인지 확인 하 고 클릭 한 다음 **완료**합니다.  
  
9. 2-추가 인증서 각 그룹에 federation 서버에 대 한 추가 6 단계를 반복 합니다.  
