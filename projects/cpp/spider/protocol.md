### spider/protocol

The Spider uses is a fully-binary protocol for every network-based communication.

##### Protocol Messages
Our protocol is based on tiny objects called messages.
These can be serialized to obtain a binary form and then unserialized back to their original structure.
They also can be converted to JSON objects or simply expressed as a human-readable string.

In order to ease the reading of protocol messages, we use a header containing the size of the upcoming data in bytes.
It is expressed as a 4-byte-long unsigned integer.

All multi-bytes values are represented in Little-Endian.

##### ReplyCode
|       Name       |   Size   |     Value    |
|------------------|----------|--------------|
|       Magic      |  4 bytes |      `1`     |
| ConfirmationCode |  4 bytes |  `1` or `0`  |


##### End
|       Name       |   Size   |     Value    |
|------------------|----------|--------------|
|       Magic      |  4 bytes |      `2`     |

##### RawData
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|       Magic      |  4 bytes |      `3`     |
|       Size       |  4 bytes |  `unsigned`  |
|       Data       |   Size   |    `bytes`   |

##### Hello
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|       Magic      |  4 bytes |      `4`     |
|    MacAddress    |  6 bytes |    `bytes`   |
|      Version     |  2 bytes |  `unsigned`  |
|     MD5 Hash     | 16 bytes |    `bytes`   |


##### KeyEvent
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|       Magic      |  4 bytes |      `5`     |
|     Timestamp    |  8 bytes |  `unsigned`  |
|      KeyCode     |  4 bytes |   `KeyType`  |
|       State      |  4 bytes |  `unsigned`  |

##### MouseClick
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|       Magic      |  4 bytes |      `6`     |
|     Timestamp    |  8 bytes |  `unsigned`  |
|         X        |  4 bytes |  `unsigned`  |
|         Y        |  4 bytes |  `unsigned`  |
|      Button      |  4 bytes | `ButtonType` |

##### MouseMove
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|       Magic      |  4 bytes |      `7`     |
|     Timestamp    |  8 bytes |  `unsigned`  |
|         X        |  4 bytes |  `unsigned`  |
|         Y        |  4 bytes |  `unsigned`  |

##### ImageData
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|       Magic      |  4 bytes |      `8`     |
|       Size       |  4 bytes |  `unsigned`  |
|       Data       |   Size   |    `bytes`   |

##### StealthMode
|       Name       |   Size   |     Value    |
|------------------|----------|--------------|
|       Magic      |  4 bytes |      `9`     |

##### ActiveMode
|       Name       |   Size   |     Value    |
|------------------|----------|--------------|
|       Magic      |  4 bytes |     `10`     |

##### Screenshot
|       Name       |   Size   |     Value    |
|------------------|----------|--------------|
|       Magic      |  4 bytes |     `11`     |

##### RList
|       Name       |   Size   |     Value    |
|------------------|----------|--------------|
|       Magic      |  4 bytes |     `12`     |

##### RListReply
|       Name       |     Size     | Value/Format |
|------------------|--------------|--------------|
|       Magic      |    4 bytes   |     `13`     |
|      Number      |    4 bytes   |  `unsigned`  |
|   MacAddresses   |  Number * 6  |    `bytes`   |

##### RActiveMode
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|       Magic      |  4 bytes |     `14`     |
|    MacAddress    |  6 bytes |    `bytes`   |

##### RStealthMode
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|       Magic      |  4 bytes |     `15`     |
|    MacAddress    |  6 bytes |    `bytes`   |

##### RScreenshot
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|       Magic      |  4 bytes |     `16`     |
|    MacAddress    |  6 bytes |    `bytes`   |

##### WindowChange
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|       Magic      |  4 bytes |     `17`     |
|       Size       |  4 bytes |  `unsigned`  |
|    String Data   |   Size   |    `bytes`   |

##### RunShell
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|       Magic      |  4 bytes |     `18`     |
|       Size       |  4 bytes |  `unsigned`  |
|    String Data   |   Size   |    `bytes`   |

##### RRunShell
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|       Magic      |  4 bytes |     `19`     |
|    MacAddress    |  6 bytes |    `bytes`   |
|       Size       |  4 bytes |  `unsigned`  |
|    String Data   |   Size   |    `bytes`   |

