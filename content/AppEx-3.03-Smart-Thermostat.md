
# Application Exercise "Smart Thermostat"

Your team is designing the core control system for a Smart Thermostat. The system needs to track temperature readings and control the heating/cooling modes. Rules:

1. Target temperatures must always be between 50 and 90 ℉.
2. The thermostat can be in *heat*, *cool*, or *off* mode; it must never have both heating and cooling active at the same time.
3. The system must not switch to *heat* mode if the target temperature is lower than the current temperature; likewise, it must not switch to *cool* mode if the target temperature is higher than the current temperature.

You're deciding how to divide responsibilities between two classes:

- `ThermostatMode`: responsible for boolean states `_heatMode`, `_coolMode`.
- `SmartThermostat`: responsible for temperatures.

Below are proposed class designs. Question: Which UML design best protects the system from entering an invalid or unsafe state, while keeping class responsibilities clean and properly encapsulated?

A)

```mermaid
classDiagram
    class SmartThermostat {
        +double currentTemp
        +double targetTemp
        +ThermostatMode mode
        +SmartThermostat(double currentTemp, double targetTemp)
    }
    class ThermostatMode {
        +bool heat
        +bool cool
        +ThermostatMode()
        +void SetHeat()
        +void SetCool()
        +void SetOff()
    }
    SmartThermostat <-- ThermostatMode
```

B)

```mermaid
classDiagram
    class SmartThermostat {
        -double _currentTemp
        -double _targetTemp
        -ThermostatMode _mode
        +SmartThermostat(double currentTemp, double targetTemp)
        +double GetCurrentTemp()
        +void SetCurrentTemp(double temp)
        +double GetTargetTemp()
        +void SetTargetTemp(double temp)
        +ThermostatMode GetMode()
        +void SetMode(ThermostatMode mode)
    }
    class ThermostatMode {
        -bool _heat
        -bool _cool
        +ThermostatMode()
        +bool GetHeat()
        +void SetHeat(bool heat)
        +bool GetCool()
        +void SetCool(bool cool)
    }
    SmartThermostat <-- ThermostatMode
```

C)

```mermaid
classDiagram
    class SmartThermostat {
        -double _currentTemp
        -double _targetTemp
        -ThermostatMode _mode
        +SmartThermostat(double currentTemp, double targetTemp)
        +double GetCurrentTemp()
        +void SetCurrentTemp(double temp)
        +double GetTargetTemp()
        +void SetTargetTemp(double temp)
        +ThermostatMode GetMode()
        +void SetMode(ThermostatMode mode)
    }
    class ThermostatMode {
        -bool _heat
        -bool _cool
        +ThermostatMode()
        +bool GetHeat()
        +void SetHeat(bool heat)
        +bool GetCool()
        +void SetCool(bool cool)
    }
    SmartThermostat <-- ThermostatMode
```

D)

```mermaid
classDiagram
    class SmartThermostat {
        -double _currentTemp
        -double _targetTemp
        -ThermostatMode _mode
        +SmartThermostat(double currentTemp, double targetTemp)
        +double GetCurrentTemp()
        +double GetTargetTemp()
        +void SetTargetTemp(double temp)
        +ThermostatMode GetMode()
    }
    class ThermostatMode {
        -bool _heat
        -bool _cool
        +ThermostatMode()
        +void Heat()
        +void Cool()
        +void Off()
        +string GetModeString()
    }
    SmartThermostat <-- ThermostatMode
```

E)

```mermaid
classDiagram
    class SmartThermostat {
        -double _currentTemp
        -double _targetTemp
        -ThermostatMode _mode
        +SmartThermostat(double currentTemp, double targetTemp)
        +double GetCurrentTemp()
        +double GetTargetTemp()
        +void SetTargetTemp(double temp)
        +bool RequestModeChange(string requestedMode)
        +string GetStatusSummary()
    }
    class ThermostatMode {
        -bool _heat
        -bool _cool
        +ThermostatMode()
        +bool ChangeMode(bool enableHeat, bool enableCool)
        +string GetCurrentMode()
    }
    SmartThermostat <-- ThermostatMode
```

F)

```mermaid
classDiagram
    class SmartThermostat {
        -double _currentTemp
        -double _targetTemp
        -ThermostatMode _mode
        +SmartThermostat(double currentTemp, double targetTemp)
        +double GetCurrentTemp()
        +double GetTargetTemp()
        +void AdjustTargetTemperature(double delta)
        +void HeatTo(double newTargetTemp)
        +void CoolTo(double newTargetTemp)
        +void TurnOff()
        +string GetStatusSummary()
    }
    class ThermostatMode {
        -bool _heat
        -bool _cool
        +ThermostatMode()
        +void SetModeFlags(bool heat, bool cool)
        +bool IsHeatActive()
        +bool IsCoolActive()
    }
    SmartThermostat <-- ThermostatMode
```

---
