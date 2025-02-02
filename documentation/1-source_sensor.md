# 1. SOURCE SENSOR

These parameters are used to determine where the source data can be found. If you use the [Nordpool integration](https://github.com/custom-components/nordpool), or an integration which uses the same attributes, you don't need to provide any of the parameters, but it is advised to provide the `sensor` as it will be more resource friendly if the macro doesn't need to search for it.

## 🚨 IMPORTANT NOTES 🚨
* It is advised to provice all parameters if they don't match the defaults. Although the macro will search for the attributes and keys, it is more resource friendly if they are already provided.
* If your sensor uses other attributes for the data of today and tomorrow you need to provide the correct `sensor` parameter or the correct `attr_today` and `attr_tomorrow` parameters. It can't find the right sensor if the atrributes differ from the defaults, and it can't find the right attributes if the right sensor is not provided.
* In case `datetime_in_data` is set to `false` the attribute finder will not work, you need to make sure to set `attr_today`, `attr_tomorrow` and/or `attr_all` yourself.

## PARAMETERS

### **sensor** <span style="color:grey">_string_</span>
The entity_id of the sensor containing the source data
***
### **attr_today** <span style="color:grey">_string (default: raw_today)_</span>
The attribute which has the datetimes and prices for today used by the macro
***
### **attr_tomorrow** <span style="color:grey">_string (default: raw_tomorrow)_</span>
The attribute which has the datetimes and prices for tomorrow used by the macro
***
### **attr_all** <span style="color:grey">_string (default: prices)_</span>
The attribute which contains both the data of today and tomorrow if provided by the sensor
***
### **time_key** <span style="color:grey">_string (default: start)_</span>
The key used in the attributes of your integration for the start times of the hours
***
### **value_key** <span style="color:grey">_string (default: price)_</span>
The key used in the attributes of your integration for the price values
***
### **datetime_in_data** <span style="color:grey">_boolean (default: true)_</span>
In case the source data only provides the price values, without information about the date and time, set this to `false`
***
### **data_minutes** <span style="color:grey">_integer (default: 60)_</span>
The number of minutes each item in the source data represents. Only used in combination with `datetime_in_data=false`. Defaults to 1 hour (60 minutes)

## EXAMPLE

```jinja
{% from "cheapest_energy_hours.jinja" import cheapest_energy_hours %}
{% set output = cheapest_energy_hours(sensor='sensor.cheap_energy', attr_today="forecast_today", attr_tomorrow="prices_tomorrow", time_key="datetime", value_key="value") %}
```

## DATA PROVIDER SETTINGS

This section will give the attribute and key settings for energy providers. The name links to the (custom) component used for the data.
If your provider is missing, you can create a Pull Request to add them, or create an [issue](<https://github.com/TheFes/cheapest-energy-hours/issues/new>), and give the details there so I can add them.

|Data Provider|parameters|comment|
|---|---|---|
|[ENTSO-E](<https://github.com/JaccoR/hass-entso-e>)|`attr_today='prices_today', attr_tomorrow='prices_tomorrow', time_key='time', value_key='price'`||
|[Nordpool](<https://github.com/custom-components/nordpool>)||all set by default|
|[Tibber](<https://github.com/Danielhiversen/home_assistant_tibber_custom>)|`attr_today='today', attr_tomorrow='tomorrow', datetime_in_data=false`|This uses the custom component, not the core integration|
|[Zonneplan](<https://github.com/fsaris/home-assistant-zonneplan-one>)|`attr_all='forecast', value_key='electricity_price'`||

### NAVIGATION
[PREVIOUS: CONTENTS](./0-how-to.md) | [CONTENTS](0-how-to.md) | [NEXT: BASIC DATA](2-basic_data.md)
