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
