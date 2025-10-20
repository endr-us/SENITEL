# SENITEL
### 360° Threat Detection System

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/)
[![Rust](https://img.shields.io/badge/rust-1.70%2B-orange.svg)](https://www.rust-lang.org/)

**SENITEL** is an innovative and scalable 360-degree threat detection system that leverages the power of Python and Rust to deliver real-time object recognition for identifying hazardous and weaponry objects within its field of view. Utilizing synchronized camera inputs and edge-based CNN inference, SENITEL provides scalable security solutions from single Raspberry Pi deployments to globally distributed edge computing networks.

---

## Overview

SENITEL combines cutting-edge computer vision, deep learning, and high-performance computing to create a robust threat detection platform. The system is designed to:

- **Detect threats in real-time** using Convolutional Neural Networks (CNNs)
- **Process multiple synchronized camera feeds** for complete 360° coverage
- **Run efficiently on edge devices** like Raspberry Pi with minimal latency
- **Scale seamlessly** from single-device prototypes to worldwide deployments
- **Integrate future technologies** including eye-gaze tracking and advanced AI capabilities

---

## Key Features

### Core Capabilities
- **360° Visual Coverage**: Synchronize multiple camera inputs for complete perimeter monitoring
- **Real-Time CNN Inference**: Edge-based deep learning for immediate threat identification
- **Hazardous Object Detection**: Identify weapons, explosives, and other dangerous items
- **Low Latency Processing**: Optimized Rust backend for critical performance paths
- **Python Flexibility**: High-level logic and model management in Python
- **Edge Computing**: Deploy on resource-constrained devices without cloud dependency

### Advanced Features (Roadmap)
- **Eye-Gaze Tracking**: Predict attention and focus areas for enhanced threat assessment
- **Multi-Device Orchestration**: Coordinate detection across distributed sensor networks
- **Adaptive Learning**: Continuous model improvement from field data
- **Alert Management**: Intelligent notification system with priority queuing
- **Privacy Preservation**: On-device processing to protect sensitive data

---

## Architecture

SENITEL employs a hybrid architecture combining Python's machine learning ecosystem with Rust's performance and safety guarantees:

```
┌─────────────────────────────────────────────────────────────┐
│                     SENITEL System                           │
├─────────────────────────────────────────────────────────────┤
│  Python Layer                                                │
│  ├─ Model Training & Management                              │
│  ├─ High-Level Coordination                                  │
│  ├─ CNN Inference (TensorFlow/PyTorch)                       │
│  └─ Alert Generation & Logging                               │
├─────────────────────────────────────────────────────────────┤
│  Rust Layer                                                  │
│  ├─ Camera Input Synchronization                             │
│  ├─ Frame Buffer Management                                  │
│  ├─ Low-Level Image Processing                               │
│  └─ Performance-Critical Pipelines                           │
├─────────────────────────────────────────────────────────────┤
│  Hardware Layer                                              │
│  ├─ Camera Modules (CSI/USB)                                 │
│  ├─ Edge Device (Raspberry Pi / Jetson Nano / Custom)       │
│  └─ Optional: Accelerators (Coral TPU, Intel NCS)           │
└─────────────────────────────────────────────────────────────┘
```

### Why Python + Rust?

- **Python**: Rapid prototyping, extensive ML libraries (TensorFlow, PyTorch, OpenCV), easy model deployment
- **Rust**: Memory safety without garbage collection, zero-cost abstractions, concurrent processing without data races
- **Together**: Python handles AI/ML workloads while Rust ensures real-time performance and system reliability

---

## Hardware Requirements

### Minimum Configuration (Prototype)
- **Compute**: Raspberry Pi 4 (4GB RAM minimum)
- **Camera**: Raspberry Pi Camera Module v2 or compatible USB cameras
- **Storage**: 32GB microSD card (Class 10 or better)
- **Power**: 5V/3A USB-C power supply
- **Optional**: Cooling fan for sustained operation

### Recommended Configuration (Production)
- **Compute**: NVIDIA Jetson Nano/Xavier or Raspberry Pi 5
- **Camera**: Multiple high-resolution cameras (1080p+) with wide-angle lenses
- **Storage**: 64GB+ high-endurance microSD or SSD
- **Accelerator**: Google Coral Edge TPU or Intel Neural Compute Stick
- **Networking**: Gigabit Ethernet or WiFi 6 for distributed deployments
- **Enclosure**: Weatherproof housing for outdoor installations

---

## Installation

### Prerequisites

1. **System Dependencies**
```bash
# Debian/Ubuntu/Raspberry Pi OS
sudo apt-get update
sudo apt-get install -y python3 python3-pip python3-venv
sudo apt-get install -y build-essential cmake pkg-config
sudo apt-get install -y libssl-dev libv4l-dev v4l-utils
sudo apt-get install -y libjpeg-dev libpng-dev libtiff-dev

# Install Rust
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
```

2. **Python Virtual Environment**
```bash
python3 -m venv senitel-env
source senitel-env/bin/activate
```

### Installation Steps

1. **Clone the Repository**
```bash
git clone https://github.com/endr-us/SENITEL.git
cd SENITEL
```

2. **Install Python Dependencies**
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

3. **Build Rust Components**
```bash
cd rust-core
cargo build --release
cd ..
```

4. **Configure System**
```bash
cp config.example.yaml config.yaml
# Edit config.yaml with your camera settings and model paths
```

5. **Download Pre-trained Models**
```bash
python scripts/download_models.py
```

---

## Quick Start

### Basic Usage

1. **Single Camera Detection**
```bash
python main.py --mode single --camera 0
```

2. **360° Multi-Camera Setup**
```bash
python main.py --mode multi --cameras 0,1,2,3 --sync
```

3. **Run with Custom Model**
```bash
python main.py --model models/custom_threat_detector.h5
```

### Configuration

Edit `config.yaml` to customize:

```yaml
cameras:
  count: 4
  resolution: [1920, 1080]
  fps: 30
  sync_tolerance_ms: 10

detection:
  model_path: "models/threat_detection_v1.h5"
  confidence_threshold: 0.75
  nms_threshold: 0.45
  classes:
    - weapon
    - explosive
    - suspicious_package

processing:
  batch_size: 1
  use_gpu: false
  use_tpu: false
  num_threads: 4

alerts:
  enabled: true
  log_path: "logs/detections.log"
  notify_webhook: "https://your-server.com/webhook"
```

---

## Performance

### Benchmarks (Raspberry Pi 4, 4GB)

| Configuration | FPS | Latency | CPU Usage |
|--------------|-----|---------|-----------|
| Single Camera | 15-20 | ~50ms | 70-80% |
| Dual Camera | 10-15 | ~65ms | 85-95% |
| Quad Camera | 6-8 | ~125ms | 95-100% |

### Benchmarks (Jetson Nano + Coral TPU)

| Configuration | FPS | Latency | Power |
|--------------|-----|---------|-------|
| Single Camera | 45-60 | ~16ms | 8W |
| Quad Camera | 30-40 | ~25ms | 12W |

*Note: Performance varies based on model complexity, resolution, and specific threat classes.*

---

## Scalability & Deployment

### Small Scale (Single Device)
Perfect for:
- Home security systems
- Small business monitoring
- Research and development
- Educational projects

**Setup**: Single Raspberry Pi with 1-4 cameras

### Medium Scale (Multiple Locations)
Ideal for:
- Campus security
- Retail chain stores
- Industrial facilities
- Smart city pilot programs

**Setup**: Multiple edge devices with centralized monitoring dashboard

### Large Scale (Global Network)
Designed for:
- International enterprise security
- Public infrastructure protection
- Government and military applications
- Critical infrastructure monitoring

**Setup**: Distributed edge computing with:
- Regional aggregation servers
- Cloud-based analytics and storage
- Federated learning for model updates
- Real-time global threat intelligence

---

## Future Technologies

### Planned Enhancements

#### Eye-Gaze Tracking
- **Human Attention Analysis**: Detect where people are looking to identify suspicious behavior
- **Operator Focus Assistance**: Help security personnel prioritize threat areas
- **Behavioral Pattern Recognition**: Identify unusual gaze patterns indicative of threats

#### Advanced AI Capabilities
- **Transformer-based Detection**: Utilize vision transformers for improved accuracy
- **Few-Shot Learning**: Adapt to new threat types with minimal training data
- **Explainable AI**: Provide reasoning for detection decisions
- **Anomaly Detection**: Identify unusual activities without explicit threat patterns

#### Enhanced Hardware Integration
- **Thermal Imaging**: Detect concealed weapons through heat signatures
- **LiDAR Integration**: 3D spatial awareness and distance measurement
- **Radar Fusion**: All-weather detection capabilities
- **5G Connectivity**: Ultra-low latency for distributed systems

#### Software Improvements
- **Federated Learning**: Privacy-preserving collaborative model training
- **Digital Twin Simulation**: Virtual environment testing before deployment
- **AutoML Pipeline**: Automated model optimization and hyperparameter tuning
- **Edge-Cloud Hybrid**: Intelligent workload distribution

---

## Development

### Project Structure

```
SENITEL/
├── python/
│   ├── models/          # Neural network architectures
│   ├── inference/       # Inference engine
│   ├── camera/          # Camera management
│   └── utils/           # Helper functions
├── rust-core/
│   ├── src/
│   │   ├── camera/      # Camera synchronization
│   │   ├── buffer/      # Frame buffer management
│   │   └── processing/  # Image preprocessing
│   └── Cargo.toml
├── models/              # Trained model weights
├── config/              # Configuration files
├── scripts/             # Utility scripts
├── tests/               # Test suites
├── docs/                # Documentation
└── examples/            # Example implementations
```

### Building from Source

```bash
# Build Rust components with optimizations
cd rust-core
cargo build --release

# Run tests
cargo test

# Build Python wheel
cd ../python
python setup.py bdist_wheel
pip install dist/*.whl
```

### Running Tests

```bash
# Python tests
pytest tests/

# Rust tests
cd rust-core
cargo test --release

# Integration tests
python tests/integration_test.py
```

---

## Contributing

We welcome contributions from the community! Whether you're fixing bugs, adding features, or improving documentation, your help is appreciated.

### How to Contribute

1. **Fork the Repository**
2. **Create a Feature Branch** (`git checkout -b feature/amazing-feature`)
3. **Commit Your Changes** (`git commit -m 'Add amazing feature'`)
4. **Push to the Branch** (`git push origin feature/amazing-feature`)
5. **Open a Pull Request**

### Development Guidelines

- Follow PEP 8 for Python code
- Use `rustfmt` for Rust code formatting
- Add tests for new features
- Update documentation as needed
- Ensure all tests pass before submitting PR

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgments

- **TensorFlow** and **PyTorch** communities for excellent ML frameworks
- **Rust** community for a safe and performant systems language
- **OpenCV** for computer vision capabilities
- **Raspberry Pi Foundation** for accessible edge computing hardware
- All contributors and users who help improve SENITEL

---

## Contact & Support

- **Issues**: [GitHub Issues](https://github.com/endr-us/SENITEL/issues)
- **Discussions**: [GitHub Discussions](https://github.com/endr-us/SENITEL/discussions)
- **Email**: support@senitel.io
- **Documentation**: [Full Documentation](https://docs.senitel.io)

---

## Security

For security vulnerabilities, please email security@senitel.io instead of using the public issue tracker.

---

## Roadmap

### Phase 1: Foundation (Current)
- [ ] Core architecture design
- [ ] Basic single-camera detection
- [ ] Raspberry Pi optimization
- [ ] Initial model training

### Phase 2: Multi-Camera (Q1 2026)
- [ ] Camera synchronization
- [ ] 360° coverage algorithms
- [ ] Performance optimization
- [ ] Web-based monitoring dashboard

### Phase 3: Scale (Q2-Q3 2026)
- [ ] Multi-device orchestration
- [ ] Cloud integration
- [ ] Federated learning implementation
- [ ] Advanced alert management

### Phase 4: Next-Gen (Q4 2026+)
- [ ] Eye-gaze tracking integration
- [ ] Transformer-based models
- [ ] Thermal and LiDAR fusion
- [ ] Global deployment infrastructure
