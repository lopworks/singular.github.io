---
title: Singular API Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - Shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - authentication
  - account
  - customer
  - merchant
  - payment
  - definitions
  - utilities

search: true

code_clipboard: true
---

# Introduction

Welcome to Singular API. The platform is a single source for securely accessing APIs in several business domains using well defined RESTful interfaces. For convenience, all APIs may be accessed using the format below:

<aside class="notice">
https://api.singularapi.com/api/v:version/:domain/:singular_id/:class/
</aside>

where

- `:version` - specifies the version of API. Options currently include 1
- `:domain` - specifies the API domain to be accessed. Options currently include finance
- `:singular_id` - each provider (an API source) on Singular API has a unique ID
- `:class` - specifies the API class to be accessed within a domain
- `:operation` - specifies the class operation to be accessed

Other parameters may be required depending on the particular API operation.

As an example, to access information about a customer with an account ID 1098766565 held within a financial institution assigned Singular API ID 00234000054, the sample request below may be used

```shell
curl "https://api.singularapi.com/api/v1/finance/00234000054/customer?operation=details&account_id=1098766565"
  -H "Authorization: meowmeowmeow"
```

`https://api.singularapi.com/api/v1/finance/00234000054/customer?operation=details&account_id=1098766565`


We have provided a language binding in Shell. The language binding can be viewed from the code block area on the right. 

