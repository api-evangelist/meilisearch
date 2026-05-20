---
title: "Patching LMDB: how we made Meilisearch’s vector store 3× faster"
url: "https://www.meilisearch.com/blog/3xfaster-vector-store"
date: "Wed, 18 Mar 2026 00:00:00 GMT"
author: "Clément Renault"
feed_url: "https://www.meilisearch.com/feed.xml"
---
We patched LMDB to support nested read transactions on uncommitted writes - eliminating full database scans and making Meilisearch's vector store 3× faster
