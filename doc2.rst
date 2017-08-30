
#. In case external services (type=LoadBalancer) should be supported

   A. Create an external/provider network
   B. Create subnet/pool range of external CIDR 
   C. Connect external subnet to kuryr-kubernetes router
   D. Configure Kuryr.conf public ip subnet to point external subnet
   
   ::[neutron_defaults]
     public_ip_subnet=  external_subnet_id 


Alternative configuration
~~~~~~~~~~~~~~~~~~~~~~~~~
It is actually possible to avoid this routing by performing a deployment change
that was successfully pioneered by the people at EasyStack Inc. which consists
