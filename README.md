# YOLOv1 Custom Vehicle Detection

This project implements YOLOv1 for vehicle detection using either the original Pascal VOC dataset or any custom dataset in Pascal VOC format (e.g., exported from Roboflow).

## Project Structure

```
main/
  requirements.txt
  config/
    voc.yaml
  dataset/
    voc.py
  loss/
    yolov1_loss.py
  models/
    yolo.py
  tools/
    train.py
    infer.py
  utils/
    visualization_utils.py
<your_custom_dataset>/  # For custom datasets (example: my_dataset/)
  train/
  test/
  valid/ (optional)
data/  # For original Pascal VOC (VOC2007, VOC2012, etc.)
  VOC2007/
  VOC2012/
  VOC2007-test/
```

## Setup

1. **Install dependencies**
   ```bash
   pip install -r main/requirements.txt
   ```

---

## Using the Original Pascal VOC Dataset

1. **Download Pascal VOC**
   - Download VOC2007 and/or VOC2012 from the official site or [hosted mirrors](http://host.robots.ox.ac.uk/pascal/VOC/).
   - Place the extracted folders in `data/` so you have, for example, `data/VOC2007/`, `data/VOC2012/`, etc.

2. **Configure**
   - In `main/config/voc.yaml`, set:
     ```yaml
     train_im_sets: ['data/VOC2007', 'data/VOC2012']
     test_im_sets: ['data/VOC2007-test']
     num_classes: 20
     ```
   - The dataset loader will use the 20 VOC classes by default.

3. **Train**
   ```bash
   python main/tools/train.py --config main/config/voc.yaml
   ```

4. **Inference**
   ```bash
   python main/tools/infer.py --config main/config/voc.yaml --weights voc/yolo_voc2007.pth --img_path path/to/image.jpg
   ```

---

## Using a Custom Dataset (Pascal VOC Format)

1. **Prepare Your Dataset**
   - Place your Pascal VOC-format dataset in a folder (e.g., `my_dataset/`).
   - Each split (`train`, `test`, etc.) should contain `Annotations/`, `JPEGImages/`, and `ImageSets/Main/` with the appropriate `.txt` files listing image IDs.

2. **Configure**
   - In `main/config/voc.yaml`, set:
     ```yaml
     train_im_sets: ['my_dataset/train']
     test_im_sets: ['my_dataset/test']
     num_classes: 1  # or the number of your custom classes
     ```
   - For a single class (e.g., 'car'), the dataset loader will use `['car']` by default. For multi-class, update the class list in `main/dataset/voc.py`.

3. **Train**
   ```bash
   python main/tools/train.py --config main/config/voc.yaml
   ```

4. **Inference**
   ```bash
   python main/tools/infer.py --config main/config/voc.yaml --weights voc/yolo_voc2007.pth --img_path path/to/image.jpg
   ```


## Notes
- The dataset loader and model are already adapted for both Pascal VOC and custom datasets.
- For multi-class custom datasets, update the class list in `main/dataset/voc.py` and `num_classes` in the config.
- For evaluation, use or adapt `tools/infer.py` or add a script for mAP/IoU calculation.



## Results

The following images are the predictions on the test folder of the custom `voc_format_data`, which is by default the dataset that this model works on (You may change the input data yourself accordingly to the instructions above)

![alt text](Screenshot%202025-07-10%20153533.png)
![alt text](Screenshot%202025-07-10%20153546.png)
![alt text](Screenshot%202025-07-10%20153602.png)
![alt text](Screenshot%202025-07-10%20153617.png)



## License
This project is for educational and research purposes.
