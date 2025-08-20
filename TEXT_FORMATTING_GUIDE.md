# Orpheus TTS Text Formatting Guide for LLMs

## Purpose
This guide helps LLMs (Language Models) properly format text for optimal speech synthesis using Orpheus TTS.

## Basic Formatting Rules

### 1. Single Continuous Line Format (Recommended)
For best results, format text as a single continuous line with proper punctuation:

```
This is the first sentence. This is the second sentence. Here's another thought. And this continues smoothly.
```

### 2. Punctuation is Critical
- **Always end sentences** with proper punctuation (. ! ?)
- **Use commas** for natural pauses within sentences
- **Avoid line breaks** unless you specifically want a pause

### 3. Emotion Tags
Insert emotion tags directly in the text where the emotion should occur:

```
Hello there! <laugh> This is exciting. <sigh> Sometimes things are tough. <chuckle> But we keep going!
```

Available emotion tags:
- `<laugh>` - Laughter
- `<chuckle>` - Light laugh
- `<sigh>` - Sighing sound
- `<cough>` - Coughing
- `<sniffle>` - Sniffling
- `<groan>` - Groaning
- `<yawn>` - Yawning
- `<gasp>` - Gasping

## Text Preparation Examples

### Example 1: Story/Narrative
**Input (multi-line):**
```
Once upon a time
There was a brave knight
He lived in a castle
The castle was very tall
```

**Formatted for TTS:**
```
Once upon a time, there was a brave knight. He lived in a castle. The castle was very tall.
```

### Example 2: Dialogue
**Input:**
```
John said hello
Mary replied hi there
How are you today
I'm doing great thanks
```

**Formatted for TTS:**
```
John said, "Hello." Mary replied, "Hi there! How are you today?" "I'm doing great, thanks!"
```

### Example 3: With Emotions
**Input:**
```
I can't believe it worked
This is amazing
Wait what was that noise
Oh it's just the cat
```

**Formatted for TTS:**
```
I can't believe it worked! <laugh> This is amazing! <gasp> Wait, what was that noise? <sigh> Oh, it's just the cat.
```

## Step-by-Step Formatting Process

1. **Read through the entire text** to understand context
2. **Identify sentence boundaries** and add proper punctuation
3. **Merge lines** into continuous text (unless breaks are intentional)
4. **Add emotion tags** where appropriate for expressiveness
5. **Review punctuation** to ensure natural speech flow

## Common Issues and Solutions

### Issue: Missing punctuation
**Problem:** `This is line one This is line two`
**Solution:** `This is line one. This is line two.`

### Issue: Hard line breaks
**Problem:**
```
This is
a sentence
broken up
```
**Solution:** `This is a sentence broken up.`

### Issue: Lists or bullets
**Problem:**
```
- First item
- Second item
- Third item
```
**Solution:** `First item. Second item. Third item.`

### Issue: Dialogue formatting
**Problem:** `Person A: Hello Person B: Hi`
**Solution:** `Person A said, "Hello." Person B replied, "Hi."`

## Command Line Usage

### For single-line format (recommended):
```bash
python gguf_orpheus.py --file formatted_text.txt --voice tara --single-line
```

### For preserving formatting:
```bash
python gguf_orpheus.py --file formatted_text.txt --voice tara
```

## Best Practices for LLMs

1. **Default to single-line format** unless specifically asked to preserve formatting
2. **Always ensure proper punctuation** at sentence ends
3. **Use emotion tags sparingly** - too many can sound unnatural
4. **Consider the voice character** when adding emotions (some voices suit certain emotions better)
5. **Test with small samples first** before processing large texts

## Output File Structure

When processing text, files are saved with descriptive names:
- Format: `{voice}_{source}_{timestamp}.wav`
- Example: `tara_file_20250819_143022.wav`
- Location: Always in the `outputs/` folder

## Sample Formatting Function (Pseudocode)

```python
def format_for_orpheus_tts(text):
    # Remove extra whitespace and line breaks
    lines = text.strip().split('\n')
    
    # Process each line
    formatted_lines = []
    for line in lines:
        line = line.strip()
        if line:
            # Add period if missing punctuation
            if line and line[-1] not in '.!?,;:':
                line += '.'
            formatted_lines.append(line)
    
    # Join with spaces
    formatted_text = ' '.join(formatted_lines)
    
    # Clean up spacing
    formatted_text = ' '.join(formatted_text.split())
    
    return formatted_text
```

## Quick Reference

| Text Type | Formatting Approach |
|-----------|-------------------|
| Story/Book | Single line with proper punctuation |
| Dialogue | Add quotation marks and attributions |
| Lists | Convert to sentences with periods |
| Poetry | Preserve line breaks (don't use --single-line) |
| Technical | Spell out abbreviations, add pauses with commas |
| Emotional | Add appropriate emotion tags |

## Remember
The goal is natural-sounding speech. When in doubt, read the text aloud yourself and add punctuation where you naturally pause or change tone.
