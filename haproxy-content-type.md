# Set the content-type header based on the file extension

```
http-request set-var(txn.path) path

acl is_file var(txn.path) -m beg /api/files/
acl is_pdf var(txn.path) -m end .pdf
acl is_xml var(txn.path) -m end .xml

http-response set-header content-type application/pdf if is_file is_pdf
http-response set-header content-type application/xml if is_file is_xml
```
