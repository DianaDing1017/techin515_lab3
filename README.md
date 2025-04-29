# TECHIN515 Lab 3: Sorting Hat Project Documentation (English Version)

This project implements a magical **Sorting Hat system using ESP32**. A 10-question personality quiz is displayed on an OLED screen, and the user selects answers using four physical buttons. The responses are input into a pre-trained machine learning model (TinyML decision tree), which predicts the user's assigned Hogwarts house: **Gryffindor, Hufflepuff, Ravenclaw, or Slytherin**.

---

## Project Highlights

- Questions and options are displayed on a 128x32 OLED screen  
- User selects answers with four physical buttons (GPIO14, 27, 26, 25)  
- Options scroll automatically; the quiz progresses question by question  
- Final house prediction is displayed after the quiz  
- Model is trained in Python and deployed to ESP32 as a `.h` file

---

## Model Training Summary

The model was trained using Python with `scikit-learn` and `micromlgen`. A custom dataset of 5000 entries was generated, each containing 10 responses and a corresponding house label. The model is a decision tree with a maximum depth of 5, and achieves approximately **83% accuracy** on a test set.

---

## User Interaction Flow

1. OLED displays questions and scrolling options  
2. User answers each question by pressing buttons A/B/C/D (mapped to 1–4)  
3. The system records each answer  
4. After all 10 questions, the model makes a prediction  
5. The OLED shows the predicted house, and the result is also printed via Serial Monitor

---

## Lab Manual Questions & Answers

### Question 1: Are all 10 questions equally important? If not, which one(s) would you remove and why?

Not all 10 questions contribute equally to prediction accuracy. For example, **Question 7: “Preferred pet?”** tends to be chosen based on aesthetics or randomness rather than house-relevant traits. During training, this question showed low distinguishing power across different house labels.

To improve user experience without sacrificing performance, I would remove **Question 7**. This reduces quiz fatigue and speeds up interaction, while maintaining strong classification performance.

---

### Question 2: If you were to improve the Sorting Hat, what technical improvements would you make?

#### Model Enhancements:

- Use more complex models such as **Random Forests** to improve accuracy and generalization  
- Apply **feature importance analysis** to refine the question set and reduce redundancy

#### Hardware Improvements:

- Add a **speaker module** to provide verbal feedback like:  
  *“You belong to Slytherin!”*  

#### Model Suitability:

The current decision tree model works well for structured, low-dimensional inputs (10 questions with 1–4 values).  
However, if higher-dimensional sensor data (e.g., speech or motion) is introduced, I would switch to a **lightweight CNN** for its pattern recognition capabilities.  
This would require moving to **TensorFlow Lite + TinyML** for efficient edge deployment.

## Link to access the video of my working sorting hat prototype:
https://drive.google.com/file/d/1ZVp4G4k0W5idJweDegXqP2BDV_yRfUOZ/view?usp=sharing 
