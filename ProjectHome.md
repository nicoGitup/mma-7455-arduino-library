# !!! NOTICE !!! #
A new version of the library is available for all users of the new Arduino 1.0 IDE please download MMA\_7455\_UNO.zip for older versions of the IDE (up to 0023) please download MMA\_7455.zip.

# Overview #

This Library is a small wrapper to easily read out Freescale's 3-Axis Accelerometer "MMA7455L" via two-wired interface (I2C). This library will run under Arduino enabling a simple and very cheap accelerometer to your projects.

# Wiring #
<img src='http://blogs.iad.zhdk.ch/embodied-interaction-basics-hs11/files/2011/11/MMA7455_Anschluss.png' />

# Functions #
**MMA\_7455**<br>
This function creates an instance of MMA_7455 Library and enables the Wire Library (for i2c communication)<br>
<br>
<b>initSensitivity(int)</b><br>
With this function you basically set the sensitivity level of the sensor. Three values are allowed: 2 for 2g, 4 for 4g and 8 for 8g sensitivity<br>
<br>
<b>calibrateOffset(float, float, float)</b><br>
To calibrate the offset of the sensor, these function is called once in the setup(). Therefore insert the actual readings if the sensor is placed on a flat surface, so that the output could be corrected. The values should equal to: xVal=0, yVal=0, zVal=64<br>
<br>
<b>readAxis(char)</b><br>
By assigning the axis to the functions variable ('x', 'y' or 'z') the sensor gives back the reading of this axis as unsigned char character.<br>
<br>
<h1>Example Code (Arduino)</h1>
<pre><code>// Example which uses the MMA_7455 library<br>
// Moritz Kemper, IAD Physical Computing Lab<br>
// moritz.kemper@zhdk.ch<br>
// ZHdK, 20/11/2011<br>
<br>
#include &lt;Wire.h&gt; //Include the Wire library<br>
#include &lt;MMA_7455.h&gt; //Include the MMA_7455 library<br>
<br>
MMA_7455 mySensor = MMA_7455(); //Make an instance of MMA_7455<br>
<br>
char xVal, yVal, zVal; //Variables for the values from the sensor<br>
<br>
void setup()<br>
{<br>
  Serial.begin(9600);<br>
  // Set the sensitivity you want to use<br>
  // 2 = 2g, 4 = 4g, 8 = 8g<br>
  mySensor.initSensitivity(2);<br>
  // Calibrate the Offset, that values corespond in <br>
  // flat position to: xVal = -30, yVal = -20, zVal = +20<br>
  // !!!Activate this after having the first values read out!!!<br>
  //mySensor.calibrateOffset(5, 20, -68);<br>
}<br>
<br>
void loop()<br>
{<br>
  xVal = mySensor.readAxis('x'); //Read out the 'x' Axis<br>
  yVal = mySensor.readAxis('y'); //Read out the 'y' Axis<br>
  zVal = mySensor.readAxis('z'); //Read out the 'z' Axis<br>
  <br>
  Serial.print(xVal, DEC);<br>
  Serial.print("\t");<br>
  Serial.print(yVal, DEC);<br>
  Serial.print("\t");<br>
  Serial.println(zVal, DEC);<br>
}<br>
</code></pre>