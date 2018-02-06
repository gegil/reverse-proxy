Reverse proxy and load balancing with HAproxy
---------------------------------------------

The goal: to have one or more server to handle a web application. The servers will be managed by load balancing mechanism provided by HAproxy application.
The servers will be accessible by the user, they will be behind a proxy server that will present communicate the requests from the user to the servers. And at the same time the reverse proxy domain name will have an SSL certificate attached to it for secure communication (info below).

The HAproxy application will be installed on the main server which will communicate with the back-end web servers. The back-end servers are not accessible to anyone beside the main server.

HAproxy support virtual hosts; using the configuration file, the administrator can add additional domains including subdomains (with the same SLD - second-level domain).

With HAproxy also provide the option to use several domains and subdomains with the same IP. HAproxy will strip the full domain name from the HTTP\S header and communicate with the configured backend servers.
This will have the load balancer share the resources of the servers linked to the full domain name.

The communication between the HAproxy server and the backend servers is http based. While the communication between the end user and the HAproxy server is https based. Using the mentioned SSL certificate.

Since each domain name or require its own certificate. To ensure that HAproxy can access the certificates for all domains, the certificated need to reside in the same folder. 
Which is different from the single domain configuration that required a certificate full path.
 




The SSL certificate is provided by let’s encrypt (https://letsencrypt.org) 
SSL automation and installation can use the project getssl project from - https://github.com/srvrco/getssl/blob/master/getssl

The SSL domain verification process include a local key file installation and key verification thru http to the domain.

getssl script download:
curl --silent https://raw.githubusercontent.com/srvrco/getssl/master/getssl > getssl ; chmod 700 getssl

getssl script execution:
./getssl -c example.com

