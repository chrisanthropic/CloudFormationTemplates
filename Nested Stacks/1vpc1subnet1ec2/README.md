### WHAT
A small example of CloudFormation nested stacks that creates a single ec2 instance inside a Vpc with a public-facing subnet and an ec2 security group that allows SSH access on port 22.

## Master.json
This is the 'core' template that calls the nested stacks. It contains the parameters required by the nested stacks, references the nested stacks, and passes the 'outputs'  from both nested stacks once finished.

## VpcStack.json
This stack uses some of the parameters passed by Master.json, builds a single vpc with a public subnet, attaches an internet gateway, and creates a route table.

## WebStack.json
This stack depends on the successful completion of the VpcStack so that it can be created inside that Vpc. It uses some of the parameters passed by Master.json, builds an ec2 instance using a default Amazon AMI, creates a security group that allows SSH access, and places the instance inside the previously created Vpc.


### HOW
- Upload the VpcStack.json and WebStack.json to an S3 bucket that you control.
- Modify the 2 instances of the phrase `YOUR-S3-BUCKET` in `Master.json` with the URL of your S3 bucket.
- Launch the `Master.json` stack.
