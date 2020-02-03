# CompiledHive
NAU Capstone 2018/19 CompiledHive Git Repository Managed Through GitHub

# Introduction 
The application space for drones is growing ever larger. Whether they are programmed to deliver packages to doorsteps or send medical supplies into a war-torn country, drones are becoming ever more useful. Drones, while initially designed for military use, have recently become widespread in the commercial market. Currently, most drones are controlled by a single user to achieve a single task, such as filming a landscape from a bird’s eye perspective or moving an object for a long distance. With the advancement of control and navigation systems, drones will be able to complete a myriad of new tasks. A swarm of drones can move in formations to create images in the sky. A delivery company can create an autonomous fleet to carry packages to and from a warehouse. However, to accomplish these complex tasks, drones must be researched to make their movements precise. Dr. Truong Nghiem, this project’s client, is at the forefront of this research.
 
Dr. Nghiem works in the Intelligent Control Systems (ICONS) Laboratory at Northern Arizona University (NAU). Dr. Nghiem has over 10 years of experience researching the control and optimization of various technologies using computer science and machine learning. Having published over 25 peer-reviewed papers, Dr. Nghiem has extensive experience with scientific computing and simulation. Dr. Ngheim’s work has spanned numerous domains, including energy systems for buildings, smart grids, embedded real-time control systems, and verification of control systems. Having been recently hired by the School of Informatics, Computing, and Cyber Systems (SICCS) at NAU, he is continuing his research in intelligent control of numerous systems.
 
Dr. Nghiem researches various topics in the SICCS department, which include researching smart energy systems and safe autonomous systems. One particular topic is researching how swarms of drones are controlled autonomously. The eventual goal of this research is to find the optimal way to perform numerous concurrent tasks using the drone swarm. However, the current workflow Dr. Nghiem uses is cumbersome.

Currently, Dr. Nghiem's’ system uses 8 sensors placed in a room. These sensors communicate with any active drones in the system, each drone being controlled through the stacking of two technologies, Robot Operating System (ROS) and CrazyFlie. To use this system, a Python script instructing the flight path or coordinate locations for each drone must be embedded into the system hierarchy.  Not only does writing a new script for each flight take time, but file paths in the existing hierarchy must be changed to point at the new file, and each drone wished to be flown must be connected manually. These problems will be alleviated through the construction of a graphical user interface (GUI) to simplify the system and drone setup.

This application was designed to connect with ROS, alleviating the need to manually connect. The application was designed to take user inputs to set up all necessary details to set a flight path, initiate the flight, display the flight in real time, and log all requested details. The logged details include the drones connected, their flights, the imported code or the input coordinates, and all significant events that occurred during the flight. The final project is a Linux application that includes the following attributes and capabilities:
 
Allow any user trained in the system to connect up to 7 drones
Allow the programming of any number of flight paths and simulated obstacles
Initiate the flight process through the GUI
Display the locations of each active drone on a 3D visualization
Log important events and the locations of each drone during a single flight
Detect any crashes or erroneous behavior and end all active flights

With this application, Dr. Nghiem’s research process will be significantly shortened. Not only did he save time in developing the GUI himself, but the setup time for any flight path he or any research assistant wishes to design much quicker than the previous system. However to make the application useful to Dr. Nghiem, the following development process was used.



# Process Overview 

The team adopted an agile-like development process. Each week on Tuesday the team held a meeting where each member discussed what they had completed and what needed to be worked on. Then as a group, each member would be assigned new tasks to complete for the next week. Additionally, each meeting the overall project progress would be analyzed. Each Wednesday the team would update Dr. Nghiem on the project’s progress, and each Thursday the team would update the team mentor. To develop the application, subsections of the projects were developed simultaneously and merged together upon completion. 

The following tools were utilized by the group during development:
GitHub
GitHub was chosen as the version control system. 
Slack
Slack was utilized for communication between the team
Google Drive
Google Drive was selected for document management

The group consisted of four members, each taking on some positions
Adam: Recorder, Coder
Documented all meetings, main developer of the backend, simulator, and the visualization

