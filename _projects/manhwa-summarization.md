---
title: "Automatic Manhwa Summarization"
excerpt: "AI-powered video generation system that creates automated manhwa summaries with GPT-4-V, voice synthesis, and dynamic video editing"
date: 2024-12-15
tags: [python, ai, computer-vision, video-processing, openai, tts, moviepy]
github: "https://github.com/clsandoval/manhwa-summarization"
layout: single
author_profile: true
---

## Project Overview

The Automatic Manhwa Summarization system is an innovative AI-powered tool that transforms manhwa (Korean comics) into engaging video summaries. The system combines computer vision, natural language processing, and video production techniques to automatically generate narrated video content from static manhwa panels.

### Key Capabilities
- **🎨 Panel Analysis**: GPT-4-V powered visual understanding of manhwa panels
- **📝 Script Generation**: Contextual storytelling with narrative continuity
- **🎙️ Voice Synthesis**: High-quality text-to-speech with multiple providers
- **🎬 Video Production**: Dynamic transitions, effects, and subtitle integration
- **🖼️ Background Generation**: AI-generated atmospheric backgrounds with DALL-E 3
- **⚡ Batch Processing**: Multi-threaded audio generation for efficiency

## Technical Architecture

### System Workflow

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Manhwa        │    │   GPT-4-V       │    │   Script        │
│   Panels        │────│   Analysis      │────│   Generation    │
└─────────────────┘    └─────────────────┘    └─────────────────┘
          │                       │                       │
          ▼                       ▼                       ▼
┌─────────────────────────────────────────────────────────────────┐
│                    VIDEO GENERATION PIPELINE                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐ │
│  │ TTS Generation  │  │ Background      │  │ Subtitle        │ │
│  │ (PlayHT/11Labs) │  │ Generation      │  │ Generation      │ │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘ │
│                                                                 │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐ │
│  │ Dynamic Effects │  │ MoviePy         │  │ Final Video     │ │
│  │ & Transitions   │  │ Composition     │  │ Assembly        │ │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘ │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Tech Stack
- **AI/ML**: OpenAI GPT-4-V, DALL-E 3, Whisper
- **TTS Providers**: PlayHT, ElevenLabs
- **Video Processing**: MoviePy, OpenCV
- **Audio Processing**: Mutagen, AssemblyAI
- **Image Processing**: PIL, scikit-image
- **Async Processing**: Threading for parallel operations

## Core Features

### 1. Intelligent Panel Analysis

The system uses GPT-4-V to understand manhwa panels and maintain narrative context:

```python
@retry_with_exponential_backoff
def gpt_inference_context(
    client, prompt, image_path, context_path, model="gpt-4o-mini", detail="low"
) -> tuple[int, dict]:
    
    with open(context_path, "r") as f:
        context = f.read()
    
    content = [{
        "type": "image_url",
        "image_url": {
            "url": f"data:image/jpeg;base64,{encode_image(image_path)}",
            "detail": detail,
        },
    }]
    
    response = client.chat.completions.create(
        model=model,
        messages=[
            {"role": "system", "content": prompt},
            {"role": "user", "content": f"Context so far: {context}"},
            {"role": "user", "content": content},
        ],
        response_format={"type": "json_object"},
        max_tokens=1000,
    )
    
    return response.usage.total_tokens, json.loads(response.choices[0].message.content)
```

### 2. Contextual Story Generation

The AI maintains story continuity by tracking characters, scenes, and narrative progression:

```json
{
    "CURRENT_PANEL": "current panel narration",
    "STORY_SUMMARY": "high level story summary",
    "ACTIVE_SCENES": [
        {
            "SCENE_NAME": "NAME",
            "CHARACTERS": [
                {"NAME": "CHARACTER_NAME", "BACKSTORY": "BACKSTORY"}
            ],
            "SCENE_CONTEXT": "SCENE_CONTEXT"
        }
    ]
}
```

### 3. Dynamic Video Effects

Advanced video processing with multiple transition types:

