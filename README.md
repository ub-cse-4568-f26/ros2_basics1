# ROS2 Basics 1

### Deadline: September 05, 2025 11:59 p.m.

***This activity is to be done as individuals, not with partners nor with teams.***

### How to get started →

To complete this activity, begin by reading this entire writeup, making sure you have a good understanding of it. Take note of the topics in the [resources](#Resources) section as your questions might already be covered there. Go through all the deliverables and if you have any queries make sure to get them resolved by consulting the instruction staff

---
## Introduction


Robot Operating System or ROS is a middleware that makes it convenient to develop robotics applications. The core concepts in ROS include packages, ros2 nodes, ros2 topics and  communication between nodes using the publisher-subscriber paradigm. The video lectures introduced these concepts theoretically and this activity focuses the practical implementation through a follow along code demo. 

---
## Activity Information


### Objectives

- Learn how to create a ros2 package
- Understand the concepts of nodes and topics
- Learn how to write a publisher in ROS2
- Learn how to a write a subscriber in ROS2
- Learn how to write a launch file

### Resources

- How to create a ros2 package using `ros2 pkg create`: [https://docs.ros.org/en/foxy/Tutorials/Beginner-Client-Libraries/Creating-Your-First-ROS2-Package.html](https://docs.ros.org/en/foxy/Tutorials/Beginner-Client-Libraries/Creating-Your-First-ROS2-Package.html)
- How to write a simple publisher and subscriber: [https://docs.ros.org/en/foxy/Tutorials/Beginner-Client-Libraries/Writing-A-Simple-Cpp-Publisher-And-Subscriber.html](https://docs.ros.org/en/foxy/Tutorials/Beginner-Client-Libraries/Writing-A-Simple-Cpp-Publisher-And-Subscriber.html)
- Writing a launch file: [https://docs.ros.org/en/foxy/Tutorials/Intermediate/Launch/Creating-Launch-Files.html](https://docs.ros.org/en/foxy/Tutorials/Intermediate/Launch/Creating-Launch-Files.html)
### Requirements

- Your package should build when dropped into a workspace and compiled using `colcon build --packages-select <package_name>`. If it does not you automatically get a zero.
- Your launch file should execute and launch your nodes.
- Your package, nodes and launch files should follow the naming convention, if your code does not work due to the filenames being incorrect, you will receive zero points.

### What we provide

- Detailed instructions on the file names/ conventions to followed
- Detailed instructions on the deliverables
- Expected output

### What to submit

```bash
ros2_basics1
└── ros2_basics_1 
    ├── launch
    │   └── ros2_basics_1.launch.py # Your launch file for activity 2
    ├── ros2_basics_1
    │   └── simple_pub.py # Your ROS publisher for part 2
    │   └── simple_sub.py # Your ROS subscriber for for part 4
    ├── package.xml
    ├── setup.py
    ├── setup.cfg
    ├──
    ├── resource
    |    └── ros2_basics_1
    └── test
```

*Please make sure you adhere to the structure above, if your package doesn’t match it the grader will invariably give you a **zero***

### Grading considerations

- **Late submissions:** Carefully review the course policies on submission and late assignments. Verify before the deadline that you have submitted the correct version.
- **Environment, names, and types:** You are required to adhere to the names and types of the functions and modules specified in the release code. Otherwise, your solution will receive minimal credit.

---
## Part 1 : Create a catkin package


### Steps: 
1. Clone this repository inside the src directory of your catkin workspace
2. Create a ros2 package with the same name as the cloned repository by running the `ros2 pkg create` command from the src directory of your ros2 workspace adding `ament_python` as your build_type. This should create the files that are necessary to convert your cloned repository into a ros2 package

### Expected Output:

You should now have the following directory structure in your ros2 workspace

```bash
ros2_ws
├── build
├── install
├── log
└── src
└── ros2_basics1
    └── README.md
    └── ros2_basics_1 
        ├── launch
        │   └── activity2.launch.py # Your launch file for activity 2
        ├── ros2_basics_1
        │   └── simple_pub.py # Your ROS publisher for part 2
        │   └── simple_sub.py # Your ROS subscriber for for part 3
        │   └── republisher.py # Your ROS subscriber for for part 4
        ├── package.xml
        ├── setup.py
        ├── setup.cfg
        ├──
        ├── resource
        |    └── ros2_basics_1
        └── test
```

---
## Part 2 : Simple Publisher


In this part, you will write a simple ROS publisher that will publish an incrementing count using the `std_msgs/Int32` on the topic `/count` . Your publisher should start counting from 0 and continue publishing till the process is manually terminated.  

### Details:

1. Write your publisher in a python file named `simple_pub.py` 
2. Name your ros2 node `activity2_pub` 
3. Build you package with `colcon build` and source your ros2 workspace
4. Run your publisher node using `ros2 run` 

### Note:

1. You can test if your publisher is working using the `ros2 topic echo` CLI tool
2. Make sure that the topic name is correct and there are no typos. This is a common source of errors
<!-- 3. If your node does not launch use the `chmod` terminal command to make your python file executable -->

### Expected Output:

Your publisher should publish incrementing integers on the topic `/count` using the `std_msgs/Int32` message 

---
## Part 3 : Simple Subscriber

In this part, you will write a simple ROS2 subscriber that will subscribe to the messages published by your publisher from part 2 on the topic `/count`. Your subscriber should unpack the value of the count and print it out using rclpy.Node’s logger. This subscriber should run till it is manually terminated

### Details:

1. Write your subscriber in a python file named `simple_sub.py` 
2. Name your ros2 node `activity2_sub` 
3. Build you package with `colcon build` and source your ros2 workspace
4. Run your publisher and subscribers in different terminals using `ros2 run` 

### Note:

1. Make sure that your publisher is running when you test your subscriber
2. Make sure that the topic name is correct and there are no typos. This is a common source of errors
<!-- 3.  If your node does not launch use the `chmod` terminal command to make your python file executable -->

### Expected Output:

Your subscriber should print the integer that it received on the terminal 

---
## Part 4 : Republisher

In this part, you will write a *single rosnode* *that has both, a publisher and a subscriber*. Your subscriber should subscribe to the topic `/count` , same as your subscriber from part 3 but instead of printing the value it should square it and pass it to the publisher. Your publisher should publish this value on the topic `/squared_count` using the message type `std_msgs/Int32` like your publisher from part 2

### Details:

1. Write your republisher in a python file named `republisher.py` 
2. Name your ros2 node `activity2_repub` 
3. Build you package with `colcon build` and source your catkin workspace
4. Run your publisher, subscriber and republisher  in different terminals using `ros2 run` 

### Note:

1. Make sure that your publisher from part 2 is running when you test this node
2. Make sure that the topic name is correct and there are no typos. This is a common source of errors
<!-- 3. If your node does not launch use the `chmod` terminal command to make your python file executable -->

### Expected Output:

Your republisher should square the values that the original publisher is publishing and publish them on a new topic. Using rostopic echo on this topic should return squared values 

---
## Part 5 : Launch files

By now, you must have realized that launching these nodes one by one using ros2 run is a tedious process. This is where the ROS2 launch files and ros2 launch utility come into picture. `ros2 launch` allows us to write one python file which specifics all the nodes to be run and runs them all for us. 

For part 5, you must write a launch file that launches the nodes you wrote in parts 2, 3 and 4 using a single launch file. 

### Details:

1. Create a directory named `launch` inside your ros2 package
2. Create a launch file named `activity2.launch.py` inside the launch directory
3. Write your launch file such that it launches all your nodes from parts 2, 3 and 4

### Expected Output:

Using the command `ros2 launch ros2_basics_1 activity2.launch.py` should run all your nodes

---
# Submission and Assessment

Submit using the Github upload feature on [autolab](https://autolab.cse.buffalo.edu)

**Note: Make sure your code complies to all instructions, especially the naming conventions. Failure to comply will result in zero credit**

You will be graded on the following. Penalties are listed under each point, absolute values, w.r.t assignment total.

    Part 1 (create a catkin package) [20%]
        If your package doesnt follow the specified conventions but builds [-10%]
    Part 2 (Simple Publisher) [20%]
        If your publisher publishes to the wrong topic or your node doesn’t run (we will use rosrun to check) [-20%]
    Part 3 (Simple Subscriber) [20%]
        If your subscriber does not print out the correct values or doesn't run [-20%]
    Part 4 (Republisher) [20%]
        If your republisher publishes to the wrong topic or your node doesn’t run (we will use rosrun to check) [-20%]
    Part 5 (Launch Files) [20%]
        If your launch file only runs one/two nodes out of the three [-10%]
        If your launch file doesn’t launch any nodes/ doesnt work[-20%]

