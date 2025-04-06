# E-Book_ReaderTSC

Schema bloc:

```mermaid
flowchart TB
  subgraph Power
    USB[USB-C Input] -->|5V| Charger["Li-Ion Charger (MCP73831)"]
    Charger -->|Charging| Battery["LiPo Cell (2500mAh)"]
    Battery --> LDO["LDO Regulator (3.3V)"]
  end

  subgraph Core
    LDO -->|3.3V| MCU["ESP32-C6-WROOM-1"]
    MCU -- USB --> USB
  end

  subgraph Peripherals
    LDO --> Display["E-Ink Display (7.5in)"]
    LDO --> SD["SD Card Slot"]
    LDO --> RTC["RTC (DS3231)"]
    LDO --> Sensor["Enviro Sensor (BME688)"]
    LDO --> Gauge["Fuel Gauge (MAX17048)"]
    MCU -- SPI --> Display
    MCU -- SPI --> SD
    MCU -- GPIO --> Btns["Buttons (x3)"]
    MCU -- I2C --> Sensor
    MCU -- I2C --> Gauge
    MCU -- I2C --> RTC
  end
