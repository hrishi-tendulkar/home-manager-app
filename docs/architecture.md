# System Architecture

Home Manager is structured as a small set of cooperating components that support capture, organization, and follow-up over time.

The architecture emphasizes clarity, consistency, and the ability to evolve as the product grows.

---

## Core components

### Capture layer

The capture layer accepts incoming information from multiple entry points, including manual input, photos, documents, and conversational text.

Its responsibility is to make capture fast and forgiving, without requiring users to decide how information should be structured upfront.

---

### Normalization layer

The normalization layer interprets captured inputs and maps them into the core data model.

This includes identifying relevant categories, services, and occurrences, and extracting useful details when available. Normalization improves consistency while preserving the original context of capture.

---

### Home record

The home record stores structured information about the home over time.

It maintains a history of services and occurrences along with supporting context such as notes, costs, and attachments. This record acts as the system’s long-term memory.

---

## Context assembly

Home Manager builds context by combining structured home history with situational signals such as timing, recency, and the user’s current intent.

Context is derived from the home record rather than reconstructed independently for each interaction. This supports consistent reasoning over time while remaining responsive to what matters in the moment.

---

### Intelligence layer

The intelligence layer operates over assembled context to support summaries, reminders, and guidance.

It surfaces relevant information based on history and timing rather than constant monitoring or alerts.

---

## Role of AI in the system

AI supports interpretation, summarization, and guidance within the capture and intelligence layers.

It operates on top of a stable data model and assembled context, allowing behavior to improve over time without changing the underlying structure of the product.

---

## Architectural intent

The system is designed to remain understandable as it evolves.

Each component has a clear responsibility, which allows new capabilities to be added while preserving traceability, user trust, and product coherence.
