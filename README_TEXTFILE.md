# Using Text Files with Orpheus TTS

You can now use text files as input for Orpheus TTS! This is perfect for converting longer texts, stories, or documents to speech.

## Basic Usage

```bash
# Activate the virtual environment
cd ~/repos/orpheus-tts-local
source venv/bin/activate

# Convert a text file to speech (preserves line breaks for natural pauses)
python gguf_orpheus.py --file your_text.txt --voice tara --output output.wav

# Convert to single continuous line (no pauses at line breaks)
python gguf_orpheus.py --file your_text.txt --voice tara --output output.wav --single-line
```

## Examples

### Simple text file conversion
```bash
python gguf_orpheus.py --file story.txt
```

### Specify voice and output
```bash
python gguf_orpheus.py --file document.txt --voice leo --output narration.wav
```

### With custom parameters
```bash
python gguf_orpheus.py --file script.txt --voice mia --temperature 0.8 --output performance.wav
```

## Text File Format

Your text files can include:
- Plain text
- Multiple paragraphs
- Emotion tags: `<laugh>`, `<chuckle>`, `<sigh>`, `<cough>`, `<sniffle>`, `<groan>`, `<yawn>`, `<gasp>`

### Example text file content:
```
Hello there! <laugh> Welcome to this demonstration.
I can speak with emotions <sigh> and vary my tone.
This makes the speech sound more natural and engaging!
```

## Important Notes

1. **File encoding**: Text files should be UTF-8 encoded
2. **File size**: For very long texts, the generation might take a while
3. **Line breaks handling**: 
   - **Default mode**: Each line is treated as a sentence (periods added if missing)
   - **--single-line mode**: All text merged into one continuous line
4. **Cannot use both**: You cannot use `--text` and `--file` at the same time
5. **Output location**: All WAV files are automatically saved to the `outputs/` folder

## Tips

- For books or long documents, consider breaking them into chapters
- Test with different voices to find the best one for your content
- Use emotion tags sparingly for best results
- Adjust temperature (0.1-1.0) for more or less variation in speech
