# NeuralSynthesis: A Rust-Based Neural Network Construction and Execution Framework

NeuralSynthesis is a high-performance, extensible framework written in Rust for building, training, and executing neural networks. It provides a modular architecture allowing developers to easily define custom layers, activation functions, and training algorithms. The primary goal of this project is to offer a robust and efficient platform for both research and deployment of neural network-based solutions. NeuralSynthesis leverages Rust's safety and performance characteristics to provide a reliable and fast runtime environment, making it suitable for resource-constrained environments as well as large-scale deployments.

The framework is designed with flexibility and extensibility in mind. Users can define their own custom layer types, loss functions, and optimization algorithms by implementing simple traits. This allows for experimentation with novel architectures and training techniques without modifying the core codebase. NeuralSynthesis supports various numerical backends, enabling users to choose the most suitable one for their specific hardware and performance requirements. By providing a well-defined API and comprehensive documentation, NeuralSynthesis aims to simplify the development and deployment of neural network applications.

NeuralSynthesis offers a number of benefits over existing deep learning frameworks. Rust's memory safety guarantees prevent common errors like segmentation faults and data races, leading to more stable and reliable applications. Its zero-cost abstractions allow for high-performance execution without sacrificing code clarity. The frameworks modular design makes it easy to integrate with other Rust libraries and systems. Furthermore, NeuralSynthesis is designed to be highly portable, allowing it to run on a variety of platforms, including embedded systems and web browsers via WebAssembly.

## Key Features

*   **Modular Layer Architecture:** Define custom layers by implementing the `Layer` trait. This includes specifying the forward pass, backward pass, and parameter updates. Example: Implementing a custom convolutional layer with a specific filter size and stride involves defining the weight and bias parameters, the forward computation using convolution operations, and the backward computation to calculate gradients.
*   **Customizable Activation Functions:** Support for a wide range of activation functions, including ReLU, sigmoid, tanh, and custom functions defined using closures or dedicated structs that implement the `Activation` trait. Users can easily extend the framework with novel activation functions tailored to their specific needs.
*   **Multiple Numerical Backends:** Choose from different numerical backends for optimized performance on various hardware architectures. Currently supports `ndarray` (CPU-based) and aims for future support for `GPU` via `wgpu` for accelerated computation. Switching between backends is achieved via feature flags during compilation.
*   **Automatic Differentiation:** Utilizes reverse-mode automatic differentiation to efficiently compute gradients for complex neural network architectures. This allows for efficient training of deep models without requiring manual derivation of gradients for each layer. The differentiation process is transparent to the user, simplifying the development of new layer types.
*   **Optimizers:** Includes implementations of common optimization algorithms such as Stochastic Gradient Descent (SGD), Adam, and RMSprop. The `Optimizer` trait allows users to define custom optimization algorithms. Configuration options such as learning rate, momentum, and weight decay can be easily adjusted.
*   **Serialization and Deserialization:** Models can be serialized to and deserialized from files using `serde`, enabling easy storage and loading of trained networks. This allows for the creation of persistent models that can be deployed and reused without retraining.
*   **WebAssembly Support:** The framework can be compiled to WebAssembly, allowing neural networks to be executed in web browsers. This opens up possibilities for client-side inference and integration with web applications.

## Technology Stack

*   **Rust:** The core programming language, providing memory safety, performance, and concurrency features.
*   **ndarray:** A multidimensional array library for numerical computation. Used as the primary numerical backend for CPU-based operations.
*   **serde:** A serialization and deserialization framework for Rust, used for saving and loading models.
*   **rand:** A random number generator library used for initializing model parameters.
*   **wgpu (Planned):** A low-level graphics API that will be used to implement a GPU-accelerated numerical backend.

## Installation

1.  **Install Rust:** Download and install Rust from the official website: [https://www.rust-lang.org/](https://www.rust-lang.org/)
2.  **Clone the Repository:** Clone the NeuralSynthesis repository from GitHub:
    git clone https://github.com/jjfhwang/NeuralSynthesis.git
3.  **Navigate to the Project Directory:**
    cd NeuralSynthesis
4.  **Build the Project:** Build the project using Cargo, Rust's package manager:
    cargo build
5.  **Run Tests:** Run the unit tests to verify the installation:
    cargo test

## Configuration

NeuralSynthesis can be configured through environment variables and feature flags during compilation.

*   **Numerical Backend:** The default numerical backend is `ndarray`. To enable GPU support (when implemented), use the `gpu` feature flag:
    cargo build --features gpu
*   **Logging Level:** The logging level can be configured using the `RUST_LOG` environment variable. For example, to enable debug logging:
    RUST_LOG=debug cargo run
*   **Model Saving Path:** The default path for saving trained models can be configured using the `MODEL_PATH` environment variable.

## Usage

Basic example of creating and training a simple neural network:

// src/main.rs

use neural_synthesis::network::Network;
use neural_synthesis::layers::Dense;
use neural_synthesis::activations::ReLU;
use neural_synthesis::optimizers::SGD;

fn main() {
    let mut network = Network::new();
    network.add_layer(Dense::new(784, 128, ReLU::new()));
    network.add_layer(Dense::new(128, 10, ReLU::new()));

    let optimizer = SGD::new(0.01);
    // Assumes `train_data` and `train_labels` are loaded elsewhere.
    let train_data: Vec<Vec<f64>> = vec![vec![0.0; 784]; 100]; // Dummy data
    let train_labels: Vec<usize> = vec![0; 100]; // Dummy labels

    network.train(&train_data, &train_labels, optimizer, 10); // Train for 10 epochs
}

Further details about the API can be found in the `src/lib.rs` file and the associated documentation (generated using `cargo doc`).

## Contributing

We welcome contributions to NeuralSynthesis! Please follow these guidelines:

1.  Fork the repository.
2.  Create a new branch for your feature or bug fix.
3.  Write tests for your code.
4.  Ensure that all tests pass.
5.  Submit a pull request with a clear description of your changes.

## License

This project is licensed under the MIT License. See the [LICENSE](https://github.com/jjfhwang/NeuralSynthesis/blob/main/LICENSE) file for details.

## Acknowledgements

We would like to thank the Rust community for providing excellent tools and libraries. We also acknowledge the contributions of all individuals who have helped to shape this project.