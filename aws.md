- [lambda](#lambda)
  - [python](#python)
- [ec2](#ec2)

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

# ec2

- **user-data** logs: `sudo cat /var/log/cloud-init-output.log`
- **user-data** script: `sudo cat /var/lib/cloud/instances/i-420/user-data.txt`
