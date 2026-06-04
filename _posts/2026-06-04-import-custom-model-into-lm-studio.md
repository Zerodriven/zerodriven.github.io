---
layout: single
date: 2026-06-04
categories: AI
classes: wide
---
Within LM studio there's obviously a way to download models natively, however in some instances several models from HuggingFace don't appear.

1. Download model from HuggingFace (Other places exist)
2. Open command prompt
3. Run the following command:

```powershell
lms.exe import path
(e.g. "lms import C:\Users\Jason\Downloads\model.gguf")
```

4. Follow the prompts.
5. Done.