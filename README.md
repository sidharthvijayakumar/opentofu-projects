# open-tofu-projects
This will use reference from the open-tofu-modules repository

Sample to use a module from https://github.com/sidharthvijayakumar/opentofu-modules

Use a suitable tag which fits your need and this is the sample how to use the tag from modules repo

```bash
module "ec2" {
  source                        = "git::https://github.com/sidharthvijayakumar/opentofu-modules.git//modules/aws-ec2?ref=aws-ec2/v0.0.1"
  name                          = "single-instance"
  ami                           = "ami-00141e1168ad5e0c7"
  instance_type                 = "t2.micro"
  subnet_id                     = "subnet-48236104"
  availability_zone             = "ap-south-1b"
  vpc_security_group_ids        = [module.web_server_sg.id]
  associate_public_ip_address   = true
  key_name                      = "demo-key-pair"
  create_spot_instance          = false
  create_iam_instance_profile   = true
  monitoring                    = true
  # user_data                   = file("./scripts/user-data.sh")
  ebs_volumes = {
      "/dev/xvdf"   = {
        size        = 10
        type        = "gp3"
      }
  }

  iam_role_policies = {
    SSM                  = "arn:aws:iam::aws:policy/AmazonSSMManagedInstanceCore"
    SecretsManagerAccess = "arn:aws:iam::aws:policy/SecretsManagerReadWrite"
  }

  tags = {
    Terraform   = "true"
    Environment = "dev"
  }
}
```