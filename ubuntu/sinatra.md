### sinatra settings

* :bind - server hostname or IP address

String specifying the hostname or IP address of the interface to listen on when the :run setting is enabled. The default value in the development environment is 'localhost' which means the server is only available from the local machine. In other environments the default is '0.0.0.0', which causes the server to listen on all available interfaces.

To listen on all interfaces in the development environment (for example if you want to test from other computers in your local network) use:

    set :bind, '0.0.0.0'

This can also be set from the command line with the -o option. If you set the bind option in your application it will override anything set on the command line.

* :port - server port

The port that should be used when starting the built-in web server when the :run setting is enabled. The default port is 4567. To set the port explicitly:

    set :port, 9494


<http://www.sinatrarb.com/configuration.html>
