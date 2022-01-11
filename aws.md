<!-- MarkdownTOC autolink="true" levels="1,2" -->

- [lambda](#lambda)
  - [python](#python)

<!-- /MarkdownTOC -->
# lambda

## python

- add the contents of lib and lib64 site-packages to your .zip file.
```bash
cd $virtual_env/lib/python3.6/site-packages
zip -r9 ~/createthumbnail.zip *
```
    - to include all hidden files, use the following option `zip -r9 ~/createthumbnail.zip .`
- add your python code to the .zip file
```bash
cd ~
zip -g createthumbnail.zip createthumbnail.py
```
