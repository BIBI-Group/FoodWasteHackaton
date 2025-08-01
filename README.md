# 🍽️ Food Waste Estimation – Hackathon Project

## 📌 Project Summary

This project was developed at the **Food Waste Hackathon (August 2025)**, focusing on estimating food waste from annotated images of lunch trays using computer vision.

We worked with three datasets:

* Two provided by the organizers (375 and 255 annotated images)
* One created collaboratively by participants (61 new images)

Our pipeline standardizes data types, enriches annotations, and enables modeling and visualization using FiftyOne and Hugging Face.

---

## 📂 Datasets

### 1. Original Datasets from Google Drive

* **Dataset A**: 375 annotated images
* **Dataset B**: 255 annotated images
* Each image includes:

  * Image file
  * Ingredient list
  * Weight per ingredient
  * ... many other attributes, but we focused on the ingredients and weight per ingredient, as this was the core goal of the hackathon.

**Problem 1**: Dataset B lacked food segmentation.

**Solution**: We applied YOLOv8-E to each image to generate segmentation masks and stored the results directly in the FiftyOne dataset.

**Problem 2**: Dataset B did not include vector representations for image similarity, clustering, or zero-shot classification.

**Solution**: We generated CLIP-like embeddings for each image and added them to the FiftyOne dataset for future analysis (e.g., food type clustering or search).

**Problem 3**: Inconsistent data formats (e.g., `kcal_after` stored as string in some samples and float in others)

**Solution**: We developed a preprocessing script to convert all numeric attributes to float or int

**Upload**: Both cleaned datasets were merged and uploaded to Hugging Face: [Hugging Face Dataset]((https://huggingface.co/datasets/FoodWasteProjectBIBI/food_waste_merged_fiftyOneDS))

---

### 2. New Collaborative Dataset (61 Images)

We created a new set of 61 images in collaboration with other groups. Each image was annotated with:

* Ingredient list
* Weight per ingredient
* Split: train / test

**Problem 1**: The dataset did not include annotation of ingredient names, ingredient weights and train/test split compatible with the other datasets in FiftyOne format.

**Solution**: We built a Python script to generate annotations compatible with the original datasets, and uploaded the results to the same Hugging Face dataset.

**Problem 2 and 3**: Same as above.

**Solution**: Same as above.

---

## 🛠️ How to Reproduce

### 1. Clone the repository

```
git clone https://github.com/YOUR-ORG/food-waste-project.git
cd food-waste-project
```

### 2. Install dependencies

```
pip install -r requirements.txt
```

### 3. Run data cleaning script

```
python scripts/clean_dataset.py
```

This will:

* Convert mixed data types
* Merge the datasets
* Save a standardized version for FiftyOne

### 4. Visualize with FiftyOne

```python
import fiftyone as fo

dataset = fo.load_dataset("your_dataset_name")
session = fo.launch_app(dataset)
```

---

## 🧠 Next Steps

* Train a model to estimate food waste directly from images
* Use Grounding DINO for object detection and segmentation
* Use CLIP to assist with tagging and image similarity

---

## 🤝 Team

* Shahabeddin Dayani [@shahabday](https://github.com/shahabday)
* Zerina Besic [@zerina-dev](https://github.com/zerina-dev)
* Vivek Chavan [@Vivek9Chavan](https://github.com/Vivek9Chavan)
* Murilo Polla [@mrpolla](https://github.com/mrpolla)

---

## 📎 References

* [FiftyOne](https://voxel51.com/fiftyone/)
* [Hugging Face Datasets](https://huggingface.co/docs/datasets)
* [Grounding DINO](https://huggingface.co/IDEA-Research/grounding-dino-base)
* [CLIP](https://huggingface.co/openai/clip-vit-base-patch32)

---

## 📜 License

MIT License – see `LICENSE`
