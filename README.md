# ITalk-57 Dataset

**ITalk-57** is a multimodal dataset of 57 recorded online presentations, contributed as part of the paper:

**"In-Situ Presenter: Augmenting Online Presentations through Interactive Presenter-Content Alignment"**  
**Paper Link**: _TBD_

This dataset captures presenter behavior in a presentation interface that allows full dynamic control over webcam placement and layout during slide delivery. It supports research on multimodal alignment, expressive video-mediated communication, and adaptive presentation tools.

---

## 📁 Dataset Contents

We release data from 16 consented participants (out of 20), each of whom presented slides using a web-based tool that allowed repositioning, resizing, and toggling visibility of their webcam video.

### Per Participant Folder Structure (Recommended)

```
ITalk-57/
├── participant_01/
│   ├── personal/
│   │   ├── slides.pdf
│   │   ├── script.txt
│   │   ├── presentation.mp4
│   │   ├── webcam_only.mp4
│   │   └── interaction_log.json
│   ├── tutorial/
│   │   └── ...
│   └── professional/
│       └── ...
├── participant_02/
│   └── ...
├── README.md
├── LICENSE
└── CITATION.cff
```

Each subfolder (e.g., `personal/`, `tutorial/`, `professional/`) represents a **presentation category** from the study. Every folder contains:

- `slides.pdf`: The full slide deck shown during the presentation (7 slides)
- `script.txt`: The full text script accompanying the slides (aligned to slides by segment)
- `presentation.mp4`: A full video showing slides + webcam composited in real-time
- `webcam_only.mp4`: The presenter’s segmented webcam feed with transparent background
- `interaction_log.json`: Time-stamped log of presenter webcam manipulations

---

## 📄 JSON Log Format: `interaction_log.json`

Each JSON file contains metadata and time-series logs of presenter video manipulation events throughout the talk.

### Top-Level Metadata Fields

```json
{
  "category": "personal",
  "subCategory": "hometown",
  "events": [ ... ]
}
```

- `category`: One of the three genre categories used in the study (`personal`, `tutorial`, `professional`)
- `subCategory`: Specific topic for the presentation (e.g., `"hometown"`, `"hobby"`, etc.)
- `events`: A list of all webcam interaction events over time

### Webcam Interaction Event Fields

Each item in `events` includes:

- `timestamp` *(float)*: Seconds since start of the talk when the event occurred  
- `slideNumber` *(int)*: The index of the slide being shown at that time (starting from 1)  
- `webcamPosition` *(dict)*: CSS-style absolute position of the webcam on the slide  
  - `top`, `left`, `right`, `bottom`: string values (e.g., `"204px"`), empty string if not applicable  
- `webcamSize` *(dict)*: Width and height of the webcam in pixels  
  - `width`, `height`: integer values in pixels  
- `isFullScreen` *(bool)*: `true` if webcam was in full-screen mode at the time  
- `isHidden` *(bool)*: `true` if webcam was hidden at the time  

### Example

```json
{
  "timestamp": 32.47,
  "slideNumber": 3,
  "webcamPosition": {
    "top": "150px",
    "left": "220px",
    "bottom": "",
    "right": ""
  },
  "webcamSize": {
    "width": 640,
    "height": 360
  },
  "isFullScreen": false,
  "isHidden": false
}
```

This means: at 32.47s on slide 3, the presenter manually positioned the webcam in the upper-left quadrant, sized it 640×360px, and it was visible and not full-screen.

---

## 🧠 Study Summary

- **Participants**: 20 recruited, 16 consented for release
- **Categories**: 3 (personal stories, tutorials, professional talks)
- **Decks**: 6 total (2 per category), 7 slides per deck
- **Presentation Tool**: Custom web tool enabling real-time webcam control (reposition, resize, full-screen, hide)
- **Logging**: All webcam state changes recorded as structured JSON events

---

## 💡 Research Use Cases

- Training or benchmarking adaptive presenter systems  
- Analyzing expressive video framing strategies  
- Studying gesture-speech-content alignment  
- Investigating layout-aware presenter behavior  
- Developing multimodal or LLM-powered slide augmentation interfaces  

---

## 📜 Citation

If you use this dataset in your work, please cite:  _TBD_



---

## ⚠️ Ethical Use

- All included videos are from participants who explicitly consented to public release.
- Contains identifiable facial video; use is restricted to **non-commercial academic research**.
- Prohibited uses: identity recognition, surveillance, deepfake generation, or commercial deployment.

---

## 📄 License

This dataset is shared under the **Creative Commons Attribution-NonCommercial 4.0 (CC BY-NC 4.0)** license.  
More details: [https://creativecommons.org/licenses/by-nc/4.0/](https://creativecommons.org/licenses/by-nc/4.0/)

