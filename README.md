<p align="center">
  <img src="doc/mitograph.png" width="auto" height="380" title="MoCo Logo">
</p>

# MitoGraph Enhanced - Z-Adaptive Processing with Improved Dark Region Sensitivity

This is an enhanced version of MitoGraph with significant improvements to z-adaptive processing and dark region detection. The modifications specifically address the original MitoGraph's limitation in detecting mitochondrial structures in darker regions of the image, particularly when using z-adaptive mode.

## 🎯 Core Problem Addressed

### **The Dark Region Problem**
In many fluorescence microscopy images of mitochondria, particularly in live-cell imaging:
- **Intensity Variations**: Mitochondria can appear significantly darker in certain cellular regions
- **Depth-Related Dimming**: Deeper z-slices often show reduced fluorescence intensity
- **Photobleaching Effects**: Extended imaging can cause uneven brightness across the sample
- **Original Algorithm Failure**: The original z-adaptive algorithm would set thresholds too high for dark regions, causing mitochondrial structures to be completely missed

### **Our Solution**
- **Enhanced Threshold Mapping**: User threshold now directly maps to local intensity characteristics
- **Dark Region Detection**: Automatic identification and special handling of low-intensity regions
- **Adaptive Sensitivity**: Dynamic adjustment of detection sensitivity based on local block statistics
- **Independent Processing**: Z-adaptive can now work independently without XY-adaptive interference

## 🚀 Key Enhancements

### 1. **Enhanced Z-Adaptive Processing**
- **Improved Dark Region Detection**: Enhanced sensitivity to low-intensity mitochondrial structures
- **Independent Z-Adaptive Mode**: Z-adaptive no longer automatically enables XY-adaptive threshold
- **Intelligent Block Processing**: Better handling of intensity variations across z-slices
- **Predictable Threshold Mapping**: User threshold now directly controls segmentation sensitivity

### 2. **Structural Connectivity Enhancement**
- **Pre-Binarization Processing**: Added `EnhanceStructuralConnectivity()` function that improves connectivity before binarization
- **Multi-Scale Gaussian Smoothing**: Applies different smoothing levels to bridge gaps while preserving details
- **Intelligent Gap Bridging**: Detects and connects weak signals surrounded by strong neighbors in 26-neighborhood
- **Adaptive Weight Fusion**: Dynamically balances original and enhanced signals based on local intensity

### 3. **Skeleton Fragment Connection**
- **Post-Skeletonization Enhancement**: Added `ConnectSkeletonFragments()` function to reduce skeleton fragmentation
- **Endpoint Detection**: Automatically identifies skeleton endpoints (degree-1 nodes)
- **Distance-Based Connection**: Connects nearby endpoints within reasonable distance thresholds
- **Intelligent Bridge Creation**: Adds new skeleton segments to connect fragmented structures

### 4. **Dark Region Optimization**
- **Enhanced Low-Intensity Detection**: Improved algorithms for detecting mitochondria in dark image regions
- **Adaptive Sensitivity Scaling**: Automatic adjustment of detection sensitivity based on local intensity
- **Noise Reduction**: Better discrimination between true mitochondrial structures and background noise

### 5. **Smart Component Filtering**
- **Adaptive Component Removal**: Minimum component size adjusts based on threshold sensitivity
- **Sensitivity-Based Thresholds**:
  - Sensitive (< 0.1): Preserves 3+ voxel components
  - Moderate (0.1-0.2): Preserves 5+ voxel components  
  - Conservative (> 0.2): Preserves 8+ voxel components

### 6. **Intelligent Activation System**
- **Automatic Enhancement**: Connectivity enhancements activate based on usage patterns
- **Activation Conditions**:
  - Z-adaptive mode: `-z-adaptive`
  - Sensitive thresholds: `-threshold < 0.2`
  - Ultra-sensitive: Additional enhancements for `-threshold < 0.1`

## 📋 Usage Examples

### **Primary Use Case: Z-Adaptive for Dark Region Detection**
```bash
# Recommended for images with dark mitochondrial structures
./MitoGraph -xy 0.0645 -z 0.2 -path /your/path -threshold 0.1 -z-adaptive
```

### **For Very Dark or Low-Contrast Images**
```bash
# Increased sensitivity for challenging dark regions
./MitoGraph -xy 0.0645 -z 0.2 -path /your/path -threshold 0.05 -z-adaptive
```

### **For Mixed Intensity Images**
```bash
# Balanced processing for images with both bright and dark regions
./MitoGraph -xy 0.0645 -z 0.2 -path /your/path -threshold 0.15 -z-adaptive
```

### **Z-Adaptive Only (Without XY-Adaptive)**
```bash
# Pure z-adaptive processing without xy-adaptive interference
./MitoGraph -xy 0.0645 -z 0.2 -path /your/path -threshold 0.1 -z-adaptive
```

### **Original Processing (For Comparison)**
```bash
# Standard processing without z-adaptive enhancements
./MitoGraph -xy 0.0645 -z 0.2 -path /your/path -threshold 0.1667
```

## 🔧 Technical Details

### **Core Z-Adaptive Improvements**
- **Enhanced `BinarizeAndConvertDoubleToCharZAdaptiveConservative()`**: Improved threshold mapping for dark regions
- **Independent Z-Adaptive Logic**: Decoupled from XY-adaptive automatic activation
- **Dark Region Enhancement**: Better sensitivity to low-intensity mitochondrial structures
- **Block-Based Processing**: Intelligent handling of intensity variations across z-slices

### **Enhanced Functions Added**
- `EnhanceStructuralConnectivity()`: Pre-binarization connectivity enhancement specifically for dark regions
- `ConnectSkeletonFragments()`: Post-skeletonization fragment connection
- Modified threshold mapping algorithms for improved dark region detection

### **Algorithm Improvements**
1. **Dark Region Threshold Mapping**: Direct user threshold to local intensity space with enhanced sensitivity
2. **Adaptive Block Processing**: Different enhancement levels based on local intensity distribution
3. **Boundary Preservation**: Maintains reasonable intensity bounds while preserving dark structures
4. **Connectivity Preservation**: Reduces over-segmentation in dark regions while maintaining structural detail

### **Debug Information**
Enhanced debug output for z-adaptive processing shows:
- Original and mapped threshold values for each z-block
- Block statistics (mean, std, min, max) with dark region indicators
- Component removal statistics optimized for dark regions
- Connectivity enhancement status and dark region detection metrics

## 🧪 Validation

These z-adaptive enhancements have been specifically tested with:
- **Dark mitochondrial networks** in low-light imaging conditions
- **Mixed intensity images** with both bright and dark mitochondrial structures
- **Various threshold sensitivity levels** for optimal dark region detection
- **Different imaging modalities** including fluorescence microscopy with low signal-to-noise ratios
- **Challenging experimental conditions** where original MitoGraph failed to detect dark structures

## 🏗️ Building

```bash
mkdir build
cd build
cmake ..
make
```
