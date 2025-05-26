---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell: cURL

toc_footers:
  - <a href='https://codia.ai' target='_blank'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Codia API
---

# Introduction

Welcome to the Codia API! You can use our API to access Anything-To-Design API endpoints, which can recognize images, pdf, psd and other format files and convert them into a unified DSL.

We have language bindings in Shell, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: Bearer {codia_api_key}"
```

> Make sure to replace `{codia_api_key}` with your API key.

Codia uses API keys to allow access to the API. You can register a new Codia API key at our [developer portal](https://codia.ai).

Codia expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer {codia_api_key}`

<aside class="notice">
You must replace <code>{codia_api_key}</code> with your personal API key.
</aside>

# Anything-To-Design

## Convert Image To Design

```shell
curl 'https://api.codia.ai/v1/open/image_to_design' \
  -H 'Authorization: Bearer {codia_api_key}' \
  -H 'Content-Type: application/json' \
  --data '{
    "image_url": "your image url"
  }'
```

> The above command returns JSON structured like this:

```json
{
  "code": 0,
  "message": "ok",
  "data": {
    // dsl here...
  }
}
```

This endpoint convert image to design.

### HTTP Request

`POST https://api.codia.ai/v1/open/image_to_design`

### Request Body

Parameter | Default | Description
--------- |---------| -----------
image_url | null    | Image URL that needs to be converted into design.
