# temperature_fans
Code for temperature controlled fans using an STM32 Nucleo-board with the F446RET MCU and the STM32CubeIDE(v1.3.0 which is more friendly to the MacOS). I will be uploading design schematics and the math to calculate the temperature from the thermistor at some point in the near future. I recommend following this video for understanding the integer to temperature conversion for those interested: https://www.youtube.com/watch?v=k4fzrTtSoNk&list=WL&index=3&t=292s

Note: The IDE currently has issues with linking an existing project to a workspace. It is probably best to build a project based on the provided .ioc file and then copy main.c (I've verified that this works)

# Materials
- STM32 F446RET Nucleo-board
- 10K ohm resistor*
- thermistor with the following specs*: 10K ohm nominal resistance, 298= nominal temperature, b-value= 3950
- 5V Fan*
- 2N222A Transistor
- Power Board capable of outputting 5V*

'*' = Generic Item, brand is not necessary as long as it meets the stated specs

# Verbal Design
- The resistor and thermistor are setup via a voltage divider (I personally powered the voltage divider with the 3.3V output pin on the Nucleo-board, the power board could be used for this as well)
- The output voltage of the divider is received and interpreted via an ADC channel in the MCU 
- Some calculations are run on the value returned from the ADC using some of the thermistors specs and the maximum ADC output (dependent on the bit resolution of the ADC) to find the current temperature in Kelvin and then convert to Farenheit. 
- if the temperature exceeds 80 degrees F, then a GPIO pin was used to open the gate on the previously mentioned transistor, allowing current to flow through the transistor and therefore the fan(s) (I also added an LED to see when current was running through for good measure). NOTE: If you want to cut down on code or simply make it more efficient, you could avoid the calculation all together and simply find the output ADC value that is equal to 80 degrees F. I did not do this because it is a small program and I wanted to understand how the calculations work. 
