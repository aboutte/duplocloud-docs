# Generate Terraform

### Execute Utility

Once Terraform Exporter Utility is configured, [export Environment Variables](install-terraform-exporter.md#prepare-environment-variable-in-bash) and execute listed commands.

> cd `tenant-terraform-generator`
>
> make run

![Utility  Execution in-progress](<../../../.gitbook/assets/image (24) (2).png>)

### View the Output

New Folders would be available under `tenant-terraform-generator\target\<customer-name>\<tenant>`

![Target Folder View](<../../../.gitbook/assets/image (6) (1) (1).png>)

Under `terraform` folder, **admin-tenant**, **aws-services** and **app** projects would be available. These projects would be referenced later to create new tenants and resources.

* **admin-tenant:**  This project manages the creation of DuploCloud tenant and tenant-related resources.
* **aws-services:** This project manages data services like Redis, RDS, Kafka, S3 buckets, Cloudfront, EMR and Elastic Search inside DuploCloud.
* **app:** This project manages DuploCloud services like EKS, ECS.
