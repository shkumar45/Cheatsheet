## aws-cli

- commands:

  ```
  $ aws
  $ pip install --upgrade awscli (upgrade to latest version)
  ```

## alias your profile

`alias aws="aws --profile skumar-personal"`

## aws-shell

- offers auto completion (but awscli has it too)
- commands:

  ```
  $ pip install aws-shell, launches a new shell

  USAGE:
  $ aws-shell --profile tii-prod
  ```

## aws-okta -

- allows to authenticate using okta credentials
- it can also be used as aws cli
- commands:

  ```
  USAGE:
  $ aws-okta exec <profile> -- <command>

  ex:
  $ aws-okta exec tii-dev -- aws ec2 describe-instances
  ```

  Alternatively we can run `$(aws-okta env <env>)` in your terminal, then run aws commands as usual. e.g.

  ```
  $ $(aws-okta env tii-dev)
  $ aws ec2 describe-hosts
  ```

## aws local cli

- a cli provided by localstack
- commands:

  ```
  $ awslocal
  ```

## create keypair

```
aws ec2 create-key-pair --key-name MyKeyPair --query 'KeyMaterial' --output text > MyKeyPair.pem chmod 400 MykeyPair.pem
```

## create your instance (ubuntu 20)

```
aws ec2 run-instances --image-id ami-005c06c6de69aee84 --count 1 --instance-type t2.micro --key-name MyKeyPair --security-group-ids sg-09b765046fec7d977 --subnet-id subnet-0b2dc751
```

## ssh into the instance

```
ssh -i MyKeyPair.pem ec2-user@<public ip of newly created instance>
$ aws ec2 describe-instances
$ aws ec2 terminate-instances --instance-ids [from above]
```



