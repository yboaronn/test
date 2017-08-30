
#. Configure kuryr.conf pod subnet and service subnet to point to the same
   subnet created in step (1)::

    [neutron_defaults]
    pod_subnet = e0a888ab-9915-4685-a600-bffe240dc58b
    service_subnet = d6438a81-22fa-4a88-9b05-c4723662ef36

#. In case external services (type=LoadBalancer) should be supported
     Create an external/provider network
     Create subnet/pool range of external CIDR 
     Connect external subnet to kuryr-kubernetes router
     Configure Kuryr.conf public ip subnet to point external subnet::
     
     
     [neutron_defaults]
     public_ip_subnet=  external_subnet_id 
 
#. Configure Kubernetes API server to use only a subset of the service
   addresses, **10.2.0.0/17**. The rest will be used for loadbalancer *vrrp*
   ports managed by Octavia. To configure Kubernetes with this CIDR range you
   have to add the following parameter to its command line invocation::

    --service-cluster-ip-range=10.2.0.0/17

   As a result of this, Kubernetes will allocate the **10.2.0.1** address to the
   Kubernetes API service, i.e., the service used for pods to talk to the
   Kubernetes API server. It will be able to allocate service addresses up until
   **10.2.127.254**. The rest of the addresses, as stated above, will be for
   Octavia load balancer *vrrp* ports. **If this subnetting was not done,
   Octavia would allocate *vrrp* ports with the Neutron IPAM from the same range
   as Kubernetes service IPAM and we'd end up with conflicts**.
