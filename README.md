# Protocol Definition for DTLP
Data Transmission Laser Protocol - a protocol for sending data with a laser beam to a laser receiver. 

This document defines the correct way of syncronized work between two modules - a transmitter and receiver, shows the properties of each version of the protocol which should be implemented in a connection.

The versioning of the protocol shows the major changes and has only one segment, i.e. X, while the protocol software implementation can have semantic versioning, i.e. X.Y.Z. where X is a major version (The version of implemented protocol), Y is a minor version showing software feature updates and Z is a patch version, showing software bugfixes.

## DTLP 4
The 3rd version of the protocol is stateful. A transmitter has 16 laser lasers and receiver has 16 photodiodes. 8 for zeros and 8 for ones. Once in BYTE_DURATION milliseconds the transmitter enables the lasers regarding byte. If this is a "a" letter the byte is 01100001 so in this case the transmitter will enable needed lasers of zeros and one.
The connection starts with a handshake - a long laser singal with HANDSHAKE_SIGNAL_DURATION duration. Right after it the receiver have to collect incoming bytes. 
![image](https://github.com/data-transmission-laser-protocol/protocol-definition/assets/22774727/33e1854f-46c4-4a49-b0d0-d4c4cd65be6c)



The connection will be closed when the incoming byte is 00000000. That means, when the receiver received null byte.

##### Properties

| Property    | Standardized value | Description |
| :---:        |    :----:   |          :---: |
| HANDSHAKE_SIGNAL_DURATION | 100 | The duration of handshake signal in milliseconds. The handshake is one long signal sending before upcoming data transmission. Should be longer than one BYTE_DURATION. It should be the same on both transmitter and receiver ends. |
| BYTE_DURATION | - | The duration of one byte in milliseconds and depends on the exact hardware. It should be the same on both transmitter and receiver ends.|



# Upcoming Versions

- The upcoming 5th version of the protcol will be like TCP protcol - a data will be break down into chunks and sent by packets. Both transmitter and receiver will have a laser and photoresistor(diode), so when the first machine sends a data to the second, the second one will confirm incoming data and when all is done - will inform to get the next packet. By that way there will not be transmitter/receiver machines, but a machine, which can transmit and receive. 

### Licence 
This software is under the CC BY-NC-ND 4.0 licence. For more info see: https://github.com/data-transmission-laser-protocol/protocol-definition/blob/main/LICENCE
