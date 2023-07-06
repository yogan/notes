# HTTP

## Resources

* [Hypertext Transfer Protocol (HTTP/1.1): Semantics and
  Content](https://tools.ietf.org/html/rfc7231)
  * [4.1 Request Methods](https://tools.ietf.org/html/rfc7231#section-4.1)
  * [6. Response Status Codes](https://tools.ietf.org/html/rfc7231#section-6)
* [HTTP Status Codes](https://httpstatuses.com/)

## Tools

### HTTPie

[HTTPie](https://httpie.org/) is a better `curl`. Read the
[documentation](https://httpie.org/doc).

Simple GET or DELETE requests (`http://` is optional, and for `localhost`, even
the hostname is):

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

### HTTP Prompt

[HTTP Prompt](http://http-prompt.com) is an interactive command-line HTTP client
featuring autocomplete and syntax highlighting.

Installation:

```sh
sudo apt install python-pip
pip install --user http-prompt
# pip installs to ~/.local/bin/, but does not tell anyone.
# check if this is part of your $PATH, e.g. for my fish setup:
path
add_path ~/.local/bin/
```

Usage (see the [user
guide](http://docs.http-prompt.com/en/latest/user-guide.html#quickstart) for
details):

```sh
$ http-prompt localhost:3001

> cd /api/resource
> get                             # sends HTTP request: GET /api/resource
…                                 # response, paged and /w syntax highlighting

> Content-Type:application/json   # set a header
# set some body parameters as JSON:
> number:=1234
> is_ok:=true
> names:=["foo","bar"]
> user:='{"username": "foo", "password": "bar"}'
> post                            # send the POST request with header and body
```

HTTP Prompt is using `httpie`, and you can preview the calls it will make with

```sh
> httpie post   # or any other HTTP verb
```

Note that headers, body data, etc. is persisted, so it will be included in every
request. You can check the current environment with `env` and remove stuff with
`rm`:

```sh
> env
cd http://localhost:3001/api/stuff
'jsondata:={"crazy": "object here"}'
Content-Type:application/json
> rm -h Content-Type              # remove that header
> rm *                            # clear everything
```

### Insomnia

[Insomnia](https://insomnia.rest) is a graphical API client (Rest, GraphQL, WS, …), similar to Postman.
Can store collections of API endpoints, supports multiple environments, etc. Free version is sufficient
for most stuff.

### jq

[jq](https://stedolan.github.io/jq/) is like `sed` for JSON data.

Can be used together with `curl` or `http` to filter out data from lengthy JSON
results. Minimal example:

```sh
> http some.web-api.org/stuff
{ "foo": "bar", "otherStuff": "i dont care for", ... }

> http some.web-api.org/stuff | jq .foo
"bar"
```

Dealing with arrays:

```sh
> http some.web-api.org/list
[{ "foo": 1, "bar": "a" }, { "foo": 2, "bar": "b" }, ...]

> http some.web-api.org/list | jq '.[] | .foo'
1
2
```
