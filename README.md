# E-Book_ReaderTSC

Schema bloc:

```mermaid
flowchart TB
  USB-C -->|5V| Charger["Battery Charger (MCP73832)"]
  Charger -->|Charging| LiPo["LiPo Battery"]
  LiPo --> LDO["3V3 LDO"]
  LiPo --> DC5["5V DC/DC"]

  ESP32["ESP32-C3-WROOM"]

  LDO -->|3.3V| ESP32
  LDO -->|3.3V| Display
  LDO -->|3.3V| SDCard
  LDO -->|3.3V| TempSensor
  LDO -->|3.3V| Buttons

  ESP32 -- SPI --> Display["1.5'' E-Ink Display (200x200px)"]
  ESP32 -- SPI --> SDCard["SD Card"]
  ESP32 -- GPIO --> Buttons["Buttons (3x)"]
  ESP32 -- I2C --> TempSensor["Temp/RH Sensor (BME680)"]
  ESP32 -- USB --> USB-C
end
