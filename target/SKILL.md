---
name: video-report
description: >
  Debug and generate reports about video rendering issues using Remotion. Use when the user says: 'video not working', 'video report', 'debug this video', 'test video rendering', 'render this video', or reports a broken video URL that needs to be tested with Remotion's render pipeline.
  Do NOT trigger for: turning a video into a website (use video-to-website), general video analysis or summarization, or video editing tasks unrelated to Remotion rendering.
---

# Video Report

Debug video rendering issues by testing videos through the Remotion render pipeline and generating verbose reports.

---

## Process

### Step 1: Get the Video URL

The user provides a video URL that isn't working. Download or reference the URL.

### Step 2: Set Up the Test

Place the video URL as the `src` in the test component:

```
packages/example/src/NewVideo.tsx
```

Update the `src` prop to point to the user's video URL.

### Step 3: Render with Verbose Logging

Run the Remotion render command from the `packages/example` directory:

```bash
cd packages/example
bunx remotion render NewVideo --log=verbose
```

### Step 4: Analyze and Report

After rendering, report back with:

```
## Video Report: [URL or filename]

### Render Result
- **Status**: [Success / Failed at frame X / Timeout]
- **Duration**: [render time]
- **Resolution**: [width x height]

### Issues Found
- [Error messages from verbose log]
- [Frame-specific failures if any]

### Recommendation
- [Fix suggestion based on the error]
```

---

## Good vs Bad Example

❌ **Bad (no detail):**
> The video doesn't work. Try a different format.

✅ **Good (diagnostic report):**
> ## Video Report: user-clip.mp4
> ### Render Result
> - **Status**: Failed at frame 142
> - **Error**: `Could not decode frame — unsupported codec (HEVC/H.265)`
>
> ### Recommendation
> Re-encode with H.264 codec: `ffmpeg -i user-clip.mp4 -c:v libx264 -crf 23 user-clip-h264.mp4`
