---
title: 연결 지점 서비스에서 클라이언트 호스트 캐시 자동 검색을 구성
description: 이 가이드 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache 배포에 대해 설명
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: ea1c34fd-5a33-4228-9437-9bb3d44230eb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b12fa6f9e11c8816d74c9013dd80b3fa38d0a478
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
#  <a name="configure-client-automatic-hosted-cache-discovery-by-service-connection-point"></a>연결 지점 서비스에서 클라이언트 호스트 캐시 자동 검색을 구성

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 절차 그룹 정책을 사용 하 고 다음 BranchCache\ 가능 Windows 운영 체제를 실행 하는 domain\ 가입 컴퓨터에서 호스트 BranchCache 캐시 모드 구성 사용할 수 있습니다.

- Windows 10 Enterprise
- Windows 10 Education
- Windows 8.1 Enterprise
- Windows 8 Enterprise

> [!NOTE]  
> Windows Server 2008 R2 또는 Windows 7을 실행 하는 컴퓨터가 도메인에 가입 구성, Windows Server 2008 R2 참조 [BranchCache 배포 가이드](https://technet.microsoft.com/library/ee649232.aspx)합니다.

회원 **도메인 관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.

### <a name="to-use-group-policy-to-configure-clients-for-hosted-cache-mode"></a>그룹 정책을 사용 하 여 호스팅된 캐시 모드에 대 한 클라이언트 구성 하려면

1. 설치 된 Active Directory 도메인 서비스 거부 있는 컴퓨터에서 서버 관리자를 엽니다 로컬 서버를 클릭 **도구**을 차례로 클릭 하 고 **그룹 정책 관리**합니다. 그룹 정책 Management console을 엽니다.

2. 그룹 정책 관리 콘솔 다음 경로 확장: **숲:** *corp.contoso.com*, **도메인**, *corp.contoso.com*, **그룹 정책 개체**, 여기서 *corp.contoso.com* 구성 BranchCache 클라이언트 컴퓨터 계정 있는 도메인 이름입니다.

3. Right\ 클릭 **그룹 정책 개체**을 차례로 클릭 하 고 **새로**합니다. **새 GPO** 대화 상자를 엽니다. **이름**, 새 그룹 정책에 대해 이름을 입력 \(GPO\) 개체 합니다. 예를 들어, 개체 BranchCache 클라이언트 컴퓨터의 이름을 지정 하려면 입력 **BranchCache 클라이언트 컴퓨터**합니다. 클릭 **확인**합니다.

4. 그룹 정책 관리 콘솔에서 **그룹 정책 개체** 선택 하 고 세부 정보 창 right\-클릭 GPO 방금 만든 합니다. 예를 들어, GPO BranchCache 클라이언트 컴퓨터 이름을 right\ 클릭 **BranchCache 클라이언트 컴퓨터**합니다. 클릭 **편집**합니다. 그룹 정책 편집기 Management console을 엽니다.

5. 그룹 정책 편집기 Management console에서 다음 경로 확장: **컴퓨터 구성**, **정책**, **관리 템플릿: 정의 \(ADMX files\) 정책이 로컬 컴퓨터에서 검색**, **네트워크**, **BranchCache**합니다.

6. 클릭 **BranchCache**, 세부 정보 창에서 다음 double\ 클릭 **BranchCache 켜기**합니다. **BranchCache 켜기** 대화 상자를 엽니다.
  
7.  에 **BranchCache 켜기** 대화 상자를 클릭 **사용**, 클릭 한 다음 **확인**합니다.

8. 그룹 정책 편집기 Management console에서 되도록 **BranchCache** 여전히 선택 되어 세부 정보 창 double\ 클릭 한 다음에 **사용 자동 호스트 캐시 검색 서비스 연결 지점에서**합니다. 정책 설정 대화 상자를 엽니다.

9. 에 **사용 자동 호스트 캐시 검색 서비스 연결 지점에서** 대화 상자를 클릭 **사용**, 클릭 한 다음 **확인**합니다.

10. BranchCache에서 콘텐츠를 다운로드 하 고 캐시 클라이언트 컴퓨터를 사용 하도록 설정 하려면 파일 콘텐츠 서버 server\ 기반: 확인 하는 그룹 정책 편집기 Management console에서 **BranchCache** 여전히 선택 되어 세부 정보 창 double\ 클릭 한 다음에 **네트워크 파일에 대 한 BranchCache**합니다. **네트워크 파일에 대 한 구성 BranchCache** 대화 상자를 엽니다. 
11. 에 **네트워크 파일에 대 한 구성 BranchCache** 대화 상자를 클릭 **사용**합니다. **옵션**최대 왕복 네트워크 대기 시간에 대 한 밀리초에서 숫자 값을 입력 하 고 클릭 한 다음 **확인**합니다.
  
    > [!NOTE]
    > 기본적으로 컴퓨터 80 밀리초 왕복 네트워크 대기 넘으면 파일 서버에서 콘텐츠를 캐시 합니다.
  
12. 할당 BranchCache 캐시 각 클라이언트 컴퓨터에서 하드 디스크 공간의 양을 구성 하려면: 확인 하는 그룹 정책 편집기 Management console에서 **BranchCache** 여전히 선택 되어 세부 정보 창 double\ 클릭 한 다음에 **클라이언트 컴퓨터 캐시에 사용 된 디스크 공간이 백분율 설정**합니다. **클라이언트 컴퓨터 캐시에 사용 된 디스크 공간이 백분율 설정** 대화 상자를 엽니다. 클릭 **사용**를 선택한 다음 **옵션** 비율의 BranchCache 캐시에 대 한 클라이언트 각 컴퓨터에서 사용 되는 하드 디스크 공간을 나타내는 숫자 값을 입력 합니다. 클릭 **확인**합니다.

13. 일을 세그먼트가 유효한 BranchCache 데이터 캐시 클라이언트 컴퓨터에 기본 연령 지정 하려면: 확인 하는 그룹 정책 편집기 Management console에서 **BranchCache** 선택 되어 세부 정보 창 double\ 클릭 한 다음에 **부문에 적합 한 연령 데이터 캐시에 명시 된**합니다. **부문에 적합 한 연령 데이터 캐시에 명시 된** 대화 상자를 엽니다. 클릭 **사용**, 세부 정보 창에서 원하는 일 수를 입력 합니다. 클릭 **확인**합니다.

14. 배포에 대 한 적절 하 게 클라이언트 컴퓨터에 대 한 추가 BranchCache 정책 설정의 구성 합니다.

15. 지점 클라이언트 컴퓨터에서 그룹 정책의 명령을 실행 하 여 새로 고침 **gpupdate /force**, 하거나 클라이언트 컴퓨터를 다시 부팅 합니다.

이제 BranchCache 호스트 캐시 모드 배포 완료 되었습니다.

이 가이드 기술에 대 한 자세한 내용은 참조 [추가 리소스](11-Bc-Hcm-additional-resources.md)합니다.