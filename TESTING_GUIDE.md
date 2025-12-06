# Testing Guide for Repository Owner

This guide helps you test the fixed Kaggle dataset access functionality.

## Quick Test (5 minutes)

### Prerequisites
1. A Kaggle account (free at https://www.kaggle.com)
2. Your kaggle.json file (download from https://www.kaggle.com/settings/account)

### Testing Steps

1. **Open the notebook in Colab**
   - Click this link: https://colab.research.google.com/github/amber-khurshid/Amber-raja/blob/main/22P-9295_Amber_lab10.ipynb
   - Or use the badge in README.md

2. **Read Cell 1**
   - Verify the instructions are clear
   - Check that the setup guide makes sense

3. **Run Cell 4 (Kaggle Setup)**
   ```
   Expected: 
   - "Please upload your kaggle.json file:" message
   - File chooser button appears
   - After upload: "✓ Kaggle credentials configured successfully!"
   
   Test:
   - Upload your kaggle.json
   - Verify success message appears
   
   Edge Case:
   - Try uploading a wrong file (e.g., test.txt)
   - Should see: ValueError with "kaggle.json not found in uploaded files"
   ```

4. **Run Cell 5 (Download Dataset)**
   ```
   Expected:
   - Dataset downloads (may take 2-5 minutes for ~2-3 GB)
   - "✓ Dataset downloaded successfully!"
   - File size shown (e.g., "File size: 2.34 GB")
   
   Note: Large download, requires stable internet
   ```

5. **Run Cell 6 (Check Files)**
   ```
   Expected:
   - Shows cityscape-dataset.zip in directory listing
   ```

6. **Run Cell 7 (Extract Dataset)**
   ```
   Expected:
   - "✓ Dataset extracted to /content/cityscape-dataset"
   - Shows extracted folders
   
   Rerun Test:
   - Run cell again
   - Should see: "Dataset directory already exists. Skipping extraction."
   ```

7. **Run Cell 8 (Inspect Structure)**
   ```
   Expected:
   - Tree-like directory structure display
   - Shows folders like leftImg8bit, gtFine, etc.
   ```

8. **Run Cells 9-11 (Setup)**
   ```
   Expected:
   - Libraries import successfully
   - No errors
   ```

9. **Run Cell 12 (Build Datasets)**
   ```
   Expected:
   - "✓ Found IMG_DIR: /content/cityscape-dataset/..."
   - "✓ Found MASK_DIR: /content/cityscape-dataset/..."
   - "Building datasets..."
   - "✓ Datasets created successfully"
   
   Success Criteria:
   - Both IMG_DIR and MASK_DIR found automatically
   - No FileNotFoundError
   - Datasets build without errors
   ```

10. **Spot Check Remaining Cells**
    - Cell 13-14: Data visualization (optional but nice to see)
    - Don't need to run full training (takes time)

## What to Look For

### ✅ Success Indicators
- Clear prompts for user actions
- Green checkmarks (✓) for successful steps
- File size and progress information
- Auto-detected paths shown
- No errors or warnings

### ⚠️ Warning Signs (These are OK)
- "⚠ Could not auto-detect IMG_DIR" → Path fallback working
- Large download time → Dataset is big, this is normal
- "Dataset directory already exists" → Duplicate prevention working

### ❌ Problems (Report These)
- File upload doesn't work
- Download fails with 403 error → Need to accept dataset terms on Kaggle
- Paths not found after extraction → Check dataset structure in Cell 8
- Any Python exceptions or tracebacks

## Expected Output Examples

### Cell 4 Success:
```
Please upload your kaggle.json file:
Saving kaggle.json to kaggle.json
✓ Kaggle credentials configured successfully!
```

### Cell 5 Success:
```
Dataset URL: https://www.kaggle.com/datasets/electraawais/cityscape-dataset
Downloading cityscape-dataset.zip to /content
100%|██████████| 2.34G/2.34G [03:45<00:00, 11.2MB/s]
✓ Dataset downloaded successfully!
File size: 2.34 GB
```

### Cell 12 Success:
```
✓ Found IMG_DIR: /content/cityscape-dataset/leftImg8bit
✓ Found MASK_DIR: /content/cityscape-dataset/gtFine

Building datasets...
✓ Datasets created successfully
```

## Troubleshooting During Testing

### Issue: 403 Forbidden
**Fix**: Go to https://www.kaggle.com/datasets/electraawais/cityscape-dataset and click "Download" to accept terms

### Issue: Path not found
**Fix**: Check Cell 8 output to see actual structure, adjust paths if needed

### Issue: Out of memory
**Fix**: In Cell 12, change `batch_size=4` to `batch_size=2` or `1`

### Issue: Runtime disconnected
**Fix**: Large download/processing. Just reconnect and continue where left off (extraction will be skipped if already done)

## Performance Notes

Approximate times on standard Colab:
- Cell 4: < 10 seconds
- Cell 5: 2-5 minutes (depends on internet speed)
- Cell 7: 1-2 minutes (extraction)
- Cell 12: 30-60 seconds (dataset building)

Use GPU runtime for training:
- Runtime → Change runtime type → Hardware accelerator → GPU

## What Changed - Testing Focus

Test these specific improvements:

1. **Credentials Upload** (Cell 4)
   - [ ] File upload works smoothly
   - [ ] Wrong file rejected with clear error
   - [ ] Success message appears

2. **Path Auto-Detection** (Cell 12)
   - [ ] Paths found automatically
   - [ ] Works with different dataset structures
   - [ ] Clear error if paths missing

3. **Verification Steps** (Cells 5, 7, 12)
   - [ ] Each critical step shows success/failure
   - [ ] File size shown after download
   - [ ] Duplicate extraction prevented

4. **Documentation** (README, USAGE_GUIDE)
   - [ ] Instructions are clear
   - [ ] Links work correctly
   - [ ] Troubleshooting section helpful

## Minimal Test (If Short on Time)

Just run these 5 cells to verify core functionality:
1. Cell 4 → Upload credentials
2. Cell 5 → Download (can interrupt after it starts if low on time)
3. Cell 7 → Extract (skip if didn't complete download)
4. Cell 8 → Inspect structure
5. Cell 12 → Build datasets (skip if didn't extract)

## Reporting Results

After testing, please note:
- ✅ What worked perfectly
- ⚠️ What needed adjustments
- ❌ What failed (with error messages)
- 💡 Suggestions for improvement

You can report back by:
- Creating an issue on GitHub
- Commenting on the PR
- Emailing directly

---

**Note**: Full model training (Cells 19-20) takes 30-60+ minutes and is not needed for testing the dataset access fixes. The key is verifying Cells 1-12 work correctly.

Thank you for testing! 🙏
