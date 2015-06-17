
# Informations

This library help to manage OpenId connection to FranceConnect with the Apache Oltu library.

Please note that this is a really first version with a lot of improvement remaining, but a good starting point for simply integrate FranceConnect into you applications.

Contributions (pull requests, issues, comment,...) are very welcome !

# build the library

```
mvn clean install
```

# Add it to your dependencies

```
<dependency>
	<groupId>eu.ooffee</groupId>
	<artifactId>eu.ooffee.fcconnect</artifactId>
	<version>0.0.1-SNAPSHOT</version>
</dependency>
    
```


# usage example : 

Configure your variables, connexions informations and init the configuration object and connection helper.

Connection endpoints used here are for entreprise clients, for Users endpoints refer here : https://doc.integ01.dev-franceconnect.fr/integration-fs/ 
```
String tokenUri = "https://fce.integ01.dev-franceconnect.fr/api/v1/token";
String authorizationUri = "https://fce.integ01.dev-franceconnect.fr/api/v1/authorize";
String userInfoUri = "https://fce.integ01.dev-franceconnect.fr/api/v1/userinfo";
String redirectUri = "{{your callback uri}}";
String clientId = "{{your client id}}";
String clientSecret = "{{your client secret}}";
String scope = "openid profile";
String state = "test";
String verifParameterId = "nonce";
String verifParameterValue = "toto";
    
protected FcParamConfig fpc = new FcParamConfig(tokenUri, authorizationUri, redirectUri, userInfoUri, clientId, clientSecret, scope, state, verifParameterId, verifParameterValue);

protected FcConnection fcc = new FcConnection(fpc);
    
```

In your connexion endpoint that manage the redirection 

```
URI redirect = fcc.getRedirectUri()
```    
    
In you callBack function to get the Accesstoken and userInfo 
```
String accessToken = fcc.getAccessToken(request);
		
String userInfo = fcc.getUserInfo(accessToken);
		
```