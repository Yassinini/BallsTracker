## Abbreviations & Symbols

| Term  | Meaning                                |     |
| ----- | -------------------------------------- | --- |
| RQ    | Research Question                      |     |
| FWOIF | Frames With Object In Frame            |     |
| AVG   | Averaged trajectory dataset            |     |
| FPS   | Frames per second                      |     |
| h(t)  | Height as a function of time           |     |
| e     | Coefficient of restitution             |     |
| g     | Gravitational acceleration (9.81 m/s²) |     |
| v₀    | Initial velocity                       |     |
|       |                                        |     |

## To what extent does air resistance cause deviation between the theoretical and measured trajectory of a projectile?

To measure this we must go through a process of real world data collection, data processing and physics translations.

## Data Collection

For data collection, over 10 minutes of ping pong ball footage was taken, the ping pong ball was set up to fall from a fixed angle to generate a bounce that lost its energy over time.

After initialising the set up to drop the ball from a repeatable angle, the camera (in this case a mobile phone) is set up to take video of the ball.

- The ball falls ~100 cm to the floor, bounces back up and with a horizontal movement.

- The phone is set up in wide angle mode facing the set up fall of the ball.
---
## Data processing
The python program >main.py< utilises the OpenCV and NumPy libraries of python for collecting the videos and processing them.

### Video
- OpenCV recieves the video which it encodes as images. Runs through every image to process them
- The image is turned to greyscale for easier processing every frame, then a masking threshold is made 
>grey = cv.cvtColor(smol, cv.COLOR_BGR2GRAY)
_, mask = cv.threshold(grey, 180, 255, cv.THRESH_BINARY)
mask = cv.erode(mask, kernel, iterations=5)
mask = cv.dilate(mask, kernel, iterations=5)

- This makes the entire frame black with only the ball being white![[Pasted image 20260822021820.png|466]]

### Frames
- The program uses math and numpy to calculate the number of frames in the video, the number of frames per second is extracted and then reused to get the total duration in seconds.
- FORMAT:
> total frames: 47
fps: 59.72069092245498
time: 0.7869969230769231 
number of FWOIF: 20 (frames with object inframe)
number of unused frames: 27

- The program also tracks the ball as long as it exits in frame AND IS DETECTED, keeping it in the csv format for further data work
--> This isolates the ball's motion for further analysis

## Data work
1 - The data is filtered and normalised, keeping the base of all graphs at h=0 
![[Pasted image 20260822022932.png]]
-- the graph shows 4 ball dropping trajectories which fit the **parabolic motion under constant gravitational acceleration** topic in physics

- Height under gravity:
$$h(t) = v_0 t - \frac{1}{2}g t^2$$

- Coefficient of restitution (bounce-to-bounce energy loss)
$$e = \sqrt{\frac{h_{n+1}}{h_n}}$$

## Averaging the graphs
- The next step is to find a graph that unifies all the past graphs into another graph AND its dataset, calling them the AVG
![[Pasted image 20260822023735.png]]

--> The graph above represents the AVG graphing compared to the rest of the datasets graphed.

## Working with one
To work with the data we found, we must separate a parabola of the first bounce to use that for comparison
![[Pasted image 20260822024024.png]]
