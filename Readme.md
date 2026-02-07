# Offline On-Device LLM for Mobile (iOS & Android)

## Overview

This repository explores **approaches for deploying an offline Large Language Model (LLM)** that runs **entirely on-device** for both **iOS and Android**.

The goal is to:

- Enable **private, offline AI inference** on mobile devices
- Avoid reliance on cloud APIs
- Maintain **cross-platform consistency**
- Remain compliant with **Apple App Store** and **Google Play** policies

This document outlines **three viable architectural approaches**, with clear **pros, cons, risks, and tradeoffs**, to support an informed decision by senior leadership.

---

## Why Offline LLMs on Mobile?

**Business drivers**

- User privacy (no data leaves device)
- Reduced cloud costs
- Offline functionality
- Regulatory and compliance advantages

**Technical constraints**

- Limited RAM, CPU/GPU, and battery
- App store restrictions on dynamic code execution
- Model size and performance tradeoffs

---

## Target Capabilities (Initial Scope)

- Text-only LLM inference
- Small models (≈0.5B–3B parameters)
- Quantized models (4-bit or 8-bit)
- Fully offline execution
- Streaming token generation
- Mobile-friendly latency and thermal limits

---

## Evaluated Approaches

### Approach 1: Shared Native Core (C++ / `llama.cpp`-style)

**Description**  
A single **C++ inference engine** shared across platforms, with:

- Swift wrapper for iOS
- Kotlin/NDK wrapper for Android

Models are shipped as **data files**, not executable code.

**High-level architecture**
Mobile UI (Swift / Kotlin)
↓
Platform Bridge (Swift ↔ C++, JNI ↔ C++)
↓
Shared C++ LLM Inference Engine
↓
Quantized LLM Model (on-device)

**Pros**

- One core inference implementation
- Consistent behavior across iOS and Android
- Full control over model choice and optimization
- Proven approach used by many offline LLM apps
- Strong compliance with app store policies

**Cons**

- Requires C++ expertise
- More complex build pipeline
- Manual optimization for mobile performance

**Risk Level**

- Medium (engineering complexity, well-understood tech)

**Best suited for**

- Long-term product investment
- Teams aiming for full ownership and flexibility
- Privacy-first or regulated environments

---

### Approach 2: Platform-Native ML Runtimes (Core ML + TensorFlow Lite)

**Description**  
Use **native ML runtimes per platform**:

- iOS → Core ML
- Android → TensorFlow Lite / LiteRT

Models must be **converted separately** for each platform.

**High-level architecture**
iOS App → Core ML → iOS-optimized model
Android App → TFLite → Android-optimized model

**Pros**

- Excellent platform-level optimization
- Easier integration with native tooling
- Potentially better battery efficiency
- Supported by Apple and Google ecosystems

**Cons**

- Two separate model pipelines
- Complex and fragile model conversion
- Divergent behavior across platforms
- Slower iteration and experimentation

**Risk Level**

- Medium–High (model portability & maintenance)

**Best suited for**

- Platform-specific products
- Teams already invested heavily in Core ML / TFLite
- Performance-critical but smaller-scope apps

---

### Approach 3: Google AI Edge / MediaPipe-Based Stack

**Description**  
Use Google’s **AI Edge** tooling (e.g. MediaPipe, LiteRT) as demonstrated in the `google-ai-edge/gallery` repository.

Primarily optimized for **Android-first** deployments.

**Pros**

- Strong Android support
- Backed by Google tooling
- Good examples for on-device ML patterns

**Cons**

- Not a full LLM platform
- Limited iOS parity
- Not designed as a reusable cross-platform LLM engine
- More suitable as a reference/demo than a product base

**Risk Level**

- High for cross-platform products

**Best suited for**

- Android-only or Android-first experiments
- Learning and prototyping on-device ML
- Research and exploration

---

## Comparative Summary

| Criteria                   | Shared C++ Core | Native ML Runtimes | Google AI Edge |
| -------------------------- | --------------- | ------------------ | -------------- |
| Cross-platform consistency | ⭐⭐⭐⭐        | ⭐⭐               | ⭐             |
| Performance                | ⭐⭐⭐          | ⭐⭐⭐⭐           | ⭐⭐⭐         |
| Maintenance overhead       | ⭐⭐⭐          | ⭐⭐               | ⭐⭐           |
| Model flexibility          | ⭐⭐⭐⭐        | ⭐⭐               | ⭐⭐           |
| App store compliance       | ⭐⭐⭐⭐        | ⭐⭐⭐⭐           | ⭐⭐⭐         |
| Long-term scalability      | ⭐⭐⭐⭐        | ⭐⭐               | ⭐             |

---

## Recommendation (Initial)

For a **production-grade, cross-platform offline LLM**, the **Shared Native Core approach** offers the best balance of:

- Control
- Maintainability
- Compliance
- Long-term scalability

Other approaches remain valuable for:

- Platform-specific optimization
- Research and proof-of-concepts

---

## Next Steps

1. Select preferred architecture
2. Validate with a small model (≤1B parameters)
3. Measure:
   - Latency
   - Battery usage
   - Thermal impact
4. Iterate on UX and performance constraints
5. Decide on production readiness

---

## Status

This repository currently focuses on **architecture evaluation and decision-making**.  
Implementation will begin once a direction is approved.