Alexis: Release Manager, Coder
Ensured all code followed the coding standards, main developer and designer of the GUI

Austin: Architect, Coder
Managed the architecture of the system, helped develop the backend and the simulator, lead the effort to fix the current drone system

Gavin: Team Lead, Customer Communicator, Coder
Lead and organized team, managed communication with Dr. Nghiem, helped develop the GUI, backend and visualization



# Requirements
To develop the product Dr. Nghiem required, an extensive requirements acquisition phase was held. 
The team met with Dr. Nghiem on multiple occasions to fully understand the project. During each meeting Dr. Nghiem was questioned on the features of the product. Afterwards the team would re-analyze and re-write the requirements. After multiple meetings, the requirements met Dr. Nghiem’s specifications. In tandem with client meetings, the team did individual research on the technologies used in the current system. This research, along with client meetings, culminated in the following list of requirements.

The following list of functional requirements detail exactly what the end product achieves:
The application connects with ROS to control the drone flight system
The application displays a graphical user interface to interact with the drone system
The system  accepts user designed flight paths
The GUI displays a 3D visualization of flight routine information in real time
The application logs: 
All connected drones
Drone locations at a user specified interval
The flight path imported by the user
The coordinates entered by the user
Erroneous behavior
Starting/Stopping of the flight
The system detects and handle crashes and disconnected drones and handle flights accordingly

Not only does the application meet the functionality requirements, but it also performs to the standards that Dr. Nghiem wishes:
The 3D Visualization updates at least 10 times per second.
The Visualization  has a latency of fewer than 0.5 seconds.
The user can import a pre-programmed flight within 30 seconds.
The user can input a path with 10 points in under 2 minutes.
Any active flights are terminated within 30 seconds of the user’s command.
The user only needs to change the ROS files less than 10% of the time.

The application was built to run on Dr. Nghiem’s Linux machine running Ubuntu 16.04, which is located within the ICONS lab. It also must interface with the current drone flight system, which is a hybrid between the drone flight system CrazyFlie 2.0, and the Kinetic version of ROS.

# Architecture and Implementation
The application’s architecture includes 3 main modules. The control module, which is the central hub for the application, the GUI module, the user’s main entry point into the application, and the flight script, which is modified and passed into CrazyFlie/ROS to control the drones. This system is loosely based on the Model View Controller model. However, focus on the view portion of the model is less important to the overall product, and is relegated to being a part of the control portion. The Control Node gathers the user data from the GUI and initializes the flights. It sends the CrazyFlie /ROS simulator flight destinations that were either calculated from the flight script, or that the user input. The simulator sends back the current locations of each drone connected to the system. The diagram below details these main modules.


		Diagram 1: Detailed architectural diagram of the main components of the planned solution


#### The GUI Module:
The GUI module is  front facing portion of the application. All necessary input will be input on this screen. The user will: 

Input which drones will be active during the next flight 
Import all user-written flight paths
Connect drones to flight paths
Add coordinates to remaining drones
Input dimensions for simulated objects
Toggle which information is to be displayed on the 3D visualization
Toggle which information is to be logged
Initiate the flight

Once the flight is initiated, a new screen displays a 3D visualization with all the information requested by the user. If left at default it will show the drone, sensor, and object locations. This screen also notifies the user of any major events, including errors, starting/stopping a flight, and collisions with simulated obstacles. 

#### The Control Module:
The control module will be the main portion of the application. This program will initiate the GUI portion of the application, and modify all the user input to integrate with the flight path. The control module will tell the flight path which drones to control, include all coordinates or the flight path, and place the modified file in the correct directory for the ROS/CrazyFlie backend to fly. Once placed, the control module will initiate the flight and start receiving all locational data and wait for erroneous behavior. All coordinates and erroneous behavior will be passed into the visualization portion of the GUI. In case of errors or user input from the GUI, the control module will also initiate a landing sequence to override the current flight. 

