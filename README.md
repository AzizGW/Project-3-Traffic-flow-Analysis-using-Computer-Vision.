# Traffic flow Analysis using Computer Vision.
## 1. Introduction

The focus of this project is to analyze traffic flow dynamics for one side of a traffic light intersection through the lens of computer vision, leveraging a sample (one week data) from the dataset provided by the "Watch And Learn Time-Lapse (WALT) Dataset" project (Reddy et al., 2022). This dataset contains various vehicle types and pedestrian traffic across different times and locations. The primary motivation is to understand the distribution of traffic components (cars, buses, trucks, and persons, etc...)

Here are two example images (Figure 1 & 2) from the dataset illustrating the typical scene at different times:

<div align="center">
    <img src="https://github.com/AzizGW/Project-3-Traffic-flow-Analysis-using-Computer-Vision./assets/119353586/f5a81c61-576c-4673-b8aa-97de36e5342c" alt="2021-05-02t02-53-20 058081" width="70%">
    <br>
    <i>Figure 1. Example from the dataset</i>
</div>
<br>
</br>
  
<div align="center">
    <img src="https://github.com/AzizGW/Project-3-Traffic-flow-Analysis-using-Computer-Vision./assets/119353586/ba9f57c4-5d85-495d-9cc1-eccee28e95dd" alt="2021-05-03t16-48-40 497551" width="70%">
    <br>
    <i>Figure 2: Example from the dataset</i>
</div>

## 2. Method

### 2.1. Dataset

The sample dataset used for this analysis comprises over 5600 images spanning one week, from 2021 May 1st (00:00) to May 7th (20:59). These images were sourced from the Watch And Learn Time-Lapse (WALT) project website (Here) and their the paper can be accessed (Here). 

### 2.2. Preprocessing Images.

A preprocessing step was applied to all images to correct time zone discrepancies. The original images timestamps suggested sunrise at around 9 AM and sunset at around 12 Am in Pittsburgh, PA, during early May, which is inaccurate. To correct this, the time for each image was decreased by 3 hours ensuring the data accurately reflected the local time. This adjustment was crucial for accurately analyzing the traffic flow relative to the time of day, particularly for capturing the dynamics of morning and evening rush hours correctly.

### 2.3. Model

For object the detection and classification within the images I used pre-trained Faster R-CNN model. It was utilized along with the COCO instance category names, which facilitated the identification and classification of multiple objects such as cars, buses, trucks, and persons.

### 2.4. Borderline Technique

<div align="center">
    <img src="https://github.com/AzizGW/Project-3-Traffic-flow-Analysis-using-Computer-Vision./assets/119353586/0cae9022-0c34-4bc6-89a5-74b70d4be689" alt="screenshot-2024-03-01-at-16 23 20" width="70%">
    <br>
    <i>Figure 3. Illustration of the borderline technique</i>
</div>
<br>
</br>
Given the specific camera angle and location, which captures a long street scene with activity, including many parked cars, a blue borderline with a y coordinate of 240 was added in the image processing algorithm. This borderline ,as can be seen in Figure 3 and 4, was placed to include only the vehicles in close proximity to the traffic light, effectively filtering out parked cars and distant traffic not directly relevant to the immediate traffic light analysis. Without the implementation this borderline many objects will be detected which should be ignored for this type of analysis (See Figure 5). Finally, the confidence score was also used to filter the results by including only detected objects with a confidence score of 0.80 and above.

<br>
</br>
<div align="center">
    <img src="https://github.com/AzizGW/Project-3-Traffic-flow-Analysis-using-Computer-Vision./assets/119353586/6a61f081-3162-42ee-87b8-dfad05b37f15" alt="screenshot-2024-03-01-at-16 25 31" width="70%">
    <br>
    <i>Figure 4. Object detection using a borderline.</i>
</div>
<br>
</br>

<div align="center">
    <img src="https://github.com/AzizGW/Project-3-Traffic-flow-Analysis-using-Computer-Vision./assets/119353586/fcdd8f17-5d91-4a8a-96d1-9306f4a36036" alt="screenshot-2024-03-01-at-20 37 00" width="70%">
    <br>
    <i>Figure 5. Object detection without using a borderline.</i>
</div>

## 3. Results

