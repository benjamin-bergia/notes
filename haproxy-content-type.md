# Set the content-type header based on the file extension

```
http-request set-var(txn.path) path

acl is_file var(txn.path) -m beg /api/files/
acl is_pdf var(txn.path) -m end .pdf
acl is_xml var(txn.path) -m end .xml

http-response set-header content-type application/pdf if is_file is_pdf
http-response set-header content-type application/xml if is_file is_xml
```

The request path is added to a transaction-scoped variable that will still be available during the processing of the response.
Accessing the request path during the response processing wouldn't work.
