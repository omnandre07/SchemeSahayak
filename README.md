# SchemeSahayak – Pan-India Voice-First AI Government Scheme Navigator

**Idea Submission for AI for Bharat Hackathon**  
**Track**: Student Track – AI for Communities, Access & Public Impact  
**Submitted by**: Om Nandre  
**Date**: February 2026  

## Overview

SchemeSahayak is a browser-based, voice-first AI assistant designed to help underserved citizens across India (especially rural and low-literacy users) discover, understand, and apply for government schemes.

Users can speak or type their situation in natural language (Hindi, English, or regional language mix), e.g.:  
- “Main Maharashtra ka chhota kisaan hoon, kya yojana mil sakti hai?”  
- “I’m a student from UP, any scholarships available?”

Powered by **Amazon Bedrock**, the AI:  
- Matches eligibility for 30+ central schemes + relevant state-specific schemes  
- Uses progressive clarifying questions (yes/no flow) for accurate results  
- Provides simple explanations, required documents, application steps, official links, and CSC/office tips  
- Works in low-bandwidth/offline mode via browser caching  
- Includes shareable summaries for family/community spread  

## Repository Contents

- **requirements.md**  
  Functional & non-functional requirements, user stories, acceptance criteria (generated via Kiro Spec flow)

- **design.md**  
  High-level architecture, components, tech stack, data flow, and implementation notes (generated via Kiro Design flow)

## Why GenAI?

Unlike rule-based portals (e.g., myScheme.gov.in forms), GenAI enables dynamic, conversational matching, handles ambiguous/fuzzy queries, and delivers personalized, natural-language explanations at scale.

## Key Differentiators

- Pan-India coverage (central + state schemes)  
- True offline/low-bandwidth readiness (PWA caching)  
- Progressive low-literacy friendly flow (yes/no clarification)  
- Community sharing + visual icons for better accessibility  
- Responsible design: no data storage, disclaimers, confidence scores

## Technologies (Prototype Plan)

- Frontend: HTML/JS, Web Speech API (voice), PWA/Service Worker (offline)  
- AI: Amazon Bedrock (LLM reasoning & matching)  
- Optional: Amazon Polly (voice output)

## Submission Links

- Idea PDF Deck: [uploaded to hackathon portal]  
- GitHub Repo: This repository  

Thank you for reviewing!  
Looking forward to building an inclusive solution for Bharat.

Om Nandre  
nandreom31@gmail.com
