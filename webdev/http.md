# HTTP

## Resources

* [Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content](https://tools.ietf.org/html/rfc7231)
  * [4.1 Request Methods](https://tools.ietf.org/html/rfc7231#section-4.1)
  * [6. Response Status Codes](https://tools.ietf.org/html/rfc7231#section-6)
* [HTTP Status Codes](https://httpstatuses.com/)

## Tools

### HTTPie

[HTTPie](https://httpie.org/) is a better `curl`. Read the [documentation](https://httpie.org/doc).

Simple GET or DELETE requests (`http://` is optional, and for `localhost`, even the hostname is):

```sh
http get http://localhost:3001/api/stuff
http delete :3001/api/stuff
```

Data is [implicitly sent as JSON](https://httpie.org/doc#json):

```sh
http PUT example.org name=John email=john@example.org
```

Add some [custom headers](https://httpie.org/doc#http-headers):

```sh
http example.org \
  User-Agent:Bacon/1.0 \
  'Cookie:valued-visitor=yes;foo=bar' \
  X-Foo:Bar \
  Referer:http://httpie.org/
```