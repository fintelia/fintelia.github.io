---
layout: post
title: Understanding Rust HashMap Performance (Part 1)
---

{{ page.title }}
================

In this post I will attempt to measure current HashMap performance in Rust and
explore how API changes could enable more performant usages of this data
structure. This goal is motivated in part by a [recent pre-RFC](https://internals.rust-lang.org/t/pre-rfc-abandonning-morals-in-the-name-of-performance-the-raw-entry-api/7043/41).

# Goal

In this first part I will simply attempt to construct a new HashMap a Vec of
(key, value) pairs:

```rust
use std::collections::HashMap;

#[inline(always)]
fn make_hashmap(v: Vec<(i64, 64)>) -> HashMap<i64, i64> {
   v.into_iter().collect()
}

```

