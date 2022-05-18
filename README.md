# Robotic_Arm
Articulated arm project, by [Lucy Gray](https://github.com/lgray52) and [Gaby D'Alessio](https://github.com/gdaless20)

## Table_of_Contents
* [Planning](#Planning)
  * [Brainstorming and Iterations](#Brainstorming) 
  * [Materials](#Materials)
  * [Criteria and Constraints](#Criteria_and_Constraints)
  * [Schedule](#Schedule)
* [Problems and Solutions](#Problems_and_Solutions)
* [Final](#Final)

## Planning

**Goal of Project:** Our robotic arm will use an atriculated arm design that mimics human movement in order to pick up a can by extending and flexing each joint individually.  

### Brainstorming

#### Possible Solutions and Choice
For this project, we chose to use an articulated arm design out of the six basic types of robotic arms (cartesian, SCARA, cylindrical, delta, polar and articulated) because an articulated arm uses joints to move to it's desired destination. Since part of our original goal was to design a hand that would have the capabilities listed above, we did not consider a different use for an articulated arm, but rather moved through a variety of ideas about the function of the hand and the joints.

#### Base ideas and First Iteration
<img src="evidence/preliminary_design.png" alt="preliminary design for robotic hand" height="300">
The preliminary design for this project was pretty preliminary. The articulated arm-with-hand design we had decided on, but we were unsure how the servos might be used to make the joints of the fingers, wrist, and elbow move. We had an idea that we wanted each joint to be able to be individually controlled to go up and down, and that using buttons, one for each up or down movement, would be the best way to achieve control of this individual motion.

#### Second Iteration
<img src="evidence/second_iteration.png" alt="second iteration of arm plan" height="300">
For the second iteration of the plan, we expanded on preliminary ideas and decided on placing the servos in the box. We decided to connect them to each section of each digit using wire or string, and using one string with it's middle tied to connection points on each digit and it's ends attached to either side of a servo horn to create back and forth rotation by pulling backwards or forwards with the rotation of the servo. We decided to use one servo per joint, except for the wrist and elbow which would use two, or 18 servos in total (32 buttons for 16 total joints). We anticpate this might be a problem when it comes to number of servos programming programs can support, and are planning to use a second board if necessary. 

#### Final Plan
<img src="evidence/final_plan.png" alt="final iteration of design for robotic hand" height="300">
The final plan included some fairly major changes from our first design solutions. We decided to orient the hand on the side of the box so it would be actually able to grab things on a surface, and to use t-joints rather than ball joints in all of the joints in the hand. We also decided to use elastic to pull the digits back up to their original position, which we figured out we were able to do while doing a proof of concept for the motion of the joints with a servo, meaning that we will be able to eliminate the complications of trying to have one string pull two different ways and the corresponding mechanics. 


### Materials
* 3D Printing Material
* Elastic
* Fishing line
* Servos
* Metro board
* Wood
* Wires
* Acrylic
* Buttons
* Glue
* Screws


### Criteria_and_Constraints

#### Criteria
* This hand should be able to grasp an object that can fit in a hand
* It should resemble a human hand in size, shape, and function

#### Constraints
* Ability of boards available in the lab to run the target number of servos
* Target finish date 1st of February
* Mr. Helmstetter says Gaby is a safety concern; also knives and soldering
* Modelling the hand - how joints will work and move


### Schedule

**Finish Goal 01 Feb**

Rough Timeline:
* Finish code & box design by winter break
* CAD completely finished by mid-January (snow day delay 1 week - CAD completed by late Jan)
* Around mid January, have box set up for hand assembly and have preliminary wiring done (Gaby had COVID, so the CAD needed to be pushed back significantly)
* Assemble hand, fit with strings, and attach to servo late January 

Gaby - main CAD; Lucy - code, secondary CAD

[Back to Table of Contents](#Table_of_Contents)


## Problems_and_Solutions

### General:
* It became aparent very quickly that a nomenclature was needed to keep variables for servos, angles, and buttons separate. Each finger is a value 1-5: thumb is 1, pointer 2, middle , ring 4, and pinky 5 -- the wrist and elbow joints are 0. The next number would be the joint in the finger: 1 for the base joint where the digit meets the palm, the metacarpophalangeal, 2 for the middle, the proximal interphalangeal, and 3 for the top joint at the tip, the distal interphalangeal. The elbow is 0-1 and the wrist is 0-2.
* The whole project was slightly delayed by snow and Gaby unfortunately having COVID, both of which majorly disrupted our schedule but were obviously unavoidable and unintended. To be fair, the schedule was a bit ambitious from the get go, but our project timeline was delayed probably three weeks by that combination. Additionally, with the allocation of class time to module work, we ended up not having class time to finish the project. 

### Coding:
* Running 16 servos with one board
  * The first challenge was figuring out what exactly could solve this problem. The solution ended up being [this](https://www.adafruit.com/product/815) servo driver, capable of running 16 servos at one time. This driver came with a CircuitPython library for ease of coding.
  * Or so I thought. The CircuitPython library included some problematically named files and code examples with different coding grammar, but eventually worked. Until it didn't. After break, all of the libraries refused to collaborate with one another because some of the libraries had been updated to .py files rather than .mpy files. This meant they took up too much space because they were text files and not binary, and they would not run the .mpy files because they had been updated to CircuitPython 7. This took several classes to figure out, but I was able to update them all to CircuitPython 7 and .mpy files. Here is a picture of the correct files needed (they are all CircuitPython version 7). 
  <img src="evidence/correct_files.PNG" alt="files needed" height="200">
  
  wiring for servo board: <img src="evidence/servo_driver_wiring.png" alt="servo driver wiring" height="300">

* Running 32 buttons with one board
  * This was an equal problem to the servos, however the solution was slightly simpler. Using an analog_in function, the electrical value of a pin can be returned and printed. Using this idea, by placing resistors between buttons to reduce the amount of electricity flowing through the chain of buttons, a single analog pin can read the differing frequencies, and this can be used to run several buttons (I got up to 11 easily differentiable values). This is [Mr. Helmstetter's](https://github.com/helmstk1) idea. I ended up having to use 4.7kΩ resistors in order to have enough resistance to reduce the value significantly enough to easily differentiate the values produced.
  <img src="evidence/button_arm_wiring.PNG" alt="analog button wiring" height="300">
* Wiring note - make sure the batteries are oriented right. It *will* save you 30 minutes, or potentially a battery exploding on you!
* For simplicity, Mr. Helmstetter asked that I arranged variables into arrays instead of naming them according to the system, so they are named a little differently in the code. An explanation of arrays is in the code itself.

### OnShape:
* The first problem we had was finding/building a hand with enough digits for our project. For simplicity's sake, we chose [this](https://github.com/NemanjaBabic/AnimatronicRoboticHand) hand by NemanjaBabic. We decided to reduce the size before printing it, otherwise it would have been nearly a foot long from the base of the wrist to the top joint, but this did cause some problems with the holes for the strings because they were too narrow. This added a little bit more time to our construction process, as we had to physically widen the tunnels. As it turned out, the finger tip parts also didn't print with holes, and eventually we decided it was worth our time and effort to simply reprint the hand, scaled to 75% instead of 50%. The channels are manageable at this size, and the elastic is easier to insert into the hooks.
* The box also was modified to include a plate for our many, many servos, a button panel, and an opening for the hand. 

[Back to Table of Contents](#Table_of_Contents)


## Final

[Jump to CAD](#CAD)

### Code
```python
import board
from time import sleep
from analogio import AnalogIn
from adafruit_servokit import ServoKit

# do NOT need the pca library stuff

analog_A1 = AnalogIn(board.A1)
analog_A2 = AnalogIn(board.A2)
analog_A3 = AnalogIn(board.A3)

def get_voltage(pin):  # read analog pin 1 to use different buttons
    return (pin.value*3.3) / 65536

kit = ServoKit(channels=16)  # set up servo driver

# angles for different servos
angle01 = 0  # elbow
angle02 = 0  # wrist

thumb = [0, 0]

"""
An array essentially allows multiple variables in a system to be easily grouped. By
creating a list using the notation a = [#, #, #], a value is assigned to each variable
corresponding with the initial variable name. Each of these values can be called in
the code by calling them by the overall name and the number which they appear in the
list - for example, if you wanted to call a variable from the list entitled "a," and you
wanted the second one in the list, you would call it a[2].

"""

pointer = [0, 0, 0]  # array

middle = [0, 0, 0]

ring = [0, 0, 0]

pinky = [0, 0, 0]

while True:
    if get_voltage(analog_A1) > 3.17 and angle01 < 174:
        # so it doesn't go over angle limits
        angle01 = angle01 + 6  # have to adjust angle here, not inline
        kit.servo[0].angle = angle01
        # print("elbow up")  these took up too much space, so I needed to comment them out, but kept them in the code to check
        # print(get_voltage(analog_A1), "\t", angle01)

    elif get_voltage(analog_A1) > 2.45 and angle01 >= 6:
        # use elif to not have it run the above
        angle01 = angle01 - 6
        kit.servo[0].angle = angle01
        # print("elbow down")
        # print(get_voltage(analog_A1), "\t", angle01)

    elif get_voltage(analog_A1) > 2.00 and angle02 < 174:
        angle02 = angle02 + 6
        kit.servo[1].angle = angle02
        # print("wrist up")
        # print(get_voltage(analog_A1), "\t", angle02)

    elif get_voltage(analog_A1) > 1.69 and angle02 >= 6:
        angle02 = angle02 - 6
        kit.servo[1].angle = angle02
        # print("wrist down")
        # print(get_voltage(analog_A1), "\t", angle02)

    elif get_voltage(analog_A1) > 1.47 and thumb[0] < 174:
        thumb[0] = thumb[0] + 6
        kit.servo[2].angle = thumb[0]
        # print("thumb base up")
        # print(get_voltage(analog_A1), "\t", thumb[0])

    elif get_voltage(analog_A1) > 1.30 and thumb[0] > 6:
        thumb[0] = thumb[0] - 6
        kit.servo[2].angle = thumb[0]
        # print("thumb base down")
        # print(get_voltage(analog_A1), "\t", thumb[0])

    elif get_voltage(analog_A1) > 1.16 and thumb[1] < 174:
        thumb[1] = thumb[1] + 6
        kit.servo[3].angle = thumb[1]
        # print("thumb top up")
        # print(get_voltage(analog_A1), "\t", thumb[1])

    elif get_voltage(analog_A1) > 1.06 and thumb[1] > 6:
        thumb[1] = thumb[1] - 6
        kit.servo[3].angle = thumb[1]
        # print("thumb top down")
        # print(get_voltage(analog_A1), "\t", thumb[1])
        
    elif get_voltage(analog_A1) > 0.97 and pointer[0] < 174:
        pointer[0] = pointer[0] + 6
        kit.servo[4].angle = pointer[0]
        # print("pointer base up")
        # print(get_voltage(analog_A1), "\t", pointer[0])

    elif get_voltage(analog_A1) > 0.89 and pointer[0] > 6:
        pointer[0] = pointer[0] - 6
        kit.servo[4].angle = pointer[0]
        # print("pointer base down")
        # print(get_voltage(analog_A1), "\t", pointer[0])

    elif get_voltage(analog_A1) > 0.83 and pointer[1] < 174:
        pointer[1] = pointer[1] + 6
        kit.servo[5].angle = pointer[1]
        # print("pointer middle up")
        # print(get_voltage(analog_A1), "\t", pointer[1])

    elif get_voltage(analog_A2) > 3.17 and pointer[1] > 6:
        pointer[1] = pointer[1] - 6
        kit.servo[5].angle = pointer[1]
        # print("pointer middle down")
        # print(get_voltage(analog_A2), "\t", pointer[1])

    elif get_voltage(analog_A2) > 2.45 and pointer[2] < 174:
        pointer[2] = pointer[2] + 6
        kit.servo[6].angle = pointer[2]
        # print("pointer top up")
        # print(get_voltage(analog_A2), "\t", pointer[2])

    elif get_voltage(analog_A2) > 2.00 and pointer[2] > 6:
        pointer[2] = pointer[2] - 6
        kit.servo[6].angle = pointer[2]
        # print("pointer top down")
        # print(get_voltage(analog_A2), "\t", pointer[2])

    elif get_voltage(analog_A2) > 1.69 and middle[0] < 174:
        middle[0] = middle[0] + 6
        kit.servo[7].angle = middle[0]
        # print("middle base up")
        # print(get_voltage(analog_A2), "\t", middle[0])

    elif get_voltage(analog_A2) > 1.47 and middle[0] > 6:
        middle[0] = middle[0] - 6
        kit.servo[7].angle = middle[0]
        # print("middle base down")
        # print(get_voltage(analog_A2), "\t", middle[0])

    elif get_voltage(analog_A2) > 1.30 and middle[1] < 174:
        middle[1] = middle[1] + 6
        kit.servo[8].angle = middle[1]
        # print("middle middle up")
        # print(get_voltage(analog_A2), "\t", middle[1])

    elif get_voltage(analog_A2) > 1.16 and middle[1] > 6:
        middle[1] = middle[1] - 6
        kit.servo[8].angle = middle[1]
        # print("middle middle down")
        # print(get_voltage(analog_A2), "\t", middle[1])

    elif get_voltage(analog_A2) > 1.06 and middle[2] < 174:
        middle[2] = middle[2] + 6
        kit.servo[9].angle = middle[2]
        # print("middle top up")
        # print(get_voltage(analog_A2), "\t", middle[2])

    elif get_voltage(analog_A2) > 0.97 and middle[2] > 6:
        middle[2] = middle[2] - 6
        kit.servo[9].angle = middle[2]
        # print("middle top down")
        # print(get_voltage(analog_A2), "\t", middle[2])

    elif get_voltage(analog_A2) > 0.89 and ring[0] < 174:
        ring[0] = ring[0] + 6
        kit.servo[10].angle = ring[0]
        # print("ring base up")
        # print(get_voltage(analog_A2), "\t", ring[0])

    elif get_voltage(analog_A2) > 0.83 and ring[0] > 6:
        ring[0] = ring[0] - 6
        kit.servo[10].angle = ring[0]
        # print("ring base down")
        # print(get_voltage(analog_A2), "\t", ring[0])

    elif get_voltage(analog_A3) > 3.17 and ring[1] < 174:
        ring[1] = ring[1] + 6
        kit.servo[11].angle = ring[1]
        # print("ring middle up")
        # print(get_voltage(analog_A3), "\t", ring[1])

    elif get_voltage(analog_A3) > 2.45 and ring[1] > 6:
        ring[1] = ring[1] - 6
        kit.servo[11].angle = ring[1]
        # print("ring middle down")
        # print(get_voltage(analog_A3), "\t", ring[1])

    elif get_voltage(analog_A3) > 2.00 and ring[2] < 174:
        ring[2] = ring[2] + 6
        kit.servo[12].angle = ring[2]
        # print("ring top up")
        # print(get_voltage(analog_A3), "\t", ring[2])

    elif get_voltage(analog_A3) > 1.69 and ring[2] > 6:
        ring[2] = ring[2] - 6
        kit.servo[12].angle = ring[2]
        # print("ring top down")
        # print(get_voltage(analog_A3), "\t", ring[2])

    elif get_voltage(analog_A3) > 1.47 and pinky[0] < 174:
        pinky[0] = pinky[0] + 6
        kit.servo[13].angle = pinky[0]
        # print("pinky base up")
        # print(get_voltage(analog_A3), "\t", pinky[0])

    elif get_voltage(analog_A3) > 1.30 and pinky[0] > 6:
        pinky[0] = pinky[0] - 6
        kit.servo[13].angle = pinky[0]
        # print("pinky base down")
        # print(get_voltage(analog_A3), "\t", pinky[0])

    elif get_voltage(analog_A3) > 1.16 and pinky[1] < 174:
        pinky[1] = pinky[1] + 6
        kit.servo[14].angle = pinky[1]
        # print("pinky middle up")
        # print(get_voltage(analog_A3), "\t", pinky[1])

    elif get_voltage(analog_A3) > 1.06 and pinky[1] > 6:
        pinky[1] = pinky[1] - 6
        kit.servo[14].angle = pinky[1]
        # print("pinky middle down")
        # print(get_voltage(analog_A3), "\t", pinky[1])

    elif get_voltage(analog_A3) > 0.97 and pinky[2] < 174:
        pinky[2] = pinky[2] + 6
        kit.servo[15].angle = pinky[2]
        # print("pinky top up")
        # print(get_voltage(analog_A3), "\t", pinky[2])

    elif get_voltage(analog_A3) > 0.89 and pinky[2] > 6:
        pinky[2] = pinky[2] - 6
        kit.servo[15].angle = pinky[2]
        # print("pinky top down")
        # print(get_voltage(analog_A3), "\t", pinky[2])

    elif get_voltage(analog_A1) < 0.83:
        print(get_voltage(analog_A1))

    else:
        print(get_voltage(analog_A1))

    sleep(0.1)
```

### CAD

#### Hand
<img src="evidence/cad_1.PNG" alt="hand angle 1" height="300"> <img src="evidence/cad_2.PNG" alt="hand angle 2" height="300"> <img src="evidence/cad_3.PNG" alt="hand angle 3" height="300">
credit: [NemanjaBabic](https://github.com/NemanjaBabic/AnimatronicRoboticHand)

#### Box
<img src="evidence/n_box_1.PNG" alt="box angle one, with hand" height="300"> <img src="evidence/n_box_2.PNG" alt="box top view open" height="300"> <img src="evidence/n_box_3.PNG" alt="box dimetric angle 1" height="300"> <img src="evidence/n_box_4.PNG" alt="box dimetriuc angle 2" height="300">

__Button board arrangement__: 

<img src="evidence/button_board_diagram.png" alt="diagram for the button panel by joint" height="300">


#### Final Pictures


[Back to Table of Contents](#Table_of_Contents)
