### install nginx 

    sudo apt-get install python-software-properties
    sudo add-apt-repository ppa:nginx/stable && apt-get update
    ---
    W: GPG error: http://ppa.launchpad.net natty Release: The following
    signatures couldn't be verified because the public key is not available:
    NO_PUBKEY 00A6F0A3C300EE8C
    ---
    sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 00A6F0A3C300EE8C
    sudo apt-get install nginx

###
