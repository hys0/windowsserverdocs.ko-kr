---
title: 토큰 바인딩 소개
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 4623a48c-cefd-4a27-9173-2af58ac212f2
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: 2a0bb8c75fe3ca7f7befe0bd67eb3d363a5ad7a9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884234"
---
# <a name="introducing-token-binding"></a>토큰 바인딩 소개

>적용 대상: Windows Server 2016 및 Windows 10

토큰 바인딩 프로토콜에는 응용 프로그램 및 서비스 보안 토큰과 토큰 도난 완화 재생 공격을 TLS 계층 암호화 방식으로 바인딩할 수 있습니다. 여러 TLS 세션 및 연결 오랫동안 지속 되는 고유 하 게 식별할 수 있는 TLS [RFC5246] 바인딩을 확장할 수 있습니다.

버전 지원:

- Windows 10 버전 1507 – 기본적으로 꺼져 있음
    - 토큰 바인딩 프로토콜 추가 [[초안-ietf-tokbind-프로토콜-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - WinInet 및 HTTP입니다. HTTP 통해 토큰 바인딩의 SYS 지원 [[초안-ietf-tokbind-https-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/01/)
- Windows 10, 버전 1511 및 1607 및 Windows Server 2016-에서 기본적으로
    - 토큰 바인딩 프로토콜 업데이트 [[초안-ietf-tokbind-프로토콜-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - 토큰 바인딩 협상 추가 대 한 TLS 확장 [[초안-popov-tokbind-협상-00]](https://tools.ietf.org/html/draft-popov-tokbind-negotiation-00)
    - WinInet 및 HTTP입니다. 업데이트 하는 HTTP 통해 토큰 바인딩의 SYS 지원 [[초안-ietf-tokbind-https-02]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/02/)
- Windows 10 버전 1507 사용 하 여 서비스 업데이트 [KB4034668](https://support.microsoft.com/kb/KB4034668), Windows 10 서비스 업데이트 버전 1511 [KB4034660](https://support.microsoft.com/kb/KB4034660), Windows 10, 버전 1607 및 Windows Server 2016 서비스 업데이트 [KB4034658](https://support.microsoft.com/kb/KB4034658) 0.10 – 토큰 바인딩 프로토콜 버전에는 기본적으로 지원
    - 토큰 바인딩 프로토콜 업데이트 [[초안-ietf-tokbind-프로토콜-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - 토큰 바인딩 협상 추가 대 한 TLS 확장 [[초안-ietf-tokbind-협상-05]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet 및 HTTP입니다. 업데이트 하는 HTTP 통해 토큰 바인딩의 SYS 지원 [[초안-ietf-tokbind-https-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
- Windows 10 버전 1703 토큰 바인딩 프로토콜 버전 0.10 –에서 기본적으로 지원
    - 토큰 바인딩 프로토콜 업데이트 [[초안-ietf-tokbind-프로토콜-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - 토큰 바인딩 협상 추가 대 한 TLS 확장 [[초안-ietf-tokbind-협상-05]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet 및 HTTP입니다. 업데이트 하는 HTTP 통해 토큰 바인딩의 SYS 지원 [[초안-ietf-tokbind-https-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
    - 실행 중인 운영 체제에서 격리 된 보호 된 환경에서 사용 하도록 설정 하는 가상화 기반 보안을 사용 하 여 Windows 장치 토큰 바인딩 키를 유지 됩니다.

ASP.NET 지원에 대 한 정보를 찾을 수 있습니다 합니다 [.NET Framework 참조 소스](https://referencesource.microsoft.com/#System.Web/ITlsTokenBindingInfo.cs,4a5e5668f5c31170)합니다. 

.NET Framework에 대 한 내용은 다음 항목을 참조 합니다.

- [향상 된 네트워킹 기능](https://blogs.msdn.microsoft.com/dotnet/2015/11/30/net-framework-4-6-1-is-now-available/#networking)

- [.NET TokenBinding 클래스](https://msdn.microsoft.com/library/system.security.authentication.extendedprotection.tokenbinding.aspx)
