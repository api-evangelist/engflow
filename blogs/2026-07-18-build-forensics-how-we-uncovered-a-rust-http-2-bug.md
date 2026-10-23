---
title: "Build Forensics: How we uncovered a Rust HTTP/2 bug"
url: "https://blog.engflow.com/2026/07/18/build-forensics-how-we-uncovered-a-rust-http2-bug/"
date: "2026-07-18"
author: "roger"
feed_url: "https://blog.engflow.com/feed_rss_created.xml"
---
Build Forensics: How we uncovered a Rust HTTP/2 bug Last year, one of our customers began reporting that 5% of their jobs based on Meta's Buck2 build system were failing. Even though there was no simple way to reproduce the phenomenon, all signs pointed to network hangs when a Buck2 client made API calls to their EngFlow cluster. If a simple timeout was added, the request would quickly time out, potentially indicating the issue was a bug in our remote execution platform.
