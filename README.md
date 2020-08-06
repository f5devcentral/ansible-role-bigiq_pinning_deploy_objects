# Ansible Role: bigiq_pinning_deploy_objects

Performs a series of steps needed to ...

- Local Traffic > Pinning Policies
- Dns > Pinning Policies
- Fraud Protection Services > Pinning Policies
- Network Security > Pinning Policies
- Shared Security > Pinning Policies

## Requirements

None.

## Role Variables

Available variables are listed below. For their default values, see `defaults/main.yml`:

    provider_server: localhost
    provider_server_port: 443
    provider_user: admin
    provider_password: secret
    provider_loginProviderName: tmos
    provider_validate_certs: false
    provider_transport: rest
    provider_timeout: 120

Establishes initial connection to your BIG-IQ. These values are substituted into
your ``provider`` module parameter. These values should be the connection parameters
for the **CM BIG-IP** device.



## Dependencies



## Example Playbook



## License

Apache

## Author Information

This role was created in 2018 by [Tim Rupp](https://github.com/caphrim007).<br/>
This role was modified in 2019 by [Greg Crosby](https://github.com/crosbygw).

[1]: https://galaxy.ansible.com/f5devcentral/bigiq_onboard
