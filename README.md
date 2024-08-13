<!-- <p align="center">
  <a href="" rel="noopener">
 <img width=200px height=200px src="https://i.imgur.com/6wj0hh6.jpg" alt="Project logo"></a>
</p> -->

<h1 align="center">reference_signal_srvs</h1>

<div align="center">

  [![GitHub issues](https://img.shields.io/github/issues/leggedrobotics-usp/reference_signal_srvs)](https://github.com/leggedrobotics-usp/reference_signal_srvs/issues)
  ![GitHub pull requests](https://img.shields.io/github/issues-pr/leggedrobotics-usp/reference_signal_srvs)
  [![GitHub forks](https://img.shields.io/github/forks/leggedrobotics-usp/reference_signal_srvs)](https://github.com/leggedrobotics-usp/reference_signal_srvs/network)
  [![GitHub stars](https://img.shields.io/github/stars/leggedrobotics-usp/reference_signal_srvs)](https://github.com/leggedrobotics-usp/reference_signal_srvs/stargazers)
  [![GitHub license](https://img.shields.io/github/license/leggedrobotics-usp/reference_signal_srvs)](https://github.com/leggedrobotics-usp/reference_signal_srvs/blob/main/LICENSE)

</div>

---

<p align="center"> ROS1 service definitions for reference signal generation
    <br>
</p>

ROS version | Branch
-- | --
ROS2 | [ros2](https://github.com/leggedrobotics-usp/reference_signal_srvs/tree/ros2)
ROS1 | [ros1](https://github.com/leggedrobotics-usp/reference_signal_srvs/tree/ros1)

## 📝 Table of Contents
- [About](#about)
- [Getting Started](#getting_started)
- [Usage](#usage)
- [Feature requests](#feature_requests)
- [Contributing](#contributing)
- [Author](#author)

## 🧐 About <a name = "about"></a>
This repo contains the service definitions for reference signal generations, required by the [reference_signal_generator](https://github.com/leggedrobotics-usp/reference_signal_generator) package.

## 🏁 Getting Started <a name = "getting_started"></a>
This repo is a ROS1 package (catkin) dedicated to service interface definitions. Learn more about ROS services in the [ROS documentation](https://wiki.ros.org/ROS/Tutorials/UnderstandingServicesParams).

### 🛠 Prerequisites

- A ROS1 workspace (catkin)
    - See [this tutorial](https://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment) to learn how to create your own workspace.

### 💻 Installing

As mentioned above, this repo is a standard ROS package. Thus, you simply have to clone it inside your workspace's **src** directory, making sure to use the **ros1** branch.

```bash
cd <path_to_your_ros_ws>/src
git clone -b ros1 https://github.com/leggedrobotics-usp/reference_signal_srvs.git
```

Then, use **catkin** to build (**catkin build** example shown, **catkin_make** also usable)

```bash
cd <path_to_your_ros_ws>
catkin build reference_signal_srvs
```

## 🎈 Usage <a name="usage"></a>

Service message definitions (.srv files) are not directly usable by themselves. The [reference_signal_generator](https://github.com/leggedrobotics-usp/reference_signal_generator) package uses this repo's definitions to spawn services that trigger actual signal generation in a chosen ROS topic.

You can also use the definitions of this repository to build other packages related to control signal generation.

The goal of this service is to trigger a reference signal with an arbitrary number of inputs (or DOFs). Thus, most arguments are array-type. They must all have the same length.

### Request arguments

- ``string[] signal_type`` String array describing the desired signal type for each input. Supported values are ``"step", "ramp", "sine", "square", "triangle", "sawtooth", "chirp"``.
- ``float64[] initial_value`` Numeric array describing the initial value for each input. Applies to Step and Ramp signals.
- ``float64[] final_value`` Numeric array describing the final value for each input. Applies to Step signals.
- ``float64[] start_time`` Numeric array describing the time (seconds) at which each input will be started. Applies to all signals.
- ``float64[] end_time`` Numeric array describing the time (seconds) at which each input will stop. Applies to all signals. Supports ``inf`` for continuous publishing.
- ``float64[] slope`` Numeric array describing the slope for each input. Applies to Ramp signals.
- ``float64[] offset`` Numeric array describing the DC offset for each input. Applies to Sine, Square, Triangle, Sawtooth and Chirp signals.
- ``float64[] amplitude`` Numeric array describing the total amplitude for each input. Applies to Sine, Square, Triangle, Sawtooth and Chirp signals.
- ``float64[] frequency`` Numeric array describing the waveform frequency (Hz) for each input. Applies to Sine, Square, Triangle and Sawtooth signals.
- ``float64[] phase`` Numeric array describing the phase shift (degrees) for each input. Applies to Sine, Square, Triangle, Sawtooth and Chirp signals.
- ``float64[] initial_frequency`` Numeric array describing the frequency (Hz) at ``t = start_time`` for each input. Applies to Chirp signals.
- ``float64[] target_frequency`` Numeric array describing the frequency (Hz) at ``t = target_time`` for each input. Applies to Chirp signals.
- ``float64[] target_time`` Numeric array describing the time (seconds) at which the chirp frequency will linearly reach ``target_frequency`` for each input. Applies to Chirp Signals.
- ``float64 publish_rate`` Number describing the rate (Hz) at which the topic will publish the reference signal.
- ``float64 total_time`` Number describing the total duration (seconds) of all reference signals. Supports ``inf`` for continuous publishing.

Please note that, although some inputs are specific for a certain type of signal, all arrays must be supplied with the same length during the service call, filling the unused fields with any arbitrary value.

### Response arguments

- ``success`` Boolean output to indicate whether or not the reference signal was successfully published.
- ``message`` String to give more detailed information about the service call.

## 🔋 Feature requests <a name="feature_requests"></a>

Want another type of reference signal that demands an additional argument or a different type of service definition? Open an *Enhancement* issue describing it.

## 🤝 Contributing <a name="contributing"></a>

- Fork the repo
  - <https://github.com/leggedrobotics-usp/reference_signal_srvs/fork>
- Check out a new branch based and name it to what you intend to do:
  - ````bash
    git checkout -b BRANCH_NAME
    ````
- Commit your changes
  - Please provide a git message that explains what you've done;
  - Commit to the forked repository.
    ````bash
    git commit -m "A short and relevant message"
    ````
- Push to the branch
  - ````bash
    git push origin BRANCH_NAME
    ````
- Make a pull request!

## ✍️ Author <a name = "author"></a>

<a href="https://github.com/Vtn21">
 <img style="border-radius: 50%;" src="https://avatars.githubusercontent.com/u/13922299?s=460&u=2e2554bb02cc92028e5cba651b04459afd3c84fd&v=4" width="100px;" alt=""/>
 <br />
 <sub><b>Victor T. N. 🤖</b></sub></a>

Made with ❤️ by [@Vtn21](https://github.com/Vtn21)

<!-- [![Gmail Badge](https://img.shields.io/badge/-victor.noppeney@usp.br-c14438?style=flat-square&logo=Gmail&logoColor=white&link=mailto:victor.noppeney@usp.br)](mailto:victor.noppeney@usp.br) -->

<!-- -  - Idea & Initial work -->

<!-- See also the list of [contributors](https://github.com/kylelobo/The-Documentation-Compendium/contributors) who participated in this project. -->