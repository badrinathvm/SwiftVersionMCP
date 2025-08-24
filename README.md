# Swift Version MCP Server

A [Model Context Protocol (MCP)](https://github.com/modelcontextprotocol) server that provides Swift version information and toolchain details. This server allows MCP clients to query Swift installation information, version details, and development environment configuration.

## Features

- 🔍 **Swift Version Detection** - Get current Swift version information
- 🛠️ **Development Environment Info** - Access Swift toolchain and Xcode details
- 📊 **System Configuration** - Analyze Swift Package Manager setup
- 🔧 **MCP Integration** - Seamless integration with MCP-compatible clients

## Installation

### Option 1: Homebrew (Recommended)

```bash
# Add the custom tap
brew tap badrinathvm/tap

# Install the Swift Version MCP server
brew install swift-version-mcp
```

### Option 2: Build from Source

#### Prerequisites

- macOS 13.0 or later
- Swift 6.0 or later
- Xcode 16.0 or later (or Swift toolchain)

#### Build Steps

```bash
# Clone the repository
git clone https://github.com/badrinathvm/SwiftVersionMCP.git
cd SwiftVersionMCP

# Build the project
swift build --configuration release

# The executable will be available at:
# .build/release/swift-version-mcp
```

## Configuration

### MCP Client Setup

Add the following configuration to your MCP client's configuration file (typically `mcp.json`):

#### For Homebrew Installation

```json
{
  "mcpServers": {
    "swift-version-server": {
      "type": "stdio",
      "command": "swift-version-mcp"
    }
  }
}
```

#### For Local Development

```json
{
  "mcpServers": {
    "swift-version-server": {
      "type": "stdio",
      "command": "/path/to/SwiftVersionMCP/.build/release/swift-version-mcp"
    }
  }
}
```

### Supported MCP Clients

- [Claude Desktop](https://claude.ai/desktop)
- [VS Code MCP Extension](https://marketplace.visualstudio.com/search?term=mcp)
- Any MCP-compatible client supporting stdio transport

  <img width="457" height="358" alt="Screenshot 2025-08-24 at 2 25 02 PM" src="https://github.com/user-attachments/assets/04677f63-e2d0-46db-80b7-bd25463a8dae" />


## Available Tools

The server provides the following MCP tools:

### `swift_version`

Returns comprehensive Swift version and environment information.

**Parameters:** None


## Usage Examples

Once configured with your MCP client, you can:

1. **Query Swift Version**
   ```
   User: What's my Swift Version?
   Assistant: [Uses swift_version tool to get current version]
   ```

2. **Development Environment Check**
   ```
   User: Show me my Swift development environment details
   Assistant: [Returns complete toolchain information]
   ```

3. **Compatibility Verification**
   ```
   User: Is my Swift version compatible with iOS 17 development?
   Assistant: [Analyzes version and provides compatibility info]
   ```

## Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   MCP Client    │    │  Swift Version  │    │  Swift System   │
│  (Claude, etc.) │◄──►│   MCP Server    │◄──►│   Commands      │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

The server acts as a bridge between MCP clients and the local Swift installation, providing structured access to Swift toolchain information.

## Development

### Project Structure

```
SwiftVersionMCP/
├── Package.swift                 # Swift Package Manager manifest
├── Sources/SwiftVersionMCP/
│   ├── main.swift               # Server entry point and main logic
│   └── ...
├── README.md
└── .gitignore
```

### Key Components

- **MCP Server**: Handles client communication via stdio transport
- **Swift Version Tool**: Queries system Swift installation
- **Transport Layer**: Manages MCP protocol communication

### Building for Development

```bash
# Build in debug mode
swift build

# Run the server directly
swift run SwiftVersionMCP

# Run tests (if available)
swift test
```

### Dependencies

- **MCP Swift SDK**: Model Context Protocol implementation for Swift
- **Foundation**: Core Swift libraries for system interaction

## Troubleshooting

### Common Issues

**Server not starting:**
```bash
# Check if Swift is properly installed
swift --version

# Verify the executable exists
which swift-version-mcp  # For Homebrew installation
```

**MCP client can't connect:**
- Verify your `mcp.json` configuration
- Check that the executable path is correct
- Ensure the MCP client supports stdio transport
- Restart your MCP client after configuration changes

**Permission errors:**
```bash
# Ensure proper file permissions
chmod +x /path/to/swift-version-mcp
```

### Debug Mode

For development and debugging, you can run the server with additional logging:

```bash
# Enable verbose logging (if supported)
swift-version-mcp --verbose

# Or check the server's help
swift-version-mcp --help
```

## Contributing

We welcome contributions! Please:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

### Development Guidelines

- Follow Swift coding conventions
- Add appropriate documentation for new features
- Ensure compatibility with MCP protocol specifications
- Test with multiple MCP clients when possible

## Roadmap

- [ ] Additional Swift toolchain information
- [ ] Swift package dependency analysis
- [ ] Xcode project compatibility checks
- [ ] Multi-toolchain support
- [ ] Performance optimizations

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Related Projects

- [Model Context Protocol](https://github.com/modelcontextprotocol) - MCP specification and tools
- [MCP Swift SDK](https://github.com/modelcontextprotocol/swift-sdk) - Swift implementation of MCP
- [Homebrew Tap](https://github.com/badrinathvm/homebrew-tap) - Installation via Homebrew

## Support

- **Issues**: [GitHub Issues](https://github.com/badrinathvm/SwiftVersionMCP/issues)
- **Discussions**: [GitHub Discussions](https://github.com/badrinathvm/SwiftVersionMCP/discussions)
- **MCP Community**: [Model Context Protocol Community](https://github.com/modelcontextprotocol)

---

Made with ❤️ for the Swift and MCP communities.
