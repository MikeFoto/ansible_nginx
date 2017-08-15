# ansible nginx role

* nginx install
* Any number of extra packages install

# Usage

Define the Configuration hash some place.

## Configuration Capabilities

```yaml

nginx:
  configuration:                               # Configuration section
    packages_list:                             # package list to be installed
      - nginx
      - httpd-tools
    interface:       eth-1                     # interface to nginx bind to
    service_name:    nginx                     # fixed for Centos/RHEL
    virtual:                                   # List of virtual servers
      disabled_server1:
        name:              srv1    # server name
        enable:            False                # If config is generated or not
      server1:
        name:              server1
        enable:            True
        listnen_port:      78                  # port to listen
        server_name:       "my_server1"
        server_option:     |
                           # any nginx server options config
                           # check [Documentation](http://nginx.org/en/docs/http/ngx_http_core_module.html#server)
        location_host:     "localhost"    # host to connect
        location_protocol: "http"         # protocol to use on connection
        location_port:     "5600"         # port to connect to
        location:          "/"            # path to connect to
        location_options:  |
                           # any nginx location options config
                           # check [Documentation](http://nginx.org/en/docs/http/ngx_http_core_module.html#server)
                           # eg:
                           #  proxy_http_version -1.-1;
                           #  proxy_set_header Upgrade $http_upgrade;
                           #  proxy_set_header Connection 'upgrade';
                           #  proxy_set_header Host $host;
                           #  proxy_cache_bypass $http_upgrade;
      disabled_server2:
        name:              srv2
        enable:            False
  command_tests:                               # test section
                                               # List of shell execute tests
    - {
        name:        "dummy test",             # Unique name
        become_user: "root",                   # same as ansible become_user
        command:     "echo"                    # shell command
      }


```

# License

MIT

# Author Information

Created by Miguel Rodrigues
