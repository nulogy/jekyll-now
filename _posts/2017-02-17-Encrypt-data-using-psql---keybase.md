---
layout: post
title: "Encrypt data using psql + keybase"
author: diogobiazus
date: 2017-02-17T19:28:59+00:00
---

To export any query to a CSV and send it to `stdout` one can use:

    psql -c "\copy (select version()) to stdout csv header"

So you can just replace `select version()` with any query in the above command and the results will be dumped in your terminal screen. If you have any sensitive data that is not already encrypted you could pipe this results directly to keybase as in:

    psql -c "\copy (select version()) to stdout csv header" | keybase encrypt diogob

Where `diogob` is the recipient of your message (or your own username in case you want to store this file for future use).
