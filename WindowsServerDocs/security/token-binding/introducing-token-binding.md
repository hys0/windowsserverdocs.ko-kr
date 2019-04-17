---
title: "토큰 구속력 소개"
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 4623a48c-cefd-4a27-9173-2af58ac212f2
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: 2a0bb8c75fe3ca7f7befe0bd67eb3d363a5ad7a9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="introducing-token-binding"></a>토큰 구속력 소개

>적용 대상: Windows Server 2016 및 Windows 10

토큰 구속력 프로토콜 응용 프로그램 및 서비스 토큰 도난 완화 하 고 재생 공격에 TLS 계층을 보안에 토큰 암호화 된 연결을 허용 합니다. 여러 TLS 세션과 연결 오랫동안 지속 되는 고유 하 게 식별 데이터 TLS [RFC5246] 소스의 확장할 수 있습니다.

버전 지원:

- Windows 10 버전 1507 – 기본적으로
    - 추가 구속력 프로토콜 토큰 [[초안-ietf-tokbind-프로토콜-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - WinInet 및 HTTP.SYS HTTP 통해 토큰 구속력의 지원 [[초안-ietf-tokbind-https-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/01/)
- Windows 10 버전 1511과 1607, 및 Windows Server 2016-에 기본적으로
    - 업데이트 구속력 프로토콜 토큰 [[초안-ietf-tokbind-프로토콜-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - 토큰 구속력 협상 추가 대 한 확장 TLS [[초안-popov-tokbind-협상-00]](https://tools.ietf.org/html/draft-popov-tokbind-negotiation-00)
    - WinInet 및 HTTP.SYS HTTP 업데이트를 통해 토큰 구속력의 지원 [[초안 ietf-tokbind-https-02]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/02/)
- Windows 10 버전 1507 업데이트 서비스를 [KB4034668](https://support.microsoft.com/kb/KB4034668), Windows 10 버전 1511이 릴리스 업데이트 서비스를 [KB4034660](https://support.microsoft.com/kb/KB4034660), Windows 10 버전 1607 및 Windows Server 2016 업데이트 서비스를 [KB4034658](https://support.microsoft.com/kb/KB4034658) 에 토큰 구속력 프로토콜 버전 0.10-기본적으로 지원
    - 업데이트 구속력 프로토콜 토큰 [[초안-ietf-tokbind-프로토콜-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - 토큰 구속력 협상 추가 대 한 확장 TLS [[초안-ietf-tokbind-협상-05]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet 및 HTTP.SYS HTTP 업데이트를 통해 토큰 구속력의 지원 [[초안-ietf-tokbind-https-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
- Windows 10 버전 1703 토큰 구속력 프로토콜 버전 지원 0.10-에 기본적으로
    - 업데이트 구속력 프로토콜 토큰 [[초안-ietf-tokbind-프로토콜-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - 토큰 구속력 협상 추가 대 한 확장 TLS [[초안-ietf-tokbind-협상-05]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet 및 HTTP.SYS HTTP 업데이트를 통해 토큰 구속력의 지원 [[초안-ietf-tokbind-https-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
    - Virtualization 기반 보안 사용할 수 있는 Windows 디바이스에서 실행 중인 운영 체제 격리 된 보호 환경에서 토큰 구속력 키는 유지

ASP.NET 지원에 대 한 정보에서 찾아보실 수 있는 [.NET Framework를 참조 하십시오](https://referencesource.microsoft.com/#System.Web/ITlsTokenBindingInfo.cs,4a5e5668f5c31170)합니다. 

.NET Framework에 대 한 내용은 다음 항목을 참조 하십시오.

- [네트워킹 향상](https://blogs.msdn.microsoft.com/dotnet/2015/11/30/net-framework-4-6-1-is-now-available/#networking)

- [.NET TokenBinding 클래스](https://msdn.microsoft.com/library/system.security.authentication.extendedprotection.tokenbinding.aspx)
