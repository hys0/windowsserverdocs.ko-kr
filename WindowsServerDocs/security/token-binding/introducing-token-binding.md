---
title: 토큰 바인딩 소개
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 4623a48c-cefd-4a27-9173-2af58ac212f2
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: 52ba35808b34eb07ecd6ac92819e9dc7a693b15b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403331"
---
# <a name="introducing-token-binding"></a>토큰 바인딩 소개

>적용 대상: Windows Server 2016 및 Windows 10

토큰 바인딩 프로토콜을 사용 하면 응용 프로그램 및 서비스에서 보안 토큰을 TLS 계층에 암호화 하 여 토큰 도난 및 재생 공격을 완화할 수 있습니다. 수명이 긴 고유 하 게 식별 되는 TLS [RFC5246] 바인딩은 여러 TLS 세션 및 연결에 걸쳐 있을 수 있습니다.

버전 지원:

- Windows 10, 버전 1507 – 기본적으로 해제
    - 토큰 바인딩 프로토콜이 추가 됨 [[tokbind-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - WinInet & HTTP. SYS HTTP를 통한 토큰 바인딩 지원 [[draft-ietf-tokbind-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/01/)
- Windows 10, 버전 1511 및 1607 및 Windows Server 2016 – 기본적으로 설정
    - 토큰 바인딩 프로토콜이 업데이트 됨 [[tokbind-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - 토큰 바인딩 협상이 추가 된 TLS 확장 [[popov-tokbind-00]](https://tools.ietf.org/html/draft-popov-tokbind-negotiation-00)
    - WinInet & HTTP. SYS HTTP 업데이트를 통한 토큰 바인딩 지원 [[draft-ietf-tokbind-02]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/02/)
- Windows 10, 버전 1507 (서비스 업데이트 [KB4034668](https://support.microsoft.com/kb/KB4034668), windows 10, 버전 1511, 서비스 업데이트 [KB4034660](https://support.microsoft.com/kb/KB4034660), windows 10, 버전 1607 및 windows Server 2016 서비스 업데이트 [KB4034658](https://support.microsoft.com/kb/KB4034658) 지원 토큰 바인딩 프로토콜) 버전 0.10 – 기본적으로 설정
    - 토큰 바인딩 프로토콜이 업데이트 됨 [[tokbind-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - 토큰 바인딩 협상이 추가 된 TLS 확장 [[tokbind]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet & HTTP. SYS HTTP 업데이트를 통한 토큰 바인딩 지원 [[draft-ietf-tokbind-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
- Windows 10, 버전 1703은 기본적으로 토큰 바인딩 프로토콜 버전 0.10을 지원 합니다.
    - 토큰 바인딩 프로토콜이 업데이트 됨 [[tokbind-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - 토큰 바인딩 협상이 추가 된 TLS 확장 [[tokbind]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet & HTTP. SYS HTTP 업데이트를 통한 토큰 바인딩 지원 [[draft-ietf-tokbind-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
    - 가상화 기반 보안이 설정 된 Windows 장치는 실행 중인 운영 체제와 분리 된 보호 된 환경에서 토큰 바인딩 키를 유지 합니다.

ASP .NET 지원에 대 한 정보는 [.NET Framework 참조 소스](https://referencesource.microsoft.com/#System.Web/ITlsTokenBindingInfo.cs,4a5e5668f5c31170)에서 찾을 수 있습니다. 

.NET Framework에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [네트워킹 기능 향상](https://blogs.msdn.microsoft.com/dotnet/2015/11/30/net-framework-4-6-1-is-now-available/#networking)

- [.NET TokenBinding 클래스](https://msdn.microsoft.com/library/system.security.authentication.extendedprotection.tokenbinding.aspx)
