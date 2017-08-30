#. In case external services (type=LoadBalancer) should be supported
     #. Create an external/provider network
     #. Create subnet/pool range of external CIDR 
     #. Connect external subnet to kuryr-kubernetes router
     #. Configure Kuryr.conf public ip subnet to point external subnet
 ::

    [neutron_defaults]
    public_ip_subnet=  external_subnet_id 
