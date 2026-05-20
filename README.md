Stellar Node Runner Kit

CLI toolkit for deploying, managing, and monitoring Stellar Core and Horizon nodes.

Stellar Node Runner Kit simplifies Stellar infrastructure operations for developers, validators, and infrastructure teams. It automates setup, configuration, monitoring, and maintenance of Stellar Core and Horizon services through a single command line interface.

The goal is simple:

Run production-ready Stellar infrastructure with minimal DevOps overhead.

Features
Automated Node Setup
Install Stellar Core
Configure Horizon API
Initialize PostgreSQL database
Configure testnet or mainnet
Generate environment configuration
Docker-based deployment support
Node Lifecycle Management
Start nodes
Stop nodes
Restart services
Update Stellar Core versions
Switch networks
Reset or resync ledger state
Validator Support
Configure validator keys
Monitor validator participation
View quorum health
Track consensus activity
Monitoring and Observability
Ledger sync tracking
Peer connection monitoring
CPU and memory usage
Disk growth tracking
Error logs and alerts
Real-time node status
Developer Tooling
Stream logs directly from CLI
Export node metrics
Debugging utilities
YAML configuration system
Prebuilt environment templates
Optional API Layer
REST API for node status
Monitoring integrations
External dashboard support
Why Stellar Node Runner Kit?

Running Stellar infrastructure often requires:

manual server configuration
database setup
Horizon integration
monitoring configuration
validator tuning
infrastructure maintenance

Stellar Node Runner Kit reduces this complexity into a simple workflow.

Instead of managing multiple infrastructure components manually, developers use a single CLI interface to deploy and operate Stellar nodes.

Use Cases
Developers

Spin up local or remote Stellar nodes for:

dApp development
indexing
testing
analytics
Validators

Deploy validator-ready infrastructure with:

quorum configuration
monitoring
health checks
validator status tracking
Infrastructure Teams

Manage production-ready Stellar services with:

observability
lifecycle automation
standardized configurations
Installation
Clone Repository
git clone https://github.com/product-labo/stellar-node-runner-kit.git
cd stellar-node-runner-kit
Install Dependencies
make install
Verify Installation
snrk version
Quick Start
Initialize Testnet Node
snrk init testnet
Start Node
snrk start
Check Status
snrk status
View Logs
snrk logs
Stop Node
snrk stop
Example Commands
Network Management
snrk init mainnet
snrk switch-network testnet
snrk reset-ledger
Validator Operations
snrk validator setup
snrk validator status
snrk validator health
Monitoring
snrk monitor
snrk metrics
snrk peers
Maintenance
snrk update
snrk backup
snrk restore
Example Configuration
network: testnet

stellar_core:
  node_name: stellar-node-1
  peer_port: 11625
  http_port: 11626
  database_url: postgres://localhost/stellar

horizon:
  enabled: true
  port: 8000

validator:
  enabled: false
  secret_key: ""

monitoring:
  prometheus: true
  grafana: true
Architecture
CLI
  ↓
Configuration Layer
  ↓
Service Manager
  ├── Stellar Core
  ├── Horizon API
  ├── PostgreSQL
  └── Monitoring Stack
Roadmap
v0.1.0
CLI foundation
Stellar Core installer
Horizon setup
YAML configuration
Node lifecycle commands
v0.2.0
Validator tooling
Monitoring stack
Metrics collection
Log streaming
v0.3.0
Web dashboard
REST API
Alerting system
Performance analytics
Future
Kubernetes deployment
Cloud presets
Automated snapshots
Multi-node orchestration
Remote infrastructure management
Tech Stack
Go
Cobra CLI
Docker
PostgreSQL
Prometheus
Grafana
Project Goals
Lower the barrier to running Stellar nodes
Improve Stellar infrastructure decentralization
Simplify validator onboarding
Improve infrastructure observability
Help developers deploy Stellar services faster
Contributing

Contributions are welcome.

Areas where help is needed:

CLI improvements
Monitoring integrations
Validator tooling
Documentation
Testing
Deployment automation

See CONTRIBUTING.md for contribution guidelines.

License

MIT License

Status

Early development phase.

APIs, commands, and architecture may change before stable release.
