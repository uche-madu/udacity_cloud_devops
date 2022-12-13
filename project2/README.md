
# A High-Availability Web App (Udagram) Deployment Using AWS CloudFormation

![udagram-diagram](https://github.com/dreemer6/udacity_cloud_devops/blob/main/project2/udagram-diagram.png)

### Deployment Info:
* The `create.sh` and  `update.sh` scripts create and update the cloudformation stacks respectively.
* The `.yaml` files contain the cloudformation code, while the correspondingly named `.json` files contain the template parameters for each stack
* First: `udagram-infra*` creates the network components for the Udagram web app, including VPC, subnets, gateways, and routing
* Next: `udagram-servers*` creates the dependent server components, including necessary IAM role and instance profile, Security groups, load balancers, autoscaling group, and servers
* A public S3 bucket containing web files has been configured for static website hosting via the AWS console. The IAM role created in the `udagramservers` stack permits the private servers to `GET` S3 objects.
* For debugging purposes, the `bastionhost.*` files create a bastion host through which an Admin can SSH into the servers in the private subnets.

### Deployment Steps:
This assumes that the awscli has been installed and configured with permissions to access an AWS account.
1. Run `./create.sh udagraminfra udagram-infra.yaml udagram-infra-params.json` to create a stack named `udagraminfra` holding the underlying network components.
2. Run `./create.sh udagramservers udagram-servers.yaml udagram-servers-params.json` to creata a stack named `udagramservers` holding the server components.
3. Optionally, run `./create.sh bastionhost bastionhost.yaml bastionhost-params.json` to create a stack named `bastionhost` holding the bastion host server for debugging purposes only. It should be destroyed afterwards.
* Accessing the private servers through the bastion host would require updating the `WebServerSecGroup` resource in `udagram-servers.yaml` to allow ingress on port 22 (SSH). In that case, add the following code under `SecurityGroupIngress:`:
    ```

        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0

    ```
* Save the changes and **update** the `udagramservers` stack with: `./update.sh udagramservers udagram-servers.yaml udagram-servers-params.json`
* Other stacks can be updated similarly: `./update.sh ...`
* After debugging, remove this code from `udagram-servers.yaml` for security purposes.

### Destroying the Deployed Infrastucture
Stacks must be destroyed in reverse order. Wait for the stack deletion to be complete before deleting the underlying stack. Note that stack resources with dependencies cannot be deleted.
1. Run `aws cloudformation delete-stack --stack-name bastionhost`
2. Run `aws cloudformation delete-stack --stack-name udagramservers`
3. Run `aws cloudformation delete-stack --stack-name udagraminfra`

