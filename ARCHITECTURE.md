# Stellar Node Runner Kit - Architecture

## Overview
Stellar Node Runner Kit is a modular CLI-based infrastructure toolkit designed to simplify Stellar Core node deployment, management, and monitoring.

## High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│              CLI Interface Layer                             │
│  (Commands, Arguments, User Interaction)                    │
└─────────────────────────────────────────────────────────────┘
                            │
        ┌───────────────────┼───────────────────┐
        │                   │                   │
┌───────▼──────────┐ ┌─────▼──────────┐ ┌─────▼──────────┐
│  Core Engine     │ │  Config System │ │  Monitoring   │
│  - Setup         │ │  - YAML Parser │ │  - Metrics    │
│  - Lifecycle     │ │  - Templates   │ │  - Logging    │
│  - Validation    │ │  - Presets     │ │  - Alerts     │
└───────┬──────────┘ └─────┬──────────┘ └─────┬──────────┘
        │                   │                   │
        └───────────────────┼───────────────────┘
                            │
        ┌───────────────────┼───────────────────┐
        │                   │                   │
┌───────▼──────────┐ ┌─────▼──────────┐ ┌─────▼──────────┐
│ Stellar Core     │ │ Horizon API    │ │ Storage Layer  │
│ Integration      │ │ Integration    │ │ - Database     │
│                  │ │                │ │ - Ledger Cache │
└────────────────┘ └────────────────┘ └────────────────┘
```

## Core Components

### 1. CLI Interface Layer
- Command dispatcher and routing
- Argument parsing and validation
- User feedback and error handling
- Help documentation system

### 2. Core Engine
**Setup Module**
- Stellar Core installation
- Horizon API installation
- Network initialization (testnet/mainnet)
- Database initialization
- Configuration bootstrap

**Lifecycle Management Module**
- Start/stop/restart node
- Version updates
- Network switching
- Ledger reset/resync
- Service health checks

**Validator Module**
- Validator key configuration
- Validator registration
- Quorum set management
- Validation status tracking
- Consensus participation monitoring

### 3. Configuration System
- YAML/JSON configuration parsing
- Template engine for prebuilt configs
- Environment preset management
- Secrets/key management integration
- Configuration validation and defaults

### 4. Monitoring & Observability
**Metrics Collection**
- Ledger sync progress
- Transaction throughput
- Peer connections
- Node latency
- Resource usage (CPU, memory, disk)

**Logging System**
- Event logging
- Error logging
- Debug output streaming
- Log rotation and archival

**Alert System**
- Downtime detection
- Lag threshold alerts
- Resource exhaustion alerts
- Health status notifications

### 5. Storage Layer
- Database abstraction
- Ledger data caching
- State persistence
- Backup/restore functionality

### 6. External Integrations
- Stellar Core API wrapper
- Horizon API wrapper
- System command execution
- File I/O operations

## Directory Structure

```
stellar-node-runner-kit/
├── cmd/                          # CLI entry point
│   └── main.go                  # Application entry point
├── internal/                      # Private application code
│   ├── cli/                      # CLI command handlers
│   │   ├── setup.go             # Setup commands
│   │   ├── lifecycle.go         # Start/stop/restart commands
│   │   ├── validator.go         # Validator configuration
│   │   └── monitor.go           # Monitoring commands
│   ├── core/                     # Core business logic
│   │   ├── engine.go            # Main engine
│   │   ├── installer.go         # Installation logic
│   │   ├── manager.go           # Lifecycle management
│   │   └── validator.go         # Validator logic
│   ├── config/                   # Configuration system
│   │   ├── parser.go            # Config parsing
│   │   ├── templates.go         # Config templates
│   │   ├── presets.go           # Environment presets
│   │   └── validation.go        # Config validation
│   ├── monitor/                  # Monitoring system
│   │   ├── metrics.go           # Metrics collection
│   │   ├── logger.go            # Logging system
│   │   ├── alerts.go            # Alert system
│   │   └── dashboard.go         # Dashboard/UI
│   ├── storage/                  # Storage abstraction
│   │   ├── database.go          # Database operations
│   │   ├── ledger.go            # Ledger operations
│   │   └── backup.go            # Backup/restore
│   ├── stellar/                  # Stellar integrations
│   │   ├── core.go              # Stellar Core API
│   │   └── horizon.go           # Horizon API
│   └── utils/                    # Utilities
│       ├── executor.go          # Command execution
│       ├── file.go              # File operations
│       └── network.go           # Network utilities
├── config/                        # Configuration templates
│   ├── testnet.yml              # Testnet preset
│   ├── mainnet.yml              # Mainnet preset
│   └── default.yml              # Default template
├── tests/                         # Test suites
│   ├── unit/                    # Unit tests
│   ├── integration/             # Integration tests
│   └── e2e/                     # End-to-end tests
├── docs/                         # Documentation
│   ├── setup.md                 # Setup guide
│   ├── commands.md              # Command reference
│   ├── configuration.md         # Config guide
│   └── monitoring.md            # Monitoring guide
├── scripts/                       # Build/deploy scripts
│   ├── build.sh                 # Build script
│   ├── install.sh               # Installation script
│   └── release.sh               # Release script
├── go.mod                         # Go module definition
├── go.sum                         # Dependency checksums
├── Dockerfile                     # Container image
├── docker-compose.yml             # Local development setup
├── Makefile                       # Build commands
└── README.md                      # Project overview
```

## Data Flow

### Node Setup Flow
1. User runs `snrk setup` command
2. CLI parses configuration file or prompts for options
3. Core Engine validates configuration
4. Installer downloads and installs Stellar Core
5. Installer downloads and installs Horizon
6. Database initialization creates schema
7. Configuration files are written to system
8. Validator keys are imported (if provided)
9. Status returned to user

### Node Lifecycle Flow
1. User runs lifecycle command (start/stop/restart)
2. CLI routes to lifecycle handler
3. Manager checks current node state
4. Appropriate system commands executed
5. Health checks performed
6. Status updated in monitoring system
7. Result returned to user

### Monitoring Flow
1. Metrics collector runs on schedule or demand
2. Queries Stellar Core and Horizon APIs
3. Collects system resource metrics
4. Stores metrics in local database
5. Alert rules evaluated
6. Dashboard aggregates current state
7. Logs streamed to user output

## Technology Stack

- **Language**: Go (for performance and cross-platform support)
- **CLI Framework**: Cobra or similar
- **Configuration**: YAML/JSON with schema validation
- **Database**: SQLite or PostgreSQL abstraction
- **Monitoring**: Prometheus metrics compatible
- **Containerization**: Docker and Docker Compose
- **Testing**: Go testing framework with testify
- **Documentation**: Markdown with automated generation

## Deployment Models

### Local Development
- Docker Compose setup for quick testing
- Single-machine deployment

### Production
- Standalone binary deployment
- Systemd service management
- Container-based orchestration ready

### Cloud Integration
- Cloud-agnostic design
- Environment variable configuration
- Secret management integration
- Auto-scaling ready metrics

## Security Considerations

- Validator keys stored securely (encrypted)
- Sensitive config data separation
- API endpoint authentication
- Network security best practices
- Audit logging for critical operations
- Secrets management integration

## Scalability

- Modular design for feature addition
- Plugin architecture for extensions
- API layer for external integrations
- Horizontal scaling ready
- Database connection pooling
