# How I Set Things Up

- Used `bosh-deployment` to set up a Virtualbox-based BOSH environment.
- Used the `manifests/nginx-lite.yml` from the nginx-release repo as a starting point
- Setting up the network was a bit annoying as the BOSH documentation is a little confusing
    - I had to manually add a route to allow access to BOSH-created VMs.
    - `sudo route add -net 10.244.0.0/16     192.168.50.6`

# Testing Things Out

I wasn't able to figure out how to get just the IP to print out for the nginx VM, so here is a little curl command that retrieves the IP from the output of the `bosh vms` command:

    $ curl `bosh vms -d nginx | grep 'running' | tr '\t' ' ' | cut -d\  -f4`

Unauthorized access to web server:

    $ curl  `bosh vms -d nginx | grep 'running' | tr '\t' ' ' | cut -d\  -f4`
    <html>
    <head><title>401 Authorization Required</title></head>
    <body>
    <center><h1>401 Authorization Required</h1></center>
    <hr><center>nginx/1.17.0</center>
    </body>
    </html>

Authorized access:

    $ curl --user user:password `bosh vms -d nginx | grep 'running' | tr '\t' ' ' | cut -d\  -f4`
    <html><head><title>BOSH on IPv6</title>
    </head><body>
    <h2>Welcome to BOSH's nginx Release</h2>
    <h2>
    My hostname/IP: <b>10.244.0.2</b><br />
    Your IP: <b>192.168.50.1</b>
    </h2>
    </body></html>