#### The Flight Path:
The flight path will be a rough outline of a regular flight path. It will include areas to be filled in by the control module . The first is where all connected drones will be placed. The second will be for the user-written flight path to be inserted. This section includes a try/catch block to stop any buggy code before initiating a flight. The third section is used to implement the coordinates the user input from the GUI.

#### CrazyFlie/ROS:
CrazyFlie and ROS are part of the original system, and control the drone flights once a flight path has been input. CrazyFlie tells the drones their next location, and ROS detects the drone locations and erroneous behavior and sends the data to the control module.


#### Main Communication:
The central hub for communication is the control node. This monitors all coordinates being sent between each different node. After the GUI node is closed, all the user input information is collected by the control node, and used to format the flight path. The control node then generates the current destination from each drone. It does so by getting the next destination from the flight path file, or by checking the next manually inputted coordinate. It sends these destinations to CrazyFlie/Ros. CrazyFlie/Ros then move each drone closer to their destination and send the current coordinates back to the control node. The control node sends these new coordinates to the log file and the 3D visualization node. Using the new coordinates, the control node then generates new current destinations.
### Module and Interface Descriptions
#### The GUI Module
The GUI will consist of several different classes. Each class will be run and monitored by a main class.
#### WidgetGallery Class
The WidgetGallery class is the main controlling unit of the main GUI. It initializes all the storage methods for user input. It also opens the main window that will open other windows created by the other classes. The startFlight method will close the main window and send all need information to start the flight.

        Diagram 2: Main GUI WIndow 
#### WidgetDrone Class
The WidgetDroneclass will allow the user to connect up to seven drones. The user any either connect the drone to or flight file or add a list of coordinates. The user also needs to add a ID and drone name. 

The connect drones to flight path class will have two public methods. The corClick method will add the drone ID to a list keyed by the flight path file name in a global dictionary. It will also remove the drone from the global removeClick list. The remDrone method will remove the drone from the dictionary and add it to the removeClick list.

        Diagram 3: Drone Setting WIndow 
#### WidgetObs Class
The WidgetObs class allows the user to add simulated obstacles to the flight area for the drones to navigate around. This class will consist of:
Two coordinate entry areas, one for each corner of the simulated cube
An enter a  name of the object
An ‘Add’ Button to add the object to flight area 
A ‘cancel’ button to cancel adding and object 

The add object class will have two public methods. The addObject method will store both sets of coordinates to the global dictionary objects.

        Diagram 4: Obstacle Setting WIndow
#### toggle_vis_window Class
The ToggleVis class will allow the user to determine which elements will be displayed in the visualization. Each element will have an on/off switch, determining if that element will be shown during the flight. The elements include:
The visualization as a whole
The drone locations
The calculated drone paths
The actual drone paths
The sensor locations
The simulated objects
A ‘save’ button

The toggle visualized elements class will have one public method. Upon pressing the save  button, the saveVisConfig method will save the toggled elements in a file to be referenced during the flight. The base default will start with every element turned on.

        Diagram 5: Toggle Visualization Setting WIndow
#### toggle_log_window Class
The Toggle_Log class will work similarly to the previous class, however instead of toggling the elements shown in the visualization, it toggles the elements logged post flight. The elements are:
The active drones
The drone locations
The frequency at which the drone locations are logged
The simulated objects
The flight paths being flown
The coordinates entered
Major events that occured
A ‘save’ button

The toggle logged data class only as a single public method. Upon the user pressing the ‘save’ button, the selected preferences will be saved in a log config file. If the frequency text area is empty or does not include a positive integer, the module will remain open and the user will be notified.

       Diagram 6: Toggle Log File  Setting WIndow
#### 3D Visualization Class
The 3D visualization module will receive the coordinates from the control node and display elements based on the config file. The visualization will include one element, the visualization itself.

The 3D visualization module will have two public method. The startVisualization method will initiate the visualization with the default location of the drones sensors and objects. The updateVisualization method will take in the new drone coordinates, clear the current image and redraw  the new image. It will also calculate the flown path from the previous drone location and the current. Both methods will check the config file first to determine which elements to display. 

      Diagram 7: Visualization WIndow
