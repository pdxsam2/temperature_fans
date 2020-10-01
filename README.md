# temperature_fans
Code for temperature controlled fans using an STM32 Nucleo-board with the F446RET MCU and the STM32CubeIDE. I will be uploading design schematics and the math to calculate the temperature from the thermistor soon. I recommend following this video for understanding the integer to temperature conversion for those interested: https://www.youtube.com/watch?v=k4fzrTtSoNk&list=WL&index=3&t=292s

# Materials
- STM32 F446RET Nucleo-board
- 10K ohm resistor*
- 10K ohm thermistor*
- 5V Fan*
- 2N222A Transistor
- Power Board capable of outputting 5V*

** = Generic Item, brand is not necessary as long as it meets the stated specs

# Verbal Design
- The resistor and thermistor are setup via a voltage divider (I personally powered the circuit with the 3.3V output pin on the Nucleo-board, the power board could be used for this as well)
- The output voltage of the divider is received and interpreted via an ADC channel in the MCU 
- Some calculations are run on the value returned from the ADC, using some other values (nominal resistance and b-value of the thermistor, and maximum ADC output), to find the current temperature in Kelvin, and then converted to Farenheit. 
- if the temperature exceeds 80 degrees F, then a GPIO pin was used to open the gate on the previously mentioned transistor, allowing current to flow through the transistor and therefore the fan(s) (I also added an LED to see when current was running through for good measure). NOTE: If you want to cut down on code or simply make it more efficient, you could avoid the calculation all together and simply find the output ADC value that is equal to 80 degrees F. I did not do this because it is a small program and I wanted to understand how the calculations work. 
