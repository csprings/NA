### Implement VNA Instrument Plugin

1. copy and paste the below line in Command prompt 
```
cd C:\Program Files\Keysight\Test Automation\Packages\Python\NA\
```
![image](https://user-images.githubusercontent.com/91975559/176611051-fca7cdf0-2d71-4039-b070-ec7e4d46c213.png)

2. Open VS Code with ***code .***

    ![image](https://user-images.githubusercontent.com/91975559/176611164-4cfec8d2-ac65-4a66-b1ce-4679a224583b.png)

3. Select ***VNA.py*** file. Add below command line ***before VNA class***.
```python
from OpenTap.Plugins.BasicSteps import GenericScpiInstrument
```
![image](https://user-images.githubusercontent.com/91975559/176612588-98e3c05d-1d35-4100-9eb2-9a477cfc4130.png)

4. Replacing the below ***Atrribute*** line with the below new line
```python
@Attribute(DisplayAttribute, "VNA", "Add a description here", "Add a group name here")
```
---->
```python
@Attribute(DisplayAttribute, "VNA", "add VNA Network Analyzer", "VNA")
```
![image](https://user-images.githubusercontent.com/91975559/176612705-1da9adb9-c5a4-4050-8310-64ca5767c8bf.png)

5. On the ***__init__*** function copy and paste below lines

```python
self._io = GenericScpiInstrument()
```
```python
self.Name = "VNA"
```
```python
Prop = self.AddProperty("visa_address", "TCPIP0::127.0.0.1::hislip0::INSTR", String)
```
```python
Prop.AddAttribute(DisplayAttribute, "VISA Address", "VISA Address of the instrument to connect", "VISA")
```

6.	On the ***Open*** function, add below 3 lines of the code, that will add default visa_address to _io instance and open the instrument connection when it calls Open() method. 
```python
self._io.VisaAddress  = self.visa_address
```
```python
self._io.Open()
```

7.	On the ***Close*** function, add a line, that close the instrument connection 
```python
self._io.Close()
```

6. Let"s move to next step [Reset Test Step](https://github.com/csprings/Code-Repo/blob/gh-pages/ResetStep.md)
