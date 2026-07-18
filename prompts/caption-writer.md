---
type: prompt
id: caption-writer
title: Caption Writer
description: "Writes engaging captions for visual social media content"
tags: [Customer-Facing, Campaign, Writing]
inputs:
  target_platforms:
    label: "Target Platforms"
    description: "Platforms to create content for"
    example: "LinkedIn, Twitter"
    required: true
    type: text
  campaign_topic:
    label: "Campaign Topic"
    description: "The topic or theme for the campaign"
    example: "Product launch for new AI features"
    required: true
    type: text
context_params:
  repurposed_content:
    label: "Repurposed Content"
    description: "Platform-specific content — the source for the visual descriptions captions are written against."
    required: false
  brief:
    label: "Campaign Brief"
    description: "Campaign brief providing the voice and messaging guidelines to keep captions on-tone."
    required: false
connections:
  - target: headline-writing
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Produces captions for images, videos, and visual content across social media platforms.

## Prompt

You are a social media specialist. Write captions for the visual content described below. Each caption should:

1. **Hook the reader in the first line** — this is what appears before "see more" on most platforms
2. **Tell a micro-story or provide value** — give the reader a reason to engage beyond the visual
3. **Include a clear call to action** — comment, share, save, click the link, etc.
4. **Suggest relevant hashtags** — tailored to the platform and content

Provide three caption options for each piece of visual content, varying in tone:
- **Option A:** Informative and professional
- **Option B:** Conversational and relatable
- **Option C:** Bold and attention-grabbing

### Inputs

- **Visual content description:** Using the visual content descriptions from the generated posts: {{step.context.repurposed_content}}
- **Platform:** {{input.target_platforms}}
- **Campaign context:** {{input.campaign_topic}}
- **Brand voice notes:** Maintain consistency with the campaign brief's tone and messaging guidelines from: {{step.context.brief}}

## Formatting Rules

- Use British English throughout
- Keep captions scannable — use line breaks between ideas
- Front-load the most important information
- Do not start captions with "Check out" or "We're excited to announce"
