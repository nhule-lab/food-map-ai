# 🍜 Food Map AI

> Turn saved food videos into places you can actually visit --- or order
> from.

Food Map AI transforms short-form food videos from **TikTok, Instagram
Reels, and YouTube Shorts** into a structured, personalized food map
using a **multi-agent AI pipeline**.

Instead of letting saved food videos disappear into an endless
collection, users simply share a video link with Food Map. AI agents
automatically identify the restaurant, dishes, location, price range,
and relevant context, then save everything to an interactive map.

------------------------------------------------------------------------

## 💡 The Problem

Young urban users constantly discover restaurants, cafés, and date spots
through short-form videos, but there is no effective way to organize and
retrieve them later.

Current workarounds are fragmented:

-   📸 Screenshots contain little or no useful metadata.
-   ❤️ Saved/liked videos get buried among entertainment content.
-   📍 Manually searching Google Maps takes 2--3 minutes per location.
-   🔎 Restaurants with similar names can easily be matched to the wrong
    location.

As a result, the journey from:

**Watch → Save → Find → Visit / Order**

is broken.

Users' phones gradually become a **"graveyard" of forgotten food
places** they once wanted to try.

------------------------------------------------------------------------

## 🚀 Our Solution

### Food Video → AI Agents → Personal Food Map → Action

Users share a TikTok, Instagram Reels, or YouTube Shorts link into Food
Map.

An **Orchestrator Agent** coordinates specialized AI agents to process
the content automatically:

1.  **Scraping Agent**
    -   Retrieves video content and metadata.
2.  **Audio Agent**
    -   Extracts audio.
    -   Uses Whisper for speech-to-text transcription.
3.  **Analyst Agent**
    -   Cleans and normalizes text.
    -   Performs Named Entity Recognition (NER).
    -   Prioritizes Vietnamese-language understanding using PhoBERTv2.
    -   Combines OCR with LLM post-processing to recover restaurant and
        dish names from signs and video overlays.
4.  **Geospatial Agent**
    -   Resolves restaurant identity and location.
    -   Cross-checks candidates using Google Maps / Mapbox.
    -   Retrieves coordinates, opening hours, ratings, and other
        location metadata.

The final result is returned as structured data and displayed on the
user's personal map.

------------------------------------------------------------------------

## 🗺️ What Users Get

Each saved location can include:

-   Restaurant / café name
-   Exact map location
-   Opening hours
-   Rating
-   Price range
-   Signature dishes
-   Video source
-   AI-generated tags
-   Suitable context: dating / family / friends / solo
-   Confidence score

Example:

``` json
{
  "restaurant_name": "Example Restaurant",
  "category": "Vietnamese Food",
  "location": {
    "latitude": 10.7769,
    "longitude": 106.7009
  },
  "signature_dishes": ["Dish A", "Dish B"],
  "price_range": "$$",
  "context": ["friends", "date"],
  "confidence_score": 0.94
}
```

------------------------------------------------------------------------

## 🤖 Multi-Agent Architecture

``` text
                 ┌──────────────────┐
                 │    Video Link    │
                 │ TikTok / IG / YT │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │   Orchestrator   │
                 │      Agent       │
                 └────────┬─────────┘
                          │
           ┌──────────────┼──────────────┐
           │              │              │
           ▼              ▼              ▼
    ┌────────────┐  ┌───────────┐  ┌────────────┐
    │  Scraping  │  │   Audio   │  │  Analyst   │
    │   Agent    │  │   Agent   │  │   Agent    │
    └─────┬──────┘  └─────┬─────┘  └──────┬─────┘
          │               │                │
          │          Whisper STT      NER + OCR
          │                                │
          └───────────────┬────────────────┘
                          ▼
                 ┌──────────────────┐
                 │    Geospatial    │
                 │      Agent       │
                 └────────┬─────────┘
                          │
                   Maps / POI APIs
                          │
                          ▼
                 ┌──────────────────┐
                 │ Structured JSON  │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ Personal Food Map│
                 └────────┬─────────┘
                          │
                          ▼
                    Visit / Order
```

------------------------------------------------------------------------

## 🛒 From Discovery to Action

Food Map does not stop at discovery.

With food-delivery platform integrations such as **GrabFood /
ShopeeFood**, users could go directly from discovering a restaurant in a
video to selecting its signature dishes.

A **human-in-the-loop confirmation** ensures that the user explicitly
approves the final action before an order is submitted.

**WATCH → SHARE → EXTRACT → MAP → ORDER**

------------------------------------------------------------------------

## 🧠 Why AI-Native?

Food Map is not a static map with a chatbot added on top.

AI is responsible for transforming **unstructured multimodal content
into actionable structured data** across the core product workflow.

The multi-agent system handles:

-   Video ingestion
-   Speech understanding
-   OCR
-   Entity extraction
-   Restaurant disambiguation
-   Geospatial matching
-   Context enrichment
-   Confidence scoring

This makes Food Map primarily an **AI-Native Product**, with elements of
**Autonomous & Adaptive AI**.

------------------------------------------------------------------------

## 🧑‍💻 Built with Codex

Codex is used throughout the hackathon to accelerate development:

-   Scaffold the multi-agent architecture
-   Generate agent implementations
-   Build API wrappers
-   Implement Whisper transcription
-   Build the OCR + LLM processing pipeline
-   Debug integrations
-   Generate tests
-   Rapidly iterate on the end-to-end workflow

Our target pipeline:

**Video Link → Multi-Agent Processing → Structured JSON → Location
Verification → Interactive Food Map**

------------------------------------------------------------------------

## 🛠️ Tech Stack

**AI / Backend** - OpenAI - OpenAI Agents SDK - Whisper - PhoBERTv2 -
OCR - Python

**Location** - Google Maps API - Mapbox

**Frontend** - Web-based interactive map

**Potential Integrations** - GrabFood - ShopeeFood

------------------------------------------------------------------------

## 🎯 Target Users

Young urban users who:

-   Consume short-form food content frequently
-   Regularly search for restaurants and cafés
-   Look for date spots and places to meet friends
-   Save many food videos but rarely revisit them

Unlike travel planning, which may happen only a few times per year,
deciding **"where should we eat?"** is a recurring everyday problem.

This creates strong potential for frequent usage and long-term
retention.

------------------------------------------------------------------------

## 🏁 Hackathon MVP

For the hackathon, our goal is to demonstrate one complete end-to-end
journey:

**Paste a food video link → AI extracts restaurant information →
Restaurant is matched to a real location → Structured data is generated
→ Location appears automatically on Food Map**

### MVP Success Criteria

-   [ ] Accept a short-form video URL
-   [ ] Extract audio
-   [ ] Transcribe speech
-   [ ] Extract restaurant and dish entities
-   [ ] Process visible text / OCR
-   [ ] Match the restaurant to a real location
-   [ ] Generate structured JSON
-   [ ] Calculate confidence score
-   [ ] Display the location on an interactive map
-   [ ] Demonstrate an end-to-end working flow

------------------------------------------------------------------------

## 🔮 Future Vision

Food Map could evolve from a personal saved-place map into an
**AI-powered food discovery layer** that understands:

> What did I save?\
> What am I in the mood for?\
> What's nearby?\
> Who am I going with?\
> What should I order?

The goal is to close the gap between **food inspiration and real-world
action**.

------------------------------------------------------------------------

## 📌 Project Status

🚧 Built during Hackathon 2026 --- MVP in progress.
