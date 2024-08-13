---
layout: page
title: Water Pong Game
description: Interactive robot vs. human game
img: assets/img/water_pong/cover.png
importance: 2
category: University
related_publications: false
---

This project develops "Water Pong," a game where a robotic arm and a human compete by throwing balls into a triangular cup arrangement. It serves as a course project for [KEN3300 - Project 3-1](https://curriculum.maastrichtuniversity.nl/meta/465275/project-3-1){:target="_blank"}. It was conducted in collaboration with my classmates, [Loris Podevyn](https://github.com/lorispodevyn){:target="_blank"}, [Ivan Poliakov](https://github.com/M1v1savva){:target="_blank"} and [Bunyamin Thijssen](https://github.com/Wisekik){:target="_blank"}.

### Computer Vision

The computer vision system implemented in this project encompasses a full pipeline using advanced techniques for real-time object detection and tracking. The system utilizes the Hough Circle Transform to detect cups by leveraging the high contrast between the cups and the green background of the playing setup. Additionally, a YOLOv5 detection model is employed to identify reference QR-codes and track the playing ball. The main objective of the computer vision system is to ascertain the approximate coordinates of the robot's targets (cups) on the board using the QR-codes as reference points. It also tracks the game's score by monitoring the ball's trajectory and detecting when a cup has been successfully hit or missed. This tracking capability is essential for providing feedback to the robotic system, facilitating updates to the lookup table that tunes the parameters of the robotic arm.

### Robotic Throwing Arm

A comprehensive lookup table was developed to manage the configurations of the robotic arm's movements for precise targeting and ball-throwing accuracy. This table contains detailed motor configurations for each target, which are dynamically updated in real-time based on the game's progress. The lookup table algorithmically determines the angle and delay for each throw using interpolation between predefined settings. Moreover, the system incorporates a feedback loop that adjusts the motor delay incrementally if the initial throw does not hit the target, thereby refining the robot's accuracy over successive attempts.

For more details, check out the project [report](https://clem2507.github.io/assets/pdf/WaterPongReport.pdf){:target="_blank"} and the code in our [repository](https://github.com/M1v1savva/juice-pong){:target="_blank"}.

### Demo

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/water_pong/computer_vision_demo.mp4" class="img-fluid rounded z-depth-1" controls=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/water_pong/robot_throw_demo.mp4" class="img-fluid rounded z-depth-1" controls=true %}
    </div>
</div>