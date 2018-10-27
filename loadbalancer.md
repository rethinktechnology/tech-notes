# Load Balancer

**What is load balancing?** 
Load balancing is the process of distributing network traffic across multiple servers. This ensures no single server bears too much demand. By spreading the work evenly, load balancing improves application responsiveness. It also increases availability of applications and websites for users.

**What is load balancer?**
Load balancers manage the flow of information between the server and an endpoint device (PC, laptop, tablet or smartphone). 
The server could be on-premises, in a data center or the public cloud. The server can also be physical or virtualized. The load balancer helps servers move data efficiently, optimizes the use of application delivery resources and prevents server overloads. 
Load balancers conduct continuous health checks on servers to ensure they can handle requests. 
If necessary, the load balancer removes unhealthy servers from the pool until they are restored. Some load balancers even trigger the creation of new virtualized application servers to cope with increased demand.

Traditionally, load balancers consist of a hardware appliance. Yet they are increasingly becoming software-defined. This is why load balancers are an essential part of an organization’s digital strategy.

## Load balancing & SSL

Secure Sockets Layer (SSL) is the standard security technology for establishing an encrypted link between a web server and a browser. SSL traffic is often decrypted at the load balancer. When a load balancer decrypts traffic before passing the request on, it is called **SSL termination**. The load balancer saves the web servers from having to expend the extra CPU cycles required for decryption. This improves application performance.

However, SSL termination comes with a security concern. The traffic between the load balancers and the web servers is no longer encrypted. This can expose the application to possible attack. However, <i>the risk is lessened when the load balancer is within the same data center as the web servers</i>.

Another solution is the **SSL pass-through**. The load balancer merely passes an encrypted request to the web server. Then the web server does the decryption. This uses more CPU power on the web server. But organizations that require extra security may find the extra overhead worthwhile.


## Load balancing Algorithms

There is a variety of load balancing methods, which use different algorithms best suited for a particular situation.

-   Least Connection Method 
	> directs traffic to the server with the fewest active connections. Most useful when there are a large number of persistent connections in the traffic unevenly distributed between the servers.
-   Least Response Time Method 
	> directs traffic to the server with the fewest active connections and the lowest average response time.
-   Round Robin Method 
	> rotates servers by directing traffic to the first available server and then moves that server to the bottom of the queue. Most useful when servers are of equal specification and there are not many persistent connections.
-   IP Hash 
	> the IP address of the client determines which server receives the request.



## Load Balancing Benefits

Load balancing can do more than just act as a network traffic cop. Smart load balancers provide benefits like **predictive analytics** that determine traffic bottlenecks before they happen. As a result, the smart load balancer gives an organization actionable insights. These are key to automation and can help drive business decisions.

In the seven-layer **Open System Interconnection (OSI) model**, network firewalls are at levels one to three (L1-Physical Wiring, L2-Data Link and L3-Network). Meanwhile, load balancing happens between layers four to seven (L4-Transport, L5-Session, L6-Presentation and L7-Application).

Load balancers have different capabilities, which include:

-   L4 — directs traffic based on data from network and transport layer protocols, such as IP address and TCP port.
-   L7 — adds content switching to load balancing. This allows routing decisions based on attributes like HTTP header, uniform resource identifier, SSL session ID and HTML form data.
-   GSLB — Global Server Load Balancing extends L4 and L7 capabilities to servers in different geographic locations.

More enterprises are seeking to deploy cloud-native applications in data centers and public clouds. This is leading to significant changes in the capability of load balancers. In turn, this creates both challenges and opportunities for infrastructure and operations leaders.
