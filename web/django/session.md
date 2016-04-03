# Django Session

2016/04/03

デフォルトの振る舞いはHTTP onlyセッションなのでJavaScriptから読めない。
HTTP onlyセッションをやめるには`SESSION_COOKIE_HTTPONLY`を`False`に変える。
ただし、通常これは危険なことだとされる。

## 参考

- [Django Settings](https://docs.djangoproject.com/en/dev/ref/settings/#std:setting-SESSION_COOKIE_HTTPONLY)
- [Django How to use sessions - Using cookie-based sessions](https://docs.djangoproject.com/en/dev/topics/http/sessions/#cookie-session-backend)

