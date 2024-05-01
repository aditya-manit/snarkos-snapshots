## Project Overview

This project contains an Ansible playbook that automates the process of stopping a specific service on a host, taking a snapshot of a designated directory, and uploading this snapshot to an Amazon S3 bucket. It is designed to help with regular backups and maintenance of critical services and data.

### Components

- **Ansible Playbook:** Defines tasks to stop the service, archive the directory, and upload the archive to S3.
- **Variables File:** Stores all necessary parameters like service name, directory path, AWS credentials, and S3 bucket details.

### Directory Structure

```
project_root/
│
├── playbook/
│   └── stop_service_snapshot_s3.yml  # Ansible playbook
│
└── vars/
    └── all.yml  # Variables file
```

## Requirements

- **Ansible**: This project requires Ansible to be installed on the machine from which you are running the playbooks.
- **AWS CLI**: Necessary for S3 interactions, ensure it is configured correctly on all target machines.
- **Permissions**: Ensure you have the necessary permissions to stop services and access the directory on the host machines, as well as permissions to write to the specified AWS S3 bucket.

## Configuration

Before running the playbook, update the `vars/all.yml` file with the appropriate values:

```yaml
service_name: <your_service_name>
directory_to_snapshot: <path_to_directory>
s3_bucket: <your_s3_bucket_name>
s3_location: <your/s3/directory/location>
aws_access_key: <your-aws-access-key>
aws_secret_key: <your-aws-secret-key>
aws_region: <your-aws-region>
```

**Note:** It is recommended to manage sensitive data like AWS credentials securely, preferably using Ansible Vault.

## Running the Playbook

To run the playbook, navigate to the `project_root` directory and execute the following command:

```bash
ansible-playbook playbook/support_snapshot.yml -i inventory.ini
```

Replace `inventory.ini` with the path to your inventory file, which lists the hosts on which the playbook will be run.

### Inventory File Format

Ensure your inventory file is properly set up. Here’s a basic example:

```ini
[backup_hosts]
192.168.1.100 ansible_user=ubuntu
192.168.1.101 ansible_user=ubuntu
```

This file should list all hosts in the `[backup_hosts]` group and specify the necessary connection details like `ansible_user`.

## Troubleshooting

- **Permission Issues:** Ensure that the user running the playbook has sufficient privileges to stop services and access directories on the remote hosts.
- **AWS CLI Not Configured:** Verify that AWS CLI is installed and configured correctly on all target machines.
- **Ansible Errors:** Check the syntax of your playbook and variable files. Run `ansible-playbook --syntax-check playbook_path` to find syntax errors.