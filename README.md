# Consul-agent

This layer handles registering connections between consul-agents and clients

## Usage

### Requires

Consul clients require information to connect to a Consul instance, so this interface provides that communication layer.

This interface layer will set the following states, as appropriate:

- ```{relation_name}.connected``` The relation has connected, but Consul may not have provided required configuration
- ```{relation_name}.available``` The Consul charm has provided required configuration

A charm can get configuration like:

```python
@when('consul.connected')
def setup(consul):
    render(
        source='config.hcl',
        target='/etc/my_charm/config.hcl',
        context={
            'address': consul.address,
            'port': consul.port
        }
    )
```