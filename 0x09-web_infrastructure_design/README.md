# Task 0. Simple web stack

## Infrastructure Specifics:

1. **Server:**
   - A server is a computer or system that manages network resources and provides services to clients.
   - In web hosting, it stores and serves website files, responding to user requests.

2. **Domain Name:**
   - A domain name is a human-readable address representing the IP of a server on the internet.
   - Provides a user-friendly way to access websites.

3. **DNS Record (www):**
   - The www in www.foobar.com is a subdomain and a type of DNS record.
   - Often used to specify the 'www' subdomain for website hosting.

4. **Web Server:**
   - Software handling HTTP requests and serving static content (HTML, CSS, images) to browsers.

5. **Application Server:**
   - Executes application logic, processes business rules, and generates dynamic content.

6. **Database:**
   - Stores and manages structured data needed for the application.

7. **Communication with User's Computer:**
   - Server communicates with the user's computer through HTTP or HTTPS protocols.
   - Sends HTML, CSS, JavaScript, and other resources to render web pages.

## Infrastructure Issues:

1. **Single Point of Failure (SPOF):**
   - Occurs when a component failure causes the entire system to fail.
   - Example: Main server failure making the entire website inaccessible.

2. **Downtime during Maintenance:**
   - Maintenance activities (e.g., deploying new code) may cause website downtime.
   - Users unable to access the site during maintenance.

3. **Scalability Challenges:**
   - Infrastructure struggles to handle sudden increases in incoming traffic.
   - May result in slow performance or crashes during high demand.

## Mitigation Strategies:

- **Redundancy and Load Balancing:**
  - Implement redundancy for critical components to mitigate SPOF.
  - Use load balancing to distribute traffic across multiple servers.

- **Efficient Scaling:**
  - Design infrastructure to scale horizontally to handle increased traffic.
  - Adopt cloud services for dynamic scaling based on demand.

- **Rolling Deployments:**
  - Minimize downtime during maintenance by using rolling deployments.
  - Gradually update servers without taking the entire system offline.

## Conclusion:

Addressing SPOF, downtime, and scalability challenges involves strategic planning, redundancy measures, and efficient scaling mechanisms. Consider adopting best practices to ensure a reliable and seamless user experience.

# Task 1. Distributed web infrastructure

## Additional Elements and Their Purpose:

