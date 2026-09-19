# Ex05 Image Carousel
## Date: 1/09/2026

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
## Carousel.js
```
import React, { useState, useEffect } from 'react';
import './Carousel.css';

const Carousel = ({ images }) => {
  const [currentIndex, setCurrentIndex] = useState(0);
  
  // Auto-advance the carousel every 3 seconds
  useEffect(() => {
    const interval = setInterval(() => {
      goToNext();
    }, 3000);
    
    return () => clearInterval(interval);
  }, [currentIndex]);
  
  const goToPrevious = () => {
    const isFirstImage = currentIndex === 0;
    const newIndex = isFirstImage ? images.length - 1 : currentIndex - 1;
    setCurrentIndex(newIndex);
  };
  
  const goToNext = () => {
    const isLastImage = currentIndex === images.length - 1;
    const newIndex = isLastImage ? 0 : currentIndex + 1;
    setCurrentIndex(newIndex);
  };
  
  const goToImage = (index) => {
    setCurrentIndex(index);
  };
  
  return (
    <div className="carousel">
      <div className="carousel-image-container">
        <img 
          src={images[currentIndex]} 
          alt={`Slide ${currentIndex}`} 
          className="carousel-image"
        />
        
        
        <button onClick={goToPrevious} className="carousel-button left">
          ❮
        </button>
        <button onClick={goToNext} className="carousel-button right">
          ❯
        </button>
      </div>
      
      <div className="carousel-dots">
        {images.map((_, index) => (
          <span 
            key={index}
            className={`dot ${index === currentIndex ? 'active' : ''}`}
            onClick={() => goToImage(index)}
          />
        ))}
      </div>
    </div>
  );
};

export default Carousel;
```
## Carousel.css
```
.carousel {
  position: relative;
  max-width: 800px;
  margin: 0 auto;
  overflow: hidden;
}

.carousel-image-container {
  position: relative;
  width: 100%;
  height: 400px;
}

.carousel-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.carousel-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  padding: 10px 15px;
  cursor: pointer;
  font-size: 18px;
  border-radius: 50%;
  z-index: 10;
}

.carousel-button:hover {
  background-color: rgba(0, 0, 0, 0.8);
}

.carousel-button.left {
  left: 20px;
}

.carousel-button.right {
  right: 20px;
}

.carousel-dots {
  text-align: center;
  margin-top: 10px;
}

.dot {
  display: inline-block;
  width: 12px;
  height: 12px;
  margin: 0 5px;
  background-color: #bbb;
  border-radius: 50%;
  cursor: pointer;
}

.dot.active {
  background-color: #717171;
}

```
## App.js
```
import React from 'react';
import Carousel from './Carousel';
import './App.css';

function App() {
const images = [
  process.env.PUBLIC_URL + '/images/slide1.jpg',
  process.env.PUBLIC_URL + '/images/slide2.jpg',
  process.env.PUBLIC_URL + '/images/slide3.jpg'
];

  return (
    <div className="App">
      <h1>Beautiful Travel Destinations</h1>
        <p className="explore-text">Explore this beautiful location</p>
      <Carousel images={images} />
      
      <footer>
        <p>Created by: SHANMUGAKARTHIK G</p>
        <p>Register Number: 212223220105</p>
      </footer>
    </div>
  );
}

export default App;
```
## App.css
```
.App {
  text-align: center;
  padding: 20px;
}

footer {
  margin-top: 30px;
  padding: 20px;
  background-color: #f8f9fa;
  border-top: 1px solid #e9ecef;
}
.explore-text {
  font-size: 1.5rem;
  margin-bottom: 20px;
  color: #333;
  font-style: italic;
}
```
## OUTPUT
![alt text](<Screenshot (28).png>)
![alt text](<Screenshot (29).png>)
![alt text](<Screenshot (30).png>)
## RESULT
The program for creating Image Carousel using React is executed successfully.