This table (Table 1) shows the total number of detected objects (confidence of 0.80) for each category over the week-long period:
<div align="center">
<table class=""><tbody><tr><th class="wp-block-table__cell-content"><div role="textbox" aria-multiline="true" aria-label="Body cell text" aria-readonly="false" contenteditable="true" class="block-editor-rich-text__editable rich-text" style="white-space: pre-wrap; min-width: 1px;">Category</div></th><th class="wp-block-table__cell-content"><div role="textbox" aria-multiline="true" aria-label="Body cell text" aria-readonly="false" contenteditable="true" class="block-editor-rich-text__editable rich-text" style="white-space: pre-wrap; min-width: 1px;">Total Count</div></th></tr><tr><td class="wp-block-table__cell-content"><div role="textbox" aria-multiline="true" aria-label="Body cell text" aria-readonly="false" contenteditable="true" class="block-editor-rich-text__editable rich-text" style="white-space: pre-wrap; min-width: 1px;">Car</div></td><td class="wp-block-table__cell-content"><div role="textbox" aria-multiline="true" aria-label="Body cell text" aria-readonly="false" contenteditable="true" class="block-editor-rich-text__editable rich-text" style="white-space: pre-wrap; min-width: 1px;">3236</div></td></tr><tr><td class="wp-block-table__cell-content"><div role="textbox" aria-multiline="true" aria-label="Body cell text" aria-readonly="false" contenteditable="true" class="block-editor-rich-text__editable rich-text" style="white-space: pre-wrap; min-width: 1px;">Bus</div></td><td class="wp-block-table__cell-content"><div role="textbox" aria-multiline="true" aria-label="Body cell text" aria-readonly="false" contenteditable="true" class="block-editor-rich-text__editable rich-text" style="white-space: pre-wrap; min-width: 1px;">470</div></td></tr><tr><td class="wp-block-table__cell-content"><div role="textbox" aria-multiline="true" aria-label="Body cell text" aria-readonly="false" contenteditable="true" class="block-editor-rich-text__editable rich-text" style="white-space: pre-wrap; min-width: 1px;">Truck</div></td><td class="wp-block-table__cell-content"><div role="textbox" aria-multiline="true" aria-label="Body cell text" aria-readonly="false" contenteditable="true" class="block-editor-rich-text__editable rich-text" style="white-space: pre-wrap; min-width: 1px;">253</div></td></tr><tr><td class="wp-block-table__cell-content"><div role="textbox" aria-multiline="true" aria-label="Body cell text" aria-readonly="false" contenteditable="true" class="block-editor-rich-text__editable rich-text" style="white-space: pre-wrap; min-width: 1px;">Person</div></td><td class="wp-block-table__cell-content"><div role="textbox" aria-multiline="true" aria-label="Body cell text" aria-readonly="false" contenteditable="true" class="block-editor-rich-text__editable rich-text" style="white-space: pre-wrap; min-width: 1px;">1728</div></td></tr></tbody></table>
    <i>Table 1. The total number of detected objects for each category.</i>
</div>
<br>
</br>
<div align="center">
    <img src="https://github.com/AzizGW/Project-3-Traffic-flow-Analysis-using-Computer-Vision./assets/119353586/db2f7d54-e28a-4f0c-b9f2-a453edd065e6" alt="screenshot-2024-03-01-at-19 38 25" width="70%">
    <br>
    <i>Figure 6. Average Car Counts by Hour For One Week</i>
</div>

<br>
</br>

<div align="center">
    <img src="https://github.com/AzizGW/Project-3-Traffic-flow-Analysis-using-Computer-Vision./assets/119353586/de3292d1-ca53-40ec-a55c-bc0bb17c2239" alt="screenshot-2024-03-01-at-19 38 37" width="70%">
    <br>
    <i>Figure 7. Average Bus Counts by Hour For One Week</i>
</div>

  <br>
</br>

<div align="center">
    <img src="https://github.com/AzizGW/Project-3-Traffic-flow-Analysis-using-Computer-Vision./assets/119353586/f139c650-0a7a-4c40-a40c-77be6e2415de" alt="screenshot-2024-03-01-at-19 39 02" width="70%">
    <br>
    <i>Figure 8. Average Truck Counts by Hour For One Week</i>
</div>

  <br>
</br>

<div align="center">
    <img src="https://github.com/AzizGW/Project-3-Traffic-flow-Analysis-using-Computer-Vision./assets/119353586/cb7eaa4f-361c-4c96-8a97-2fe0aa200361" alt="screenshot-2024-03-01-at-19 38 51" width="70%">
    <br>
    <i>Figure 9. Average Person Counts by Hour For One Week</i>
</div>

  <br>
</br>

<div align="center">
    <img src="https://github.com/AzizGW/Project-3-Traffic-flow-Analysis-using-Computer-Vision./assets/119353586/8c591ead-709f-4f68-9690-9b36467651fc" alt="screenshot-2024-03-01-at-16 43 35" width="70%">
    <br>
    <i>Figure 10. Hourly Car Traffic Heatmap by Date (May 1st, 2021 is Saturday)</i>
</div>

  <br>
</br>

<div align="center">
    <img src="https://github.com/AzizGW/Project-3-Traffic-flow-Analysis-using-Computer-Vision./assets/119353586/b8131583-9400-457e-a539-c0d857934fcf" alt="screenshot-2024-03-01-at-16 43 57" width="70%">
    <br>
    <i>Figure 11. Hourly Bus Traffic Heatmap by Date (May 1st, 2021 is Saturday)</i>
</div>

  <br>
</br>

<div align="center">
    <img src="https://github.com/AzizGW/Project-3-Traffic-flow-Analysis-using-Computer-Vision./assets/119353586/18cadb66-b5f4-42b6-8774-22d5d8e51c2d" alt="screenshot-2024-03-01-at-16 44 30" width="70%">
    <br>
    <i>Figure 12. Hourly Truck Traffic Heatmap by Date (May 1st, 2021 is Saturday)</i>
