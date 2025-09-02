# ROS2 Basics 1

### Deadline: September 05, 2025 11:59 p.m.

***This activity is to be done as individuals, not with partners nor with teams.***

### How to get started →

To complete this activity, begin by reading this entire writeup, making sure you have a good understanding of it. Take note of the topics in the [resources](#Resources) section as your questions might already be covered there. Go through all the deliverables and if you have any queries make sure to get them resolved by consulting the instruction staff

---
## Introduction


Robot Operating System or ROS is a middleware that makes it convenient to develop robotics applications. The core concepts in ROS2 include packages, ros2 nodes, ros2 topics and  communication between nodes using the publisher-subscriber paradigm. The video lectures introduced these concepts theoretically and this activity focuses the practical implementation through a follow along code demo. 

---
## Activity Information


### Objectives

- Learn how to create a ros2 package
- Understand the concepts of nodes and topics
- Learn how to write a publisher in ROS2
- Learn how to a write a subscriber in ROS2

### Resources

- How to create a ros2 package using `ros2 pkg create`: [https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Creating-Your-First-ROS2-Package.html](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Creating-Your-First-ROS2-Package.html)
- How to write a simple publisher and subscriber: [https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Writing-A-Simple-Py-Publisher-And-Subscriber.html#](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Writing-A-Simple-Py-Publisher-And-Subscriber.html#)

### Requirements

- Your package should build when dropped into a workspace and compiled using `colcon build --packages-select <package_name>`. If it does not you automatically get a zero.
- Your nodes should be able to run using the run command
- Your package, nodes and launch files should follow the naming convention, if your code does not work due to the filenames being incorrect, you will receive zero points.

### What we provide

- Detailed instructions on the file names/ conventions to followed
- Detailed instructions on the deliverables
- Expected output

### What to submit

```
    ros2_basics1
        ├── README.md
        └── ros2_basics_pub_sub
            ├── package.xml
            ├── resource
            │   └── ros2_basics_pub_sub
            ├── ros2_basics_pub_sub
            │   ├── __init__.py
            │   ├── pub_node.py
            │   └── sub_node.py
            ├── setup.cfg
            ├── setup.py
            └── test
                ├── test_copyright.py
                ├── test_flake8.py
                └── test_pep257.py
```

*Please make sure you adhere to the structure above, if your package doesn’t match it the grader will invariably give you a **zero***

### Grading considerations

- **Late submissions:** Carefully review the course policies on submission and late assignments. Verify before the deadline that you have submitted the correct version.
- **Environment, names, and types:** You are required to adhere to the names and types of the functions and modules specified in the release code. Otherwise, your solution will receive minimal credit.

---
## Part 1 : Create a ros2 package


### Steps: 
1. Clone this repository inside the src directory of your ros2 workspace
2. Create a ros2 package with the name `ros2_basics_pub_sub` by running the `ros2 pkg create` command from the src directory of your ros2 workspace, adding `ament_python` as your build_type and `pub_node` as the node name. This should create the files that are necessary to convert your cloned repository into a ros2 package

### Expected Output:

You should now have the following directory structure in your ros2 workspace

```
ros2_ws
├── build
├── install
├── log
└── src
└── ros2_basics1
    ├── README.md
    └── ros2_basics_pub_sub
        ├── package.xml
        ├── resource
        │   └── ros2_basics_pub_sub
        ├── ros2_basics_pub_sub
        │   ├── __init__.py
        │   └── pub_node.py
        ├── setup.cfg
        ├── setup.py
        └── test
            ├── test_copyright.py
            ├── test_flake8.py
            └── test_pep257.py
```

---
## Part 2 : Simple Publisher


In this part, you will write a simple ROS2 publisher that will publish an incrementing count using the `std_msgs/Int32` on the topic `/count` at the rate `10`. Your publisher should start counting from 0 and continue publishing till the process is manually terminated.  

### Details:

1. Write your publisher in a python file named `pub_node.py` 
2. Name your ros2 node `pub_node`
3. Build your package with `colcon build --packages-select` and source your ros2 workspace
4. Run your publisher node using `ros2 run` 

### Note:

1. You can test if your publisher is working using the `ros2 topic echo` CLI tool
2. Make sure that the topic name is correct and there are no typos. This is a common source of errors

### Expected Output:

Your publisher should publish incrementing integers on the topic `/count` using the `std_msgs/Int32` message 

---
## Part 3 : Simple Subscriber

In this part, you will write a simple ROS2 subscriber that will subscribe to the messages published by your publisher from part 2 on the topic `/count`. Your subscriber should unpack the value of the count and print it out using rclpy.Node’s logger. This subscriber should run till it is manually terminated

### Details:

1. Write your subscriber in a python file named `sub_node.py` 
2. Name your ros2 node `sub_node`
3. Add the executable mapping section for `sub_node` in `setup.py`
3. Build you package with `colcon build --packages-select` and source your ros2 workspace
4. Run your publisher and subscribers in different terminals using `ros2 run` 

### Note:

1. Make sure that your publisher is running when you test your subscriber
2. Make sure that the topic name is correct and there are no typos. This is a common source of errors


### Expected Output:

Final Structure:

```
    ros2_ws
    ├── build
    ├── install
    ├── log
    └── src
    └── ros2_basics1
        ├── README.md
        └── ros2_basics_pub_sub
            ├── package.xml
            ├── resource
            │   └── ros2_basics_pub_sub
            ├── ros2_basics_pub_sub
            │   ├── __init__.py
            │   ├── pub_node.py
            │   └── sub_node.py
            ├── setup.cfg
            ├── setup.py
            └── test
                ├── test_copyright.py
                ├── test_flake8.py
                └── test_pep257.py
```

Your subscriber should print the integer that it received on the terminal 

---
# Submission and Assessment

Submit using the Github upload feature on [autolab](https://autolab.cse.buffalo.edu)

**Note: Make sure your code complies to all instructions, especially the naming conventions. Failure to comply will result in zero credit**

You will be graded on the following. Penalties are listed under each point, absolute values, w.r.t assignment total.

    Part 1 (create a ros2 package) [30%]
        If your package doesnt follow the specified conventions but builds [-30%]
    Part 2 (Simple Publisher) [35%]
        If your publisher publishes to the wrong topic or your node doesn’t run (we will use ros2 run to check) [-35%]
    Part 3 (Simple Subscriber) [35%]
        If your subscriber does not print out the correct values or doesn't run [-35%]