#### Display_Events Class
The display events module has a text area will display all major events as they are received by the control node. The display events class updates major events method and updates the text area. 
#### The Control Node
The control node is the main portion of the backend of the application. It controls the GUI node and modifies the flight paths. Additionally, it handles all communication between the application and the ROS/CrazyFlie system. This functionality is handled by one class, the Control_Node class. The UML diagram is depicted in the following diagram.

			Diagram 8: UML of the Control_Node Class
The control node class includes 4 public methods. The __init__ method will be called when the application is first opened. This method will initialize all variables and start the GUI. Once activated, the program will continuously call the GUI’s guiActive function. When the guiActive returns false, that signals the user has finished inputting all inputs for the flight. The program will then call the GUI’s getData method to receive all the flight path data that is entered by the user.

After the false flag has been found, the constructFP method will be called. This functions only goal is to modify the flight path module to fly with the users specifications. If any errors occur during this process, the method will return an integer with the corresponding error value.

Once the flight path has been constructed, the initiateFP method will be called. This method first initiates the GUI’s visualization phase with the startVisualization method, giving the visualization the initial location values for each drone and obstacle. The method then directs the ROS/CrazyFlie system to start a flight with the newly modified flight path. Afterwards, it waits for input from the system. Any new drone locations will be passed to the visualization, any major events passed to the display_events window. Any details gathered will be logged depending on the logConfig. If the flight ends as intended, this method closes the GUI and returns the int value to signal a restart for a new flight. If an error occurs or the user pressed the ‘End Flight’ button, then the int returned will signal to run the endFP method.

The endFP method will initiate a new flight path designating all connected drones to return to their starting positions. In the case a drone cannot return, the path will terminate after 30 seconds. Afterwards, this method will terminate the GUI. If the initiateFP method signals to restart for a new flight, or the endFP method has terminated, the __init__ method will resume control and restart the program.
#### The Flight Path
The flight path will be a skeletal class. It will include three sections to implement the user’s own flight path. The first section will be for inputting the drones the user wishes to be connected. The second section will be to assign the user input coordinates to the requested drones. The third will be to import the users written flight path. This section will be wrapped in a try/catch block, so when run any buggy code will be caught by a generic exception. This exception thrown will be sent to the control node to be logged. Since the flight path will be given to the ROS/CrazyFlie system, no public methods are present.
#### Implementation
Due to hardware issues, instead of implementing this system with the CrazyFlie/ROS system a simulator was designed to emulate it. However, both the simulator and the CrazyFlie/ROS system rely on sending coordinates through ROS nodes. This led to the architecture of the control node and the simulator to be based on a subsumption based model. The simulator followed an actuator and sensor architecture to follow the same properties that exist in the real system that uses this architecture to move the drone positions with radio frequencies. The flight path file was originally intended to be created each time, but in the final build the backend only interprets the flight path function the user imported and handles the setup process internally.
# Testing
Before being released, the application will be put through numerous tests. Many of the individual methods within the application will be tested using Unit tests. Any method that takes in and modifies information will be  analyzed to assure the data is returned as expected. The application also relies on multiple nodes communicating with each other to function, so extensive Integration testing will be held to confirm each link functions correctly. Lastly, multiple third parties unfamiliar with the system will be asked to initiate various tasks using the system. After attaining their feedback, the front end will be re-designed. With the suite of tests, the application will be fully functional and ready to be released. 

Communication between the different nodes is a core aspect of the application, and does not work  if this communication is broken. To prevent these issues, the bulk of testing will be to confirm all necessary data is being passed correctly. Additionally, the front end of the application will be used by multiple researches, many of which will not have much coding experience. Holding extensive usability tests will be imperative to make the user experience accessible to all potential users. While Unit testing will be held, they will not be as rigorous as the previous two. Many of the methods will be hard to test individually, as many communicate with other nodes. Additionally, many methods are used to display and open features on the GUI, which are also difficult to test with traditional Unit tests. Therefore, only methods that modify data will be tested. To assure full correctness, Unit tests, Integration tests, and Usability tests will be held.

