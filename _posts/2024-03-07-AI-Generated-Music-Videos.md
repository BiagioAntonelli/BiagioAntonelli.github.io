---
layout: post
title: "Creating AI-Generated Music Videos: A Fun Experiment"
date: 2024-02-15
categories: [AI, Projects]
---

I recently experimented with creating AI-generated music videos by combining various AI tools, and published the results in [this YouTube playlist](https://www.youtube.com/playlist?list=PLUf8wGHNmTFOquH69NS-XMX9By75Y9dlV). The results were quite interesting - check out this example:

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; border-radius: 8px; margin: 20px 0;">
    <iframe 
        src="https://www.youtube.com/embed/ltktlw9t-sw" 
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" 
        frameborder="0" 
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
        allowfullscreen>
    </iframe>
</div>


Here's a quick overview of the process:

### 1. Image Generation with Flux-dev

First, I used [Flux-dev](https://replicate.com/black-forest-labs/flux-dev) on Replicate to generate anime-style images. Here's an example prompt I used:

<div style="max-width: 600px; white-space: pre-wrap; background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 20px 0; font-family: 'Courier New', monospace; line-height: 1.6;">
An anime-style illustration of a young girl standing outside a 
stadium with a bold 'Napoli' graffiti in the background. 
The girl has her hair styled in a unique braided ponytail, 
wearing a red sports jacket with white stripes, a gray 
sweatshirt, and a gold chain necklace. Her 
expression is introspective, and she is looking downward, 
creating a thoughtful mood. The background includes a detailed 
depiction of the stadium structure under a soft blue sky with clouds.
</div>

### 2. Music Generation with Suno

For the music, I used [Suno](https://suno.com/) to generate the audio tracks. While they don't officially offer an API yet, there is an [unofficial API](https://github.com/gcui-art/suno-api) available (though I haven't tested it).

### 3. Image to Video with KLING 1.6

I then used KLING 1.6 to transform the static images into dynamic videos, adding subtle movements and transitions.

### 4. Combining Audio and Video

Finally, I wrote a simple Python script using `moviepy` to combine the generated audio and video. The script loops the video for the duration of the audio track:

```python
from moviepy.editor import VideoFileClip, ImageClip, AudioFileClip

# ... rest of the code ...
async def create_video(
    self,
    audio_file: UploadFile,
    visual_file: UploadFile,
    bottom_crop_percent: int = 0
) -> str:
    """
    Create a video from an audio file and either an image or video file.

    Args:
        audio_file: The uploaded audio file
        visual_file: The uploaded image or video file
        bottom_crop_percent: Percentage to crop from bottom (default: 0)
        
    Returns:
        str: Path to the generated video file
    """
    # Load the audio and visual files
    audio_clip = AudioFileClip(audio_path)
    
    # Create video clip and loop if necessary
    if is_image:
        visual_clip = ImageClip(visual_path).set_duration(audio_duration)
    else:
        visual_clip = VideoFileClip(visual_path)
        if visual_clip.duration < audio_duration:
            visual_clip = visual_clip.loop(duration=audio_duration)
    
    # Combine and save
    final_clip = visual_clip.set_audio(audio_clip)
    final_clip.write_videofile(
        output_path,
        codec='libx264',
        audio_codec='aac'
    )
    # ... rest of the code ...
```

### Future Improvements

An interesting next step would be to automatically generate image prompts based on song lyrics. This could create a more cohesive narrative in the music videos. The process would look something like this:

1. Split lyrics into time-based chunks
2. For each chunk, generate:
   - Text-to-image prompts for scene composition
   - Image-to-video prompts for camera movements and transitions
3. Use these prompts to create a sequence of scenes that match the song's narrative

This could lead to even more engaging and contextually relevant music videos!

Feel free to check out the example videos and let me know what you think! 