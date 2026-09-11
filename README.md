# ITalk-60 Dataset

**ITalk-60** is a multimodal dataset of 60 recorded presentation sessions, contributed as part of the paper:

**"In-Situ Presenter: Bringing Presenters into Slides via Context-Aware Composition"**  
**Paper Link**: _TBD_

This dataset captures presenter behavior in a presentation interface that allows full dynamic control over webcam placement and layout during slide delivery. It supports research on multimodal alignment, expressive video-mediated communication, and adaptive presentation tools.

---

## 📁 Dataset Contents

We release data from 16 consented participants (out of 20), each of whom presented slides using a web-based tool that allowed repositioning, resizing, and toggling visibility of their webcam video.

### Folder Structure

```
ITalk-60/
├── README.md
│
├── presentation_material/              # Canonical slides and scripts used across all sessions
│   ├── personal/
│   │   ├── hobby.pptx                  # 7-slide deck on personal hobbies
│   │   ├── hobby.txt                   # Presentation script / teleprompter notes
│   │   ├── hometown.pptx               # 7-slide deck on hometown narratives
│   │   └── hometown.txt
│   ├── tutorial/
│   │   ├── how-to-install.pptx         # 7-slide software installation tutorial
│   │   ├── how-to-install.txt
│   │   ├── time-management.pptx        # 7-slide productivity tutorial
│   │   └── time-management.txt
│   └── professional/
│       ├── product.pptx                # 7-slide tech product pitch
│       ├── product.txt
│       ├── research.pptx               # 7-slide academic research presentation
│       └── research.txt
│
├── personal/                           # Personal narrative recordings & logs
│   ├── personal_1/                     # (hometown talk: p01–p04, p09–p12, p17–p18)
│   │   ├── p01_interaction_log.json
│   │   ├── p01_presentation.mp4
│   │   ├── p01_webcam.webm
│   │   └── ...
│   └── personal_2/                     # (hobby talk: p05–p08, p13–p16, p19–p20)
│
├── tutorial/                           # Instructional tutorial recordings & logs
│   ├── tutorial_1/                     # (how-to-install talk)
│   └── tutorial_2/                     # (time-management talk)
│
└── professional/                       # Professional presentation recordings & logs
    ├── professional_1/                 # (research talk)
    └── professional_2/                 # (product pitch talk)
```

Each top-level folder (`personal`, `tutorial`, `professional`) contains all participant recordings for that presentation domain.
Each subfolder (e.g., `personal_1`) corresponds to a single presentation instance and contains:

- `slides.pdf`: Slide deck (7 slides)
- `script.txt`: Corresponding presentation script
- `*_presentation.mp4`: Composite video (slide + webcam)
- `*_webcam_only.mp4`: Webcam-only segmented feed
- `*_interaction_log.json`: Timestamped webcam manipulation log

---

## ⚠️ Notes on Session Structure & Consent

* **60 Logical Sessions / 61 JSON Logs**: Participant 15's session on `professional_2` was restarted due to an application refresh, producing `p15_interaction_log_pt1.json` and `p15_interaction_log_pt2.json`. Both segments are retained.
* **Non-Video Participants (`p05`, `p06`, `p09`)**: 3 participants (9 presentation sessions) declined public release of identifiable facial video. Their sessions preserve complete, de-identified interaction logs (`*_interaction_log.json`).
* **Webcam Stream (`p19`)**: The isolated webcam stream for `personal_2/p19` was corrupted during stream encoding, but the composite presentation video and interaction log are preserved.
* **Composite Streams (`p17`, `p16`, `p20`)**: Composite screen recordings were omitted in 5 sessions due to recording timeouts; their isolated webcam feeds and interaction logs are preserved.

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

