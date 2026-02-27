# Zen Designer Instruct

Vision-language model for design instruction following.

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

## Overview

Zen Designer Instruct is a vision-language model specialized for design tasks. Understands visual layouts, UI components, typography, and color systems. Follows design instructions to generate specifications, critique compositions, and produce structured design output.

| Property | Value |
|----------|-------|
| Parameters | 4B |
| Context | 32K |
| Modalities | Text + Vision |
| License | Apache 2.0 |

## Usage

```python
from transformers import AutoModelForCausalLM, AutoProcessor

model = AutoModelForCausalLM.from_pretrained("zenlm/zen-designer-instruct", trust_remote_code=True)
processor = AutoProcessor.from_pretrained("zenlm/zen-designer-instruct", trust_remote_code=True)

from PIL import Image
image = Image.open("mockup.png")

messages = [{"role": "user", "content": [
    {"type": "image"},
    {"type": "text", "text": "Analyze this UI design. Suggest improvements for visual hierarchy and spacing."}
]}]

inputs = processor(images=image, text=processor.apply_chat_template(messages), return_tensors="pt")
output = model.generate(**inputs, max_new_tokens=512)
print(processor.decode(output[0], skip_special_tokens=True))
```

## Related

- [zen-designer-thinking](https://huggingface.co/zenlm/zen-designer-thinking) — Design reasoning variant
- [zen-eco](https://huggingface.co/zenlm/zen-eco) — Base 4B model
- [Zen LM](https://github.com/zenlm) — Full model family

Apache 2.0 · [Zen LM](https://zenlm.org) · [Hanzo AI](https://hanzo.ai)