Unit Testing
The application being tested is written entirely using Python 2.7, so PyUnit will be the framework used for the Unit testing regime. Many of the methods found in the application rely on communicating with other nodes to function, and will not be tested by Unit testing. Many other methods are called to display information, and will also not be tested. The remaining methods all take some form of input, modify, and return it. 

In the GUI.py file, numerous methods take input in the form of a string, and validate that the user has typed in a number in the valid range. These methods will be tested to assure that the input is interpreted correctly, and modified into floats when expected. The GUI also contains methods that gather the data the user input and either outputs or returns it. These methods will be tested by setting the data structures to a certain states, and analyzing the method’s output. The GUI contains methods for adding and removing user input, but does not to error checking in this portion. For instance, the user will be able to import a python file to be used as a flight path. However, if this file does not contain a flight path, it will be caught in runtime by the backend. 

The simulator.py file contains multiple methods, each modifying a list of drone positions. These methods will each be tested by generating a series of current and next coordinates, and testing each function modifies the respective lists correctly. Since the simulator can handle up to 7 drones, the tests will include correct and incorrect coordinate files for each possible permutation of drones.

The backend.py file contains methods that check drone positions and send and receive them from other nodes. The drone position validity methods will tested by being given both valid and invalid drone locations, and analyzing the results. The backend also supports up to 7 drones, so each test suite will include testing coordinates for each permutation of drones.

The visros.py file only contains methods to initiate and display data onto a 3D graph. Therefore, the methods will not be tested by Unit tests.

The following table details one unit test from the testing suite:
Add Coordinate to Drone Path
Entering numbers between the valid coordinate ranges
A number between -4 and 4 for X and Y values, a number between 0 and 8 for Z values
(2, 2, 8),
(-2,4,7)
The coordinate will be added to the coordinate dictionary 


Integration Testing
The developed application relies heavily on communication between different nodes. The simulator node must communicate back and forth with the backend node. The backend node must communicate back and forth with the monitor node. If any of these links become severed, the application as a whole ceases to work. Therefore, each of these connections will be extensively tested.

The simulator relies on two links with the backend node. The simulator must receive drone coordinates from the backend node, and the backend must receive updated drone locations from the simulator node. To test these connections, drone coordinates will be sent between the two nodes. The coordinates will be analyzed before and after being sent to ensure correctness.

The backend relies on many links with the monitor node to function properly. Once receiving coordinates from the simulator, the backend must send them to the 3D visualization to be displayed. Additionally, the backend must send the simulated obstacles to the visualization as well. The backend must also send any major events that occur, such as drone errors or warnings, to a message display in the monitor node. The message display also includes a button that when pressed will send a signal to the backend to stop an in process flight. Each link must be tested thoroughly to ensure all the data is displayed correctly.

The following table details one integration test from the testing suite:

Sending Obstacle Dimensions between nodes
A list of at least one pair of coordinates that make up the obstacle
The obstacle or obstacles to be transferred accurately between nodes


Usability Testing
This research tool will be used by numerous researchers with varying technical experience. If the researchers are unable to use the application, the research process will take longer than Dr. Nghiem would wish for. To make the application as usable as possible, extensive tests will be held to analyze the design of the GUI.

To make the interface as usable as possible, two different types of tests will be held. The first test will include showing Dr. Nghiem the current interface after multiple revisions. The interface is already designed with his wishes in mind, so after multiple revisions it will meet his expectations. To hold this test, the following steps will be followed:
Step through the current iteration of the application
Adding multiple drones
Adding multiple flight paths
Adding multiple coordinates
Adding multiple obstacles
Starting and ending flights
Garner feedback from Dr. Nghiem
Revise current layout
Repeat steps 1 through 4 until Dr. Nghiem is satisfied
However, Dr. Nghiem will not be the only person using this application, so further testing will be required.

