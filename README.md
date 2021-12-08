# Robotic_Arm
Articulated arm project, by Lucy Gray and Gaby D'Alessio

## Table_of_Contents
* [Planning](#Planning)
  * [Brainstorming and Iterations](#Brainstorming)
  * [Materials](#Materials)
  * [Criteria and Constraints](#Criteria_and_Constraints)
  * [Schedule](#Schedule)

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
* CAD completely finished by mid-January
* Around mid January, have box set up for hand assembly and have preliminary wiring done
* Assemble hand, fit with strings, and attach to servo late January

Gaby - main CAD; Lucy - code, secondary CAD

[Back to Table of Contents](#Table_of_Contents)
