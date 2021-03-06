# SepConv-iOS (CoreML + Metal)

![Platforms](https://img.shields.io/badge/platform-iOS-lightgrey.svg) ![Swift Version](https://img.shields.io/badge/swift-5.0-orange.svg) ![License](https://img.shields.io/badge/license-MIT-blue.svg)

SepConv-iOS is a fully functioning iOS implementation of the paper [Video Frame Interpolation via Adaptive Separable Convolution](https://arxiv.org/abs/1708.01692) by _Niklaus et al_. The model was converted to CoreML starting from our own PyTorch implementation ([code](https://github.com/martkartasev/sepconv) on GitHub, [report](https://arxiv.org/abs/1809.07759) on ArXiv), while the separable convolution operation was written in Metal.

-------
## Known issues / limitations

- The input size is fixed as dictated by the ONNX format, which is why this repository contains 4 different models with different input sizes.
- The model supporting 512x512 frames as input will use a considerable amount of memory during the forward pass. The larger model (1024x1024) will likely ran out of memory on most devices.
- Artifacts (caused by clipping) may appear in the output.
- The conversion of upsampling modules via ONNX is rather limited. The `align_angles` property must be set to `false` (see conversion script), and the `_convert_upsample` in `onnx_coreml/_operators.py` must be modified to support bilinear upsampling (simply add `"bilinear": "BILINEAR"` in the `mode_convert` dictionary).


-------
## License

All files included in this project are released under the MIT license, with the exception of the icons and the CoreML models. The use of the models is allowed for academic purposes only, under the terms described [here](https://github.com/sniklaus/pytorch-sepconv).

-------
## Acknowledgements

Icons included in the app are made by [Freepik](https://www.freepik.com) from [www.flaticon.com](https://www.flaticon.com).
