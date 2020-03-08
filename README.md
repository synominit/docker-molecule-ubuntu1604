# Ubuntu 16.04 LTS (Xenial) Molecule Test Image
[![Docker Repository on Quay](https://quay.io/repository/synominit/docker-molecule-ubuntu1604/status "Docker Repository on Quay")](https://quay.io/repository/synominit/docker-molecule-ubuntu1604)

[![Build Status](https://travis-ci.com/synominit/docker-molecule-ubuntu1604.svg?branch=master)](https://travis-ci.com/synominit/docker-molecule-ubuntu1604)


Ubuntu 16.04 LTS (Xenial) Docker container for Ansible playbook and role testing.

## Tags

  - `latest`: Latest stable version of Ansible.
  - `testing`: Same as `latest`, but with additional testing dependencies, including:
    - `yamllint`
    - `ansible-lint`
    - `flake8`
    - `testinfra`
    - `molecule`

The latest tag is a lightweight image for basic validation of Ansible playbooks. The `testing` tag also includes a comprehensive suite of Ansible and infrastructure testing tools in case you want them pre-installed.

## How to Build

This image is built on Docker Hub automatically any time the upstream OS container is rebuilt, and any time a commit is made or merged to the `master` branch. But if you need to build the image on your own locally, do the following:

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. `cd` into this directory.
  3. Run `docker build -t molecule-ubuntu1604 .`

> Note: Switch between `master` and `testing` depending on whether you want the extra testing tools present in the resulting image.

## How to Use

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. Pull this image from Docker Hub: `docker pull quay.io/synominit/docker-molecule-ubuntu1604:latest` (or use the image you built earlier, e.g. `molecule-ubuntu1604`).
  3. Run a container from the image: `docker run --detach --privileged --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro quay.io/synominit/docker-molecule-ubuntu1604:latest` (to test my Ansible roles, I add in a volume mounted from the current working directory with ``--volume=`pwd`:/etc/ansible/roles/role_under_test:ro``).
  4. Use Ansible inside the container:
    a. `docker exec --tty [container_id] env TERM=xterm ansible --version`
    b. `docker exec --tty [container_id] env TERM=xterm ansible-playbook /path/to/ansible/playbook.yml --syntax-check`

## Notes

I use Docker to test my Ansible roles and playbooks on multiple OSes using CI tools like Jenkins and Travis. This container allows me to test roles and playbooks using Ansible running locally inside the container.

> **Important Note**: I use this image for testing in an isolated environment—not for production—and the settings and configuration used may not be suitable for a secure and production environments. Use on production servers/in the wild at your own risk!

## Author

Created in 2020 by [Skye Pham](https://www.skyelp.com/), DevOps Architect, Reverse Engineering and Security Specialist.
