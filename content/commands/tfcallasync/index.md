---
arguments:
- name: library.function
  type: string
- name: numkeys
  type: integer
- key_space_index: 0
  multiple: true
  name: key
  optional: true
  type: key
- multiple: true
  name: arg
  optional: true
  type: string
bannerText: 'The triggers and functions feature of Redis Stack and its documentation
  are currently in preview, and only available in Redis Stack 7.2 or later. You can
  try out the triggers and functions preview with a [free Redis Cloud account](https://redis.com/try-free/?utm_source=redisio&utm_medium=referral&utm_campaign=2023-09-try_free&utm_content=cu-redis_cloud_users).
  The preview is available in the fixed subscription plan for the **Google Cloud Asia
  Pacific (Tokyo)** and **AWS Asia Pacific (Singapore)** regions.


  If you notice any errors in this documentation, feel free to submit an issue to
  GitHub using the "Create new issue" link in the top right-hand corner of this page.

  '
categories:
- docs
- develop
- stack
- oss
- rs
- rc
- oss
- kubernetes
- clients
complexity: Depends on the function that is executed.
description: Invoke an asynchronous JavaScript function
group: triggers_and_functions
hidden: false
linkTitle: TFCALLASYNC
module: Triggers and functions
since: 2.0.0
stack_path: docs/interact/programmability/triggers-and-functions
summary: Invoke an asynchronous JavaScript function
syntax: 'TFCALLASYNC <library name>.<function name> <number of keys> [<key1> ... <keyn>]
  [<arg1> ... <argn>]

  '
syntax_fmt: TFCALLASYNC library.function numkeys [key [key ...]] [arg [arg ...]]
syntax_str: numkeys [key [key ...]] [arg [arg ...]]
title: TFCALLASYNC
---

Invoke an asynchronous JavaScript function (coroutine).

## Required arguments

<details open>
<summary><code>library name</code></summary>

The name of the JavaScript library that contains the function.
</details>

<details open>
<summary><code>function name</code></summary>

The function name to run.
</details>

<details open>
<summary><code>number of keys</code></summary>

The number keys that will follow.
</details>

<details open>
<summary><code>keys</code></summary>

The keys that will be touched by the function.
</details>

<details open>
<summary><code>arguments</code></summary>

The arguments passed to the function.
</details>

## Return

`TFCALLASYNC` returns either

* The return value of the function.
* [Error reply]({{< baseurl >}}/develop/reference/protocol-spec#resp-errors) when the function execution failed.

## Examples

{{< highlight bash >}}
TFCALLASYNC lib.hello 0
"Hello World"
{{</ highlight>}}

## See also

## Related topics
