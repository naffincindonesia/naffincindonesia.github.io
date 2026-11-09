---
layout: post
title: "Hacker101 CTF - Postbook (7/7 Flags)"
date: 2026-11-09
categories: [CTF, Hacker101, Web]
tags: [IDOR, BAC, XSS, Hacker101]
---

## Naff Inc. - Postbook Writeup

**Target:** Postbook - Hacker101 CTF  
**Result:** 7/7 Flags - 46 Points  
**Focus:** IDOR / Broken Access Control

Postbook looks like a simple diary app. Public posts for everyone, private posts only for you. But every access control check is client-side or missing.

### Recon

After signup, I noticed two things:
1. Profile URL uses `?id=` - classic IDOR signal
2. Post creation sends `user_id` in the request - I control who I post as

### Flag 0 - Stored XSS

Post title is not sanitized. A simple payload in the title executes when anyone views the timeline.

```html
<script>alert('hacked by naff')</script>
