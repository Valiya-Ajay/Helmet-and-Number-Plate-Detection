# Helmet and Number Plate Detection using YOLOv8

A deep learning project that detects motorcycle riders, checks whether each rider is **wearing a helmet or not**, and finds the **number plate** of the motorcycle in traffic images. It uses a YOLOv8 object detection model trained on a public Kaggle dataset.

## Results

Sample detections from the trained model (boxes show the class and confidence score):

![Detection result 1](images/new76.jpg)

![Detection result 2](images/new119.jpg)

![Detection result 3](images/result3.jpg)

## Problem Statement

Wearing a helmet is the best protection against fatal head injury for two-wheeler riders, but checking helmet rules by hand is slow and depends on people watching the road or CCTV footage. This project automates the first step: finding riders without helmets and locating their number plates.

## What We Did

1. Took the YOLOv8 helmet and number plate detection project as the base and studied how it works.
2. Used the Kaggle dataset **Rider With Helmet / Without Helmet, Number Plate** (images with YOLO labels).
3. Trained a **YOLOv8s** model (transfer learning from pretrained weights) on the dataset for 10 epochs.
4. Saved the best model as `weights/best.pt`.
5. Tested the model on sample images and on new traffic photos, and saved the outputs.
6. Counted riders with and without helmets and flagged the "without helmet" ones as violations.
7. Read the number plate text with an OCR step (EasyOCR) as an extra feature.
8. Prepared notebooks that show the training code and the detection code clearly.
9. Uploaded the full project to GitHub.

## Technologies Used

- Python
- Ultralytics YOLOv8 (object detection)
- OpenCV and Matplotlib (image handling and display)
- EasyOCR (number plate text reading, optional)
- Jupyter Notebook
- Kaggle / Google Colab (GPU training)

## Dataset

- **Name:** Rider With Helmet / Without Helmet, Number Plate
- **Author:** aneesarom (Kaggle)
- **Link:** https://www.kaggle.com/datasets/aneesarom/rider-with-helmet-without-helmet-number-plate
- **Format:** images with YOLO text labels for the detected classes (rider, helmet / no helmet, number plate)

The dataset is not included in this repository because of its size. Download it from the link above if you want to retrain.

## Project Structure

| Folder / File | Purpose |
| --- | --- |
| `weights/best.pt` | Trained YOLOv8 model used for detection |
| `input/` | Put the images you want to test here |
| `output/` | Saved output images |
| `results/` | Training results (graphs and `results.csv`) |
| `training_validation/` | Training and validation outputs |
| `images/` | Result photos shown in this README |
| `model/` | Model related files |
| `Training file.ipynb` | Notebook with the training code |
| `Helmet_and_Number_Plate_Detection_using_YOLO8.ipynb` | Notebook for detection on images |
| `coco128.yaml` | Dataset configuration file |
| `yolov8s.pt`, `yolo11n.pt` | Pretrained base models |

## How to Run the Project (Windows)

### Step 1: Install Python

Install Python 3.9 or newer from https://www.python.org and tick **Add Python to PATH** during installation.

### Step 2: Download the project

```
git clone https://github.com/Valiya-Ajay/Helmet-and-Number-Plate-Detection.git
cd Helmet-and-Number-Plate-Detection
```

You can also click **Code > Download ZIP** on GitHub and extract it.

### Step 3: Create and activate a virtual environment

```
python -m venv venv
venv\Scripts\activate
```

When it is active, your prompt starts with `(venv)`.

### Step 4: Install the requirements

```
pip install ultralytics
```

For number plate text reading (optional):

```
pip install easyocr
```

### Step 5: Add your images

Copy the traffic photos you want to test into the `input` folder.

### Step 6: Run detection

```
yolo detect predict model=weights\best.pt source=input save=True
```

### Step 7: See the results

The last line of the output shows where the results were saved, for example `runs\detect\predict`. Open the folder with:

```
start runs\detect
```

Each output image shows boxes around riders, helmets or no-helmet heads, and number plates, with a confidence score.

### Run from the notebook

```
pip install jupyter
jupyter notebook
```

Open `Helmet_and_Number_Plate_Detection_using_YOLO8.ipynb` and run the cells from top to bottom with **Shift + Enter**.

## How to Retrain the Model

Training on a normal laptop CPU is very slow, so use a free GPU on Kaggle or Google Colab.

1. Create a new notebook on Kaggle and turn on a GPU (T4) and Internet.
2. Add the dataset from the link above as an input.
3. Open `Training file.ipynb` and run the training cell:

```
yolo task=detect mode=train model=yolov8s.pt data=coco128.yaml epochs=10
```

4. Download the new `best.pt` from the output and replace `weights/best.pt`.

Paths in the notebook may need to be changed to match Kaggle (`/kaggle/input`) or Colab (`/content`).

## Limitations

- Accuracy is lower on distant CCTV images where heads are very small.
- Crowded scenes with many overlapping riders are harder.
- Number plates that are small, blurred or dirty may be found but cannot always be read by OCR.
- The model was trained for a small number of epochs, so more training and more data would improve it.

## Future Work

- Train for more epochs on a larger and more varied dataset (night, rain, rear-view helmets).
- Add video and live camera detection.
- Add a web interface to upload images and download a violation report.
- Link detected plate numbers to a violation record.

## Credit

This project is based on the repository by **priyadarshpv**. The dataset is by **aneesarom** on Kaggle. Model code uses the Ultralytics YOLOv8 library.

## Author

**Ajay Valiya**
GitHub: https://github.com/Valiya-Ajay
