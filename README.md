# Ex05 Image Carousel
## Date:01-09-2026

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM
App.jsx
```
import React from "react";
import Carousel from "./Carousel";

function App() {
  return (
    <div style={{
      background: "linear-gradient(135deg, #1e3c72, #2a5298)",
      minHeight: "100vh",
      display: "flex",
      justifyContent: "center",
      alignItems: "center",
      fontFamily: "Arial"
    }}>
      <Carousel />
    </div>
  );
}

export default App;
```
carousel.jsx
```
import React, { useState, useEffect } from "react";

const images = [
  "https://images.unsplash.com/photo-1507525428034-b723cf961d3e",
  "https://images.unsplash.com/photo-1491553895911-0055eca6402d",
  "https://images.unsplash.com/photo-1501785888041-af3ef285b470",
  "https://images.unsplash.com/photo-1500530855697-b586d89ba3ee",
  "https://images.unsplash.com/photo-1506744038136-46273834b3fb"
];

function Carousel() {
  const [currentIndex, setCurrentIndex] = useState(0);
  const [autoPlay, setAutoPlay] = useState(true);

  const nextImage = () => {
    setCurrentIndex((prev) => (prev + 1) % images.length);
  };

  const prevImage = () => {
    setCurrentIndex((prev) => (prev - 1 + images.length) % images.length);
  };

  useEffect(() => {
    if (!autoPlay) return;

    const interval = setInterval(() => {
      nextImage();
    }, 3000);

    return () => clearInterval(interval);
  }, [autoPlay]);

  return (
    <div style={{
      width: "500px",
      background: "#fff",
      padding: "20px",
      borderRadius: "15px",
      boxShadow: "0 10px 25px rgba(0,0,0,0.3)",
      textAlign: "center"
    }}>

      <h2 style={{ color: "#2a5298" }}>🌈 Image Carousel</h2>

      <div style={{ position: "relative" }}>
        <img
          src={images[currentIndex]}
          alt="carousel"
          style={{
            width: "100%",
            height: "300px",
            objectFit: "cover",
            borderRadius: "10px",
            transition: "0.5s"
          }}
        />

        {/* Arrows */}
        <button onClick={prevImage} style={arrowStyle("left")}>❮</button>
        <button onClick={nextImage} style={arrowStyle("right")}>❯</button>
      </div>

      {/* Dots */}
      <div style={{ marginTop: "10px" }}>
        {images.map((_, index) => (
          <span
            key={index}
            onClick={() => setCurrentIndex(index)}
            style={{
              height: "12px",
              width: "12px",
              margin: "5px",
              display: "inline-block",
              borderRadius: "50%",
              background: currentIndex === index ? "#2a5298" : "#ccc",
              cursor: "pointer"
            }}
          ></span>
        ))}
      </div>

      {/* Controls */}
      <div style={{ marginTop: "15px" }}>
        <button onClick={prevImage} style={btnStyle}>⬅ Prev</button>
        <button onClick={nextImage} style={btnStyle}>Next ➡</button>
      </div>

      <div style={{ marginTop: "10px" }}>
        <button
          onClick={() => setAutoPlay(!autoPlay)}
          style={{ ...btnStyle, background: autoPlay ? "#ff4b5c" : "#4caf50" }}
        >
          {autoPlay ? "Stop AutoPlay ⏸" : "Start AutoPlay ▶"}
        </button>
      </div>

    </div>
  );
}

// Styles
const btnStyle = {
  margin: "5px",
  padding: "8px 15px",
  border: "none",
  borderRadius: "8px",
  background: "#2a5298",
  color: "#fff",
  cursor: "pointer"
};

const arrowStyle = (position) => ({
  position: "absolute",
  top: "50%",
  [position]: "10px",
  transform: "translateY(-50%)",
  background: "rgba(0,0,0,0.5)",
  color: "#fff",
  border: "none",
  borderRadius: "50%",
  width: "40px",
  height: "40px",
  cursor: "pointer"
});

export default Carousel;
```


## OUTPUT

<img width="1919" height="1004" alt="image" src="https://github.com/user-attachments/assets/3895f319-c8dd-485b-b21e-15c5139ba236" />
<img width="1919" height="1008" alt="image" src="https://github.com/user-attachments/assets/f1af3b75-cdeb-4005-9fb8-7d56000b1a7a" />
<img width="1919" height="1010" alt="image" src="https://github.com/user-attachments/assets/c79f5c49-c413-4a5d-94a3-1bcf02df7723" />

## RESULT
The program for creating Image Carousel using React is executed successfully.
