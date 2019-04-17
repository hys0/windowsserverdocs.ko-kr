---
title: "Adfs와 신원 위임 시나리오"
description: "이 시나리오는 신원을 위임 체인 액세스 제어 검사를 수행 해야 하는 백 엔드 리소스에 액세스 해야 하는 응용 프로그램에 설명 합니다."
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b82d5fd749ac874d09bc54123727aaf902c4d778
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2018
---
# <a name="identity-delegation-scenario-with-ad-fs"></a>Adfs와 신원 위임 시나리오


[.NET Framework 4.5 부터는 Windows 신원을 Foundation (군) 완벽 하 게 통합 되었으며.NET Framework에 있습니다. 이 항목에서는 군 3.5 하 여 해결 군 버전 않으며.NET Framework 3.5 SP1 또는.NET Framework 4 개발 하는 경우에 사용 해야 합니다. 군.NET Framework 4.5 군 4.5 라고도에 대 한 자세한 내용은 대 한 설명서를 참조 Windows 신원을 파운데이션.NET Framework 4.5 개발 가이드에.] 

이 시나리오는 신원을 위임 체인 액세스 제어 검사를 수행 해야 하는 백 엔드 리소스에 액세스 해야 하는 응용 프로그램에 설명 합니다. 간단한 신원을 위임 체인 초기 발신자에 직접 발신자 id 정보 일반적으로 구성 됩니다.

오늘 Windows 플랫폼에서 Kerberos 위임 모델을 백 엔드 리소스만 바로 발신자 id 아니라에 초기 발신자 액세스할 수 있는 합니다. 이 모델은 일반적으로 신뢰할 수 있는 하위 시스템 모델 라고 합니다. 군의 초기 발신자 뿐만 아니라 배우 속성을 사용 하 여 위임 체인에서 바로 발신자 id를 유지 합니다.

다음 그림 Fabrikam 직원 액세스 리소스 Contoso.com 응용 프로그램에서 제공 하는 일반적인 신원을 위임 시나리오를 나타냅니다.

![신원](media/ad-fs-identity-delegation/id1.png)

이 경우에는 관여 가상 사용자는 다음과 같습니다.

- 프랭크:는 Fabrikam 직원에 게 Contoso 리소스에 액세스 하려고 합니다.
- 김: Contoso 응용 프로그램 개발자에 게 필요에 따라 변경 응용 프로그램을 구현 합니다.
- Adam: Contoso IT 관리자입니다.

이 경우 관련 된 구성 요소는 다음과 같습니다.

- web1: 링크와 함께 백 엔드 리소스 위임된 초기 발신자 id를 요구 하는 웹 응용 프로그램입니다. 이 응용 프로그램은 ASP.NET가 빌드됩니다.
- 웹 서비스 액세스 SQL Server, 위임된 함께 바로 발신자의 초기 발신자 id를 요구 하는입니다. 이 서비스는 WCF가 빌드됩니다.
- sts1: 클레임 공급자의 역할에서은 하 (web1) 응용 프로그램에서 예정 된 요구 사항을 STS 합니다. 것은 신뢰 Fabrikam.com 및도 응용 프로그램을 사용 하 여 설정 합니다.
- sts2: Fabrikam.com 공급자는 사용자의 신원 역할 이므로 Fabrikam 직원 인증을 사용 하는 최종 포인트를 제공 하는 STS 합니다. Fabrikam 직원 리소스 Contoso.com에 액세스할 수 있도록 신뢰 Contoso.com로 설정한 합니다.

>[!NOTE] 
>"ActAs 토큰" 사용 되는 일반적이 시나리오를 란 토큰 STS에서 발급 한 것을 포함 하 고 사용자의 id를 말합니다. 배우 속성 STS의 id가 포함 된 합니다.

이전 다이어그램와 같이 흐름이 시나리오에서는 다음과 같습니다.


