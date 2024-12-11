- [lambda](#lambda)
  - [python](#python)
- [ec2](#ec2)
- [s3](#s3)

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

# s3

- remove something form bucket: `aws s3 rm s3://cencosud.prod.ccom.cl.raw/vortex/year=2024/month=11/day=13/aux0/events.csv`
