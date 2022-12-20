# OIDC PKCE POC

Vanilla Liferay does not support PKCE in the OIDC SSO.
This custom code replaces `com.liferay.portal.security.sso.openid.connect.internal.OpenIdConnectAuthenticationHandlerImpl.java`
so as to take advantage of the fact that the nimbus sdk supports PKCE already.

Go to System Settings -> Module Container and blacklist the following component:
`com.liferay.portal.security.sso.openid.connect.internal.OpenIdConnectAuthenticationHandlerImpl`

This code is built again DXP 7.4 U47. There has been a lot of changes and the same code would have to
be adapted against other updates.

The following error will appear in the logs:
```
2022-10-27 12:43:42.172 ERROR [http-nio-8080-exec-8][SerializableSessionAttributeListener:59] com.nimbusds.oauth2.sdk.pkce.CodeVerifier is not serializable and will prevent this session from being replicated
```

I'll have a look and try to fix that.
But it should not prevent this from working if we are not in a scenario where session needs to be replicated.
 
## client_secret_jwt support

Added support for client_secret_jwt
Use the new ***OAuth Client Administration menu*** in the Control Menu in order to
set "token_endpoint_auth_method": "client_secret_jwt"
