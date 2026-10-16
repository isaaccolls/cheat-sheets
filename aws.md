- [lambda](#lambda)
  - [python](#python)
- [ec2](#ec2)
- [aws cli](#aws-cli)
  - [s3](#s3)
  - [secrets manager](#secrets-manager)
  - [ses](#ses)

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

# aws cli

## s3

- list: `aws s3 ls s3://cencosud.prod.ccom.cl.enriched/vortex/Chile/Jumbo-Prime/year=2024/month=12/day=24/`
- remove something form bucket: `aws s3 rm s3://cencosud.prod.ccom.cl.raw/vortex/year=2024/month=11/day=13/aux0/events.csv`
- copy: `aws s3 cp s3://cencosud.prod.ccom.cl.enriched/vortex/Chile/Jumbo-Prime/year=2024/month=12/day=24/ s3://cencosud.prod.ccom.cl.enriched/vortex/Chile/Jumbo-Prime/year=2024/month=12/day=24-real/ --recursive`

## secrets manager

- list secrets: `aws secretsmanager list-secrets`
- get secret value: `aws secretsmanager get-secret-value --secret-id cl_connect_vortex_core`

## ses

- Listar todas las direcciones suprimidas: `aws sesv2 list-suppressed-destinations --region us-east-1`
  - Filtrar por motivo (BOUNCE o COMPLAINT): `aws sesv2 list-suppressed-destinations --reasons BOUNCE --region us-east-1`
- Consultar un correo específico: `aws sesv2 get-suppressed-destination --email-address corre@prueba.com --region us-east-1`
- Quitar un correo en particular: `aws sesv2 delete-suppressed-destination --email-address corre@prueba.com --region us-east-1`
- Limpiar toda la lista:
  ```sh
  aws sesv2 list-suppressed-destinations --region us-east-1 \
    --query 'SuppressedDestinationSummaries[].EmailAddress' --output text \
  | tr '\t' '\n' \
  | while read email; do
      echo "Eliminando $email"
      aws sesv2 delete-suppressed-destination --email-address "$email" --region us-east-1
    done
  ```
