---
name: Summary
description: Describe when to use this prompt
---
Give me a summary of what work has been done as one sentence. Then give me bullet points of one sentence each of a breakdown.

Do not include any information that is not relevant to the work done. Do not include any information about the process, only the outcome. 


Below is an example of what the output must be:
```
Refactored `SongItem` to replace the long‑press trigger with a visible mobile “More” button and adjusted `DraggableSongItem` so the drag handle is injected rather than overlaid.

- Removed touch‑hold logic from `SongItem` and added a `rightAction` prop.  
- Added a mobile‑only `MoreHorizontal` button that opens the options drawer.  
- Stopped propagation on that button to avoid accidental playback.  
- Changed `DraggableSongItem` to pass its grip handle into `SongItem` via the new slot.  
- Ensured desktop hover behaviour and playlist drag‑and‑drop still function identically.
```