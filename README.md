# AI-based Image and Video Detection for Pedestrian and Vehicle in Public Areas

This project is a 6-month side project leveraging PaddleDetection to detect pedestrians and vehicles in public areas. It aims to:
- Count the number of pedestrians or vehicles in an area during a specified time period.
- Track objects over time.
- Monitor multiple areas for break-ins and return the break-in and break-out times.

## Installation

Since this project builds upon PaddleDetection, please follow the original [PaddleDetection setup instructions]([https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.8](https://github.com/PaddlePaddle/PaddleDetection/blob/release/2.8/docs/tutorials/INSTALL_cn.md)). My code extends PaddleDetection to generate the specified outputs.

For reference of the working version:
1. Python (3.12.8)
2. CUDA (12.4)
3. paddlepaddle-gpu (2.6.1.post120)

## Implementation and Usage

### Input

The program requires an `.mp4` video file and a `.json` file specifying the areas to monitor for intersection. 

The `.json` file should follow this format:
```json
{
  "section_1": [
    [x1, y1],
    [x2, y2],
    ...
  ],
  "section_2": [
    [x1, y1],
    [x2, y2],
    ...
  ],
  ...
}
```
Each section must contain 2 or more coordinate pairs. If a section has 3 or more coordinate pairs, it checks area intersection; otherwise, it checks line intersection.

Again, the object detection process is identical to PaddleDetection. After detection, this project generates a `.csv` file and checks intersections between user-specified areas and detected objects. 

Another output is a `.json` file containing object IDs, sections where break-ins occurred, and break-in/out times. 
The `.json` output file would follow this format:

for area intersection:
```json
{
  "section_1": [
    {
      "id": "object1_id",
      "section": "section_1",
      "break-in time": "time1",
      "break-out time": "time2",
    },
    {
      "id": "object2_id",
      "section": "section_1",
      "break-in time": "time3",
      "break-out time": "time4",
    },
    ...
  ],
  "section_2": [
    {
      "id": "object3_id",
      "section": "section_2",
      "break-in time": "time5",
      "break-out time": "time6",
    },
    {
      "id": "object4_id",
      "section": "section_2",
      "break-in time": "time7",
      "break-out time": "time8",
    },
    ...
  ],
  ...
}
```

for line intersection:
```json
{
  "section_1": [
    {
      "id": "object1_id",
      "section": "section_1",
      "time": "time1",
    },
    {
      "id": "object2_id",
      "section": "section_1",
      "time": "time2",
    },
    ...
  ],
  "section_2": [
    {
      "id": "object3_id",
      "section": "section_2",
      "time": "time3",
    },
    {
      "id": "object4_id",
      "section": "section_2",
      "time": "time4",
    },
    ...
  ],
  ...
}
```

The intersection check uses the coordinates of each object in each frame of the input video. Additionally, the code counts the number of objects intersecting with the specified areas.

## Output Format and Directory

### Output Files

The program generates:

* One `.mp4` file for the output video (see PaddleDetection project for samples).
* One `.csv` file containing data for the output video:
  - Columns: object type (vehicle or pedestrian) ID, frame ID, confidence, xmin, ymin, xmax, ymax.

* One `.json` file for break-in/out records:

