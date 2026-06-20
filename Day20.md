# Day 20 - Build an AI Face Puzzle Game

### Objective

To develop an interactive web-based Face Puzzle Game that uses the device camera to capture a user's photo, convert it into a puzzle, and provide an engaging gaming experience with drag-and-drop functionality, timers, scoring, and leaderboards.

---

### Key Learnings

* Working with the **MediaDevices API** (`getUserMedia`) for webcam access.
* Capturing images using **HTML Canvas**.
* Slicing images into puzzle pieces dynamically.
* Implementing **drag-and-drop** and **touch gesture** interactions.
* Managing game state and puzzle logic using JavaScript.
* Building responsive interfaces for desktop and mobile devices.
* Using **localStorage** to persist leaderboard data.
* Implementing timers, move counters, and win detection mechanisms.
* Enhancing user experience through visual feedback and animations.

---

### Questions & Answers

**Q1: How does the game capture the user's face?**
**A:** The application uses the browser's `getUserMedia()` API to access the webcam and captures a snapshot using an HTML Canvas.

**Q2: How are puzzle pieces created?**
**A:** The captured image is divided into equal sections based on the selected difficulty level (3×3, 4×4, or 5×5).

**Q3: How does the drag-and-drop mechanism work?**
**A:** Users can drag a puzzle piece and drop it onto another grid cell, which swaps the positions of the two pieces.

**Q4: How is progress tracked?**
**A:** The game continuously monitors correctly placed pieces, total moves, and elapsed time.

**Q5: How is the winner determined?**
**A:** When all puzzle pieces are placed in their correct positions, the game automatically detects completion and displays the results.

**Q6: How are best scores saved?**
**A:** Top scores are stored locally in the browser using `localStorage`, allowing users to view their best performances.

---
### Image result 
<img width="1536" height="1024" alt="1000228064" src="https://github.com/user-attachments/assets/2a661f34-a390-4e6a-b624-0149b7c0ef29" />


### Conclusion

This project demonstrates the power of modern web technologies by combining camera access, image processing, interactive gameplay, and persistent storage into a single responsive application. It provided hands-on experience with browser APIs, event handling, UI/UX design, and JavaScript game development while showcasing how engaging applications can be built without relying on external frameworks.

### Technologies Used

* HTML5
* CSS3
* Vanilla JavaScript
* Canvas API
* MediaDevices API (`getUserMedia`)
* LocalStorage
* Touch & Mouse Events

### Future Enhancements

* AI-powered face detection and auto-cropping
* Multiplayer challenge mode
* Online leaderboard
* Share results on social media
* Custom puzzle shapes and themes
* Achievement and reward system
