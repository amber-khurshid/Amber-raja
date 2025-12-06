# Kaggle Dataset Access - Usage Guide

This guide explains how to use the Cityscape Segmentation notebook with Kaggle datasets.

## Prerequisites

1. A [Kaggle account](https://www.kaggle.com/account/login) (free to create)
2. Google Colab access (free with a Google account)

## Step-by-Step Instructions

### 1. Get Your Kaggle API Token

**Why?** The Kaggle API requires authentication to download datasets.

1. Go to [https://www.kaggle.com](https://www.kaggle.com) and sign in
2. Click on your profile picture in the top-right corner
3. Select **"Settings"** from the dropdown
4. Scroll down to the **"API"** section
5. Click the **"Create New Token"** button
6. A file named `kaggle.json` will be downloaded to your computer

**Important:** Keep this file secure! It contains your API credentials.

### 2. Open the Notebook in Google Colab

Click this link to open the notebook:
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/amber-khurshid/Amber-raja/blob/main/22P-9295_Amber_lab10.ipynb)

Or manually navigate to: `https://colab.research.google.com/github/amber-khurshid/Amber-raja/blob/main/22P-9295_Amber_lab10.ipynb`

### 3. Run the Notebook Cells

**Cell 1-3:** Read the instructions and introduction

**Cell 4:** Install Kaggle and Upload Credentials
- Run this cell
- When prompted with "Please upload your kaggle.json file:", click **"Choose Files"**
- Select the `kaggle.json` file you downloaded earlier
- Wait for "Kaggle credentials configured successfully!" message

**Cell 5:** Download the Dataset
- This will download the Cityscape dataset (~2-3 GB)
- Wait for the download to complete
- You should see: "✓ Dataset downloaded successfully!"

**Cell 6-8:** Extract and Inspect Dataset
- Cell 6: Lists the downloaded files
- Cell 7: Extracts the dataset to `/content/cityscape-dataset`
- Cell 8: Shows the dataset structure to verify correct extraction

**Cell 9-11:** Import libraries and define functions
- Standard imports and helper functions for data processing

**Cell 12:** Configure Paths and Build Datasets
- Sets `IMG_DIR` and `MASK_DIR` to the correct locations
- Verifies the paths exist
- Builds train, validation, and test datasets
- You should see: "✓ Datasets created successfully"

**Cells 13-22:** Train and Evaluate the Model
- Visualize sample data
- Define the U-Net architecture
- Train the model (this will take time, especially without GPU)
- Visualize results

## Troubleshooting

### Issue: "403 Forbidden" error when downloading

**Solution:** 
1. Make sure you've accepted the dataset terms on Kaggle
2. Visit [https://www.kaggle.com/datasets/electraawais/cityscape-dataset](https://www.kaggle.com/datasets/electraawais/cityscape-dataset)
3. Click "Download" (you don't need to actually download, just accept terms)
4. Re-run the download cell

### Issue: "No such file or directory" for IMG_DIR or MASK_DIR

**Solution:**
1. Run Cell 8 to inspect the actual dataset structure
2. Look for directories named `leftImg8bit` and `gtFine`
3. Update the paths in Cell 12 if they're in a different location
4. The paths might be nested like: `/content/cityscape-dataset/Cityscape Dataset/leftImg8bit`

### Issue: "File too large" or download interrupted

**Solution:**
1. The dataset is large (~2-3 GB). Ensure stable internet connection
2. If download fails, simply re-run Cell 5
3. Consider using Colab Pro for better stability and faster downloads

### Issue: "Out of memory" during training

**Solution:**
1. In Cell 12, reduce the `batch_size` from 4 to 2 or 1
2. In Colab, go to Runtime → Change runtime type → Hardware accelerator → GPU
3. Consider using a smaller subset of the data for testing

## Tips for Best Results

1. **Use GPU:** Go to Runtime → Change runtime type → Hardware accelerator → GPU
2. **Monitor Training:** Watch the loss and IoU metrics to ensure the model is learning
3. **Adjust Hyperparameters:** Feel free to modify epochs, batch size, or learning rate
4. **Save Your Model:** Add a cell to save the trained model if you want to reuse it

## Dataset Information

- **Dataset:** Cityscape Dataset by electraawais
- **Size:** ~2-3 GB
- **Content:** Urban street scenes with semantic segmentation annotations
- **Classes:** Multiple classes including road, sidewalk, building, vehicle, pedestrian, etc.
- **Format:** Images (leftImg8bit) and corresponding masks (gtFine)

## Additional Resources

- [Kaggle API Documentation](https://github.com/Kaggle/kaggle-api)
- [U-Net Paper](https://arxiv.org/abs/1505.04597)
- [TensorFlow Documentation](https://www.tensorflow.org/)
- [Google Colab Guide](https://colab.research.google.com/notebooks/intro.ipynb)

## Support

If you encounter issues:
1. Check the troubleshooting section above
2. Ensure all previous cells ran successfully
3. Read the error messages carefully - they often indicate the exact problem
4. Contact the repository owner or open an issue on GitHub

---

**Last Updated:** December 2025