1. **Load Balancer:**
   - **Purpose:** To distribute incoming traffic across multiple servers, ensuring optimal resource utilization and preventing overloading of a single server.
   - **Distribution Algorithm:** [Specify the algorithm, e.g., Round Robin, Least Connections, etc.]
   - **Setup:** [Specify whether it's Active-Active or Active-Passive]

2. **Database Primary-Replica Cluster:**
   - **Purpose:** To enhance data availability, improve read performance, and provide failover capabilities.
   - **How It Works:** The Primary node receives write operations and replicates data to Replica nodes, which handle read operations.
   - **Difference (Application):** The application interacts with the Primary node for write operations and with Replica nodes for read operations.

## Load Balancer Configuration:

- **Distribution Algorithm:**
  - [Specify the chosen algorithm and explain its functionality, e.g., Round Robin distributes requests evenly.]

- **Active-Active vs. Active-Passive:**
  - **Active-Active Setup:**
    - All servers actively handle incoming requests simultaneously.
    - Provides load distribution and redundancy.
  - **Active-Passive Setup:**
    - One server (active) handles requests while the others (passive) remain on standby.
    - Offers redundancy with less resource utilization.

## Database Primary-Replica Cluster:

- **How It Works:**
  - The Primary node receives write operations and replicates data to Replica nodes.
  - Replica nodes handle read operations, distributing the read load.

- **Difference (Application):**
  - The application interacts with the Primary node for write operations (e.g., updating data).
  - The application interacts with Replica nodes for read operations (e.g., fetching data for display).

## Infrastructure Issues:

1. **Single Point of Failure (SPOF):**
   - Identify and address any components that, if they fail, will disrupt the entire system.

2. **Security Issues:**
   - **No Firewall:**
     - Implementing a firewall is crucial for controlling and monitoring incoming and outgoing network traffic.
   - **No HTTPS:**
     - Enabling HTTPS ensures secure communication between users and the web servers, preventing data interception.

3. **No Monitoring:**
   - Lack of monitoring tools prevents proactive issue detection and resolution.
   - Implement monitoring solutions to track performance, identify bottlenecks, and ensure system health.

## Conclusion:

Addressing SPOF, enhancing security through firewalls and HTTPS, and implementing robust monitoring are crucial for maintaining a secure, reliable, and performant infrastructure.

# Task 2. Secured and monitored web infrastructure mandatory


## Additional Elements and Their Purpose:

1. **Load Balancer:**
   - **Purpose:** To distribute incoming traffic across multiple servers, ensuring optimal resource utilization and preventing overloading of a single server.
   - **Distribution Algorithm:** [Specify the algorithm, e.g., Round Robin, Least Connections, etc.]
   - **Setup:** [Specify whether it's Active-Active or Active-Passive]

2. **Database Primary-Replica Cluster:**
   - **Purpose:** To enhance data availability, improve read performance, and provide failover capabilities.
   - **How It Works:** The Primary node receives write operations and replicates data to Replica nodes, which handle read operations.
   - **Difference (Application):** The application interacts with the Primary node for write operations and with Replica nodes for read operations.

3. **Load Balancer Security:**
   - **Firewalls (3):**
     - Implemented to control and monitor incoming and outgoing network traffic.
     - Enhances security by filtering and blocking unauthorized access.

4. **SSL Certificate:**
   - **Purpose:** To enable HTTPS and secure communication between users and the web servers.
   - **Implementation:** [Specify SSL certificate provider and configuration details.]

5. **Monitoring:**
   - **Monitoring Clients (3):**
     - Serve as data collectors for monitoring services (e.g., Sumo Logic).
     - Collect and analyze data to ensure system health, identify bottlenecks, and enable proactive issue detection.

## Load Balancer Configuration:

- **Distribution Algorithm:**
  - [Specify the chosen algorithm and explain its functionality, e.g., Round Robin distributes requests evenly.]

- **Active-Active vs. Active-Passive:**
  - **Active-Active Setup:**
    - All servers actively handle incoming requests simultaneously.
    - Provides load distribution and redundancy.
  - **Active-Passive Setup:**
    - One server (active) handles requests while the others (passive) remain on standby.
    - Offers redundancy with less resource utilization.

## Database Primary-Replica Cluster:

- **How It Works:**
  - The Primary node receives write operations and replicates data to Replica nodes.
  - Replica nodes handle read operations, distributing the read load.

- **Difference (Application):**
  - The application interacts with the Primary node for write operations (e.g., updating data).
  - The application interacts with Replica nodes for read operations (e.g., fetching data for display).

## Infrastructure Issues:

1. **Terminating SSL at Load Balancer Level:**
   - **Issue:** This prevents end-to-end encryption. Decrypting at the load balancer means traffic between the load balancer and backend servers is unencrypted.
   - **Recommendation:** Implement end-to-end encryption by terminating SSL at the web servers.

2. **Single MySQL Server Accepting Writes:**
   - **Issue:** A single point of failure for write operations. If the MySQL server fails, write operations cannot be performed.
   - **Recommendation:** Implement a more resilient setup with multiple MySQL servers capable of handling write operations.

3. **Identical Components Across Servers:**
   - **Issue:** Homogeneous components pose a risk. If a common issue arises, it affects all servers simultaneously.
   - **Recommendation:** Consider introducing diversity in components or implement rolling updates to minimize potential widespread issues.

## Security Enhancements:

1. **Firewalls:**
   - **Purpose:** To control and monitor incoming and outgoing network traffic.
   - **Implementation:** Configure firewalls to allow only necessary traffic, blocking unauthorized access.

2. **SSL Certificate:**
   - **Why HTTPS:**
     - Ensures secure communication between users and the web servers.
     - Encrypts data in transit, preventing unauthorized access or tampering.

## Monitoring and Data Collection:

1. **Monitoring:**
   - **Purpose:** To ensure system health, identify bottlenecks, and enable proactive issue detection.
   - **Data Collection:** Monitoring clients serve as data collectors for services like Sumo Logic, collecting and analyzing relevant data.

2. **Monitoring Web Server QPS:**
   - **Procedure:**
     - Configure monitoring tools to track the Query Per Second (QPS) metric for the web server.
     - Set up alerts for threshold breaches to be notified of potential performance issues.

## Conclusion:

Enhancing security with firewalls and SSL, implementing diverse components, and employing robust monitoring practices contribute to a secure, reliable, and performant infrastructure.

# task 3. Scale up

## Infrastructure Overview:

1. **Load Balancer Cluster:**
   - **Purpose:** To distribute incoming traffic across multiple servers, ensuring optimal resource utilization and preventing overloading of a single server.
   - **HAProxy Configuration:** Set up as a cluster with failover capabilities, enhancing availability and reliability.

2. **Server (HAProxy Cluster Node):**
   - **Purpose:** Adds redundancy and fault tolerance to the load balancer setup.
   - **Configuration:** Configured as an additional node in the HAProxy cluster.

3. **Web Server:**
   - **Purpose:** To handle the presentation layer, serving static content (HTML, CSS, images) to users' browsers.
   - **Configuration:** Separated from the application server for better resource allocation and scalability.

4. **Application Server:**
   - **Purpose:** To execute application logic, process business rules, and generate dynamic content.
   - **Configuration:** Decoupled from the web server for improved modularity and scalability.

5. **Database Server:**
   - **Purpose:** To store and manage structured data required for the application.
   - **Configuration:** Separated from other components for better security, scalability, and maintainability.

## Load Balancer Configuration:

- **Distribution Algorithm:**
  - [Specify the chosen algorithm, e.g., Round Robin, Least Connections, etc.]
  - **Cluster Configuration:** Load balancer configured as a cluster for high availability and failover.

- **Active-Active vs. Active-Passive:**
  - **Active-Active Setup:**
    - All servers actively handle incoming requests simultaneously.
    - Provides load distribution and redundancy.
  - **Active-Passive Setup:**
    - One server (active) handles requests while the others (passive) remain on standby.
    - Offers redundancy with less resource utilization.

## Database Primary-Replica Cluster:

- **How It Works:**
  - The Primary node receives write operations and replicates data to Replica nodes.
  - Replica nodes handle read operations, distributing the read load.

- **Difference (Application):**
  - The application interacts with the Primary node for write operations (e.g., updating data).
  - The application interacts with Replica nodes for read operations (e.g., fetching data for display).

## Additional Server and Load Balancer Node:

- **Server (HAProxy Cluster Node):**
  - **Purpose:** Adds redundancy and fault tolerance to the load balancer setup.
  - **Configuration:** Added as an additional node to the HAProxy cluster for improved reliability.

## Infrastructure Issues:

1. **Terminating SSL at Load Balancer Level:**
   - **Issue:** This prevents end-to-end encryption. Decrypting at the load balancer means traffic between the load balancer and backend servers is unencrypted.
   - **Recommendation:** Implement end-to-end encryption by terminating SSL at the web servers.

2. **Single MySQL Server Accepting Writes:**
   - **Issue:** A single point of failure for write operations. If the MySQL server fails, write operations cannot be performed.
   - **Recommendation:** Implement a more resilient setup with multiple MySQL servers capable of handling write operations.

3. **Identical Components Across Servers:**
   - **Issue:** Homogeneous components pose a risk. If a common issue arises, it affects all servers simultaneously.
   - **Recommendation:** Consider introducing diversity in components or implement rolling updates to minimize potential widespread issues.

## Security Enhancements:

1. **Firewalls:**
   - **Purpose:** To control and monitor incoming and outgoing network traffic.
   - **Implementation:** Configure firewalls to allow only necessary traffic, blocking unauthorized access.

2. **SSL Certificate:**
   - **Why HTTPS:**
     - Ensures secure communication between users and the web servers.
     - Encrypts data in transit, preventing unauthorized access or tampering.

## Monitoring and Data Collection:

1. **Monitoring:**
   - **Purpose:** To ensure system health, identify bottlenecks, and enable proactive issue detection.
   - **Data Collection:** Monitoring clients serve as data collectors for services like Sumo Logic, collecting and analyzing relevant data.

2. **Monitoring Web Server QPS:**
   - **Procedure:**
     - Configure monitoring tools to track the Query Per Second (QPS) metric for the web server.
     - Set up alerts for threshold breaches to be notified of potential performance issues.

## Conclusion:

Enhancing security with firewalls and SSL, implementing diverse components, employing robust monitoring practices, and adding additional nodes to the load balancer cluster contribute to a secure, reliable, and performant infrastructure.
