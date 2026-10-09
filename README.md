# Image Signal Boundary Lab

**Color Field** — an experimental, browser-based visualizer for image signals and the boundaries of an RGB cube.

Load a photograph, adjust exposure, saturation, or the tone curve, and watch the distribution of its RGB values move through—and sometimes outside—the unit cube. Touching a boundary is not, by itself, an error. The aim is to **observe** image transformations rather than automatically judge image quality.

*Work in progress. Built for exploration and education.*

## Features

- Interactive 3D RGB cube with density / particle views and rotation.
- Floating mini-cube while scrolling on mobile, with side-switch and minimize controls.
- Live analysis: out-of-range pixels, upper and lower exceedance, boundary contact, maximum exceedance, and per-channel rates.
- Exposure (EV), saturation, and an editable tone curve (tap to add a point, drag to adjust).
- Simplified vectorscope, source/result previews, and a frequency-ranked color palette.
- Local JPEG, PNG, WebP, or AVIF input **where supported by the browser**. A generated demo is included.
- Single-file application: no build step, dependencies, account, or server-side image upload.

## Try it

Open [index.html](./index.html) in a modern browser. If GitHub Pages is enabled for this repository, the same file serves as the entry point.

The default adjustment is **+0.00 EV**, **100% saturation**, and an **identity tone curve** with no editable control points. “Reset to original” restores these settings.

## Signal model and important limitations

1. The browser decodes an image into an sRGB canvas; sRGB-encoded channel values are converted to **linear RGB** for processing. The workflow assumes an sRGB interpretation and is not a complete ICC color-management or RAW pipeline.
2. The operations are applied in this order: **channel-wise tone curve → common RGB exposure multiplier → saturation adjustment about relative luminance**.
3. Floating-point values below 0 or above 1 are retained for RGB-cube and numerical analysis. Values are clipped only for the image preview and the display-encoded vectorscope/palette.
4. **Contact** with 0 or 1 and **exceedance** outside [0, 1] are distinct events. Neither alone proves visible damage or perceptual error.
5. Input images are resized for interactive performance (longest side up to 700 px in the current implementation). Numerical counts cover **all pixels of this resized analysis image**, not necessarily every pixel in the original file. The cube, vectorscope, and palette use samples or bins for visualization.
6. The vectorscope is an illustrative chroma projection of display-encoded RGB data, **not a calibrated video measurement instrument**.

This prototype should not be used as a certified color, HDR, or image-quality measurement tool.

## Privacy

Selected images are read and processed locally in the browser. The application does not send image contents to a server and does not include external analytics or dependencies in its current implementation. As with any website, hosting infrastructure may receive ordinary requests for the page itself.

## License and attribution

Code and original demo artwork are made available under the [MIT License](./LICENSE).

Copyright © 2026 **goldkiss2010-ai**.

When using third-party photographs with this tool, rights to those photographs remain with their respective owners; the software license does not grant rights to user-supplied images.

---

## 日本語

**Color Field** は、RGBキューブ内外の信号分布を観察する実験的なブラウザー用ツールです。露出・彩度・トーンカーブを変更すると、信号の分布と数値解析が更新されます。境界への接触そのものを異常とはみなしません。

画像の処理はブラウザー内で行われます。現状は簡易モデルで、元画像を縮小して解析するため、精密な色管理・品質判定には使用しないでください。

コードと自作デモ画像はMITライセンスで公開しています。第三者が撮影した画像の権利は各権利者に帰属します。
