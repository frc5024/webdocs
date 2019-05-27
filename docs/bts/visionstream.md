# The WIP VisionStream Protocol

This is in no way final, just an idea. Unless you are writing the code behind this protocol, please ignore this page.

## Discovery
A client should start by connecting to the robot's NetworkTables server. Next, check the `port` field of the `VisionStream` table. If this table does not exsist, the server is not live.

## Control messages
These messages are sent by the client to the server over UDP

### Hello
| Size | Absolute value? | Use |
|--|--|--|
| 1 Byte | 0x01 | Signify that this is a hello message |
| 4 Bytes | | 4 bytes to be used as a "client ID". This can be anything |

### Disconnect
| Size | Absolute value? | Use |
|--|--|--|
| 1 Byte | 0x02 | Signify that this is a disconnect message |
| 4 Bytes | | 4 bytes to be used as a "client ID". This should be the same as the ID used in the Hello message |

### New data
| Size | Absolute value? | Use |
|--|--|--|
| 1 Byte | 0x03 | Signify that this is a new data message |
| 2 Bytes | | A uint16 that must increment every message. This must also be sent over NetworkTables in the `VisionStream/counter` field. If this counter falls behind the NetworkTables counter on the server (ex. packets are lost), the server will switch over to reading only from NetworkTables and will assume a disconnect message was sent. The `VisionStream/canRead` field will be changed tby the server to `false` to signal the client to try reconnecting. |
| 4 Bytes| | 4 chars to be used as a name for the data. If this name has been seen before, the server will cound this as a request to override the field with the new data. The client must also push a field into the `VisionStream/data` table with the same name, and a type of `double` |
| 8 Bytes | | A double to contain the data. This must also be pushed to NetowkrTables in the orrect field of the `VisionStream/data` table. |