1. Contoso Fabrikam 직원 id 및 배우 속성에서 바로 발신자 id 모두 포함 된 ActAs 토큰 얻는 구성 되어 있습니다. 김 이러한 변경 후 응용 프로그램을 구현 했습니다.
2. Contoso ActAs 토큰 백 엔드 서비스를 전달 하기 위해 구성 되어 있습니다. 김 이러한 변경 후 응용 프로그램을 구현 했습니다.
3. Contoso 웹 서비스 sts1 호출 하 여 ActAs 토큰 확인 하도록 구성 되어 있습니다. Adam sts1 위임 요청을 처리할 수 있게 되었습니다.
4. Fabrikam 사용자 프랭크 Contoso 응용 프로그램에 액세스 하 고 백 엔드 리소스에 대 한 액세스 제공 됩니다.

## <a name="set-up-the-identity-provider-ip"></a>(IP) Id 공급자 설정

프랭크 Fabrikam.com 관리자에 사용할 수 있는 세 가지 옵션은 다음과 같습니다.


1. 구입 하 고 (ADFS) Active Directory® Federation Services 등 STS 제품을 설치 합니다.
2. 구독 클라우드 STS 제품 같은 live Id STS 합니다.
3. 사용자 지정 STS 군을 사용 하 여 빌드입니다.

이 샘플 시나리오에 대 한에서는 가정 프랭크 option1 선택 하 고 ADFS IP STS 설치 합니다. 그 시작점과 끝점, 사용자가 인증 \windowsauth 라는 구성 합니다. ADFS 제품 설명서를 참조 하 여 Adam Contoso IT 관리자에 게 프랭크 Contoso.com 도메인 보안을 설정 합니다.

## <a name="set-up-the-claims-provider"></a>클레임 공급자 설정

옵션 id 공급자에 대 한 앞에서 설명한 대로 같은 Adam, Contoso.com 관리자에 사용할 수 있는 됩니다. 이 샘플 시나리오에 대 한에서는 가정 Adam 1 옵션을 선택 하 고 ADFS 2.0 RP STS 설치 합니다.

## <a name="set-up-trust-with-the-ip-and-application"></a>신뢰 IP와 응용 프로그램을 설정

Adam은 ADFS 설명서를 참조 하 여 보안 Fabrikam.com와 응용 프로그램을 설정 합니다.

## <a name="set-up-delegation"></a>위임 설정

ADFS 위임 처리를 제공합니다. ADFS 설명서를 참조 하 여 Adam ActAs 토큰 처리를 수 있습니다.

## <a name="application-specific-changes"></a>특정 응용 프로그램 변경

기존 응용 프로그램에 신원 위임에 대 한 지원을 추가 하는 다음과 같은 변경 사항이 만들어야 합니다. 김 군을 사용 하 여 이러한 변경 합니다.


- 해당 web1 sts1에서 받은 부트스트랩 토큰을 캐시 합니다.
- 발급 토큰 CreateChannelActingAs를 사용 하 여 백 엔드 웹 서비스에는 채널을 만듭니다.
- 백 엔드 서비스 메서드를 호출.

## <a name="cache-the-bootstrap-token"></a>캐시 된 부트스트랩 토큰

부트스트랩 토큰은 초기 토큰 STS에서 발급 및 응용 프로그램에서 클레임 추출 합니다. 이 샘플 시나리오에서이 토큰 sts1 프랭크 사용자에 대해 발급 및 응용 프로그램 캐시 합니다. 다음 코드 샘플 토큰 ASP.NET 응용 프로그램에서을 부트스트랩 검색 하는 방법을 보여 줍니다.

