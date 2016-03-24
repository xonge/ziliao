1. "lucadegasperi/oauth2-server-laravel": "5.1.*"
2. LucaDegasperi\OAuth2Server\Storage\FluentStorageServiceProvider::class,
   LucaDegasperi\OAuth2Server\OAuth2ServerServiceProvider::class,
3. 'Authorizer' => LucaDegasperi\OAuth2Server\Facades\Authorizer::class,
4. \LucaDegasperi\OAuth2Server\Middleware\OAuthExceptionHandlerMiddleware::class,
5. 'oauth' => \LucaDegasperi\OAuth2Server\Middleware\OAuthMiddleware::class,
   'oauth-user' => \LucaDegasperi\OAuth2Server\Middleware\OAuthUserOwnerMiddleware::class,
   'oauth-client' => \LucaDegasperi\OAuth2Server\Middleware\OAuthClientOwnerMiddleware::class,
   'check-authorization-params' => \LucaDegasperi\OAuth2Server\Middleware\CheckAuthCodeRequestMiddleware::class,