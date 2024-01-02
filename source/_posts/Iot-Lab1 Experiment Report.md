---
title: IoT-Lab1 Experiment Report
date: 2023-10-26 19：40
tags: 
    - learning
categories: 
    - Iot  
    - homework
---  
# IoT -Lab1 Experiment Report  

## What is IoT?  

The Internet of things(IoT) describes the network of physical objects—“things”—that are embedded with sensors, software, and other technologies for the purpose of connecting and exchanging data with other devices and systems over the internet.Totally,IoT means that connect things(like everday objects)to the Internet for the purpose to record and change the data to help our life to be eaiser and better.  
  

## Why is IoT so important?  
Reference from <https://www.oracle.com/internet-of-things/what-is-iot/>  

---

## Counterfit  

![20231026155352](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231026155352.png)  

## What is Counterfit?  
As you can see above--CounterFit -Fake IoT Hardware,Counterfit is a is a tool that is designed to fake various IoT hardware components, such as LEDs, buttons, temperature sensors and the like, that you can then access from IoT device code running on your computer rather than on an IoT device.  
    
Counterfit is made of two parts:  
* The CounterFit app - this is a web app run locally where you can connect fake sensors and actuators to your virtual hardware
* Shims - these are libraries that fake popular hardware APIs so you can take code that runs against well known hardware and run it against the CounterFit app.

Tips:The Counterfit app is just a web app run locally where you can connect fake sensors and actuators to your virtual hardware,but not an app which can provide you the fake sensors to do your virtual hardware.It means that after downloading Counterfit,you can not use it directly.And you should put the sensors you need and set up the environment and so on.  

---  
## Homework Requirement  
This is the homework requirment:  
The URL where the requirement is located:<https://github.com/CounterFit-IoT/CounterFit>
![20231026184041](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231026184041.png)  

---
## Install and run the app(Counterfit):  
* Install the Counterfit app:
* ``` sh
  pip install counterfit
  ```  
* ```
    counterfit
  ```  
We can see that the app is launching and listening for web requests on port 5000.  
![20231026185041](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231026185041.png)  
So now we can open a web browser to start adding virtual sensors and actuators to our project.  
Let us to open a web browser requests on port 5000:  
* Enter http://localhost:5000/  

![20231026185659](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231026185659.png)  
## If you want to run the app on another port  
you just need to set the `--port` when you run the app  
* ```
  counterfit --port 5050
  ```  
It means run the app on port 5050  

---

We can see that the upper right corner shows we "Disconnected".That's because we just run the Counterfit app but not to connect it with your device(computer).  
So we can write an "app.py" to connect to Counterfit just like it.  
![20231026190805](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231026190805.png)  
We can browse the "Samples".It provide us the sensors and anything we need.In the app.py in the folder named "light-sensor-controlled-led",we can see how to work the LEDs.  
![20231026191425](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231026191425.png)  
We can see that it also includes Counterfit-connection.So we run the app.py in the other file.  
* ``` 
  python3 app.py 
  ```  

Back to the web browser,we can see that it is "Connected"(Because we run the Counterfit-connection).  
![20231026191805](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231026191805.png)  
Now we can create sensor(light) and actuator(LED).  
![20231026191930](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231026191930.png)  
Read the app.py,we can see that LED will turn off when the value of sensor more than 200.  
* Set a value less than 200 to the sensor and set a actuator(LED)  
![20231026192203](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231026192203.png)  
And run the app.py again.  
* ```
  python3 app.py
  ```  
After that,we can see the LED turn on  
![20231026192555](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231026192555.png)  
If you want to change the color of LED,you just need to pick another color and push the button "Set".Then the color is changed.  
![20231026192738](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231026192738.png)  
## At this point,the homework is completed  
After completing this homework,I want to say something same as the word in the introduction of IoT-IoT is really fun!And I can learn many things from this homework!!