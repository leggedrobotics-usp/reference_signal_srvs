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

<p align="center"> ROS2 service definitions for reference signal generation
    <br>
</p>

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
This repo is a ROS2 package (ament_cmake) dedicated to service interface definitions. Learn more about ROS2 services in the [ROS2 documentation](https://docs.ros.org/en/rolling/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Services/Understanding-ROS2-Services.html).

### 🛠 Prerequisites

- A ROS2 workspace (colcon)
    - See [this tutorial](https://docs.ros.org/en/rolling/Tutorials/Beginner-Client-Libraries/Creating-A-Workspace/Creating-A-Workspace.html) to learn how to create your own workspace.

### 💻 Installing

As mentioned above, this repo is a standard ROS2 package. Thus, you simply have to clone it inside your workspace's **src** directory.

```bash
cd <path_to_your_ros2_ws>/src
git clone https://github.com/leggedrobotics-usp/reference_signal_srvs.git
```

Then, use **colcon** to build.

```bash
cd <path_to_your_ros2_ws>
colcon build --symlink-install
```

## 🎈 Usage <a name="usage"></a>

Service message definitions (.srv files) are not directly usable by themselves. The [reference_signal_generator](https://github.com/leggedrobotics-usp/reference_signal_generator) package uses this repo's definitions to spawn services that trigger actual signal generation in a chosen ROS2 topic.

You can also use the definitions of this repository to build other packages related to control signal generation.

### Common arguments for all interfaces

- Request arguments
    - ``publish_rate`` Rate (Hz) to publish the reference signal (defaults to 1.0).
    - ``total_time`` Total time (seconds) to publish the reference signal. Publisher will automatically stop after this period. Set to ``inf`` to publish indefinitely.

- Response arguments
    - ``success`` Boolean output to indicate whether or not the reference signal was successfully published.
    - ``message`` String to give more detailed information about the service call.

### Request arguments specific to each interface

- **Step**
    - ``initial_value`` Starting value of the step signal (defaults to 0.0).
    - ``final_value`` Final value of the step signal (defaults to 1.0).
    - ``step_time`` Time (seconds) to trigger the step signal (defaults to 0.0).
- **Ramp**
    - ``initial_value`` Starting value of the ramp signal (defaults to 0.0).
    - ``slope`` Growth rate of the ramp signal (defaults to 1.0).
    - ``start_time`` Time (seconds) to trigger the ramp signal (defaults to 0.0).
- **Wave** (applies to square, sine, sawtooth and triangle waves)
    - ``offset`` DC offset applied to the waveform (defaults to 0.0).
    - ``amplitude`` Total amplitude of the waveform (defaults to 1.0).
    - ``frequency`` Frequency (Hz) of the waveform (defaults to 1.0).
- **Chirp** (linear frequency-swept cosine)
    - ``offset`` DC offset applied to the waveform (defaults to 0.0).
    - ``amplitude`` Total amplitude of the waveform (defaults to 1.0).
    - ``initial_frequency`` Frequency (Hz) at time zero (defaults to 1.0).
    - ``target_frequency`` Frequency (Hz) at ``target_time`` (defaults to 1.0)
    - ``target_time`` Time (seconds) corresponding to ``target_frequency`` (defaults to 1.0)

## 🔋 Feature requests <a name="feature_requests"></a>

Want another type of reference signal that demands a different type of service definition? Open an *Enhancement* issue describing it.

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
