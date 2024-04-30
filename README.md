# Protocol Definition for DTLP
Data Transmission Laser Protocol - a protocol for sending data with a laser beam to a laser receiver. 

This document defines the correct way of syncronized work between two modules - a transmitter and receiver, shows the properties of each version of the protocol which should be implemented in a connection.

The versioning of the protocol shows the major changes and has only one segment, i.e. X, while the protocol software implementation can have semantic versioning, i.e. X.Y.Z. where X is a major version (The version of implemented protocol), Y is a minor version showing software feature updates and Z is a patch version, showing software bugfixes.

# Protocol Versions

### DTLP 1
The first version of the protocol is a representation of binary data. Each laser light represents a 1 bit, while no light represents 0 bit. The connection starts with a handshake - a long laser singal with HANDSHAKE_SIGNAL_DURATION duration. Right after it the receiver have to collect incoming bits. When 8 bits received, i.e. that's a byte, the data should be converted into string. The laser transmitter sends bits once in BIT_DURATION. If it's the 1 bit, the laser beam should be enabled for BIT_DURATION milliseconds, otherwise if it's the 0 bit, the laser should be disabled for BIT_DURATION milliseconds. The receiver reads the current state of a physical module once in BIT_DURATION and depending on a digital output writes the incoming bit. The connection will be closed when the incoming byte is 00000000. That means, when the receiver receives no light for BIT_DURATION * 8, the connection will be closed. 

##### Flow chart
![image](https://github.com/data-transmission-laser-protocol/protocol-definition/assets/22774727/56b0da43-078d-41bc-94f0-385882b73c0f)


##### Properties

| Property    | Standardized value | Description |
| :---:        |    :----:   |          :---: |
| HANDSHAKE_SIGNAL_DURATION | 100 | The duration of handshake signal in milliseconds. The handshake is one long signal sending before upcoming data transmission. Should be longer than one bit duration. It should be the same on both transmitter and receiver ends. |
| BIT_DURATION | - | The duration of one bit in milliseconds and depends on the exact hardware. It should be the same on both transmitter and receiver ends. The ordinary digital photoresistor module can handle downt to 70ms per bit|

### DTLP 2
The same DTLP 1 but with encryption and decryption of data. The encryption should be sync and use one key for encrypting and decrypting. The Encryption algorithm is depending on the exact situation and solution and will not be defined here.
By encryption and decryption of data, in case of [MITM attack](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) the potential 3rd party transmitter of an attacker will not be able to send a wrong data, because the receiver will try to decrypt the incoming payload and it'll not be able to process the data since there will be an error of decrypting the data. So the encryption of the data solves two potential issues: be sure the transmitter is known transmitter; be sure that the data is not processed by MITM attack.


# Upcoming Versions
- The upcoming 3rd version will involve 8 transmitters and 8 receivers. Each laser and receiver will represent a bit. By that way in one bit period (BIT_DURATION) the transmitter will be able to send a whole byte and the receiver will be able to receive it. x8 for speed.

- The upcoming 4th version will include the following: 8 lasers for 1 and 8 lasers for 0 bits for the transmitter; 8 photodiodes for 1 and 8 photodiodes for 0 bits for the receiver. That's it 16 lasers for a transmitter and 16 photodiodes for receiver. By that way there will be implemented PDT([parallel data transmission](https://en.wikipedia.org/wiki/Parallel_communication)). x2 for speed.

- The upcoming 5th version of the protcol will be like TCP protcol - a data will be break down into chunks and sent by packets. Both transmitter and receiver will have a laser and photoresistor(diode), so when the first machine sends a data to the second, the second one will confirm incoming data and when all is done - will inform to get the next packet. By that way there will not be transmitter/receiver machines, but a machine, which can transmit and receive. 

### Licence 
This software is under the CC BY-NC-ND 4.0 licence. For more info see: https://github.com/data-transmission-laser-protocol/protocol-definition/blob/main/LICENCE
