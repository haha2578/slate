---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell: cURL

toc_footers:
  - <a href='https://codia.ai/api-keys' target='_blank'>Sign Up for a Developer Key</a>

includes:
  - schema
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Codia API
---

# Introduction

Welcome to the Codia API! You can use our API to access VisualStruct API endpoints, which can recognize images, pdf, psd and other format files and convert them into a unified DSL.

We have language bindings in Shell, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Get Started

Getting started with the Codia API is easy! Follow these three simple steps to begin converting your Screenshots and PDFs into structured designs.

## Step 1: Activate Your Subscription

Before you can start using the Codia API, you need to activate a subscription plan. Our API supports two distinct scenarios:

- **Screenshot to Design conversion**: Convert Screenshots (PNG, JPG, etc.) into design structures. [Learn more about Screenshot Visual Struct →](https://codia.ai/visual-struct)
- **PDF to Design conversion**: Convert PDF documents into design structures. [Learn more about PDF to Visual Struct →](https://codia.ai/pdf-to-visual-struct)

<aside class="notice">
Important: You need to purchase separate subscriptions for each scenario you plan to use. If you need both Screenshot and PDF conversion capabilities, you'll need to activate subscriptions for both services.
</aside>

## Step 2: Generate Your API Key

Once you've completed your subscription purchase:

1. Navigate to your **Personal Center** in your Codia account
2. Go to the [API Keys section](https://codia.ai/api-keys) to request an API key
3. Your generated API key will work for both Screenshot and PDF conversion scenarios

![API Key Generation](https://static.codia.ai/resources/apikey.png)

<aside class="success">
Good news! Unlike subscriptions, your API key is universal and works across all scenarios once generated.
</aside>

## Step 3: Make Your First API Call

You're now ready to start converting your content! Depending on your use case, you can:

- **Convert images**: Use the [Convert Image To Design](#convert-image-to-design) endpoint
- **Convert PDFs**: Use the [Convert PDF To Design](#convert-pdf-to-design) endpoint

Both endpoints are documented below with complete examples and parameter descriptions to help you get started quickly.


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

# VisualStruct API

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
    // The Schema Object Here...
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

## Convert PDF To Design

```shell
curl 'https://api.codia.ai/v1/open/pdf_to_design' \
  -H 'Authorization: Bearer {codia_api_key}' \
  -H 'Content-Type: application/json' \
  --form 'pdf_file=@"xx.pdf"' \
  --form 'page_no="0"'
```

> The above command returns JSON structured like this:

```json
{
  "code": 0,
  "message": "ok",
  "data": {
    "configuration": {
      "scalingFactor": 1,
      "baseWidth": 1940,
      "measurementUnit": "px"
    },
    "pages": [
      {
        // The Schema Object Here...
      }
    ],
    "size": {
      "height": 1080,
      "width": 1940
    }
  }
}
```

This endpoint convert pdf to design.

### HTTP Request

`POST https://api.codia.ai/v1/open/pdf_to_design`

### Request Body

Parameter | Default | Description
--------- |---------| -----------
pdf_file | null    | PDF file that needs to be converted into design.
page_no | null    | Pages index of the PDF that need to be converted. Example: [0, 1]
