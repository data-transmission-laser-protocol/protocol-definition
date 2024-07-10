# Protocol Definition for DTLP
Data Transmission Laser Protocol - a protocol for sending data with a laser beam to a laser receiver. 

This document defines the correct way of syncronized work between two modules - a transmitter and receiver, shows the properties of each version of the protocol which should be implemented in a connection.

The versioning of the protocol shows the major changes and has only one segment, i.e. X, while the protocol software implementation can have semantic versioning, i.e. X.Y.Z. where X is a major version (The version of implemented protocol), Y is a minor version showing software feature updates and Z is a patch version, showing software bugfixes.

## DTLP 2
The same DTLP 1 but with encryption and decryption of data. The encryption should be sync and use one key for encrypting and decrypting. The Encryption algorithm is depending on the exact situation and solution and will not be defined here.
By encryption and decryption of data, in case of [MITM attack](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) the potential 3rd party transmitter of an attacker will not be able to send a wrong data, because the receiver will try to decrypt the incoming payload and it'll not be able to process the data since there will be an error of decrypting the data. So the encryption of the data solves two potential issues: be sure the transmitter is known transmitter; be sure that the data is not processed by MITM attack.

##### Properties

| Property    | Standardized value | Description |
| :---:        |    :----:   |          :---: |
| ENCRYPTION_KEY | - | The key to encrypt and decrypt. Since the hardware working with this protocol may have limited resources it's decided to have a sync encryption algorithms - with a single key for encryption and decryption |



# Upcoming Versions
- The upcoming 3rd version will involve 8 transmitters and 8 receivers. Each laser and receiver will represent a bit. By that way in one bit period (BIT_DURATION) the transmitter will be able to send a whole byte and the receiver will be able to receive it. x8 for speed.

- The upcoming 4th version will include the following: 8 lasers for 1 and 8 lasers for 0 bits for the transmitter; 8 photodiodes for 1 and 8 photodiodes for 0 bits for the receiver. That's it 16 lasers for a transmitter and 16 photodiodes for receiver. By that way there will be implemented PDT([parallel data transmission](https://en.wikipedia.org/wiki/Parallel_communication)). x2 for speed.

- The upcoming 5th version of the protcol will be like TCP protcol - a data will be break down into chunks and sent by packets. Both transmitter and receiver will have a laser and photoresistor(diode), so when the first machine sends a data to the second, the second one will confirm incoming data and when all is done - will inform to get the next packet. By that way there will not be transmitter/receiver machines, but a machine, which can transmit and receive. 

### Licence 
This software is under the CC BY-NC-ND 4.0 licence. For more info see: https://github.com/data-transmission-laser-protocol/protocol-definition/blob/main/LICENCE
