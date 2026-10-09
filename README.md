# 色のかたち / Shape of Color

RGB信号の分布と変形を、三次元空間で観察するブラウザー用ビジュアライザーです。

**画像**モードでは写真からRGB分布をつくり、露出・彩度・トーンカーブによる変化を観察します。**CUBE**モードでは写真に依存しない均一なRGB立方体を使い、信号変換そのものを可視化します。

**Shape of Color** is an experimental, browser-based visualizer for RGB signal distributions and their transformations. Its **画像 (Image)** mode uses real photographs; its **CUBE** mode starts from a synthetic, uniformly sampled RGB cube. The goal is observation, not automatic judgment of image quality. Contact with a boundary is not by itself an error.

*Work in progress. Built for exploration and education.*

## Features

- Interactive 3D RGB cube with density / particle views and rotation.
- Floating mini-cube while scrolling on mobile, with side-switch and minimize controls.
- Live analysis: out-of-range pixels, upper and lower exceedance, boundary contact, maximum exceedance, and per-channel rates.
- Exposure (EV), saturation, and an editable tone curve (tap to add a point, drag to adjust).
- Simplified vectorscope, source/result previews, and a frequency-ranked color palette.
- Local JPEG, PNG, WebP, or AVIF input **where supported by the browser**. A generated demo is included.
- Single-file application: no build step, dependencies, account, or server-side image upload.

## View modes

Use **画像 / 入力画像の分布** for photographs and image-derived statistics. Use **CUBE / 均一RGB立方体** for a **separate conceptual visualization**. Cube mode does **not** use the uploaded image as its input.

### CUBE: uniform starting volume

CUBE is an **image-independent concept visualizer**. It starts with 13,824 evenly stratified synthetic RGB samples: one point in each cell of a 24 × 24 × 24 division of the unit cube. All displayed particles use consistent size and nominal opacity.

The concept view offers independent exposure, saturation and an editable RGB tone curve (tap to add, drag to adjust), plus optional signal Log and clipping. These operations apply in the order:

`Tone curve → signal Log → exposure → saturation → optional clip`

The original cube and point distribution remain faintly visible after a transform (ghost overlay). The twelve transformed edges are drawn to make the change of shape visible. **There is no extra surface-particle layer or surface highlighting.** The out-of-range percentage describes the interior samples *before* optional clipping.

The camera automatically fits the full transformed object, including the exact transformed corners; zoom (45–180% of the fitted framing) remains adjustable. On phones, the cube follows scrolling as a floating mini-view while editing the concept curve, independently of the image-based 画像 mode. The mini-view can be rotated, minimized, or moved to the other side of the screen.

The view-coordinate mapping (Linear, sRGB or normalized Log) is independent of the signal transforms, and never changes the stored synthetic values. Display modes are particles (default in CUBE), density and Log density. Coordinate Log, signal Log, and density Log are three distinct operations.

The photo-based 画像 workspace retains its own image input, transforms, numerical analysis, vectorscope and normal small floating cube. CUBE edits do not change 画像 input data.

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

**色のかたち / Shape of Color** は、RGBキューブ内外の信号分布を観察する実験的なブラウザー用ツールです。露出・彩度・トーンカーブを変更すると、信号の分布と数値解析が更新されます。境界への接触そのものを異常とはみなしません。

画像の処理はブラウザー内で行われます。現状は簡易モデルで、元画像を縮小して解析するため、精密な色管理・品質判定には使用しないでください。

コードと自作デモ画像はMITライセンスで公開しています。第三者が撮影した画像の権利は各権利者に帰属します。
