---
layout: page
title: Where Is My Stuff?
description: Custom few-shot object detector for visually impaired people
img: assets/img/humanware/stellartrek-in-hand.jpg
importance: 1
category: Work
related_publications: false
---

## Overview

"Where Is My Stuff?" is an innovative project developed during my 16-month tenure at [HumanWare](https://www.humanware.com/en-canada/home){:target="_blank"}, a company dedicated to creating devices that enhance the daily lives of visually impaired individuals. This project aimed to integrate advanced object detection capabilities into HumanWare's [StellarTrek](https://store.humanware.com/hca/stellartrek.html){:target="_blank"} device, a GPS-equipped camera system initially designed for navigation assistance.

The primary goal was to develop a feature analogous to "FaceID" for iPhones, but tailored for locating personal objects. Unlike generic object detection, this system needed to identify specific items belonging to the user, such as their unique keys, wallet, or glasses. The challenge was to create a solution that could run efficiently on the StellarTrek's Snapdragon 660 processor while addressing two key aspects:

1. Enabling visually impaired users to easily capture support images of their objects.
2. Implementing a robust detection pipeline for locating registered objects using few-shot images.

---

## Architecture

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/humanware/wims_diagram.drawio.svg" title="WIMS Diagram Architecture" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Architecture diagram of the "Where Is My Stuff?" feature.
</div>

### 1. User-Friendly Object Registration

To overcome the challenges faced by visually impaired users in representing the 3D world and feeling the camera angles, we developed an intuitive registration process:

1. Users are instructed to touch the object first, creating a physical connection between the camera and the item.
2. A detection model aims to detect overlapping hands and objects in the frame.
3. The user interface provides step-by-step guidance through the capturing process based on real-time model predictions.
4. Multiple images (5 to 10) are captured for each object to create a comprehensive support set.

<div class="row justify-content-center">
    <div class="col-md-8 text-center">
        {% include video.liquid path="assets/video/humanware/object_registration.mp4" class="img-fluid rounded z-depth-1" controls=true %}
    </div>
</div>
<div class="caption">
    Demonstration of the object registration process.
</div>

### 2. Custom Detection Pipeline

The heart of the "Where Is My Stuff?" feature is a custom-built detection pipeline designed to operate within the performance constraints of the StellarTrek device:

1. **Region Proposal Network (RPN)**: A YOLOv8-nano object detector identifies potential object candidates in the scene.
2. **Embedding Network**: A MobileNetV3-small backbone generates lower-dimension embeddings to represent objects, trained using a triplet loss approach for better object discrimination.
3. **Classification Model**: A One-Class SVM model trained on support-set object embeddings performs anomaly detection, distinguishing between registered objects and other items.
4. **Single-Object Tracking (SOT)**: Once an object is stably detected, the NanoTrackV3 model guides the user to its location using an audio feedback system.

<div class="row justify-content-center">
    <div class="col-md-8 text-center">
        {% include video.liquid path="assets/video/humanware/object_detection.mp4" class="img-fluid rounded z-depth-1" controls=true %}
    </div>
</div>
<div class="caption">
    Demonstration of the few-shot object detection process.
</div>

---

## Key Features

- **Few-shot learning**: Ability to recognize specific objects from a small set of support images.
- **On-device processing**: All computations run locally on the StellarTrek's Snapdragon 660 processor.
- **User-friendly interface**: Tailored for visually impaired users, with audio guidance and feedback.
- **Adaptive object recognition**: Learns and identifies user-specific items rather than generic object categories.
- **Real-time tracking**: Guides users to their objects using directional audio cues.

This project demonstrates the potential of combining computer vision, machine learning, and user-centered design to create impactful solutions for individuals with visual impairments.