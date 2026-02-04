# Osaurus Vision

An Osaurus plugin that provides macOS Vision framework capabilities for AI agents. Enables text detection, face analysis, background removal, pose detection, and more.

## Tools

### Detection Tools (Read-only)

| Tool | Description |
|------|-------------|
| `detect_text` | Detect and recognize text in images using OCR |
| `detect_document` | Detect document boundaries for perspective correction |
| `detect_barcodes` | Detect and decode barcodes and QR codes |
| `detect_faces` | Detect faces with optional facial landmarks |
| `detect_rectangles` | Detect rectangular shapes (documents, cards, screens) |
| `classify_image` | Classify images using Apple's built-in classifier |
| `detect_horizon` | Detect horizon angle for auto-rotation |
| `detect_body_pose` | Detect human body poses (19 joint positions) |
| `detect_hand_pose` | Detect hand poses with finger joint positions |
| `detect_animals` | Detect cats and dogs with bounding boxes |

### Image Processing Tools

| Tool | Description |
|------|-------------|
| `blur_faces` | Automatically blur all faces in an image |
| `auto_crop` | Smart crop focusing on salient regions |
| `generate_saliency_map` | Generate attention/objectness heatmaps |
| `remove_background` | Remove background, output transparent PNG |

## Example Usage

```
# Detect text in a screenshot
detect_text(image_path: "screenshot.png")

# Remove background from a photo
remove_background(image_path: "photo.jpg", output_path: "photo_nobg.png")

# Blur faces for privacy
blur_faces(image_path: "group.jpg", output_path: "group_blurred.jpg", blur_radius: 40)

# Auto-crop to 16:9 aspect ratio
auto_crop(image_path: "photo.jpg", output_path: "cropped.jpg", aspect_ratio: "16:9")
```

## Requirements

- macOS 15.0 or later
- Osaurus 0.5.0 or later

## Development

1. Build:
   ```bash
   swift build -c release
   ```

2. Extract manifest (to verify):
   ```bash
   osaurus manifest extract .build/release/libosaurus-vision.dylib
   ```
   
3. Package (for distribution):
   ```bash
   osaurus tools package osaurus.vision 0.1.0
   ```
   This creates `osaurus.vision-0.1.0.zip`.
   
4. Install locally:
   ```bash
   osaurus tools install ./dev.osaurus.vision-0.1.0.zip
   ```
   
## Publishing

This project includes a GitHub Actions workflow (`.github/workflows/release.yml`) that
automatically builds and releases the plugin when you push a version tag.

To release:
```bash
git tag v0.1.0
git push origin v0.1.0
```

For manual publishing:

1. Package it with the correct naming convention:
   ```bash
   osaurus tools package <plugin_id> <version>
   ```
   The zip file MUST be named `<plugin_id>-<version>.zip`.
   
2. Host the zip file (e.g. GitHub Releases).

3. Create a registry entry JSON file for the central repository.

## License

MIT
