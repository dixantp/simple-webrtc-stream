## Plan for a Scalable WebRTC Streaming Platform
This readme outlines the plan to evolve the initial one-to-one WebRTC prototype into a scalable, multi-stream broadcasting platform.

## Objective
The goal is to build a robust streaming solution that can hanlde multiple pre-composed AV streams from various producers and distribute them to a large number of concurrent viewers in real-time. The system should be reliable and serve as a reusable framework for future projects.

## Core Architecture: SFU Model
We will move from the initial peer-to-peer (P2P) model to a more scalable client-server architecture using a Selective Forwarding Unit (SFU)
- Why can SFU? P2P is not scalable to beyond a few viewers, An SFU will act as a central media server that receives a single stream from each producer and efficiently forwards it to all subscribing clients. This keeps the producer's upload bandwidth requirements low, regardless of the audience size.
- Functionality: The system will operate on a "publish-subscribe" pattern. Producers will "publish" their streams to the SFU, and viewers will "subscribe" to the specific streams they wish to watch.

## Key Technical Details & Requirements
- Latency: The platform will leverage WebRTC to maintain very low latency, targeting under 500ms (typically 150-300ms) for a near real-time interactive experience. 
- Content Source: The producers will provide pre-mixed AV content. This simplifies the client-side implementation, as it removes the need for live device management and real-time audio/video composition in the browser.
- Stream Management: The SFU must support receiving multiple (e.g., 6-12) final AV streams simultaneously and allow clients to select which streams to view.

## Implementation Plan
1. Select & Deploy an SFU: Choose a robust, open-source SFT (LiveKit is a strong candidate). Deploy this SFU to a cloud provider.
2. Integrate Clients: Refactor the existing `sender` and `receiver` clients to communicate with the SFU instead of directly with each other. The `sender` will become a "publisher" and the `receiver` a "subscriber"
3. Cloud hosting: The SFU will be hosted on a cloud service. While AWS is the preferred choice, other providers like GCP are also viable options.

## Required Resources and Dependencies
- A dedicated Cloud Provider Account