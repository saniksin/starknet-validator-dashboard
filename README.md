# Starknet Validator Attestation Dashboard

A comprehensive Grafana dashboard for monitoring Starknet validator attestation metrics in real-time.

## 🎯 Features

- **Real-time monitoring** of validator performance and blockchain state
- **Visual alerts** with color-coded thresholds for critical metrics
- **Complete coverage** of all essential validator metrics
- **Easy deployment** with Docker Compose example

## 📋 Requirements

- **Eqlabs Attestation Service** for Starknet Version **0.4.0** or higher
- **Grafana** :latest version
- **Prometheus** with access to validator metrics
- **Docker & Docker Compose** (for example deployment)

> ⚠️ **Important**: Versions below Starknet 0.4.0 may not support all metrics endpoints required by this dashboard.

## 🚀 Quick Start

### 1. Deploy Monitoring Stack

Use the provided example to set up Grafana and Prometheus:

```bash
# Clone or download this repository
git clone https://github.com/saniksin/starknet-validator-dashboard.git
cd starknet-validator-dashboard

# Navigate to example directory
cd example

# Edit prometheus configuration
# Replace 'host.docker.internal:9090' with your validator metrics endpoint
nano prometheus/prometheus.yml

# Start services
docker-compose up -d
```

### 2. Configure Grafana Data Source

1. Open Grafana at http://localhost:3000
2. Login with `admin` / `admin` and chage your password.
3. Go to **Configuration** → **Data Sources**
4. Click **Add data source** → **Prometheus**
5. Set URL to `http://prometheus:9090`
6. Click **Save & Test**

### 3. Import Dashboard

1. Download `dashboard.json` from this repository
2. **Important**: Edit the file and replace the UID:
   ```json
   "datasource": {
     "type": "prometheus",
     "uid": "YOUR_PROMETHEUS_UID_HERE"  // Replace "cesll5v5v88hse" to your prometheus UID
   }
   ```
3. In Grafana: **Dashboards** → **Import**
4. Upload the modified `dashboard.json`
5. Select your Prometheus data source
6. Click **Import**

## 📊 Dashboard Panels

| Panel | Description | Alert Thresholds |
|-------|-------------|------------------|
| ⛓️ Latest Block Number | Current blockchain tip | None |
| 🔰 Epoch Starting Block | Block number where current epoch began | None |
| 📊 Current Epoch Progress | Visual progress gauge (0-100%) | Yellow: >90% |
| ✅ Assigned Block to Attest | Target block for current attestation | None |
| ⏳ Blocks Until Attestation | Countdown to attestation deadline | 🔴 <1, 🟡 1-9, 🟢 ≥10 |
| ✅ Confirmed Attestations | Total successful attestations | None |
| 📬 Attestations Submitted | Total submission attempts | None |
| ❌ Attestation Failures | Failed attestation count | None |
| 🆔 Current Epoch ID | Active epoch identifier | None |
| 💰 STRK Balance | Operational account balance | 🔴 <10, 🟡 10-100, 🟢 >100 |
| ⏱️ Minutes Since Last Attestation | Time since last successful attestation | 🟢 <60, 🟡 60-120, 🔴 >120 |
| 😴 Missed Epochs Count | Epochs without successful attestation | 🟢 0, 🟡 1-2, 🔴 ≥3 |
| 📏 Epoch Length | Blocks per epoch | None |
| 🕒 Last Attestation Timestamp | Timestamp of most recent attestation | None |

## 🔧 Configuration

### Required Metrics

Your Starknet validator should expose these metrics at `/metrics`:

```
validator_attestation_starknet_latest_block_number
validator_attestation_current_epoch_starting_block_number
validator_attestation_current_epoch_assigned_block_number
validator_attestation_current_epoch_id
validator_attestation_current_epoch_length
validator_attestation_attestation_confirmed_count
validator_attestation_attestation_submitted_count
validator_attestation_attestation_failure_count
validator_attestation_missed_epochs_count
validator_attestation_last_attestation_timestamp_seconds
validator_attestation_operational_account_balance_strk
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues, feature requests, or pull requests.

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🙏 Acknowledgments

- Built for **Pathfinder Attestation Service** validators
- Compatible with **Starknet Version 0.4.0+**
- Community-driven monitoring solution 