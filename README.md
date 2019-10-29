# How I Set Things Up

- Used `bosh-deployment` to set up a Virtualbox-based BOSH environment.
- Used the `manifests/nginx-lite.yml` from the nginx-release repo as a starting point
- Setting up the network was a bit annoying as the BOSH documentation is a little confusing
    - I had to manually add a route to allow access to BOSH-created VMs.
    - `sudo route add -net 10.244.0.0/16     192.168.50.6`

# Testing Things Out

I wasn't able to figure out how to get just the IP to print out for the nginx VM, so here is a little curl command that retrieves the IP from the output of the `bosh vms` command:

    curl `bosh vms -d nginx | grep 'running' | tr '\t' ' ' | cut -d\  -f4`
