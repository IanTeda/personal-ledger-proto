<!-- Improved compatibility of back to top link -->
<a name="readme-top"></a>

<!-- Repo Badges | https://shields.io/badges -->
<div align="center">
  
[![License: GPL][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]

</div>

---

<!-- PROJECT HEADER -->
<br />
<div align="center">
    <a href="https://github.com/IanTeda/personal-ledger-proto">
        <img src="docs/images/logo.png" alt="Logo" width="80" height="80">
    </a>
    <h3 align="center">Personal Ledger | Proto</h3>
    <p align="center">
        Protobuf definitions for the Personal Ledger project, providing shared gRPC API specifications across applications.
        <br />
        <a href="https://ianteda.github.io/personal-ledger-proto/"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    ·
    <a href="https://github.com/IanTeda/personal-ledger">Personal Ledger (Parent Repo)</a>
    ·
    <a href="https://ianteda.github.io/personal-ledger-proto/issues">Report Bug</a>
    ·
    <a href="https://ianteda.github.io/personal-ledger-proto/issues">Request Feature</a>
    ·		
  </p>
</div>

## Overview

This repository contains Protocol Buffer (protobuf) definitions that define the gRPC APIs for the Personal Ledger backend services. These definitions ensure consistent interfaces between the backend server and client applications, enabling reliable communication.

The Personal Ledger project aims to provide users with an intuitive interface for insights into their spending habits and investment positions, presenting information clearly and concisely to support informed financial decisions.

## Features

- **Categories Service**: Complete CRUD operations for financial categories, including batch operations, filtering, pagination, and activation/deactivation.
- **Utilities Service**: Basic utility functions like health checks and ping operations.
- **Type Safety**: Strongly typed messages with validation and clear field definitions.
- **Extensibility**: Modular design allowing easy addition of new services and messages.

## Repository Structure

```
proto/
├── categories.proto    # Categories service definitions
├── utilities.proto     # Utilities service definitions
├── LICENSE             # GPL-3.0 license
└── README.md           # This file
```

### Proto Files

#### `categories.proto`
Defines the CategoriesService with the following capabilities:
- Category management (create, read, update, delete)
- Batch operations for multiple categories
- Lookup by ID, code, or URL slug
- Filtering and pagination for category lists
- Activation/deactivation of categories
- Support for category types (Asset, Equity, Expense, Income, Liability)

Key messages include:
- `Category`: Core category data structure
- `CategoryTypes`: Enum for category classification
- Various request/response pairs for each operation

#### `utilities.proto`
Provides basic utility services:
- `Ping`: Health check endpoint for service availability

## Usage

### Generating Code

This repository is used as a git submodule in the main Personal Ledger backend project. The build process automatically generates Rust code from these protobuf definitions using `tonic_prost_build`.

To generate code manually:

```bash
# Install protoc and the Rust tonic plugin
# On Ubuntu/Debian:
sudo apt-get install protobuf-compiler
cargo install tonic-build

# Generate Rust code
tonic_build::configure()
    .protoc_arg("--experimental_allow_proto3_optional")
    .build_client(true)
    .build_server(true)
    .compile_protos(&["proto/categories.proto", "proto/utilities.proto"], &["proto/"])?;
```

### Integration

The generated code is integrated into the Rust backend via the `build.rs` script, which:
- Compiles all `.proto` files in the `proto/` directory
- Generates both client and server code
- Includes well-known protobuf types
- Outputs to the Cargo build directory

## Dependencies

- **Protocol Buffers**: Version 3 (proto3 syntax)
- **gRPC**: For RPC definitions
- **Google Protobuf**: Timestamp and FieldMask types
- **Rust**: `tonic` and `prost` crates for code generation

## Development

### Adding New Services

1. Create a new `.proto` file in the `proto/` directory
2. Define your service and messages following proto3 syntax
3. Update the `build.rs` file in the parent repository to include the new file
4. Regenerate the code and implement the service logic

### Best Practices

- Use clear, descriptive names for messages and fields
- Include comments explaining the purpose of each field
- Follow the existing patterns for request/response structures
- Use appropriate protobuf types for data representation
- Maintain backward compatibility when possible

## Contributing

1. Fork the repository
2. Create a feature branch for your changes
3. Make your modifications to the `.proto` files
4. Ensure the changes compile and generate valid code
5. Test the integration with the main backend
6. Submit a pull request

Please ensure all changes maintain API compatibility and follow the established patterns.

## License

This project is licensed under the GNU General Public License v3.0 - see the [LICENSE](LICENSE) file for details.

## Related Projects

- [Personal Ledger Backend](https://github.com/IanTeda/personal-ledger-backend): Main Rust backend server
- [Personal Ledger Web](https://github.com/IanTeda/personal-ledger-react): Web Client application (planned)
- [Personal Ledger TUI](https://github.com/IanTeda/personal-ledger-react): Terminal application (planned)


<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
<!-- https://shields.io/badges -->
[contributors-shield]: https://img.shields.io/github/contributors/IanTeda/personal-ledger-proto.svg?style=for-the-badge
[contributors-url]: https://github.com/IanTeda/personal-ledger-proto/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/IanTeda/personal-ledger-proto.svg?style=for-the-badge
[forks-url]: https://github.com/IanTeda/personal-ledger-proto/network/members
[stars-shield]: https://img.shields.io/github/stars/IanTeda/personal-ledger-proto.svg?style=for-the-badge
[stars-url]: https://github.com/IanTeda/personal-ledger-proto/stargazers
[issues-shield]: https://img.shields.io/github/issues/IanTeda/personal-ledger-proto.svg?style=for-the-badge
[issues-url]: https://github.com/IanTeda/personal-ledger-proto/issues
[license-shield]: https://img.shields.io/github/license/IanTeda/personal-ledger-proto.svg?style=for-the-badge
[license-url]: https://github.com/IanTeda/personal-ledger-proto/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/ianteda