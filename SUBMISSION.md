# NewsPrism: Breaking the Echo Chamber with Amazon Nova Sonic 2

## Inspiration
The inspiration for **NewsPrism** comes from a growing concern about the "Echo Chamber" effect in modern media. Today, algorithms are designed to keep us engaged, which often means feeding us news that reinforces our existing biases. This has led to a deeply polarized society where "shared reality" is disappearing. 

We asked ourselves: *What if we could use AI not to tell people what to think, but to show them HOW to think critically?* We wanted to create a tool that acts like a prism, taking the "white light" of a single news narrative and refracting it into its constituent spectrum of perspectives. By hearing from multiple, grounded viewpoints simultaneously, users can act as a "Jury" and form their own, more balanced conclusions.

## What it does
NewsPrism is an AI-powered news analysis platform that dissects any article or report into a multi-perspective debate.

1.  **Deep Extraction**: It takes a URL, extracts the core content, and strips away the noise.
2.  **Multi-Agent Analysis**: It deploys three specialized AI agents:
    *   **The Sentinel (Nova 2 Pro)**: Analyzes through a market-focused, right-leaning lens.
    *   **The Advocate (Nova 2 Pro)**: Analyzes through a social-equity, left-leaning lens.
    *   **The Jurist (Nova 2 Pro)**: A neutral fact-checker that identifies missing context and emotive language.
3.  **Polarization Index**: It calculates a "Polarization Score" (0-100) to show how biased the original report was.
4.  **Live Debate (Powered by Nova Sonic 2)**: The agents enter a real-time, low-latency debate. Users can listen to the agents challenge each other, ask them questions, and guide the discussion.
5.  **Prism Synthesis**: The system identifies the "Shared Reality"—the core facts that all perspectives agree upon.

## How we built it
We built NewsPrism using a modern full-stack architecture optimized for the **AWS ecosystem**, focusing on a "Separation of Concerns" between reasoning and speed:

*   **Frontend**: A high-performance **React 18** application. We utilized **Tailwind CSS** for a "New York Times" inspired aesthetic, emphasizing typography and white space. **Framer Motion** was used to handle the complex layout transitions between the "Prism Analysis" view and the "Live Debate" overlay.
*   **Backend**: An **Express.js** server running on Node.js. The backend serves two primary purposes: 
    1.  **Content Extraction**: Using specialized scrapers to pull clean text from news URLs, bypassing ads and trackers to provide a "Source Brief."
    2.  **Bedrock Proxy**: Securely communicating with the **Amazon Bedrock** API using the `@aws-sdk/client-bedrock-runtime`.
*   **AI Orchestration (Amazon Bedrock)**:
    *   **Amazon Nova 2 Pro**: This is our "Heavy Lifter." We use it for the initial deep analysis. Its 200k+ context window and high reasoning scores allow it to digest long-form investigative journalism and identify subtle biases that smaller models might miss.
    *   **Amazon Nova Sonic 2 (Nova 2 Lite)**: This is our "Speed Demon." We use it for the **Live Debate**. By utilizing the ConverseStream API, we achieve ultra-low "Time to First Token" (TTFT), which is critical for making the agent-to-agent and agent-to-user interactions feel fluid and natural.
*   **Agentic Workflow**: We implemented a state-machine based moderator pattern. The system maintains a "Debate State" in the frontend, tracking which agent has spoken, what points have been raised, and when the user (The Jury) has intervened.

## Challenges we ran into
*   **Latency in Live Interaction**: During early prototyping with larger models, the "Live Debate" had 5-10 second pauses between speakers, which killed the immersion. We solved this by architecting a streaming pipeline using **Amazon Nova Sonic 2**, reducing the perceived latency to sub-second levels.
*   **Persona Grounding & Hallucination**: It was challenging to ensure agents remained "grounded" in the article rather than hallucinating general political talking points. We solved this through **Chain-of-Thought (CoT)** prompting, where agents are required to first "extract evidence" from the source before "forming an opinion."
*   **Objective Bias Scoring**: Creating a "Polarization Index" that didn't feel biased itself was difficult. We addressed this by having the "Jurist" agent (the neutral one) perform a multi-pass evaluation: first identifying "loaded words," then "missing perspectives," and finally calculating a weighted score based on these objective metrics.
*   **Audio Synchronization**: Synchronizing the text transcript with the (planned) audio output required careful management of the streaming buffers to ensure that the "Speaking" indicator in the UI matched the actual text being generated.

## Accomplishments that we're proud of
*   **The "Sonic" Debate Experience**: We are incredibly proud of how fast and responsive the Live Debate feels. Using **Amazon Nova Sonic 2** allowed us to achieve near-human response times, making the AI agents feel like real participants in a high-stakes discussion.
*   **The "Jury" Interaction Model**: We successfully implemented a UI/UX pattern where the user isn't just a passive observer but an active "Jury." The ability for the user to intervene, ask questions, and redirect the debate in real-time is a unique and powerful feature.
*   **The Shared Reality Synthesis**: Successfully creating a feature that extracts what *everyone* agrees on, even in a highly polarized debate, feels like a genuine step toward better public discourse.
*   **Visual Identity**: We created a UI that feels authoritative and "news-like," which helps build trust with the user. The "On Air" indicator and the real-time voice waveforms add a layer of professional polish.

## What we learned
*   **Specialization Wins**: We learned that using different models for different tasks (Nova 2 Pro for deep thought, Sonic 2 for speed) is far more effective than trying to use one model for everything. This "Tiered Intelligence" approach is now a core part of our design philosophy.
*   **Latency is UX**: In AI applications, latency isn't just a technical metric; it's the difference between a tool that feels like a "chatbot" and one that feels like a "participant." **Nova Sonic 2** was the game-changer here.
*   **The Value of Friction**: Sometimes, "friction" (like forcing a user to listen to a dissenting view) is a feature, not a bug. It promotes the critical thinking we set out to inspire.
*   **The Moderator-Debater Pattern**: We discovered that having a "Moderator" agent (even if hidden) to manage the state of the debate is much more effective than letting agents talk to each other directly, as it prevents "agent loops" and ensures the user remains the priority.

## What's next
*   **Multimodal Evidence (Amazon Nova 2 Image)**: We plan to integrate image generation to create visual metaphors for each perspective's core arguments, making the analysis even more intuitive.
*   **Real-time Sentiment (AWS Lambda & X API)**: Using **AWS Lambda** to pull live social media data to show how the "public" perspective compares to our AI analysts in real-time.
*   **Global Expansion**: Adding agents that represent international geopolitical perspectives (e.g., how a story is viewed in the Global South vs. the West) to provide a truly global "Prism."
*   **Audio Prism (Amazon Nova 2 TTS)**: Implementing high-fidelity text-to-speech to allow users to listen to the debate as a podcast-style briefing while commuting, with distinct voices for each agent.
*   **Browser Extension**: Building a NewsPrism extension that allows users to "refract" any news article they are currently reading with a single click.

---
*NewsPrism: Refracting the news to find the truth. Powered by Amazon Nova Sonic 2.*
