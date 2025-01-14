# Awesome Software Architecture Resources 📚

A curated collection of awesome articles, videos, patterns, and principles for learning and practicing software architecture across different domains.

## Table of Contents
- [Blockchain Architecture](#blockchain-architecture)
- [AI/ML Systems](#aiml-systems)
- [E-Commerce](#e-commerce)
- [Cloud Native](#cloud-native)
- [FinTech](#fintech)
  - [Global Payment Processing System](#global-payment-processing-system)
- [Social Media Platforms](#social-media-platforms)

---

## FinTech

### Global Payment Processing System

#### Overview
This section explores the architecture of a **Global Payment Processing System**, inspired by PayPal. The system is designed to handle high transaction volumes, serve both merchants and consumers worldwide, and support features like one-time payments, recurring payments, refunds, and dispute resolutions.

#### Key Requirements
- **Functional Requirements**:
  - Support for one-time payments, recurring payments, refunds, and dispute resolutions.
  - Multi-currency support with real-time exchange rates.
- **Non-Functional Requirements**:
  - High reliability (99.99% uptime).
  - Scalability to handle thousands of transactions per second.
  - Low latency and top-notch security.
  - Compliance with international regulations like PCI DSS and KYC.

#### Architecture Layers
1. **Client Layer**:
   - Interfaces for users to interact with the system via:
     - Web applications (e.g., account management, payment initiation).
     - Mobile applications (iOS/Android for payments, balance checks).
     - APIs for third-party integrations (e.g., merchants embedding payment systems).

2. **Service Layer**:
   - Core business logic implemented using microservices:
     - **User Service**: Handles user authentication and profile management.
     - **Payment Service**: Processes payments, interacts with external gateways, and manages currency conversions.
     - **Account Service**: Tracks user balances and ensures integrity during transactions.
     - **Fraud Detection Service**: Monitors transactions in real-time using machine learning models.
     - **Notification Service**: Sends transaction updates via email, SMS, or push notifications.
   - Communication between services is asynchronous using message brokers like Kafka.

3. **Data Layer**:
   - **Relational Databases** (e.g., PostgreSQL): For transactional data ensuring ACID compliance.
   - **NoSQL Databases** (e.g., Cassandra, MongoDB): For session data, logs, and high-throughput operations.
   - **Caching** (e.g., Redis): For frequently accessed data to reduce latency.

#### Key Components
- **Payment Gateway**:
  - Acts as the entry point for payment requests.
  - Handles encryption, authorization, and fraud detection.
  - Example: Amazon API Gateway.
- **Payment Processor**:
  - Communicates with card networks (e.g., Visa, Mastercard) and banks to validate and settle transactions.
  - Ensures compliance with distributed transactions and manages retries.

#### Patterns and Practices
- **Microservices Architecture**:
  - Each service owns its database to ensure loose coupling and data independence.
  - Services communicate via Kafka topics for decoupling and asynchronous processing.
- **Database Optimization**:
  - Horizontal partitioning (sharding) based on user IDs or regions.
  - Read replicas for improved performance and redundancy.
  - Indexing frequently queried fields.
- **Caching**:
  - Redis for session data and frequently accessed information.
- **Security**:
  - TLS for data in transit and encryption for data at rest.
  - Multi-factor authentication and role-based access control (RBAC).
- **Fraud Detection**:
  - Real-time monitoring using machine learning models.
  - Flagging suspicious transactions and triggering additional verification steps.
- **Resilience Patterns**:
  - **Circuit Breaker**: Prevents overloading external services during failures.
  - **Idempotency Keys**: Ensures no duplicate transactions during retries.
  - **Saga Pattern**: Manages distributed transactions with compensating actions for failures.

#### Transaction Flow
1. **Login**:
   - User sends credentials to the API Gateway.
   - User Service validates credentials and generates a JWT token.
   - Session data is cached in Redis for fast future access.
2. **Payment Initiation**:
   - User sends payment details to the API Gateway.
   - Payment Service verifies account balance and locks the amount.
   - Interacts with external payment gateways (e.g., Visa) for authorization.
   - Updates transaction status and notifies the user.
3. **Fraud Detection**:
   - Fraud Detection Service analyzes transactions in real-time.
   - Flags suspicious activities and triggers additional verification if needed.
4. **Notification**:
   - Notification Service sends confirmation messages asynchronously.

#### Scaling Strategies
- **Horizontal Scaling**:
  - Microservices scale independently based on demand.
- **Load Balancing**:
  - Distributes traffic across multiple servers for high availability.
- **Asynchronous Processing**:
  - Offloads non-critical tasks to message queues for faster response times.
- **Database Optimization**:
  - Partitioning, sharding, and read replicas for handling large datasets.

#### Tools and Technologies
- **Message Brokers**: Kafka, RabbitMQ.
- **Databases**: PostgreSQL, Cassandra, MongoDB.
- **Caching**: Redis.
- **API Gateway**: Amazon API Gateway.
- **Security**: TLS, RBAC, Multi-factor authentication.

---
## Networking Protocols

### Overview
This section provides a comprehensive overview of **Networking Protocols** that are essential for understanding how data moves across networks, ensuring security, reliability, and scalability. These protocols are critical for building robust systems and are widely used in various domains, including cloud computing, IoT, and enterprise systems.

### Key Protocols and Their Roles (with Examples)
1. **HTTP/HTTPS**:
   - **Role**: HTTP is like sending postcards (unencrypted), while HTTPS encrypts data for secure communication.
   - **Example**: HTTPS is essential for websites handling sensitive information, such as online banking or e-commerce platforms like Amazon.

2. **TCP/IP**:
   - **Role**: TCP ensures reliable data delivery, while IP provides the address for routing.
   - **Example**: TCP/IP is the foundation of the internet, used in everything from web browsing to email communication.

3. **UDP**:
   - **Role**: A faster, less reliable protocol used for live streams and gaming.
   - **Example**: Online gaming platforms like Fortnite or live video streaming services like Twitch use UDP for low-latency communication.

4. **DNS**:
   - **Role**: The internet's phonebook, translating domain names to IP addresses.
   - **Example**: When you type "google.com" into your browser, DNS resolves it to Google's IP address. Vulnerable to DNS spoofing attacks.

5. **FTP/SFTP**:
   - **Role**: File transfer protocols, with SFTP offering encryption for secure file transfers.
   - **Example**: FTP is used for transferring files to web servers, while SFTP is preferred for secure file uploads in enterprise environments.

6. **SSH**:
   - **Role**: Secure remote login protocol, creating encrypted tunnels for secure communication.
   - **Example**: System administrators use SSH to securely access remote servers for maintenance and troubleshooting.

7. **Email Protocols (SMTP, POP3, IMAP)**:
   - **Role**: Handle sending and receiving emails.
   - **Example**: Gmail uses IMAP for syncing emails across devices, while SMTP is used to send emails.

8. **SNMP**:
   - **Role**: Monitors network devices.
   - **Example**: Used by IT teams to monitor routers, switches, and servers for performance and faults.

9. **ICMP**:
   - **Role**: Used for diagnostics (e.g., ping), but can be exploited for network mapping.
   - **Example**: The `ping` command uses ICMP to check if a server is reachable.

10. **ARP/DHCP**:
    - **Role**: Handle address resolution and IP assignment.
    - **Example**: ARP resolves IP addresses to MAC addresses in local networks, while DHCP assigns IP addresses to devices when they connect to a network.

### Advanced Protocols (with Examples)
1. **SSL/TLS**:
   - **Role**: Encrypts web traffic.
   - **Example**: Online shopping websites like eBay use TLS to secure payment information.

2. **Telnet/RDP**:
   - **Role**: Remote access protocols, with Telnet being insecure compared to SSH.
   - **Example**: RDP is used by IT support teams to remotely troubleshoot user systems.

3. **SMB/CIFS**:
   - **Role**: File-sharing protocols, often targeted for data theft.
   - **Example**: SMB is used in Windows networks for sharing files and printers.

4. **NTP**:
   - **Role**: Synchronizes network clocks.
   - **Example**: Used in financial systems to ensure accurate timestamps for transactions.

5. **SIP**:
   - **Role**: Manages VoIP calls.
   - **Example**: SIP is used in services like Zoom or Microsoft Teams for setting up voice and video calls.

6. **Kerberos**:
   - **Role**: A secure authentication protocol using tickets.
   - **Example**: Used in enterprise environments for single sign-on (SSO) systems.

7. **MQTT/Modbus**:
   - **Role**: Used in IoT and industrial systems.
   - **Example**: MQTT is used in smart home devices like Amazon Echo, while Modbus is used in factory automation.

8. **BGP**:
   - **Role**: Routes internet traffic.
   - **Example**: BGP is critical for ISPs to manage internet traffic between different networks.

9. **IPSec**:
   - **Role**: Secures IP packets with encryption and authentication.
   - **Example**: Used in VPNs to secure communication between remote users and corporate networks.

### Patterns and Practices
- **Resilience Patterns**:
  - **Circuit Breaker**: Prevents overloading external services during failures.
  - **Idempotency Keys**: Ensures no duplicate transactions during retries.
  - **Saga Pattern**: Manages distributed transactions with compensating actions for failures.
- **Security**:
  - TLS for data in transit and encryption for data at rest.
  - Multi-factor authentication and role-based access control (RBAC).
- **Caching**:
  - Redis for session data and frequently accessed information.

### Tools and Technologies
- **Message Brokers**: Kafka, RabbitMQ.
- **Databases**: PostgreSQL, Cassandra, MongoDB.
- **Caching**: Redis.
- **API Gateway**: Amazon API Gateway.
- **Security**: TLS, RBAC, Multi-factor authentication.

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct and the process for submitting pull requests.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

---

> 🚀 This repository is continuously updated. Star it to stay updated with new resources!
