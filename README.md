
# GitLab Docker Setup
This repository provides a guide and resources to set up a GitLab environment using Docker Compose. Follow the steps below to configure and run GitLab with secure credentials and persistent data storage.
## Prerequisites

- Docker and Docker Compose installed on your system.
- Basic knowledge of Docker and GitLab setup.

### Minimum Requirements for GitLab on Server
- **2 Cores**: The recommended number of CPU cores.
- **4GB RAM**: The recommended memory size for all installations
## Step-by-Step Setup
### **Step 1**: Change GitLab Image Version
In the `docker-compose.yml` file, change the GitLab image version to your desired version. Look for the following section in your `docker-compose.yml` file:

```bash
  services:
    gitlab:
        image: 'gitlab/gitlab-ee:latest'
        # Change to your desired version
```

Update the image version as needed, for example:

```bash
  image: 'gitlab/gitlab-ee:14.9.0-ce.0'
```

---
### **Step 2**: Set GitLab Root Password
Create a file to store the root password for GitLab:

```bash
  echo 'YourSecurePasswordHere' > secrets/gitlab_root_password
```

Make sure to replace `'YourSecurePasswordHere'` with your desired secure password.

---
### **Step 3**: Set GitLab Root Email
Create a file to store the root email for GitLab:

```bash
  echo 'admin@example.com' > secrets/gitlab_root_email
```

Replace `'admin@example.com'` with your desired admin email address.

---
### **Step 4**: Secure the Secrets
Set the correct file permissions for the password and email files:

```bash
  chmod 600 secrets/gitlab_root_password secrets/gitlab_root_email
```

---
### **Step 5**: Set the GitLab Home Path
You need to define a path for GitLab's data storage. To do this:

- Open your `.bashrc` file for editing: 

```bash
  nano ~/.bashrc
  # or
  vim ~/.bashrc
```

- Add the following line to set the GITLAB_HOME environment variable:
```bash
  export GITLAB_HOME=/path/to/your/gitlab/data
```
Replace `/path/to/your/gitlab/data` with the desired path for your GitLab data directory

- Save and close the file, then apply the changes:
```bash
  source ~/.bashrc
```

- Verify that the GITLAB_HOME variable is set correctly:
```bash
  echo $GITLAB_HOME
```
You should see the path to your GitLab data directory.

---
### **Step 6**: Set the GitLab External URL
Set the `external_url` for your GitLab instance by adding an environment variable in the `docker-compose.yml` file.

```bash
  environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'http://gitlab.example.com'
```
To set the `external_url` to your desired domain (e.g., `http://gitlab.example.com`),

---
### **Step 7**: Start GitLab Services
Run the following command to start the GitLab services in detached mode:

```bash
  docker-compose up -d
```
This will bring up the GitLab instance with the configurations you’ve set.

---
## Notes
Note: Please wait for 3 to 4 minutes after starting the container, as GitLab services take some time to initialize. Once GitLab is fully started, you can access it using the external_url you configured (e.g., http://gitlab.example.com).
