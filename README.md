# Cloverpad - Serial Communication Protocol

This folder contains the [Protocol Buffers](https://protobuf.dev/) definitions for the [Cloverpad](https://github.com/Cloverpad)'s serial communication protocol. It is used by the following projects:

- [Cloverpad HE Firmware](https://github.com/Cloverpad/cloverpad-he-firmware)
- [Cloverpad Web Configurator](https://github.com/Cloverpad/cloverpad-configurator-web)

## Protocol Description

`commands.proto` contains the top-level structs for the protocol:

- `Command`: A command that is sent from the host to the keypad
- `Response`: The keypad's response to a command

The intended control flow is as follows:

- **Host**:
  - Encode command as bytes
  - Send command length over serial interface, as an unsigned 32-bit integer in little endian byte order
  - Send command data over serial interface
- **Keypad**:
  - Read command length from serial interface
  - Read command data from serial interface
  - Decode command data
  - Process command
  - Encode response as bytes
  - Send response length over serial interface, as an unsigned 32-bit integer in little endian byte order
  - Send response data over serial interface
- **Host**:
  - Read response length from serial interface
  - Read response data from serial interface
  - Decode response data
  - Process response

### Nanopb Options

Some of the definition files have additional [Nanopb](https://jpa.kapsi.fi/nanopb/) options provided. `string` and array types are constrained in size to make encoding/decoding easier on the firmware side.

More details can be found [here](https://jpa.kapsi.fi/nanopb/docs/reference.html#defining-the-options-in-a-.options-file).

## License

The files in this repository are licensed under [GPL-3.0](./LICENSE).