To increase the usability for researchers new to using the tool, usage tests will be held. An individual not apart of the development team will be tasked with holding demos for various third parties. This individual will ask the tester to perform a series of tasks using application, asking for feedback at each step. Once these tests are completed, the feedback will be gathered and weighed into the redesign process. The tasks to be asked are as follows:
Add 7 drones to the system
Remove a drone, then re-add it
Import 2 flight paths into the system
Remove a flight path, then re add it
Connect 3 drones to one flight path, and add 1 to the other
Remove a drone from the first flight path, and add it to the second
Add 5 coordinates to the remaining 3 drones’ flight paths
Remove 1 coordinate from each drone’s flight path
Add 3 simulated obstacles, name 1
Remove a simulated obstacle
Start the flight, and end it after 10 seconds


During the tests, these questions will be asked by the test giver:
Is it clear where and how to connect a drone?
How can you remove a drone?
Is it clear where and how to import a flight path?
How can you remove a flight path?
Is it clear where and how to connect a drone to a flight path?
How can you tell which drones are connected to a flight path?
Is it clear where to add or remove coordinates to a drone’s flight path?
Is it clear where to add a simulated obstacle?
Where do you name a simulated obstacle?
Where are the drones on the visualization?
Where are the obstacles on the visualization?
How do you stop the flight?

After weighing the feedback from these questions, the front end will be redesigned to make the application user friendly.

To select a good sample of testers, the following requirements will be used:
Family members will not be selected
Half of the testers will be non CS friends or classmates
25% of the testers will be CS students currently in Capstone
The remaining testers will be Junior CS students or lower
Each test will include a single proctor and a single tester. The CS students will be found in the ACM room or in other classes the members of the development team are in. 
These tests will occur over the two weeks before UGRADS presentations. The GUI will be shown to Dr. Nghiem for the first time at the beginning of the two weeks. After the initial redesign, the usage tests will be held with at least 5 individuals unfamiliar with the software. By the end of the first week. This redesign will be shown to Dr. Nghiem for further feedback. The third redesign will be completed by the end of the second week. 

After performing usability tests during the design phase, the GUI interface was altered. From Dr. Nghiem’s initial comments, the input areas on the GUI were sectioned off and labeled. After garnering feedback from other students, the positions of these sections were modified.

# Project Timeline
This section outlines the full schedule of Capstone in the Spring semester of 2019. It is split into phases that are described below. The schedule is displayed in an easily understandable Gantt chart in diagram 9.



### Phase Descriptions
#### Restoration Phase
At the beginning of the project, a portion of the current system was non-functional. The first goal was  to install and update the drone system and fix any erroneous software or machinery.  Currently, the software is still not functional.
#### Software Design Phase
The software design phase was to analyze all requirements of the project and design each part of the planned solutions to fulfil the requirements. This phase was concluded after writing the software design document.
#### GUI Development Phase
The GUI development phase was to take the design from the previous phase and implement it with Python and PyQt4. This phase was completed within the week of the software design document submission.
3D Visualization Development Phase
The 3D visualization development phase is to develop the visualization that will be integrated into the main GUI. 
#### Backend Development Phase
The backend phase was to develop the control module that handles all of the data communication between nodes. This phase took a bit longer to complete than we hoped as the team faced issues with packet loss in ROS and had to refactor the file.
#### Error and Crash Detection Phase
The error and crash detection phase will be to design the necessary classes to receive error notifications from ROS and land all the drones safely. 
#### Software Testing Phase
The software testing phase will take the application from the alpha phase to the beta. It will take place just after Spring break and will be used to debug and test all aspects of the project.
#### Deployment Phase
The deployment phase will be preparing for the end of the semester by finishing the website and getting ready for the Capstone presentation at UGRADS.

# Future Work
While the time it takes for Dr. Nghiem to research drone swarms will already be shortened due to this application, it can still be improved further. In future renditions of this software, the user will be able to initiate the system by only opening a single application, and when a flight is over, the application will terminate automatically. Currently if the user wishes to manually enter a flight path, they must enter each coordinate for the drone to fly to. In a future revision, the user will be able to draw the flight path in an input on the GUI, and the system will interpret it. Lastly, when the CrazyFlie/ROS system is functional, the application will be integrated with it.