```python
def ken_burns_generator(width, height, image_length, scale_factor):
    """Generate Ken Burns effect variations for dynamic panel presentation"""
    width, height = math.floor(width * scale_factor), math.floor(height * scale_factor)
    start_width = width - 1920
    start_height = height - 1080

    transitions = [
        functools.partial(ken_burns, image_length, 0, 
                         random.randint(-start_height, -int(0.1 * height)), 
                         -start_width, 0),
        functools.partial(ken_burns, image_length, -start_width, 
                         random.randint(-start_height, -int(0.1 * height)), 
                         0, 0),
        # Additional transition variations...
    ]
    
    return transitions
```

### 4. Multi-Provider TTS Integration

Flexible text-to-speech with multiple providers:

```python
def playht_generate_audio(script, path):
    """Generate high-quality speech with PlayHT API"""
    payload = {
        "content": [script],
        "voice": "fil-PH-Wavenet-D",
        "trimSilence": True,
        "globalSpeed": "110%",
    }
    
    # API call and file processing
    response = requests.post(tts_url, json=payload, headers=headers)
    # ... handle conversion and download
```

### 5. Intelligent Panel Filtering

Automated filtering to remove non-story panels:

```python
def filter_images(image_paths):
    """Filter out title pages and meta information panels"""
    info_panel_paths = []
    for image_path in image_paths:
        response = openai_client.chat.completions.create(
            model="gpt-4o",
            messages=[{
                "role": "system",
                "content": """Classify panel as STORY or OTHER. STORY panels 
                           feature main story events. OTHER panels are titles, 
                           glossaries, meta information."""
            }],
            response_format={"type": "json_object"}
        )
        # Process classification results
```

## Processing Pipeline

### Chapter Processing Workflow

1. **Panel Analysis**: GPT-4-V analyzes each manhwa panel for story content
2. **Script Generation**: AI generates contextual narration maintaining story flow
3. **Translation**: Optional translation to target language with style consistency
4. **Audio Generation**: Multi-threaded TTS processing for efficiency
5. **Background Creation**: DALL-E 3 generates atmospheric chapter backgrounds
6. **Video Assembly**: MoviePy combines panels, audio, effects, and subtitles

### Configuration Management

```python
# Flexible chapter range processing
CHAPTER_START = 20
CHAPTER_END = 30

# Multi-platform path handling
if platform == "win32":
    OS_DELIMETER = "\\"
else:
    OS_DELIMETER = "/"
```

## Advanced Features

### Dynamic Visual Effects

The system implements multiple visual techniques to prevent repetitive content:

#### Transition Types
- **Ken Burns Effect**: Gradual zoom and pan movements
- **Pan Down**: Vertical scrolling for tall panels  
- **Zoom In/Out**: Dynamic scaling effects
- **Gaussian Blur Backgrounds**: Atmospheric depth

#### Subtitle Integration
- **Word-level timing**: Precise synchronization with speech
- **Dynamic highlighting**: Visual emphasis on spoken words
- **Multi-line support**: Proper text wrapping and positioning

### Multi-Language Support

```python
# Translation with style consistency
if LANGUAGE:
    tokens, script = gpt_text_inference(
        client,
        f"Translate to {LANGUAGE}. Maintain consistency with: {previous_scripts_string}. "
        f"Follow this transcript style: {EXAMPLE_TRANSCRIPT}",
        script
    )
```

### Batch Processing Optimization

```python
# Parallel audio generation for efficiency
threads = []
for idx in range(len(chapter_scripts)):
    thread = threading.Thread(
        target=playht_generate_audio,
        args=(chapter_scripts[idx], audio_path)
    )
    thread.start()
    threads.append(thread)

# Wait for all threads to complete
for thread in threads:
    thread.join()
```

## Technical Challenges & Solutions

### Challenge 1: Maintaining Narrative Continuity
**Problem**: Each panel needs context from previous panels for coherent storytelling.

**Solution**: Implemented context persistence system that tracks story summary, active scenes, and character information across panel processing.

