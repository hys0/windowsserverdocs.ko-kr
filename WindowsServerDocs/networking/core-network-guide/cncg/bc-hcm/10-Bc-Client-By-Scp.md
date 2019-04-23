---
title: 서비스 연결 지점별 클라이언트 자동 호스트 캐시 검색 구성
description: 이 가이드에서는 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache를 배포 하는 방법 지침을 제공
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: ea1c34fd-5a33-4228-9437-9bb3d44230eb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bd77fc76a999517cb8372aec8dfad25b4dd5be3b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829724"
---
#  <a name="configure-client-automatic-hosted-cache-discovery-by-service-connection-point"></a>서비스 연결 지점별 클라이언트 자동 호스트 캐시 검색 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 절차를 하는 데 그룹 정책을 사용 하도록 설정 하 고 도메인에서 BranchCache 호스트 캐시 모드를 구성\-다음 BranchCache를 실행 중인 컴퓨터를 가입\-Windows 운영 체제를 지원 합니다.

- Windows 10 Enterprise
- Windows 10 Education
- Windows 8.1 Enterprise
- Windows 8 Enterprise

> [!NOTE]  
> Windows Server 2008 R2 또는 Windows 7을 실행 하는 도메인에 가입 된 컴퓨터를 구성 하려면 Windows Server 2008 r 2를 참조 하십시오. [BranchCache 배포 가이드](https://technet.microsoft.com/library/ee649232.aspx)합니다.

멤버 자격이 **Domain Admins**, 또는 이와 동등한 최소한이이 절차를 수행 하려면 필요 합니다.

### <a name="to-use-group-policy-to-configure-clients-for-hosted-cache-mode"></a>그룹 정책을 사용 하 여 호스트 캐시 모드에 대 한 클라이언트를 구성 하려면

1. Active Directory 도메인 서비스 서버 역할은 설치 된 컴퓨터에서 서버 관리자를 열고 로컬 서버를 클릭 하 여 **도구**, 를 클릭 하 고 **그룹 정책 관리**합니다. 그룹 정책 관리 콘솔을 엽니다.

2. 그룹 정책 관리 콘솔에서 다음 경로 확장: **포리스트:** *corp.contoso.com*, **도메인**를 *corp.contoso.com*하십시오 **그룹 정책 개체**여기서 *corp.contoso.com* 구성할는 BranchCache 클라이언트 컴퓨터 계정이 있는 도메인의 이름입니다.

3. 오른쪽\-클릭 **그룹 정책 개체**, 를 클릭 하 고 **새로**합니다. **새 GPO** 대화 상자가 열립니다. **이름**, 새 그룹 정책 개체에 대 한 이름을 입력 \(GPO\)합니다. 예를 들어 개체 BranchCache 클라이언트 컴퓨터의 이름을 하려는 입력 **BranchCache 클라이언트 컴퓨터**합니다. **확인**을 클릭합니다.

4. 그룹 정책 관리 콘솔에서 **그룹 정책 개체** 선택 되며, 세부 정보 창 오른쪽에 있는\-방금 만든 GPO를 클릭 합니다. 예를 들어 GPO BranchCache 클라이언트 컴퓨터를 이름을 마우스 오른쪽 단추로\-클릭 **BranchCache 클라이언트 컴퓨터**합니다. 클릭 **편집**합니다. 그룹 정책 관리 편집기 콘솔을 엽니다.

5. 그룹 정책 관리 편집기 콘솔에서 다음 경로 확장: **컴퓨터 구성**하십시오 **정책을**, **관리 템플릿: 정책 정의 \(ADMX 파일\) 로컬 컴퓨터에서 검색**, **네트워크**하십시오 **BranchCache**합니다.

6. 클릭 **BranchCache**, 다음 세부 정보 창에서 두 배로 늘려야\-클릭 **BranchCache 설정**합니다. **BranchCache 설정** 대화 상자가 열립니다.
  
7.  에 **BranchCache 설정** 대화 상자, 클릭 **Enabled**, 클릭 하 고 **확인**합니다.

8. 그룹 정책 관리 편집기 콘솔에서 **BranchCache** 여전히을 선택한 다음 세부 정보 창 큰따옴표로\-클릭 **자동 호스트 캐시 검색 사용 서비스 연결 지점에**합니다. 정책 설정 대화 상자가 열립니다.

9. 에 **자동 호스트 캐시 검색 사용 서비스 연결 지점에** 대화 상자를 클릭 **Enabled**, 클릭 하 고 **확인**합니다.

10. BranchCache 파일 서버에서 다운로드 및 캐시 콘텐츠를 클라이언트 컴퓨터를 사용 하도록 설정 하려면\-기반 콘텐츠 서버: 그룹 정책 관리 편집기 콘솔 **BranchCache** 여전히을 선택한 다음 세부 정보 창 큰따옴표로\-클릭 **네트워크 파일용 BranchCache**합니다. **네트워크 파일용 BranchCache 구성** 대화 상자가 열립니다. 
11. 에 **네트워크 파일용 BranchCache 구성** 대화 상자를 클릭 하 여 **사용**. **옵션**, 최대 왕복 네트워크 대기 시간에 대 한 숫자 값을 밀리초 단위로 입력 하 고 클릭 한 다음 **확인**합니다.
  
    > [!NOTE]
    > 기본적으로 클라이언트 컴퓨터 왕복 네트워크 대기 시간이 80 밀리초 보다 긴 경우 파일 서버에서 콘텐츠를 캐시 합니다.
  
12. BranchCache 캐시에 대 한 각 클라이언트 컴퓨터에 할당 된 하드 디스크 공간의 크기를 구성 합니다. 그룹 정책 관리 편집기 콘솔 **BranchCache** 여전히을 선택한 다음 세부 정보 창 큰따옴표로\-클릭 **클라이언트컴퓨터캐시에사용되는디스크공간의백분율설정**. **클라이언트 컴퓨터 캐시에 사용 되는 디스크 공간의 백분율 설정** 대화 상자가 열립니다. 클릭 **Enabled**, 를 선택한 다음 **옵션** BranchCache 캐시에 대 한 각 클라이언트 컴퓨터에서 사용 하는 하드 디스크 공간의 백분율을 나타내는 숫자 값을 입력 합니다. **확인**을 클릭합니다.

13. 일을 세그먼트는 유효한 클라이언트 컴퓨터에서 BranchCache 데이터 캐시의 기본 보존 기간을 지정: 그룹 정책 관리 편집기 콘솔 **BranchCache** 여전히을 선택한 다음 세부 정보 창 큰따옴표로\-클릭 **데이터 캐시의 세그먼트 보관 기간 설정**합니다. **데이터 캐시의 세그먼트 보관 기간 설정** 대화 상자가 열립니다. 클릭 **Enabled**, 세부 정보 창에서 원하는 날짜 수를 입력 합니다. **확인**을 클릭합니다.

14. 배포에 적절 하 게 클라이언트 컴퓨터에 대 한 추가 BranchCache 정책 설정을 구성 합니다.

15. 명령을 실행 하 여 지점의 클라이언트 컴퓨터에서 그룹 정책 새로 고침 **gpupdate /force**, 또는 클라이언트 컴퓨터를 다시 부팅 합니다.

BranchCache 호스트 캐시 모드 배포 완료 되었습니다.

에 대 한 자세한 내용은이 가이드의 기술 참조 [추가 리소스](11-Bc-Hcm-additional-resources.md)합니다.