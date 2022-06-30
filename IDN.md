[back](https://github.com/csprings/NA/blob/main/VNA.md)
### IDN Test Step Plugin development

1.	Select ***IDN.py*** file and add(from) VNA class to this IDN.py file.
```python
from .VNA import *
```
![image](https://user-images.githubusercontent.com/91975559/176617241-8ba491ad-02e1-43a2-9df1-3325823ea196.png)

2.	Change ***attribute*** of the IDN TestStep. 
```python
@Attribute(DisplayAttribute, "Reset", "Add a description here", "Add a group name here")
```
---->
```python
@Attribute(DisplayAttribute, "IDN", "Reset the instrument to default setting", "Network Analyzer") 
```
![image](https://user-images.githubusercontent.com/91975559/176618763-8ef6ebb3-5484-43f6-a761-499492c0cefa.png)

3.  Add ***setting attribute***, which will choose and connect the instrument. Similar to the VNA.py, reuse exist example code.
```python
Prop = self.AddProperty("vna", None, VNA)
```
![image](https://user-images.githubusercontent.com/91975559/176617531-93fdd331-f679-46e7-90ea-9f882354d38a.png)

```python
Prop.AddAttribute(DisplayAttribute, "Instrument", "The instrument to connect", "Resources")
```
![image](https://user-images.githubusercontent.com/91975559/176617622-c7eadbb1-f227-4dc2-b019-af7e0c68ea4f.png)

And ***delete*** or ***comment out*** rest of the lines with ***“ctrl +/”***.

4.	Scroll down to **Run()** method and add the below 2 lines to send ***“*idn?”*** SCPI command and print a response of idn command into the log window.
```python
idn = self.vna._io.ScpiQuery("*idn?")
```
![image](https://user-images.githubusercontent.com/91975559/176618207-aaf7492a-6b2f-464d-97f0-6a6be5d31bf8.png)

```python
self.Info(idn)
```
![image](https://user-images.githubusercontent.com/91975559/176618324-6f6e7e99-0fb8-4c47-9b49-d5959a78581c.png)

