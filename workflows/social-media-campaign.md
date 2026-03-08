---
type: workflow
id: social-media-campaign
title: Social Media Campaign
description: "Multi-platform content creation: briefing, content generation, caption writing, and scheduling"
tags: [Production, Customer-Facing]
connections:
  - target: content-briefing
    type: uses
  - target: content-repurposing
    type: uses
  - target: create-content-brief
    type: uses
  - target: repurpose-content
    type: uses
  - target: social-media-post-generator
    type: uses
  - target: caption-writer
    type: uses
  - target: anthropic-claude
    type: runs_on
metadata:
  estimated_duration: "5-10 minutes"
  trigger: manual
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