```
// Get the Bootstrap Token
SecurityToken bootstrapToken = null;

IClaimsPrincipal claimsPrincipal = Thread.CurrentPrincipal as IClaimsPrincipal;
if ( claimsPrincipal != null )
{
    IClaimsIdentity claimsIdentity = (IClaimsIdentity)claimsPrincipal.Identity;
    bootstrapToken = claimsIdentity.BootstrapToken;
}
```
군은 방법을 제공 [CreateChannelActingAs](https://msdn.microsoft.com/library/ee733863.aspx), 토큰 발행 요청 ActAs 요소로 지정된 보안 토큰을 보완 하는 지정 된 형식의 채널을 만드는 합니다. 이 방법으로 부트스트랩 토큰 전달 하 고 메서드를 호출 하는 데 필요한 서비스 반환된 채널에 수 있습니다. 프랭크의 id이 샘플 경우에서에 [배우](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.iclaimsidentity.actor.aspx) 속성 web1의 id로 설정 합니다.

코드는와 웹 서비스에 대 한 호출 하는 방법을 보여 [CreateChannelActingAs](https://msdn.microsoft.com/library/ee733863.aspx) ComputeResponse, 서비스의 방법 중 하나에서 반환된 채널 전화:

```
// Get the channel factory to the backend service from the application state
ChannelFactory<IService2Channel> factory = (ChannelFactory<IService2Channel>)Application[Global.CachedChannelFactory];

// Create and setup channel to talk to the backend service
IService2Channel channel;
lock (factory)
{
// Setup the ActAs to point to the caller's token so that we perform a 
// delegated call to the backend service
// on behalf of the original caller.
    channel = factory.CreateChannelActingAs<IService2Channel>(callerToken);
}

string retval = null;

// Call the backend service and handle the possible exceptions
try
{
    retval = channel.ComputeResponse(value);
    channel.Close();
} catch (Exception exception)
{
    StringBuilder sb = new StringBuilder();
    sb.AppendLine("An unexpected exception occurred.");
    sb.AppendLine(exception.StackTrace);
    channel.Abort();
    retval = sb.ToString();
}

```
## <a name="web-service-specific-changes"></a>웹 서비스 관련 변경

웹 서비스 WCF와 기본 제공 되 고 구속력 있는 적절 한 발행인이 주소와 구성 IssuedSecurityTokenParameters 된 후 군에 사용 되므로 유효성 검사는 ActAs 군에서 자동으로 처리 됩니다. 

웹 서비스에서 응용 프로그램에 필요한 특정 방법을 제공 합니다. 서비스에서 필요한 특정 코드 사항을 없습니다. 다음 코드 샘플 IssuedSecurityTokenParameters와 웹 서비스의 구성 보여 줍니다.

```
// Configure the issued token parameters with the correct settings
IssuedSecurityTokenParameters itp = new IssuedSecurityTokenParameters( "http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1" );
itp.IssuerMetadataAddress = new EndpointAddress( "http://localhost:6000/STS/mex" );
itp.IssuerAddress = new EndpointAddress( "http://localhost:6000/STS" );

// Create the security binding element
SecurityBindingElement sbe = SecurityBindingElement.CreateIssuedTokenForCertificateBindingElement( itp );
sbe.MessageSecurityVersion = MessageSecurityVersion.WSSecurity11WSTrust13WSSecureConversation13WSSecurityPolicy12BasicSecurityProfile10;

// Create the HTTP transport binding element
HttpTransportBindingElement httpBE = new HttpTransportBindingElement();

// Create the custom binding using the prepared binding elements
CustomBinding binding = new CustomBinding( sbe, httpBE );

using ( ServiceHost host = new ServiceHost( typeof( Service2 ), new Uri( "http://localhost:6002/Service2" ) ) )
{
    host.AddServiceEndpoint( typeof( IService2 ), binding, "" );
    host.Credentials.ServiceCertificate.SetCertificate( "CN=localhost", StoreLocation.LocalMachine, StoreName.My );

// Enable metadata generation via HTTP GET
    ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
    smb.HttpGetEnabled = true;
    host.Description.Behaviors.Add( smb );
    host.AddServiceEndpoint( typeof( IMetadataExchange ), MetadataExchangeBindings.CreateMexHttpBinding(), "mex" );

// Configure the service host to use WIF
    ServiceConfiguration configuration = new ServiceConfiguration();
    configuration.IssuerNameRegistry = new TrustedIssuerNameRegistry();

    FederatedServiceCredentials.ConfigureServiceHost( host, configuration );

    host.Open();

    Console.WriteLine( "Service2 started, press ENTER to stop ..." );
    Console.ReadLine();

    host.Close();
}
```

## <a name="next-steps"></a>다음 단계
[광고 FS 개발](../../ad-fs/AD-FS-Development.md)  
