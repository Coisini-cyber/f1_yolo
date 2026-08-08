  f1_yolo – Ultralytics YOLOv8 Training Run (train2)

  This repository contains the outputs of a YOLOv8 detection training run performed with Ultralytics YOLO11n.
  All files are the direct products of that run: training arguments, metrics, visualisations, and model checkpoints.

  📂 Repository Tree

  f1_yolo/
  ├── args.yaml                 # Training hyper‑parameters (YAML)
  ├── results.csv               # Per‑epoch training/validation metrics (CSV)
  ├── results.png               # Combined loss/mAP/precision/recall curves
  ├── BoxF1_curve.png           # F1‑score vs confidence threshold
  ├── BoxPR_curve.png           # Precision‑Recall curve
  ├── BoxP_curve.png            # Precision vs confidence threshold
  ├── BoxR_curve.png            # Recall vs confidence threshold
  ├── confusion_matrix.png      # Confusion matrix (raw counts)
  ├── confusion_matrix_normalized.png   # Normalised confusion matrix
  ├── labels.jpg                # Example image with ground‑truth labels
  ├── train_batch0.jpg          # Sample training batch 0 (image + GT boxes)
  ├── train_batch1.jpg          # Sample training batch 1
  ├── train_batch2.jpg          # Sample training batch 2
  ├── train_batch3060.jpg       # Later training batch (illustrates convergence)
  ├── train_batch3061.jpg
  ├── train_batch3062.jpg
  ├── val_batch0_labels.jpg     # Validation batch 0 – ground truth
  ├── val_batch0_pred.jpg       # Validation batch 0 – model predictions
  ├── val_batch1_labels.jpg
  ├── val_batch1_pred.jpg
  ├── val_batch2_labels.jpg
  ├── val_batch2_pred.jpg
  └── weights/
      ├── best.pt               # Best checkpoint (highest mAP_0.5:0.95)
      └── last.pt               # Last checkpoint (final epoch)

  ▎ Tip: If you prefer a lighter repository, add the unwanted file patterns to .gitignore (e.g., *.jpg, *.png, *.pt) or
  ▎ use Git LFS for the large binary files.

  🚀 Quick Start

  1. Clone the repo

  git clone https://github.com/<your-username>/f1_yolo.git
  cd f1_yolo

  2. View the training configuration

  cat args.yaml
  Typical entries:
  - task: detect
  - model: yolov8n.pt (or the base model you used)
  - data: path/to/dataset.yaml
  - epochs, batch, imgsz, lr0, optimizer, augmentation settings, etc.

  3. Load the model for inference

  from ultralytics import YOLO

  # Load the best checkpoint (or last.pt)
  model = YOLO("weights/best.pt")

  # Run inference on an image or folder
  results = model.predict(source="path/to/image.jpg", conf=0.25)

  # Show or save results
  results[0].show()               # opens a window with detections
  results[0].save(save_dir="preds")  # saves annotated images

  4. Review training progress

  - Open results.png to see loss, mAP, precision, recall curves.
  - Open the Box*_curve.png files to decide on an optimal confidence threshold.
  - Examine the confusion matrices to understand per‑class performance.

  5. Continue training / fine‑tune

  # Continue from the last checkpoint
  yolo task=detect mode=train model=weights/last.pt data=path/to/dataset.yaml epochs=50 batch=16

  # Or start a fresh run using the same hyper‑parameters
  yolo task=detect mode=train model=yolov8n.pt data=path/to/dataset.yaml cfg=args.yaml

  📈 Metrics (from results.csv)

  The CSV contains one row per epoch with columns such as:
  - epoch
  - train/box_loss
  - train/cls_loss
  - train/dfl_loss
  - metrics/precision
  - metrics/recall
  - metrics/mAP_0.5
  - metrics/mAP_0.5:0.95
  - val/box_loss
  - val/cls_loss
  - val/dfl_loss

  Open the file in Excel, pandas, or any spreadsheet tool for detailed analysis and plotting.

  🛠️ Requirements

  - Python ≥ 3.8
  - ultralytics (install via pip install ultralytics)
  - Optional: opencv-python, matplotlib, pandas for visualisation/analysis.

  pip install ultralytics opencv-python matplotlib pandas

  📄 License

  The files in this repo are training outputs.
  The underlying Ultralytics YOLOv8 code is licensed under the AGPL‑3.0 license.
  See the Ultralytics YOLOv8 License for details.

  🙋‍♂️ Contact / Support

  If you have questions about the training setup, model usage, or wish to share improvements, feel free to open an issue
  or drop a message.

  Happy detecting! 🚦
