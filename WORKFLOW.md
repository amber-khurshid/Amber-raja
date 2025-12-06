# Workflow Diagram

## Kaggle Dataset Access Workflow

```
┌─────────────────────────────────────────────────────────────┐
│  STEP 1: Get Kaggle API Credentials                        │
├─────────────────────────────────────────────────────────────┤
│  1. Go to kaggle.com/settings/account                       │
│  2. Click "Create New Token"                                │
│  3. Download kaggle.json file                               │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ↓
┌─────────────────────────────────────────────────────────────┐
│  STEP 2: Open Notebook in Google Colab                     │
├─────────────────────────────────────────────────────────────┤
│  Click the "Open in Colab" badge or use the direct link    │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ↓
┌─────────────────────────────────────────────────────────────┐
│  CELL 1: Read Instructions                                  │
├─────────────────────────────────────────────────────────────┤
│  • Comprehensive setup guide                                │
│  • Prerequisites and requirements                           │
│  • Troubleshooting tips                                     │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ↓
┌─────────────────────────────────────────────────────────────┐
│  CELL 4: Setup Kaggle API                                   │
├─────────────────────────────────────────────────────────────┤
│  !pip install -q kaggle                                     │
│  files.upload() ← Upload your kaggle.json here              │
│  Setup credentials in ~/.kaggle/                            │
│  ✓ Verification: "Credentials configured successfully!"     │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ↓
┌─────────────────────────────────────────────────────────────┐
│  CELL 5: Download Dataset                                   │
├─────────────────────────────────────────────────────────────┤
│  !kaggle datasets download -d electraawais/cityscape-..     │
│  ✓ Verification: Check file exists and show size            │
│  Output: "✓ Dataset downloaded successfully!"               │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ↓
┌─────────────────────────────────────────────────────────────┐
│  CELL 6: Check Downloaded Files                             │
├─────────────────────────────────────────────────────────────┤
│  !ls -lh                                                    │
│  Verify cityscape-dataset.zip is present                    │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ↓
┌─────────────────────────────────────────────────────────────┐
│  CELL 7: Extract Dataset                                    │
├─────────────────────────────────────────────────────────────┤
│  !unzip -q cityscape-dataset.zip -d /content/cityscape-...  │
│  Extract to: /content/cityscape-dataset                     │
│  List extracted contents                                    │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ↓
┌─────────────────────────────────────────────────────────────┐
│  CELL 8: Inspect Dataset Structure                          │
├─────────────────────────────────────────────────────────────┤
│  Walk through directory structure                           │
│  Display folder hierarchy                                   │
│  Show sample files                                          │
│  → Helps identify correct paths for IMG_DIR/MASK_DIR        │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ↓
┌─────────────────────────────────────────────────────────────┐
│  CELLS 9-11: Setup and Helper Functions                     │
├─────────────────────────────────────────────────────────────┤
│  • Import TensorFlow and dependencies                       │
│  • Define image/mask parsing functions                      │
│  • Setup data augmentation                                  │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ↓
┌─────────────────────────────────────────────────────────────┐
│  CELL 12: Configure Paths and Build Datasets                │
├─────────────────────────────────────────────────────────────┤
│  IMG_DIR = "/content/cityscape-dataset/leftImg8bit"         │
│  MASK_DIR = "/content/cityscape-dataset/gtFine"             │
│  ✓ Verify paths exist                                       │
│  Build train/val/test datasets                              │
│  Output: "✓ Datasets created successfully"                  │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ↓
┌─────────────────────────────────────────────────────────────┐
│  CELLS 13-14: Data Visualization                            │
├─────────────────────────────────────────────────────────────┤
│  • Display sample images and masks                          │
│  • Verify data loading is correct                           │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ↓
┌─────────────────────────────────────────────────────────────┐
│  CELLS 15-18: Build U-Net Model                             │
├─────────────────────────────────────────────────────────────┤
│  • Define encoder and decoder blocks                        │
│  • Build complete U-Net architecture                        │
│  • Compile model with loss and metrics                      │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ↓
┌─────────────────────────────────────────────────────────────┐
│  CELLS 19-20: Train Model                                   │
├─────────────────────────────────────────────────────────────┤
│  • Setup callbacks (early stopping)                         │
│  • Train for up to 40 epochs                                │
│  • Monitor loss and IoU metrics                             │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ↓
┌─────────────────────────────────────────────────────────────┐
│  CELL 21: Visualize Training Results                        │
├─────────────────────────────────────────────────────────────┤
│  • Plot loss over epochs                                    │
│  • Plot Mean IoU over epochs                                │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ↓
┌─────────────────────────────────────────────────────────────┐
│  CELLS 22-23: Evaluate and Predict                          │
├─────────────────────────────────────────────────────────────┤
│  • Define visualization function                            │
│  • Show predictions on test images                          │
│  • Compare: Original | True Mask | Predicted Mask           │
└─────────────────────────────────────────────────────────────┘

═══════════════════════════════════════════════════════════════

## Key Improvements Made

✓ Added automatic kaggle.json upload prompt
✓ Added verification after each critical step
✓ Fixed extraction path to /content/cityscape-dataset
✓ Corrected IMG_DIR and MASK_DIR paths
✓ Added dataset structure inspection
✓ Added path existence checks before training
✓ Removed 18 redundant task cells
✓ Added comprehensive instructions

═══════════════════════════════════════════════════════════════

## Before vs After

BEFORE:
❌ Manual kaggle.json setup with !mv command
❌ Wrong extraction paths
❌ Hardcoded /kaggle/input paths (Kaggle Kernels specific)
❌ No verification steps
❌ 40 cells with many redundant ones
❌ Confusing task section at the end

AFTER:
✅ Interactive file upload with files.upload()
✅ Correct extraction to /content/cityscape-dataset
✅ Colab-compatible paths
✅ Verification at each step
✅ 23 streamlined cells
✅ Clear, linear workflow

═══════════════════════════════════════════════════════════════
```