### Challenge 2: Video Repetitiveness Prevention  
**Problem**: Static panels could create monotonous video content.

**Solution**: Developed comprehensive transition system with Ken Burns effects, panning, zooming, and background blur variations, randomized for each panel.

### Challenge 3: Multi-Provider TTS Reliability
**Problem**: TTS services have varying reliability and rate limits.

**Solution**: Implemented retry mechanisms with exponential backoff and support for multiple TTS providers (PlayHT, ElevenLabs) with seamless fallback.

### Challenge 4: Large-Scale Processing Efficiency
**Problem**: Processing hundreds of panels sequentially is time-intensive.

**Solution**: Multi-threaded audio generation and batch processing capabilities with configurable chapter ranges.

## Testing & Quality Assurance

### Content Validation
- Panel classification accuracy testing
- Story continuity verification  
- Translation quality assessment
- Audio-visual synchronization validation

### Performance Optimization
- Memory usage monitoring during video processing
- Processing time benchmarking across different chapter lengths
- API rate limit handling and optimization

## Real-World Applications

### Content Creation
- **Manhwa Publishers**: Automated promotional content generation
- **Content Creators**: Rapid video summary production
- **Educational Use**: Literature analysis and storytelling studies
- **Accessibility**: Audio-visual content for visually impaired users

### Technical Innovation
- **AI-Assisted Media**: Demonstrates practical AI application in creative workflows
- **Multi-Modal Processing**: Combines vision, language, and audio AI models
- **Scalable Pipeline**: Production-ready system for batch content processing

## Performance Metrics

### Processing Capabilities
- **Panel Analysis**: ~2-5 seconds per panel (GPT-4-V)
- **Audio Generation**: ~10-30 seconds per segment (varies by TTS provider)  
- **Video Assembly**: ~5-10 minutes per chapter (10-20 panels)
- **Memory Usage**: ~2-4GB during peak video processing

### Quality Metrics
- **Story Coherence**: Maintained across chapter boundaries
- **Audio Quality**: High-fidelity TTS with natural pacing
- **Visual Appeal**: Dynamic transitions prevent monotony
- **Subtitle Accuracy**: Word-level synchronization with audio

## Future Enhancements

### Planned Features
- **Character Voice Assignment**: Different voices for different characters
- **Emotional Tone Analysis**: Dynamic voice modulation based on scene emotion  
- **Interactive Timelines**: Clickable chapter navigation
- **Real-time Processing**: Live streaming capability for ongoing series

### Research Applications  
- **Media Analysis**: Studying visual storytelling patterns
- **AI Creativity**: Exploring AI-assisted creative content production
- **Accessibility Technology**: Improving content accessibility for diverse audiences

## Code Organization

```
manhwa-summarization/
├── generate_audio.py         # Main script generation and TTS
├── generate_backgrounds.py   # DALL-E background creation
├── generate_video.py         # Video assembly pipeline  
├── generate_subtitles.py     # Subtitle processing
├── funcs.py                  # Core utility functions
├── filter.py                 # Panel classification
├── config.py                 # Configuration management
├── requirements.txt          # Dependencies
└── text/                     # Prompts and context files
    ├── prompt.txt           # GPT-4-V analysis prompt
    ├── context.txt          # Story context storage
    └── example_transcript.txt # Translation style guide
```

## Development Practices

### Code Quality
- **Retry Mechanisms**: Robust API failure handling
- **Type Safety**: Clear parameter typing and validation
- **Error Handling**: Graceful degradation with detailed logging
- **Modularity**: Separated concerns across specialized modules

### Documentation
- **Inline Comments**: Clear explanation of complex algorithms
- **Configuration Options**: Well-documented parameter tuning
- **API Integration**: Detailed examples for each service provider

This project showcases the intersection of computer vision, natural language processing, and multimedia production, creating an innovative solution for automated content creation in the digital media landscape. The comprehensive approach to AI integration, video processing, and quality assurance makes it a robust foundation for creative AI applications.