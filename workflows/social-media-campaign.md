---
type: workflow
id: social-media-campaign
title: Social Media Campaign
description: "Multi-platform content creation: briefing, content generation, caption writing, and scheduling"
tags: [Production, Customer-Facing, Campaign, Writing]
connections:
  - target: content-briefing
    type: uses
  - target: content-repurposing
    type: uses
  - target: content-ideation
    type: uses
  - target: headline-writing
    type: uses
  - target: llm-service
    type: runs_on
  - target: brand-voice-guide
    type: references
  - target: social-media-platform-guide
    type: references
  - target: social-media-post-templates
    type: references
  - target: image-briefing
    type: uses
metadata:
  estimated_duration: "5-10 minutes"
  trigger: manual
execution:
  - skill: "content-briefing"
    step_type: "generation"
  - skill: "content-repurposing"
    step_type: "generation"
  - skill: "content-ideation"
    step_type: "generation"
  - skill: "headline-writing"
    step_type: "generation"
  - skill: "image-briefing"
    step_type: "generation"
---

## Overview

This workflow produces a complete social media campaign from a single content brief. It generates platform-specific posts, captions for visual content, and a scheduling plan across LinkedIn, Twitter/X, Instagram, and Facebook.

## Pipeline Stages

### Stage 1: Campaign Briefing

**Input:** Campaign topic, target audience, key messages, target platforms

Invoke the **create-content-brief** prompt to produce a campaign brief covering objectives, target audience, key messages, and platform strategy.

**Output:** Campaign brief with per-platform content requirements.

### Stage 2: Content Generation

**Input:** Campaign brief from Stage 1 + source content (if repurposing existing material)

Two parallel paths:

#### 2a. Original Content

Invoke the **social-media-post-generator** prompt to create platform-specific posts from the campaign brief.

#### 2b. Repurposed Content

If source content exists (blog post, article, video transcript), invoke the **repurpose-content** prompt to transform it into platform-specific formats using the **content-repurposing** skill.

**Output:** Draft posts for each target platform.

### Stage 3: Caption Writing

**Input:** Visual content descriptions + platform targets

Invoke the **caption-writer** prompt to produce captions for any visual content (images, videos, carousels) included in the campaign. Provides three tone options per visual.

**Output:** Captions matched to visual assets.

### Stage 4: Review and Schedule

**Input:** All generated content from Stages 2-3

Manual review step. Collate all posts and captions, review for consistency, and schedule according to platform best practices (see social media platform guide for optimal posting times).

**Output:** Finalised campaign content with scheduled publication times.

## Error Handling

- If a platform's character limit is exceeded, revise the post rather than truncating
- If visual assets are not yet available, generate placeholder captions and mark for update
- If brand voice drifts across platforms, the review stage should harmonise tone

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.campaign_topic}}` | Yes | Campaign topic | `Paste the relevant brief, notes, source material, or dataset here.` |
| `{{input.target_audience}}` | Yes | target audience | `Paste the relevant brief, notes, source material, or dataset here.` |
| `{{input.key_messages}}` | Yes | key messages | `Paste the message, transcript, or conversation you want the workflow to process.` |
| `{{input.target_platforms}}` | No | target platforms | `Paste the relevant brief, notes, source material, or dataset here.` |

## Outputs

| Name | Description |
|------|-------------|
| Campaign brief | Campaign brief with per-platform content requirements |
| Draft posts for each target platform | Draft posts for each target platform |
| Captions matched to visual assets | Captions matched to visual assets |
| Finalised campaign content | Finalised campaign content with scheduled publication times |

## Setup

Before running this workflow:

1. No external services required — paste your content directly and provide any supporting context as inputs or source nodes.
2. Review the included documents, assets, or source nodes and customise them to match your team, brand, or domain conventions where needed.
3. No specific AI provider or API key is required beyond your configured skrptiq LLM provider.

## Provider Notes

- Most stages work with any capable model; stronger models usually improve synthesis, judgement, and writing quality.
- Extraction, classification, and formatting steps generally run well on smaller or faster models.
- Because there are no vendor-specific integrations here, provider choice is mostly a trade-off between speed, quality, and cost.

## Example Input

To test this workflow immediately after import:

```
Campaign Topic: "Paste the relevant brief, notes, source material, or dataset here."
Target Audience: "Paste the relevant brief, notes, source material, or dataset here."
Key Messages: "Paste the message, transcript, or conversation you want the workflow to process."
Target Platforms: "Paste the relevant brief, notes, source material, or dataset here."
```

