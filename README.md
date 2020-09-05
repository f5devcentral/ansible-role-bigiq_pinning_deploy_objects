# Ansible Role: bigiq_pinning_deploy_objects

Performs a series of steps needed to pin and deploy BIG-IQ object(s) to a BIG-IP device managed on BIG-IQ.

This role currently supports only SSL Certificates & Keys, WAF Policy and Security Logging Profiles.

If you are interested for other type of objects, [open an issue on GitHub](https://github.com/f5devcentral/ansible-role-bigiq_pinning_deploy_objects/issues).

## Role Variables

Available variables are listed below. For their default values, see `defaults/main.yml`.

Establishes initial connection to your BIG-IQ. These values are substituted into
your ``provider`` module parameter. These values should be the connection parameters
for the **CM BIG-IQ** device.

        provider:
          user: admin
          server: 10.1.1.4
          server_port: 443
          password: secret
          loginProviderName: tmos
          validate_certs: no

Define the list of existing objects you want to pin and deploy.

    modules: 
      - name: ltm
        pins:
          - { type: "sslCertReferences", name: "demo.crt" }
          - { type: "sslKeyReferences", name: "demo.key" }
      - name: asm
        pins:
          - { type: "attachedPoliciesReferences", name: "myWAFpolicy1" }
          - { type: "attachedPoliciesReferences", name: "myWAFpolicy2" }
      - name: shared_security
        pins:
          - { type: "logProfileReferences", name: "mySecurityLoggingProfile" }

Define the target device where you want to pin and deploy the objects.
It can be either device_address or device_name.
If you are deploying to a HA pair, only specify one of the device address or name, the role will push automatically to 
all the devices part of the cluster (supports only clusters with 2 devices).

    device_address: 10.1.1.7

or

    device_name: bigip.example.com

Define the deployment Task Name (optional):

    bigiq_task_name: "Deployment through Ansible/API"

## Example Playbook

    ---
    - hosts: all
      connection: local
      vars:
        provider:
          user: admin
          server: "{{ ansible_host }}"
          server_port: 443
          password: secret
          loginProviderName: tmos
          validate_certs: no

      tasks:
          - name: Pin and deploy SSL certificate & key, WAF policy and Security Logging Profile to device
            include_role:
              name: f5devcentral.bigiq_pinning_deploy_objects
            vars:
              bigiq_task_name: "Deployment through Ansible/API"
              device_address: 10.1.1.7
              modules: 
                - name: ltm
                  pins:
                    - { type: "sslCertReferences", name: "demo.crt" }
                    - { type: "sslKeyReferences", name: "demo.key" }
                - name: asm
                  pins:
                    - { type: "attachedPoliciesReferences", name: "myWAFpolicy1" }
                    - { type: "attachedPoliciesReferences", name: "myWAFpolicy2" }
                - name: shared_security
                  pins:
                    - { type: "logProfileReferences", name: "mySecurityLoggingProfile" }
            register: status

## License

Apache

## Author Information

This role was created in 2020 by [Romain Jouhannet](https://github.com/rjouhann).

[1]: https://galaxy.ansible.com/f5devcentral/bigiq_pinning_deploy_objects
