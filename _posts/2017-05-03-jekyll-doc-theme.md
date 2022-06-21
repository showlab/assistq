---
title:  "AssistQ Dataset"
---


In each data folder, there are several files: 

#### (1) video.mp4 / video.mov: instructional video;

#### (2) script.txt: the video script with the timestamp. 


        0:00:00-0:00:04 How to start, stop, start and stop airfryer? Turn the temperature knob anticlockwise to 120 degrees. 

        0:00:04-0:00:07 Turn the time knob clockwise to 10 minutes. 

        ...

The meaning of the annotation (from left to right): start time-end time: text script. The time format follows HH:MM:SS.

#### (3) buttons.csv: button bounding-box annotation. 
 

        button1,362,86,185,72,airfryer-user.jpg,960,1280

        button2,378,330,185,170,airfryer-user.jpg,960,1280

        ...

The meaning of the annotation (from left to right): button name, top-left x, top-left y, width, height, image filename, image width, image height. 

#### (4) images/ folder: the folder contains the image files mentioned in buttons.csv.

Question-Answer Annotations: we aggregate the annotations of all data samples in train.json. A video can have `multiple questions`, and each question needs to be answered in multiple steps and multiple modalities. Specifically, each data index (e.g., coffeemachine_d2stw, diffuser_lxcd4) corresponds to a list that contains multiple question-answer pairs:

        {'aircon_utr3b': [{...}, {...}, {...}, {...}, {...}, {...}], 'airfryer_gye82': [{...}, {...}, {...}, {...}, {...}], 'airfryer_pe2j7': [{...}, {...}, {...}, {...}, {...}, {...}, {...}, {...}, {...}], 'airfryer_w9rzm': [{...}, {...}, {...}, {...}, {...}, {...}, {...}, {...}, {...}, ...], 'bicycle_g8h94': [{...}, {...}, {...}], ...}

For each data sample, there are multiple question-answer pairs:

    [ 

        { 

        "question": "How to bake a cake at 120 degrees for 15 minutes?", 

        "answers": [

        ["Turn <button1> clockwise", "Turn <button1> anticlockwise", "Turn <button2> clockwise", "Turn <button2> anticlockwise to 0 minutes", "Turn <button1> to 200 degrees", "Turn <button1> to 120 degrees", "Turn <button1> to 180 degrees", "Turn <button2> clockwise to 3 minutes", "Turn <button2> clockwise to 10 minutes", "Turn <button2> clockwise to 15 minutes"], 

        ["Turn <button1> clockwise", "Turn <button1> anticlockwise", "Turn <button2> clockwise", "Turn <button2> anticlockwise to 0 minutes", "Turn <button1> to 200 degrees", "Turn <button1> to 120 degrees", "Turn <button1> to 180 degrees", "Turn <button2> clockwise to 3 minutes", "Turn <button2> clockwise to 10 minutes", "Turn <button2> clockwise to 15 minutes"]

        ], #  candidate answers of each step (2 steps in this case)

        "correct": [6, 10],  # correct answer index of each step (starting from 1). We would not release this in the testing set

        "images": ["airfryer-user.jpg", "airfryer-user.jpg"] # user view image of each step, mentioned in buttons.csv

            },

        {...},

        ...

    ]
