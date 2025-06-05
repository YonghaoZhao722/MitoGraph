# MitoGraph VTK 9 Compatibility Fork

This fork of MitoGraph adds compatibility with modern VTK 9.x libraries while maintaining full backward compatibility with VTK 8.x.

## Key Features

✅ **VTK 9.x Support** - Works with VTK 9.4.2 and later  
✅ **Backward Compatible** - Still supports VTK 8.2.0+  
✅ **Modern CMake** - Updated to CMake 3.12+ standards  
✅ **Same Interface** - All original command-line options preserved  
✅ **Homebrew Ready** - Works with `brew install vtk`  

## Quick Start

### Installation via Homebrew (Recommended)

```bash
# Install dependencies
brew install cmake vtk

# Clone this fork
git clone https://github.com/YonghaoZhao722/MitoGraph.git
cd MitoGraph

# Build
mkdir build && cd build
cmake ..
make

# Test
./MitoGraph -xy 0.0645 -z 0.2 -path ../data -export_image_binary
```

### What's New in This Fork

- **Modern VTK Support**: Compatible with VTK 9.x installed via Homebrew
- **API Updates**: Fixed deprecated `FindPoint()` calls for VTK 9
- **Clean Code**: Removed deprecated `register` keywords
- **Better CMake**: Modular VTK component loading
- **Documentation**: Comprehensive build instructions included

## Build Requirements

- macOS 10.15+
- CMake 3.12+
- VTK 8.2.0+ or VTK 9.x
- C++11 compatible compiler

## Differences from Original

This fork maintains 100% functional compatibility with the original MitoGraph while adding:

1. **VTK 9 API Compatibility**: All `FindPoint(x,y,z)` calls updated to `FindPoint(point[3])`
2. **Deprecated API Fixes**: Replaced `vtkLongArray` with `vtkTypeInt64Array`
3. **Modern C++**: Removed deprecated `register` storage class specifiers
4. **Improved Build System**: Better VTK version detection and module loading

## Documentation

- [VTK 9 Build Instructions](build_instructions_vtk9.md) - Detailed setup guide
- [Original README](README.md) - Original MitoGraph documentation

## Compatibility Matrix

| VTK Version | Status | Notes |
|-------------|--------|--------|
| VTK 8.2.0   | ✅ Supported | Original target version |
| VTK 9.0+    | ✅ Supported | Main improvement in this fork |
| VTK 9.4.2   | ✅ Tested | Current Homebrew version |

## Contributing

This fork welcomes contributions! Please feel free to:
- Report compatibility issues
- Submit improvements
- Add support for additional VTK versions

## License

This project maintains the same GPL-2.0 license as the original MitoGraph.

## Acknowledgments

- Original MitoGraph developers: Matheus Viana and team
- VTK development community for modern API improvements 