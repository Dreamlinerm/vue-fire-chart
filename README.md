# Vue Fire Chart

![Example Image](vue-fire-chart/dist/example.png)

## Props

- **circleOptions** `{number}`: The labels for the circles. 
  - **example/default**: `["Braunkohle", "Steinkohle", "Erdgas", "Windkraft"]`
  
- **circleData** `{number}`: The height of the circles. 
  - **example/default**: `[1137, 853, 381, 10]`
  
- **yaxisTitle** `{string}`: The title of the y-axis. 
  - **example/default**: `"Gramm CO₂ je erzeugter kWh"`
  
- **textColor** `{string}`: The color of the text. 
  - **example/default**: `"white"`
  
- **fontSize** `{string}`: The font-size of the text. 
  - **example/default**: `"0.3em"`
  
- **colors** `{array}`: The colors of the circles. 
  - **example/default**: `["#d23227", "#f67d20", "#ffe10c", "#fffffd"]`
  
- **circle** `{boolean}`: If the circles should be circles or ovals. 
  - **example/default**: `true`