# Rate limit requests based on the user-agent

```
acl is_bot req.fhdr(user-agent) -m sub -i claudebot
acl is_bot req.fhdr(user-agent) -m sub -i googleother
acl is_bot req.fhdr(user-agent) -m sub -i facebookexternalhit
acl is_bot req.fhdr(user-agent) -m sub -i amazonbot
acl is_bot req.fhdr(user-agent) -m sub -i semrushbot
acl is_bot req.fhdr(user-agent) -m sub -i yandex
acl is_bot req.fhdr(user-agent) -m sub -i bytespider
acl is_bot req.fhdr(user-agent) -m sub -i applebot
acl is_bot req.fhdr(user-agent) -m sub -i bingbot
acl is_bot req.fhdr(user-agent) -m sub -i dotbot

stick-table type string len 128 size 100k expire 1h store http_req_rate(10s)
http-request track-sc0 req.fhdr(user-agent) if is_bot
http-request deny deny_status 429 hdr retry-after 30 if { sc_http_req_rate(0) gt 10 }
```
