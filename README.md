# Protocol Definition for DTLP
Data Transmission Laser Protocol - a protocol for sending data with a laser beam to a laser receiver. 

This document defines the correct way of syncronized work between two modules - a transmitter and receiver, shows the properties of each version of the protocol which should be implemented in a connection.

The versioning of the protocol shows the major changes and has only one segment, i.e. X, while the protocol software implementation can have semantic versioning, i.e. X.Y.Z. where X is a major version (The version of implemented protocol), Y is a minor version showing software feature updates and Z is a patch version, showing software bugfixes.

## DTLP 3
The 3rd version of the protocol works the following way: Once in BYTE_DURATION the transmitter enables and disables the lasers (which are 8) depending on current byte. The receiver reads the values from photodiodes once in BYTE_DURATION. When received null byte - the connection is closed and the data converted from bin to str.

##### Properties

| Property    | Standardized value | Description |
| :---:        |    :----:   |          :---: |
| HANDSHAKE_SIGNAL_DURATION | 100 | The duration of handshake signal in milliseconds. The handshake is one long signal sending before upcoming data transmission. Should be longer than one bit duration. It should be the same on both transmitter and receiver ends. |
| BYTE_DURATION | - | The duration of one byte in milliseconds and depends on the exact hardware. It should be the same on both transmitter and receiver ends.|



# Upcoming Versions

- The upcoming 4th version will include the following: 8 lasers for 1 and 8 lasers for 0 bits for the transmitter; 8 photodiodes for 1 and 8 photodiodes for 0 bits for the receiver. That's it 16 lasers for a transmitter and 16 photodiodes for receiver. By that way there will be implemented PDT([parallel data transmission](https://en.wikipedia.org/wiki/Parallel_communication)). x2 for speed.

- The upcoming 5th version of the protcol will be like TCP protcol - a data will be break down into chunks and sent by packets. Both transmitter and receiver will have a laser and photoresistor(diode), so when the first machine sends a data to the second, the second one will confirm incoming data and when all is done - will inform to get the next packet. By that way there will not be transmitter/receiver machines, but a machine, which can transmit and receive. 

### Licence 
This software is under the CC BY-NC-ND 4.0 licence. For more info see: https://github.com/data-transmission-laser-protocol/protocol-definition/blob/main/LICENCE
