[![license](http://img.shields.io/badge/license-apache_2.0-red.svg?style=flat)](https://github.com/florintp-onboarding/florintp-onboarding/packer_build_an_image/LICENSE)

## The scope of this repository is build a Docker image using Packer

These assets are provided to perform the tasks described in the [Packer Learning - Build a Docker Image](https://learn.hashicorp.com/tutorials/packer/docker-get-started-build-image?in=packer/docker-get-started) guide and adapted for a workout example.

----


## Which are the main tools used to accomplish this task?


## Packer and Docker
-	Packer Website: https://www.packer.io , https://www.docker.com
-	Packer Discussion forum: [Discuss](https://discuss.hashicorp.com/c/packer/)
- Packer Documentation: [https://www.packer.io/docs](https://www.packer.io/docs)
- Packer Tutorials: [HashiCorp's Learn Platform](https://learn.hashicorp.com/packer)
- Docker Website: https://www.docker.com (https://www.docker.com/get-started/)
- Docker Documentation: [https://docs.docker.com](https://docs.docker.com/)


## Steps performed
With Packer installed, it is time to build your first image. For speed, simplicity's sake, and because it's free to download, you will build a Docker container. You can download Docker [here](https://www.docker.com/get-started/) if you don't have it installed.

### 1. Install the minimal required packges (for MAC M1)
- Install [Packer](https://learn.hashicorp.com/tutorials/packer/getting-started-install?in=packer/docker-get-started) ( [Direct Download](https://www.packer.io/downloads) )
- Install [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- Install [gh](https://cli.github.com/manual/installation)
- Install [docker](https://www.docker.com/products/docker-desktop)

```
brew install hashicorp/tap/packer
brew install gh
brew install git
brew install packer
brew install docker
```

### 2. Clone current repository
```shell
gh repo clone florintp-onboarding/packer_build_an_image
```

### 3. Create the working directory
```
mkdir packer_tutorial
cd packer_tutorial
```

### 4. Write Packer template
touch docker-ubuntu.pkr.hcl
```
tee -a docker-ubuntu.pkr.hcl << EOFT1
packer {
  required_plugins {
    docker = {
      version = ">= 0.0.7"
      source = "github.com/hashicorp/docker"
    }
  }
}

source "docker" "ubuntu" {
  image  = "ubuntu:xenial"
  commit = true
}

build {
  name    = "learn-packer"
  sources = [
    "source.docker.ubuntu"
  ]
}
EOFT1
```

### 5. Initialize Packer configuration
```
packer init .
```

### 6. Format and validate your Packer template
```
packer fmt .
```

### 7. Validate the template. If Packer detects any invalid configuration, Packer will print out the file name, the error type and line number of the invalid configuration. The example configuration provided above is valid, so Packer will return nothing.
``` shell
packer validate .
 ```
 
 ### 8. Build Packer image 
 ```
 packer build docker-ubuntu.pkr.hcl
 ```
 
 
 #### 9. Find the latest built image
 ```
 docker images
 ````
 
 ### 10. Identify the image id and add a tag to it for an easy identification
 ```plaintext
For example the Docker image created few seconds ago, 9eb9731ac5d8 is captured in the output of docker images like below:

$ docker images

REPOSITORY                    TAG                            IMAGE ID       CREATED              SIZE
<none>                        <none>                         9eb9731ac5d8   About a minute ago   119MB
....

$ docker tag 9eb9731ac5d8 9eb9731ac5d8:ubuntu_packer1

$ docker images

REPOSITORY                    TAG                            IMAGE ID       CREATED              SIZE
9eb9731ac5d8                  ubuntu_packer1                 9eb9731ac5d8   About a minute ago   119MB

```
