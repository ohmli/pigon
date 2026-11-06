# 🐿️ Squirrel Detector

A browser-based squirrel detector. Point a camera at your yard, feeder, or window, and the page watches the live feed and snaps a photo whenever a squirrel shows up.

**Live demo:** https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/

Everything runs locally in your browser. Video is never uploaded anywhere.

## Features

- Live camera feed with boxes drawn around detected squirrels
- Automatic snapshots with a timestamp and confidence score
- Optional sound and desktop notification on each sighting
- Adjustable confidence threshold and delay between photos
- Camera picker (useful on phones with front and rear cameras)
- "Test with a video file" button to try it on a clip before going live
- Single static file with no build step and no backend

## Use it

1. Open the live demo link above (or `index.html` locally).
2. Press **Start camera** and allow camera access.
3. Wait a few seconds the first time while the AI models download.
4. Squirrel sightings appear in the **Sightings** gallery. Click **Save** on any photo to download it.

Works in current versions of Chrome, Edge, Firefox, and Safari. Camera access requires HTTPS (GitHub Pages provides this) or `localhost`.

## Deploy your own copy on GitHub Pages

1. Fork this repo, or create a new public repo and upload `index.html`.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select `main` and `/ (root)`, then save.
4. After about a minute, your site is live at `https://<your-username>.github.io/<repo-name>/`.

## Tips

- **Placement matters.** Squirrels are small in frame. Put the camera close to the spot they visit, and keep it steady with good light.
- **Using a phone as the camera.** Open the page on the phone, prop it up, plug it in, and turn off auto-lock. The tab must stay open and in the foreground for detection to run.
- **Too many false alarms?** Raise the confidence slider. Cats, dogs, and branches can occasionally fool the classifier.
- **Missing squirrels?** Lower the slider, improve the lighting, or move the camera closer.

## How it works

Detection is a two-stage pipeline running in your browser with [TensorFlow.js](https://www.tensorflow.org/js):

1. **[COCO-SSD](https://github.com/tensorflow/tfjs-models/tree/master/coco-ssd)** finds animal-shaped objects in each frame (birds, cats, dogs, teddy bears, and similar, which are the labels squirrels are most often given).
2. **[MobileNet v2](https://github.com/tensorflow/tfjs-models/tree/master/mobilenet)**, trained on ImageNet, classifies each cropped object and the full frame. The *fox squirrel* class counts as a squirrel.

A squirrel must be seen in two consecutive checks before the page alerts, and a cooldown timer prevents repeated photos of the same visitor.

## Limitations

- Accuracy is best for a clear, fairly large squirrel. Tiny, dark, blurry, or partly hidden animals may be missed.
- ImageNet's squirrel class is based on the fox squirrel, so other species and chipmunks may score lower.
- Snapshots are held in the page only. Save the ones you want before closing the tab.
- The AI libraries and model weights load from a CDN, so the first visit needs an internet connection.

## Privacy

No video, images, or detections are sent to any server. The only network requests are for the page's libraries and model files.

## Credits

Built with TensorFlow.js, COCO-SSD, and MobileNet.
