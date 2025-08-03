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

HuggingFace Dataset: https://huggingface.co/datasets/FoodWasteProjectBIBI/food_waste_dataset_with_added_samples


### 3. Changed the Model – CLIP Embeddings Instead of SBERT + ResNet

We replaced the previous dual-encoder setup (SBERT for ingredients + ResNet for images) with CLIP (openai/clip-vit-base-patch32) for joint image–text embeddings.

Created embeddings for each (photo, ingredient string) pair, enabling semantic alignment between visual and textual features.

Froze the CLIP backbone and fine-tuned a lightweight regression head to predict ingredient weight.

### 4. Attempted Localization with Grounding DINO + SAM (Not Completed)

We explored using Grounding DINO for open-vocabulary ingredient localization and Segment Anything (SAM) for pixel-accurate masks. The goal was to compute ingredient visibility and use mask area as a proxy for weight (area ≈ grams). However, we didn’t complete the integration in time to include it in the final pipeline.

### 5. Zero-shot evaluations with Vision-Language Models with reasoning.
We evaluated Google's Gemini 2.5-Pro in a zero-shot setting by prompting it with food plate images and asking for estimated ingredient-wise food waste. Despite having no training on the dataset, Gemini demonstrated strong per-ingredient reasoning and correlation with ground truth, though it underestimated absolute quantities.

**Observations:** Gemini achieved competitive Spearman correlation (ρ ≈ 0.71) with zero-shot inference. Simple post-hoc rescaling (×2) significantly improved total MAE without hurting relative ranking. Results suggest VLMs can generalize surprisingly well to domain-specific estimation tasks without fine-tuning.

<img src="https://github.com/user-attachments/assets/a770b671-52f7-45a3-816f-085e2fd25696" alt="image" style="width:70%;" />


## 🛠️ How to Reproduce

### 1. Clone the repository

```
git clone https://github.com/BIBI-Group/FoodWasteHackaton.git
cd food-waste-project
```

### 2. Install packages

```
numpy
torch
Pillow
transformers
scikit-learn
scipy
fiftyone
```

### 3. Run google notebooks

```
(t.b.d.)
```

### 4. Visualize with FiftyOne

```python
(t.b.d.)
```

---

## 🧠 Next Steps

* Use Grounding DINO for object detection and segmentation
  
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
