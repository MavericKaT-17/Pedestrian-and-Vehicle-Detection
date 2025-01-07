# AI-based Image and Video Detection for Pedestrian and Vehicle in Public Areas

This project is a 6-month side project leveraging PaddleDetection to detect pedestrians and vehicles in public areas. It aims to:
- Count the number of pedestrians or vehicles in an area during a specified time period.
- Track objects over time.
- Monitor multiple areas for break-ins and return the break-in and break-out times.

## Installation

Since this project builds upon PaddleDetection, please follow the original [PaddleDetection setup instructions](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.8). My code extends PaddleDetection to generate the specified outputs.

## Implementation and Usage

### Input

The program requires an `.mp4` video file and a `.json` file specifying the areas to monitor for intersection. The `.json` file should follow this format:
```json
{
  "area_1": [
    [x1, y1],
    [x2, y2],
    ...
  ],
  "area_2": [
    [x1, y1],
    [x2, y2],
    ...
  ],
  ...
}
