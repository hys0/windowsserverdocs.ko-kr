---
title: Windows Admin Center 개요
description: Windows Admin Center(Project Honolulu)를 사용하여 Windows Server를 관리하는 방법을 설명합니다.
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: high
ms.prod: windows-server-threshold
ms.openlocfilehash: d941e9884dced40ce750645b662d8df73503bc41
ms.sourcegitcommit: 475292afc919c6d17569f05007a97bc6b92dd225
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2019
ms.locfileid: "9267779"
---
# Windows Admin Center

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center를 시작합니다!

**Windows Admin Center**(코드명 **Project Honolulu**)는 Windows Server 기본 제공 관리 도구의 혁신으로서, 로컬 및 원격 서버 관리의 모든 측면을 통합하는 단일 창입니다. 로컬로 배포되는 브라우저 기반 관리 환경이므로 인터넷 연결과 Azure를 사용할 필요가 없습니다. Windows Admin Center를 통해 인터넷에 연결되지 않은 개인 네트워크를 포함하여 배포의 모든 측면을 완전히 제어할 수 있습니다.

## 소개

>[!VIDEO https://www.youtube.com/embed/PcQj6ZklmK0]

![Windows Admin Center 정보 그래픽](media/WAC1809Poster_thumb.PNG)

[PDF 다운로드](https://github.com/MicrosoftDocs/windowsserverdocs/raw/master/WindowsServerDocs/manage/windows-admin-center/media/WindowsAdminCenter1809Poster.pdf)

## 빠른 시작

몇 분만에 자신의 환경에 Windows Admin Center를 구축 및 가동할 수 있습니다.

1. [다운로드](https://aka.ms/windowsadmincenter)
2. [설치](deploy/install.md)
3. [시작하기](use/get-started.md)

## 내용 한눈에 보기

<table>
    <tr></tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>이해</h3>
            <ul>
            <li><a href="understand/what-is.md">Windows Admin Center란?</a>
            <li><a href="understand/faq.md">FAQ</a>
            <li><a href="understand/case-studies.md">사례 연구</a>
            <li><a href="understand/related-management.md">관련 관리 제품</a>
            <li><a href="understand/videos.md">비디오</a>
            </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>요금제</h3>
            <ul>
            <li><a href="plan/installation-options.md">나에게 적합한 유형의 설치는 무엇입니까?</a>
            <li><a href="plan/user-access-options.md">사용자 액세스 옵션</a>
            <li><a href="plan/azure-integration-options.md">어떤 Azure 통합 옵션이 있습니까?</a>
            <br>
            </ul>
        </td>
    </tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>배포</h3>
            <ul>
            <li><a href="deploy/prepare-environment.md">사용자 환경 준비</a>
            <li><a href="deploy/install.md">Windows Admin Center 설치</a>
            <li><a href="deploy/high-availability.md">고가용성 구현</a>
         </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>구성</h3>
            <ul>
            <li><a href="configure/settings.md">Windows Admin Center 설정</a>
            <li><a href="configure/user-access-control.md">사용자 액세스 제어 및 사용 권한</a>
            <li><a href="configure/using-extensions.md">확장</a>
            <li><a href="configure/azure-integration.md">Azure와 통합</a>
            <li><a href="configure/manage-azure-vms.md">Windows Admin Center를 사용하여 Azure VM 관리</a>
            </ul>
        </td>
    </tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>사용</h3>
            <ul>
            <li><a href="use/get-started.md">시작 및 연결 추가</a>
            <li><a href="use/manage-servers.md">서버 관리</a>
            <li><a href="use/manage-hyper-converged.md">하이퍼 컨버지드 인프라 관리</a>
            <li><a href="use/manage-failover-clusters.md">장애 조치 클러스터 관리</a>
            <li><a href="use/manage-virtual-machines.md">가상 컴퓨터 관리</a>
            <li><a href="use/azure-services.md">Azure 서비스 활용</a>
            <li><a href="use/troubleshooting.md">일반적인 문제 해결 단계</a>
            <li><a href="use/logging.md">로깅</a>
            <li><a href="use/known-issues.md">알려진 문제</a>
            </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>확장</h3>
            <ul>
            <li><a href="extend/extensibility-overview.md">확장 개요</a>
            <li><a href="extend/understand-extensions.md">확장 이해</a>
            <li><a href="extend/developing-extensions.md">확장 개발</a>
            <li><a href="extend/publish-extensions.md">가이드</a>
            <li><a href="extend/publish-extensions.md">확장 게시</a>
            </ul>
        </td>
    </tr>

</table>

## 릴리스 기록

최신 출시된 기능에 대해 자세히 알아보세요.

- 버전 [1903](https://aka.ms/wac1903)은 Active Directory에서 Server 또는 PC 연결을 추가하는 기능인 Azure Monitor와 Active Directory, DHCP, DNS를 관리하는 새로운 도구의 이메일 알림을 가져옵니다.
- 버전 [1902](https://aka.ms/wac1902)에 ACL, 게이트웨이 연결 및 논리 네트워크를 관리하기 위한 새로운 SDN 도구를 포함하는 소프트웨어 정의 네트워크(SDN) 관리에 대한 공유 연결 목록 및 향상된 기능이 추가되었습니다.
- 버전 [1812](https://aka.ms/wac1812)어두운 테마 (미리보기에서) 추가됨, 전원 구성 설정, BMC 정보 및 PowerShell 지원으로 관리 가능 [추가](./configure/using-extensions.md#manage-extensions-with-powershell) 및 [연결](./use/get-started.md#use-powershell-to-import-or-export-your-connections-with-tags).
- 버전 [1809.5](https://aka.ms/wac1809.5) 는 플랫폼 전반에 걸쳐 다양한 품질 및 기능 향상과 버그 수정 및 하이퍼 컨버지드 인프라 관리 솔루션의 몇 가지 새로운 기능을 포함하는 GA 누적 업데이트입니다.
- 버전 [1809](https://cloudblogs.microsoft.com/windowsserver/2018/09/20/windows-admin-center-1809-and-sdk-now-generally-available/) 는 이전에 미리보기에 있던 기능을 GA 채널에 가져온 GA 버전이었습니다.
- 버전 [1808](https://aka.ms/WACPreview1808-InsiderBlog) 은 설치된 앱 도구, 여러 개선 사항 및 미리보기 SDK에 대한 주요 업데이트를 추가했습니다.
- 버전 [1807](https://aka.ms/WACPreview1807-InsiderBlog)은 간소화 된 Azure 연결 경험, VM 인벤토리 페이지 개선, 파일 공유 기능, Azure 업데이트 관리 통합 등을 추가했습니다. 
- 버전 [1806](https://aka.ms/WACPreview1806-InsiderBlog) 은 PowerShell 스크립트, SDN 관리, 2008 R2 연결, SDN, 예약 된 작업 및 기타 여러 개선 사항을 추가했습니다.
- 버전 1804.25 - 완전한 오프라인 환경에서 Windows Admin Center를 설치하는 사용자를 지원하기 위한 유지 관리 업데이트.
- 버전 [1804](https://cloudblogs.microsoft.com/windowsserver/2018/04/12/announcing-windows-admin-center-our-reimagined-management-experience/) - Project Honolulu가 Windows Admin Center로 변경되었으며 보안 기능 및 역할 기반 액세스 제어가 추가되었습니다. 첫 번째 GA 릴리스입니다.
- 버전 [1803](https://blogs.windows.com/windowsexperience/2018/03/13/announcing-project-honolulu-technical-preview-1803-and-rsat-insider-preview-for-windows-10) Azure AD 액세스 제어, 자세한 로깅, 크기를 조정할 수 있는 콘텐츠 및 다양한 도구 개선에 대한 지원 추가.
- 버전 [1802](https://blogs.windows.com/windowsexperience/2018/02/13/announcing-windows-server-insider-preview-build-17093-project-honolulu-technical-preview-1802)에는 접근성, 지역화, 고가용성 배포, 태그 지정, Hyper-V 호스트 설정 및 게이트웨이 인증에 대한 지원이 추가되었습니다.
- 버전 [1712](https://blogs.windows.com/windowsexperience/2017/12/19/announcing-project-honolulu-technical-preview-1712-build-05002) 더 많은 가상 컴퓨터 기능과 도구 전체 성능 향상을 추가 합니다.
- 버전 [1711](https://cloudblogs.microsoft.com/windowsserver/2017/12/01/1711-update-to-project-honolulu-technical-preview-is-now-available/) 요구가 높았던 도구(원격 데스크톱 및 PowerShell) 및 기타 개선 사항이 추가되었습니다.
- 버전 [1709](https://cloudblogs.microsoft.com/windowsserver/2017/09/22/project-honolulu-technical-preview-is-now-available-for-download/)는 최초 공용 미리 보기 릴리스로 시작했습니다.

## 업데이트 상태 유지

<a target="_blank" class="mscom-link twitter-follow-link" title="Twitter에서 Microsoft 팔로우" aria-label="Follow us on Twitter" data-info="Twitter" href="https://twitter.com/servermgmt"><picture><source srcset="//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOolR" media="(min-width:0)"><img srcset="//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOolR" alt="Follow us on Twitter" src="//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOolR"></picture></a>
 | 
<a target="_blank" class="mscom-link blogs-follow-link" title="블로그 읽기" aria-label="Visit our Blogs" data-info="Blogs" href="https://blogs.technet.microsoft.com/servermanagement/"><picture><source srcset="//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOtyw" media="(min-width:0)"><img srcset="//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOtyw" alt="Follow us on Blogs" src="//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOtyw"></picture></a>
