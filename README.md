provision-aws-system-account
=========

an ansible role to provision an AWS ready account. The role will perform the following steps to get an accout to be aws ready

* create a system account with a choose of enabling `sudo` and disable `requiretty` for the purpose of automation
* deploy `aws` key and secret key
* enable epel repo
* install python-pip
* install awscli

Requirements
------------

* python-pip
* awscli

Role Variables
--------------

* aws_key_id - an AWS access key id
* aws_secret_access_key - an AWS secret access key
* system_account - is an account that this role will work on to make it `AWS` ready.
* enable_sudoer - should this `system account` have sudo enabled. Default is `false`.
* disable_requiretty - should this `system account` disable `requiretty`. Default is `false`.
* deploy_aws_cred - should `AWS Credential` deploy to this `system account`. Default is `false`. When set to `true`, the `awscli` command line tool will also be installed.

Dependencies
------------

None

Example Playbook
----------------

The following playbook will provsion `ec2-user` and enable `sudo` and disable `requirettype`. Also configure this
`system account` to be able to talk to AWS cloud platform.

Note: for the security purpose, the `aws key` and `aws secrect key` should be encrypted use `ansbile-vault`. That's
you see this example has `vault_aws_access_key_id` and `vault_aws_secret_access_key` as they are variables defined in
`ansible-vault`. For the information how to use `ansble-vault`, please refer to [this document](http://docs.ansible.com/ansible/playbooks_vault.html).

    - hosts: all
      vars:
        system_account: ec2-user
        enable_sudoer: yes
        disable_requiretty: yes
        deploy_aws_cred: yes
        aws_key_id: "{{ vault_aws_access_key_id }}"
        aws_secret_access_key: "{{ vault_aws_secret_access_key }}"

      roles:
         - provision-aws-system-account

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
