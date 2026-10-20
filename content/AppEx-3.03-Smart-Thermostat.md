
# Application Exercise "Smart Thermostat"

## Scenario

Your team is designing the core control system for a Smart Thermostat. The system needs to track temperature readings and control the heating/cooling modes. Rules:

1. Target temperatures must always be between 50 and 90 ℉.
2. The thermostat can be in *heat*, *cool*, or *off* mode; it must never have both heating and cooling active at the same time.
3. The system must not switch to *heat* mode if the target temperature is lower than the current temperature; likewise, it must not switch to *cool* mode if the target temperature is higher than the current temperature.

You're deciding how to divide responsibilities between two classes:

- `ThermostatMode`: responsible for boolean states `_heatMode`, `_coolMode`.
- `SmartThermostat`: responsible for temperatures.

Below are proposed class designs.

## Question

Which UML design best protects the system from entering an invalid or unsafe state, while keeping class responsibilities clean and properly encapsulated?

### Option A: Public Direct Access (Open Mutation)

```mermaid
%%{init: {'classDiagram': {'textWrap': false}}}%%
classDiagram
    class SmartThermostat {
        +currentTemp : double
        +targetTemp : double
        +mode : ThermostatMode
        +SmartThermostat(currentTemp,targetTemp)
    }
    class ThermostatMode {
        +heat : bool
        +cool : bool
        +ThermostatMode()
        +SetHeat() void
        +SetCool() void
        +SetOff() void
    }
    SmartThermostat <-- ThermostatMode
```

### Option B: Pure Getter/Setter Pass-Through

```mermaid
%%{init: {'classDiagram': {'textWrap': false}}}%%
classDiagram
    class SmartThermostat {
        -_currentTemp : double
        -_targetTemp : double
        -_mode : ThermostatMode
        +SmartThermostat(currTemp,targetTemp)
        +GetCurrentTemp() double
        +SetCurrentTemp(temp double) void
        +GetTargetTemp() double
        +SetTargetTemp(temp double) void
        +GetMode() ThermostatMode
        +SetMode(mode) void
    }
    class ThermostatMode {
        -_heat : bool
        -_cool : bool
        +ThermostatMode()
        +GetHeat() bool
        +SetHeat(heat bool) void
        +GetCool() bool
        +SetCool(cool bool) void
    }
    SmartThermostat <-- ThermostatMode
```

### Option C: Delegated Mode Guarding (Smart Mode, Exposed Sub-Object)

```mermaid
%%{init: {'classDiagram': {'textWrap': false}}}%%
classDiagram
    class SmartThermostat {
        -_currentTemp : double
        -_targetTemp : double
        -_mode : ThermostatMode
        +SmartThermostat(currTemp,targetTemp)
        +GetCurrentTemp() double
        +GetTargetTemp() double
        +SetTargetTemp(temp) void
        +GetMode() ThermostatMode
    }
    class ThermostatMode {
        -_heat : bool
        -_cool : bool
        +ThermostatMode()
        +Heat() void
        +Cool() void
        +Off() void
        +GetModeString() string
    }
    SmartThermostat <-- ThermostatMode
```

### Option D: Centralized Thermostat Guarding (Fully Hidden Mode Object)

```mermaid
%%{init: {'classDiagram': {'textWrap': false}}}%%classDiagram
    class SmartThermostat {
        -_currentTemp : double
        -_targetTemp : double
        -_mode : ThermostatMode
        +SmartThermostat(currTemp,targetTemp)
        +GetCurrentTemp() double
        +GetTargetTemp() double
        +SetTargetTemp(temp) void
        +SetModeHeat() void
        +SetModeCool() void
        +SetModeOff() void
        +GetStatusSummary() string
    }
    class ThermostatMode {
        -_heat : bool
        -_cool : bool
        +ThermostatMode()
        +SetHeatState(h) void
        +SetCoolState(c) void
        +IsHeat() bool
        +IsCool() bool
    }
    SmartThermostat <-- ThermostatMode
```

### Option E: Coordinated Dual-Guarding (Shared Validation Responsibilities)

```mermaid
%%{init: {'classDiagram': {'textWrap': false}}}%%
classDiagram
    class SmartThermostat {
        -_currentTemp : double
        -_targetTemp : double
        -_mode : ThermostatMode
        +SmartThermostat(currTemp,targetTemp)
        +GetCurrentTemp() double
        +GetTargetTemp() double
        +SetTargetTemp(temp) void
        +RequestModeChange(requestedMode) bool
        +GetStatusSummary() string
    }
    class ThermostatMode {
        -_heat : bool
        -_cool : bool
        +ThermostatMode()
        +ChangeMode(enableHeat,enableCool) bool
        +GetCurrentMode() string
    }
    SmartThermostat <-- ThermostatMode
```

### Option F: Intent-Based Domain Actions (Action Methods Only)

```mermaid
%%{init: {'classDiagram': {'textWrap': false}}}%%
classDiagram
    class SmartThermostat {
        -_currentTemp : double
        -_targetTemp : double
        -_mode : ThermostatMode
        +SmartThermostat(currTemp,targetTemp)
        +GetCurrentTemp() double
        +GetTargetTemp() double
        +AdjustTargetTemperature(delta) void
        +HeatTo(newTargetTemp) void
        +CoolTo(newTargetTemp) void
        +TurnOff() void
        +GetStatusSummary() string
    }
    class ThermostatMode {
        -_heat : bool
        -_cool : bool
        +ThermostatMode()
        +SetModeFlags(heat,cool) void
        +IsHeatActive() bool
        +IsCoolActive() bool
    }
    SmartThermostat <-- ThermostatMode
```
