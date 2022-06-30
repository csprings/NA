### Implement VNA Instrument Plugin

1. copy and paste the below line in ***Command prompt*** window 
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
![image](https://user-images.githubusercontent.com/91975559/176613105-3effe214-429f-40e3-a2d2-0bde557f9e3d.png)

```python
self.Name = "VNA"
```
![image](https://user-images.githubusercontent.com/91975559/176613165-6c1cf43f-7d90-4969-ac4d-c956e8ec184a.png)

```python
Prop = self.AddProperty("visa_address", "TCPIP0::127.0.0.1::hislip0::INSTR", String)
```
![image](https://user-images.githubusercontent.com/91975559/176613387-04cf7290-1d3d-4ef7-b443-e6390948bb30.png)

```python
Prop.AddAttribute(DisplayAttribute, "VISA Address", "VISA Address of the instrument to connect", "VISA")
```
![image](https://user-images.githubusercontent.com/91975559/176613517-d98ee8dc-f348-4935-afa8-4c74f8c52c77.png)

6. Delete below lines before ***def Open(self)***

7.	On the ***Open*** function, add below 3 lines of the code, that will add default visa_address to _io instance and open the instrument connection when it calls Open() method. 
```python
self._io.VisaAddress  = self.visa_address
```
![image](https://user-images.githubusercontent.com/91975559/176613806-5b8d1dc6-ac91-4d10-8db7-152a21dfe6be.png)

```python
self._io.Open()
```
![image](https://user-images.githubusercontent.com/91975559/176613887-0885aa69-2eb0-4350-87c8-81643d936574.png)

8.	On the ***Close*** function, add a line, that close the instrument connection 
```python
self._io.Close()
```
![image](https://user-images.githubusercontent.com/91975559/176613951-31348739-1dd6-49cc-a81a-e8c5b2f55d90.png)

9. Let's build again the python Project
```
tap python build NA
```
![image](https://user-images.githubusercontent.com/91975559/176614879-96f76eb8-d8c8-465f-8cb6-a97e7129fecc.png)

10. Move to next step [IDN Test Step](https://github.com/csprings/Code-Repo/blob/gh-pages/ResetStep.md)
