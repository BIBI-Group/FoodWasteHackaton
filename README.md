Got it. Here is the **correctly formatted `README.md`** version — no conflicting escape sequences, no triple backticks inside fenced blocks, and safe to copy directly into a Markdown file:

---

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

**Problem**: Inconsistent data formats (e.g., `kcal_after` stored as string in some samples and float in others)

**Solution**: We developed a preprocessing script to:

* Convert all numeric attributes to float or int
* Standardize attribute names and units
* Remove or flag invalid entries

**Upload**: Both cleaned datasets were uploaded to Hugging Face
👉 [Hugging Face Dataset A](https://huggingface.co/datasets/YOUR-DATASET-A)
👉 [Hugging Face Dataset B](https://huggingface.co/datasets/YOUR-DATASET-B)

---

### 2. New Collaborative Dataset (61 Images)

We created a new set of 61 images in collaboration with other groups. Each image was annotated with:

* Ingredients
* Weight per ingredient

We built a Python script to generate annotations compatible with the original datasets, and uploaded the results to Hugging Face.

👉 [Hugging Face Collaborative Dataset](https://huggingface.co/datasets/YOUR-COLLAB-DATASET)

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

* Alice Smith (@alice)
* Bob Johnson (@bob)
* Murilo Polla (@murilopolla)

---

## 📎 References

* [FiftyOne](https://voxel51.com/fiftyone/)
* [Hugging Face Datasets](https://huggingface.co/docs/datasets)
* [Grounding DINO](https://huggingface.co/IDEA-Research/grounding-dino-base)
* [CLIP](https://huggingface.co/openai/clip-vit-base-patch32)

---

## 📜 License

MIT License – see `LICENSE`

---

Let me know if you'd like:

* A version in plain text (no Markdown)
* A downloadable `README.md` file
* To add your real Hugging Face links and dataset names now
