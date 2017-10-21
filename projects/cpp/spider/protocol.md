### spider/protocol

Every values uses Little Endian for bit signing

##### ReplyCode
|       Name       |   Size   |     Value    |
|------------------|----------|--------------|
|      Header      |  4 bytes |      `1`     |
| ConfirmationCode |  4 bytes |  `1` or `0`  |


##### End
|       Name       |   Size   |     Value    |
|------------------|----------|--------------|
|      Header      |  4 bytes |      `2`     |

##### RawData
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|      Header      |  4 bytes |      `3`     |
|       Size       |  4 bytes |  `unsigned`  |
|       Data       |   Size   |    `bytes`   |

##### Hello
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|      Header      |  4 bytes |      `4`     |
|    MacAddress    |  6 bytes |    `bytes`   |
|      Version     |  2 bytes |  `unsigned`  |
|       Hash       | 16 bytes |     `md5`    |


##### KeyEvent
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|      Header      |  4 bytes |      `5`     |
|     Timestamp    |  8 bytes |    `bytes`   |
|      KeyCode     |  4 bytes |   `KeyType`  |
|       State      |  4 bytes |  `unsigned`  |

##### MouseClick
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|      Header      |  4 bytes |      `6`     |
|     Timestamp    |  8 bytes |    `bytes`   |
|         X        |  4 bytes |  `unsigned`  |
|         Y        |  4 bytes |  `unsigned`  |
|      Button      |  4 bytes | `ButtonType` |

##### MouseMove
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|      Header      |  4 bytes |      `7`     |
|     Timestamp    |  8 bytes |    `bytes`   |
|         X        |  4 bytes |  `unsigned`  |
|         Y        |  4 bytes |  `unsigned`  |

##### ImageData
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|      Header      |  4 bytes |      `8`     |
|     Timestamp    |  8 bytes |    `bytes`   |
|       Width      |  4 bytes |  `unsigned`  |
|       Height     |  4 bytes |  `unsigned`  |

##### StealthMode
|       Name       |   Size   |     Value    |
|------------------|----------|--------------|
|      Header      |  4 bytes |      `9`     |

##### ActiveMode
|       Name       |   Size   |     Value    |
|------------------|----------|--------------|
|      Header      |  4 bytes |     `10`     |

##### Screenshot
|       Name       |   Size   |     Value    |
|------------------|----------|--------------|
|      Header      |  4 bytes |     `11`     |

##### RList
|       Name       |   Size   |     Value    |
|------------------|----------|--------------|
|      Header      |  4 bytes |     `12`     |

##### RListReply
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|      Header      |  4 bytes |     `13`     |

##### RActiveMode
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|      Header      |  4 bytes |     `14`     |
|    MacAddress    |  6 bytes |    `bytes`   |

##### RStealthMode
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|      Header      |  4 bytes |     `15`     |
|    MacAddress    |  6 bytes |    `bytes`   |

##### RScreenshot
|       Name       |   Size   | Value/Format |
|------------------|----------|--------------|
|      Header      |  4 bytes |     `16`     |
|    MacAddress    |  6 bytes |    `bytes`   |
