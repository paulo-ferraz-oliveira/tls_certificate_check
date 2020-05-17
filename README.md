# tls\_certificate\_validation

[![](https://img.shields.io/hexpm/v/tls_certificate_validation.svg?style=flat)](https://hex.pm/packages/tls_certificate_validation)
[![](https://travis-ci.org/g-andrade/tls_certificate_validation.png?branch=master)](https://travis-ci.org/g-andrade/tls_certificate_validation)
[![](https://circleci.com/gh/g-andrade/tls_certificate_validation/tree/master.svg?style=svg)](https://circleci.com/gh/g-andrade/tls_certificate_validation/tree/master)

`tls_certificate_validation` is a library for Erlang/OTP and Elixir that
provides TLS/SSL [connect
options](https://erlang.org/doc/man/ssl.html#type-tls_client_option)
required for negotiating connections whose security can be traced back
to a [trusted certificate
authority](https://www.mozilla.org/en-US/about/governance/policies/security-group/certs/included/).

It wraps [certifi](https://github.com/certifi/erlang-certifi) and
[ssl\_verify\_fun](https://github.com/deadtrickster/ssl_verify_fun.erl)
together with the boilerplate code required for validating [disoderly
certificate chains](https://github.com/elixir-mint/mint/issues/95).

### Usage

#### Erlang

##### 1\. Import as a dependency

rebar.config

``` erlang
{deps,
 [% [...]
  {tls_certificate_validation, "1.0.0"}
  ]}.
```

your\_application.app.src:

``` erlang
  {applications,
   [kernel,
    stdlib,
    % [...]
    tls_certificate_validation
   ]}
```

##### 2\. Make your connections safer

When using `httpc`

``` erlang
URL = "https://www.example.com/",
TlsOpts = tls_certificate_validation:connect_opts(URL),
HttpOpts = [{ssl, TlsOpts}],
httpc:request(get, {URL, []}, HttpOpts, [])
```

When using `ssl`:

``` erlang
Host = "example.com",
Options = tls_certificate_validation:connect_opts(Host),
ssl:connect(Host, 443, Options, 5000)
```

#### Elixir

##### 1\. Import as a dependency

mix.exs

``` elixir
  defp deps do
    [
      # [...]
      {:tls_certificate_validation, "1.0.0"}
    ]
  end
```

##### 2\. Make your connections safer

When using `ssl`:

``` erlang
Host = "example.com",
Options = tls_certificate_validation:connect_opts(Host),
ssl:connect(Host, 443, Options, 5000)
```

##### API Reference

The API reference can be found on
[HexDocs](https://hexdocs.pm/tls_certificate_validation/).

##### Tested setup

  - Erlang/OTP 19 or newer
  - rebar3

##### License

MIT License

Copyright (c) 2020 Guilherme Andrade

Permission is hereby granted, free of charge, to any person obtaining a
copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be included
in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS
OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

-----

*Generated by EDoc*