</div>
<br>
</br>
  

<div align="center">
    <img src="https://github.com/AzizGW/Project-3-Traffic-flow-Analysis-using-Computer-Vision./assets/119353586/35a5bdf1-15b6-420c-8235-6b2e2659e9ee" alt="screenshot-2024-03-01-at-16 44 17" width="70%">
    <br>
    <i>Figure 13. Hourly Person Traffic Heatmap by Date (May 1st, 2021 is Saturday)</i>
</div>



## 4. Analysis of Results

Observations Across Categories

**Cars**: Figure 6 shows a peak in the late afternoon (15:00 - 16:00) with an average count of approximately 46 cars. This likely corresponds to the end of the typical workday, indicating a rush hour effect. The morning hours also show increased traffic around 8:00, with 21 cars on average, suggesting morning commute patterns. The lowest car activity is observed in the early morning (4:00 - 6:00), with counts near or below 1, reflecting the quietest hours on the streets.

**Buses**: Figure 7 shows a more consistent presence throughout the day compared to cars, with a slight increase during typical commuting hours (7:00 - 9:00 and 15:00 - 16:00). The average bus count peaks at 5.85 around 15:00, which could be associated with school or work schedules. Moreover, nighttime and early morning hours (0:00 - 5:00) see the least bus activity, as expected.

**Trucks**: Figure 8 presents a normal pattern, with activity starting to increase at 7:00 and peaking at 9:00 with an average of 4.28 trucks. This suggests that trucks may be operating on a schedule that aims to avoid the heaviest commuter traffic or that aligns with delivery times for businesses opening hours.

**Persons**: As can be seen in Figure 9, the pedestrian traffic peaks in the afternoon (13:00 - 16:00), with the highest activity at 13:00, showing an average of 26 individuals. This could due to lunchtime activities. Another notable increase is observed in the late evening (18:00 - 19:00), possibly indicating leisure or shopping activities after work.

## 5. Analysis of Vision Algorithm

### 5.1. Key Adjustments and Insights

**Time Adjustment**: One critical preprocessing step was adjusting the timestamps of the images by decreasing each of them by 3 hours. This adjustment was important for aligning the dataset with the correct local time zone, as the initial timestamps led to inaccurate interpretations of daily traffic patterns, such as noticing sunrise in images that were incorrectly marked around 9 AM in Pittsburgh, PA, during May. Correcting the time ensured that the analysis of traffic patterns, including peak and low traffic hours, accurately reflected the local context and daily routines.

**Handling Parked Vehicles with a Borderline**: The challenge posed by the long street captured in the dataset was the presence of many parked vehicles, which could potentially effect the analysis of active traffic flow. To solve this, a borderline was implemented to focus the analysis on vehicles in closer proximity to the traffic light. This method effectively filtered out parked cars and other static objects, allowing for a more accurate assessment of traffic dynamics and congestion near the traffic light.

**Confidence Score Thresholding for Reliable Detections**: an enhancement to the object detection process was the adoption of a confidence score threshold of **0.80** and above for accepting detections. This thresholding was critical in minimizing wrong detections and ensuring that only detections with a high likelihood of accuracy contributed to the analysis.

### 5.2. Limitations

**Dataset size**: The dataset used in this project covers only one week in May 2021, providing a limited snapshot of traffic patterns (the original dataset includes one year of data but requires permission to access it). This range may not capture the variability influenced by seasonal changes, holidays, and special events.

**Ambiguity in Vehicle Classification**: The model sometimes classifies the same vehicle in multiple categories, notably with vehicles like pickup trucks being counted as both cars and trucks. This classification challenge could lead to inaccuracies in traffic analysis, as the distinction between personal and commercial vehicle use becomes blurred.

**Camera Angle**: The camera was only capturing one side of the traffic light, it would be more beneficial if the camera had a complete view over the intersection. However, it is worth mentioning that the WALT website provides different datasets featuring various locations and camera angles (See Figure 14).
<br>
</br>
<div align="center">
    <img src="https://github.com/AzizGW/Project-3-Traffic-flow-Analysis-using-Computer-Vision./assets/119353586/ade05ab2-10ca-4ac4-a671-bd70b8cf4855" alt="screenshot-2024-03-02-at-11 43 08" width="70%">
    <br>
    <i>Figure 14. The different locations data provided by <a href="https://www.cs.cmu.edu/~walt/">https://www.cs.cmu.edu/~walt/</a>.</i>
</div>

  

## 6. References

  1. Reddy, N. D., Tamburo, R., & Narasimhan, S. G. (2022). WALT: Watch And Learn 2D amodal representation from Time-lapse imagery. In Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (pp. 9356-9366).
  
  2. Ren, S., He, K., Girshick, R., & Sun, J. (2015). Faster r-cnn: Towards real-time object detection with region proposal networks. Advances in neural information processing systems, 28.

  3. https://www.cs.cmu.edu/~walt/
