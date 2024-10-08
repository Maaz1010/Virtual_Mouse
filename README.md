 <h1>Virtual Mouse Using Hand Gestures</h1>
  <p>This project implements a virtual mouse system using hand gestures detected by a webcam. It utilizes <b>OpenCV</b> for video capture, <b>Mediapipe</b> for hand landmark detection, and <b>PyAutoGUI</b> for simulating mouse actions like moving the cursor and clicking. The virtual mouse lets users control the computer's mouse pointer without any physical input device.</p>

  <h2>Features</h2>
  <ul>
    <li>Real-time hand tracking using Mediapipe.</li>
    <li>Mouse movement controlled by the index finger's position.</li>
    <li>Click detection using the proximity of the thumb and index finger.</li>
    <li>Works with a standard webcam and requires no additional hardware.</li>
  </ul>

  <h2>Technologies Used</h2>
  <ul>
    <li>Python for the core implementation.</li>
    <li>OpenCV for capturing webcam feed and processing images.</li>
    <li>Mediapipe for detecting hand landmarks.</li>
    <li>PyAutoGUI for controlling mouse movement and simulating clicks.</li>
  </ul>

  <h2>Code Explanation</h2>
  <p>The core functionality is implemented in Python, utilizing OpenCV, Mediapipe, and PyAutoGUI.</p>

  <h3>1. Video Capture with OpenCV</h3>
  <p>The code begins by accessing the webcam using OpenCV's <code>VideoCapture()</code> method:</p>
  <pre><code>cap = cv2.VideoCapture(0)</code></pre>
  <p>This opens the default camera and continuously reads frames in real-time.</p>

  <h3>2. Hand Detection with Mediapipe</h3>
  <p>Mediapipe's <code>Hands()</code> solution is used to detect hand landmarks:</p>
  <pre><code>hand_detector = mp.solutions.hands.Hands()</code></pre>
  <p>Mediapipe processes the webcam feed and identifies key hand landmarks, including the index finger and thumb.</p>

  <h3>3. Mouse Movement Control</h3>
  <p>The position of the index finger (landmark ID 8) is tracked, and its coordinates are used to control the mouse cursor:</p>
  <pre><code>if id == 8:
    index_x = screen_width/frame_width*x
    index_y = screen_height/frame_height*y</code></pre>
  <p>This maps the index finger’s position in the camera frame to the screen's resolution, moving the mouse accordingly.</p>

  <h3>4. Click Detection</h3>
  <p>When the thumb (landmark ID 4) and the index finger (ID 8) come close together, a mouse click is simulated:</p>
  <pre><code>if abs(index_y - thumb_y) &lt; 20:
    pyautogui.click()
    pyautogui.sleep(1)</code></pre>
  <p>The program checks the distance between the index and thumb fingers, and if it's within a threshold, a click event is triggered using <code>pyautogui.click()</code>.</p>

  <h3>5. Visual Feedback</h3>
  <p>The code uses OpenCV to draw the hand landmarks and circles around the index and thumb fingertips for visual feedback:</p>
  <pre><code>cv2.circle(img=frame, center=(x,y), radius=10, color=(0, 255, 255))</code></pre>
  <p>This helps the user see what part of their hand is being tracked.</p>

  <h3>6. Continuous Loop</h3>
  <p>The program runs in an infinite loop, constantly reading the webcam feed and processing it until the user manually closes the program.</p>

  <h2>Future Improvements</h2>
  <ul>
    <li>Adding gesture-based scrolling and dragging.</li>
    <li>Optimizing the click detection for better accuracy.</li>
    <li>Supporting multi-hand gestures.</li>
  </ul>
