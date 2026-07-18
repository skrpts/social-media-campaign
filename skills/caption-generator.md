---
type: skill
id: caption-generator
title: Caption Generator
description: "Writing engaging, platform-tuned captions for the campaign's visual content"
tags: [Production, Campaign, Writing]
connections:
  - target: llm-service
    type: runs_on
metadata:
  estimated_duration: "3 minutes"
  avg_tokens: 2000
  trigger: manual
---

## Caption Generator

This skill writes ready-to-publish captions for the visual content in a social media campaign, tuned to each target platform and aligned to the campaign brief's voice.

### Core Capability

Given the repurposed campaign content and the campaign brief, this skill produces captions for every piece of visual content — images, videos, and carousels — with a strong opening hook, a clear call to action, and platform-appropriate hashtags.

### Method

1. **Read the visuals:** Draw the visual content descriptions from the repurposed content.
2. **Match the voice:** Align tone and messaging to the campaign brief.
3. **Write variants:** Provide three tone options per visual — informative, conversational, and bold — each front-loaded and scannable.

### Output Structure

Captions grouped by visual asset, each with three tone variants and suggested hashtags. This is the terminal content deliverable, handed to the language-polish stage for a final pass.
