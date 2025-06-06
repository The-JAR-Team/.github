# FocusFlow

AI-Driven Engagement Monitoring and Interaction for Educational Videos

---

## 🚀 Project Overview

**FocusFlow** is a web-based platform designed to turn passive video lectures into an interactive, personalized learning experience. Using real-time AI-driven engagement detection, quizzes, and analytics, FocusFlow ensures that learners stay on track and educators receive actionable feedback.

---

## 💡 Motivation & Problem Statement

- Students often lose focus during recorded video lectures, especially with complex or dense topics.  
- There is no live interaction or feedback loop when watching prerecorded sessions.  
- Existing solutions rarely provide immediate, context-aware interventions.

**FocusFlow** addresses these gaps by:
1. Detecting engagement dips in real time using facial landmark tracking and a custom-trained AI model. :contentReference[oaicite:0]{index=0}  
2. Generating AI-powered quiz questions relevant to the lecture content whenever low engagement is detected. :contentReference[oaicite:1]{index=1}  
3. Rewinding or reinforcing missed segments so learners can revisit challenging material without losing context. :contentReference[oaicite:2]{index=2}

---

## 🎯 Key Features

1. **Real-Time Engagement Detection**  
   - Client-side facial landmark extraction via MediaPipe.  
   - Regression-based engagement model (continuous score) deployed in ONNX on the server. :contentReference[oaicite:3]{index=3}  

2. **AI-Powered Quiz Generation**  
   - Transcript extraction from video.  
   - Prompted to Google Gemini API to produce contextually relevant questions. :contentReference[oaicite:4]{index=4}  

3. **Interactive Quiz & Rewind Mode**  
   - Users receive quiz prompts when engagement drops below a threshold.  
   - Option to rewind to review missed segments before continuing.

4. **Analytics Dashboard**  
   - Engagement plots for individual viewers, helping them understand focus patterns. :contentReference[oaicite:5]{index=5}  
   - Aggregated class engagement data for instructors, enabling content refinement and pacing adjustments.

---

## 🔗 Live Links

- **FocusFlow Client**  
  - GitHub: https://github.com/The-JAR-Team/focus-flow-client  
  - Live Site: https://the-jar-team.github.io/focus-flow-client/

- **FocusFlow Server**  
  - GitHub: https://github.com/The-JAR-Team/focus-flow-server

- **FocusFlow Models**  
  - GitHub: https://github.com/The-JAR-Team/focus-flow-models

---

## 🛠️ Usage & Demo

1. **Sign Up / Log In**  
   - Create a new account or log in with existing credentials.

2. **Upload a Video**  
   - Administrators or instructors can upload a lecture video (or provide a YouTube link).  
   - The system extracts the transcript automatically.

3. **Watch Lecture**  
   - The UI displays the video alongside a small overlay that shows real-time engagement (e.g., a green/yellow/red indicator).  
   - Facial landmark data is streamed to the server every 500ms.  

4. **Receive Quizzes**  
   - When engagement drops below a configurable threshold (e.g., < 0.4 on a 0–1 scale), a modal pops up with contextually generated questions.  
   - Answering the question can optionally rewind the video by a set number of seconds to reinforce the missed material.

5. **Analytics Dashboard**  
   - After the session ends (or during it), learners can view a graph of their engagement score over time.  
   - Instructors access an aggregated dashboard that shows average engagement dips, most-quiz-trigger points, and suggestions for pacing refinement.

6. **Continuous Improvement**  
   - Engagement models can be retrained offline using updated datasets (e.g., DAiSEE, EngageNet).  
   - New models are exported to ONNX and deployed for seamless integration.

---

## 📐 Architecture & Technical Details

> Detailed in AIED 2025 paper: “FocusFlow: AI-Driven Engagement Monitoring and Interaction for Educational Videos.” :contentReference[oaicite:6]{index=6}

1. **Engagement Model**  
   - Trained offline on DAiSEE and EngageNet datasets. :contentReference[oaicite:7]{index=7}  
   - Preprocessing pipeline uses MediaPipe to extract 468 facial landmarks per frame, stacks sequences into tensors, and feeds them to a regression model (PyTorch → ONNX). :contentReference[oaicite:8]{index=8}  

2. **Real-Time Data Flow**  
   - Client captures webcam frames → extracts landmarks → sends JSON to an engagement endpoint.  
   - Server runs ONNX inference (`engagement.onnx`) → returns a continuous score.  
   - Score saved in a database along with timestamp for later analytics. :contentReference[oaicite:9]{index=9}  

3. **Quiz Generation**  
   - Transcript pulled at upload time or via a video API.  
   - When engagement dips, server invokes a question-generator module, which:  
     1. Reads transcript segments around the current timestamp.  
     2. Crafts a prompt like:  
        > “Generate 3 multiple-choice questions about the concept of [topic snippet] covered in the next 30 seconds of the lecture.”  
     3. Sends prompt to Gemini API → receives questions JSON → stores them for client display. :contentReference[oaicite:10]{index=10}  

4. **Analytics & Visualization**  
   - Frontend fetches engagement history and renders a time-series chart (e.g., using Chart.js).  
   - Instructors can view aggregated plots (averages, standard deviations) for all viewers.

---

## 📖 Publication & Demo Links

- **AIED 2025 Conference Paper**:  
  “FocusFlow: AI-Driven Engagement Monitoring and Interaction for Educational Videos” :contentReference[oaicite:11]{index=11}  
  – PDF: [AIED_2025_paper_5435.pdf](docs/AIED_2025_paper_5435.pdf)  
  – Published at AIED 2025 (October 27–31, 2025, Dublin, Ireland).  

- **Project Demo Video**:  
  [YouTube Demo Link](https://www.youtube.com/watch?v=kpvSBbXIIvs) :contentReference[oaicite:12]{index=12}  

---

## 🏆 Contributors & Authors

- **Renan Bazinin** (@renanbazinin)  
- **Sarel Cohen** (@sarelco)  
- **Alona Gatker** (@alonaga)  
- **Jonatan Shaya** (@jonathansh2)

> *Supervised by:* Sarel Cohen

---

## 📚 References

1. **DAiSEE Dataset**  
   Gupta, A., D’Cunha, A., Awasthi, K., Balasubramanian, V.N. (2016). _DAiSEE: Towards user engagement recognition in the wild._ :contentReference[oaicite:13]{index=13}  

2. **EngageNet Dataset**  
   Singh, M., Hoque, X., Zeng, D., Wang, Y., Ikeda, K., Dhall, A. (2023). _Do I have your attention: A large scale engagement prediction dataset and baselines._ ICMI ’23, pp. 174–182. :contentReference[oaicite:14]{index=14}  

---

## 😊 Emotions Models (in small)

A lightweight project for detecting facial emotions and boredom.

- **GitHub**: https://github.com/The-JAR-Team/Emotions-Models-Client  
- **Live Site**: https://the-jar-team.github.io/Emotions-Models-Client/  
- **Models Repo**: https://github.com/The-JAR-Team/focus-flow-models

---

## 📬 Contact & Support

- **Email**: renanba@mta.ac.il  
- **Organization Website**:  
  https://the-jar-team.github.io/focus-flow-client/ :contentReference[oaicite:15]{index=15}  

If you encounter any issues or have questions, please open an issue or submit a pull request.

---

*“Innovation through collaboration and AI-powered engagement.”*  
