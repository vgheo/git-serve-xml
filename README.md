

#Functional test - serve html/xml/xsl files from a git repo using http

## gitweb
- ISSUE: URLs used to acces files are not hierarchical - so releative links cannot be resolved

##  gitlist
v0.5.0
- DOES have hierarchical URLS - relative links are resolved

- ISSUE- implementation serves raw files with http header content-type:text/plain

### SOL1. Patch gitlist implementation - force  to text/xml
- see [patch](../../blob/master/gitlist-serve-xml.patch)
- WORKS for XML+XSL
    + XHTML (which is XML)
- limitation : ALL files are handled as xml 
    => html files (non-xhtml) are displayed as xml tree (no stylesheed)
    => all non-xml text files result in errors (invalid xml)

- ALL RAW files shall be 
    - served with Content-type:text/xml
    - in browser - rendered as XML
        - XSL transform to x/html supported
        - static xhtml supported  

####Demo:
- Supported:
  - [t.xml](../../raw/master/t.xml)
  - [t2.xml](../../raw/master/t2.xml)
  - [cds.xml](../../raw/master/cds.xml)
- Not supported:
  - [t.html](../../raw/master/t.html)
  - [t2.html](../../raw/master/t2.html)
  - [README.md](../../raw/master/README.md)

#### SOL2. Feature request to gitlist

See [request](https://github.com/klaussilveira/gitlist/issues/571).

Request on gitlist support list to impelment proper content-type handling,
esp. for xml files. 
- VAR1 - hard-code xml extension -> text/xml 
- VAR2 - use design from gitweb
    - uses system-wide mime type - extension mapping


