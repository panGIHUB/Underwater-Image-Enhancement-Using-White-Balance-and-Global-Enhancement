Objective: Enhance underwater images by correcting color distortion and improving clarity using white balance and global enhancement techniques.

Techniques Used:
White Balance Correction
Variable Contrast and Saturation Enhancement


Evaluation Metrics: MSE, PSNR, SSIM
Datasets: UIEB (Underwater Image Enhancement Benchmark) and EUVP (Enhancing Underwater Visual Perception)
Applications: Marine research, underwater photography, infrastructure inspection, and more.

Methodology
1. White Balance Correction
Purpose: Correct color distortion caused by underwater light conditions.
Process:
Calculate the average color of the image.
Compute scaling factors for each color channel (Red, Green, Blue) based on the average color.
Apply the scaling factors to balance the image.
Clip pixel values to ensure they remain within the valid range [0, 255].

CODE :-
def white_balance(image):
    avg_color = np.mean(image, axis=(0, 1))
    scale_factors = [avg_color[i] / channel_avg for i, channel_avg in enumerate(avg_color)]
    balanced_image = image * scale_factors
    balanced_image = np.clip(balanced_image, 0, 255).astype(np.uint8)
    return balanced_image

2. Variable Contrast and Saturation Enhancement
Purpose: Improve image clarity and vibrancy.
Process:
Convert the image to HSV (Hue, Saturation, Value) color space.
Adjust the contrast by scaling the Value (V) channel.
Adjust the saturation by scaling the Saturation (S) channel.
Convert the image back to the BGR color space.

CODE:- 
def variable_contrast_and_saturation_enhancement(image, contrast_factor, saturation_factor):
    hsv_image = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)
    hsv_image[:,:,2] = np.clip(hsv_image[:,:,2] * contrast_factor, 0, 255)
    hsv_image[:,:,1] = np.clip(hsv_image[:,:,1] * saturation_factor, 0, 255)
    enhanced_image = cv2.cvtColor(hsv_image, cv2.COLOR_HSV2BGR)
    return enhanced_image

    
3. Image Processing Pipeline
Read the input image.
Apply white balance correction.
Apply contrast and saturation enhancement.
Save the enhanced image.
4. Evaluation Metrics
Mean Squared Error (MSE): Measures pixel-wise differences between the original and enhanced images.
Peak Signal-to-Noise Ratio (PSNR): Evaluates image quality relative to a perfect reconstruction.
Structural Similarity Index (SSIM): Assesses similarity based on luminance, contrast, and structure.

CODE:- 
def calculate_metrics(output_image_path, reference_image_path):
    output_image = cv2.imread(output_image_path)
    reference_image = cv2.imread(reference_image_path)
    mse = np.mean((output_image - reference_image) ** 2)
    psnr = cv2.PSNR(output_image, reference_image)
    ssim_value, _ = ssim(output_image, reference_image, full=True)
    return mse, psnr, ssim_value

    Results
UIEB Dataset
Image	MSE	PSNR	SSIM
1	4088.57	16.79	0.871
2	3727.58	17.19	0.901
3	9071.00	13.33	0.917
4	5310.27	15.65	0.896
5	4994.05	15.92	0.897


EUVP Dataset
Image	MSE	PSNR	SSIM
1	6065.98	15.07	0.815
2	3662.24	17.26	0.886
3	7354.37	14.24	0.754
4	3216.55	17.83	0.899
5	5285.81	15.67	0.859
6	3583.92	17.36	0.908


Applications
Marine conservation and research.
Underwater exploration and mapping.
Underwater photography and filmmaking.
Tourism and recreation.
Aquaculture and fisheries management.
Underwater infrastructure inspection.

Important Links
UIEB Dataset Results: https://drive.google.com/drive/folders/1eMTYkEZNNcECzV8petMGKwVgKZzUQ5yZ?usp=drive_link
EUVP Dataset Results: https://drive.google.com/drive/folders/1Nk9MSTdDnOpXGgDq2G_eXNwKIWOqwzxc?usp=drive_link
Reference Paper: https://link.springer.com/article/10.1007/s11042-023-15419-5?
                 utm_source=toc&utm_medium=email&utm_campaign=toc_11042_82_30&utm_content=etoc_
                 springer_20231130
GitHub Repository: https://github.com/panGIHUB/white_balance/blob/main/white_balance_code

Conclusion
The proposed method effectively enhances underwater images by correcting color distortion and improving clarity, as demonstrated by the experimental results on UIEB and EUVP datasets. This approach has broad applications in marine research, photography, and beyond.
