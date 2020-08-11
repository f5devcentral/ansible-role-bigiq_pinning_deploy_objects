# Ansible Role: bigiq_pinning_deploy_objects

Performs a series of steps needed to pin and deploy BIG-IQ object(s) to a BIG-IP device managed on BIG-IQ.

This role currently supports only SSL Certificates and Keys.

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

Define the list of existing objects you want to pin and deploy to a BIG-IP device.

    ltm: 
      - { type: "sslCertReferences", name: "demo.crt" }
      - { type: "sslKeyReferences", name: "demo.key" }

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
          - name: Pin and deploy SSL certificate and key to device
            include_role:
              name: bigiq_pinning_deploy_objects
            vars:
              ltm: 
                - { type: "sslCertReferences", name: "demo.crt" }
                - { type: "sslKeyReferences", name: "demo.key" }
              device_address: 10.1.1.7
            register: status

## License

Apache

## Author Information

This role was created in 2020 by [Romain Jouhannet](https://github.com/rjouhann).

[1]: https://galaxy.ansible.com/f5devcentral/bigiq_pinning_deploy_objects
