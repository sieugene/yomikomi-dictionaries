# Dictionary Setup Guide

This guide explains how to add dictionaries to Yomikomi, including automatic downloads, manual installation, and creating custom dictionaries.

## Table of Contents
- [Automatic Dictionary Download (Recommended)](#automatic-dictionary-download-recommended)
- [Manual Dictionary Installation](#manual-dictionary-installation)
- [Creating Custom Dictionaries](#creating-custom-dictionaries)
- [Troubleshooting](#troubleshooting)

## Automatic Dictionary Download (Recommended)

The easiest way to add dictionaries is through the built-in download feature:

1. **Open the Dictionary Manager**
   - Click "Add Dictionary" in the application
   
2. **Get Recommended Dictionaries**
   - Click the "Get Recommended Dictionaries" button
   - Choose from available languages (English, Russian, etc.)
   - The dictionary will be downloaded automatically

3. **Continue Setup**
   - After download, proceed with template selection
   - The system will guide you through the remaining steps

## Manual Dictionary Installation

If automatic download fails or you prefer manual installation:

### Option 1: Pre-built Dictionaries

1. **Download from our repository**
   ```bash
   # Visit: https://github.com/sieugene/yomikomi-dictionaries
   ```
   
2. **Available dictionaries:**
   - `combined_terms_JMdict_english.sqlite` - English definitions
   - `combined_terms_JMdict_russian.sqlite` - Russian definitions

3. **Add to Yomikomi**
   - Click "Add Dictionary" 
   - Select "Select File" and choose the downloaded `.sqlite` file
   - Follow the template selection process

### Option 2: Build from Yomitan Dictionaries

1. **Clone the Yomikomi project**
   ```bash
   git clone https://github.com/sieugene/yomikomi.git
   cd yomikomi
   npm install  # or pnpm install
   ```

2. **Download dictionary source**
   - Visit: https://github.com/yomidevs/jmdict-yomitan
   - Download your desired dictionary (e.g., `JMdict_english.zip`)

3. **Place the dictionary file**
   ```bash
   # Create directory if it doesn't exist
   mkdir -p src/shared/data/dict/JMdict
   
   # Move your downloaded file
   mv JMdict_english.zip src/shared/data/dict/JMdict/
   ```

4. **Build the dictionary**
   ```bash
   npm run make-dictionary -- -file='JMdict_english'
   ```
   
   This will create:
   - `combined_terms_JMdict_english.json` (intermediate file)
   - `combined_terms_JMdict_english.sqlite` (final dictionary)

5. **Use the generated dictionary**
   - The `.sqlite` file can now be imported through "Add Dictionary"
   - Or you can share it with others

## Creating Custom Dictionaries

### For Advanced Users

If you want to create a dictionary from your own data:

1. **Understand the Schema**
   - Dictionaries are SQLite files with a `terms` table
   - Each term can have multiple definitions and metadata
   - Check existing dictionaries for schema reference

2. **Prepare Your Data**
   - Create a JSON array with your dictionary entries
   - Follow the same structure as JMdict entries
   - Ensure proper encoding (UTF-8)

3. **Convert to SQLite**
   - Use the `make-dictionary` script as a template
   - Modify the script to process your JSON format
   - Generate the final `.sqlite` file

4. **Configure Templates**
   - Use the Custom Template Editor in the app
   - Define parsing rules for your dictionary structure
   - Test with sample data before finalizing

### Template Configuration

When adding custom dictionaries, you may need to configure parsing templates:

- **Word Column**: Which column contains the main word/term
- **Reading Column**: Pronunciation or reading information  
- **Definition Column**: Main definition or meaning
- **Additional Fields**: Any extra metadata or classifications

## Troubleshooting

### Common Issues

**❌ Download fails with CORS error**
- Try manual installation from our repository
- Check your internet connection
- Ensure no firewall is blocking the download

**❌ "Manager not initialized" error**
- Refresh the page and try again
- Check browser console for additional errors

**❌ Dictionary file not recognized**
- Ensure the file is a valid SQLite database
- Check file extension is `.sqlite` or `.db`
- Try with a pre-built dictionary first

**❌ Template parsing errors**
- Use the template tester with sample words
- Check column names match your data structure
- Verify data types are compatible

### Getting Help

If you encounter issues:

1. **Check existing dictionaries** - Compare with working examples
2. **Use built-in testing** - Test your templates before saving
3. **Create an issue** - Visit https://github.com/sieugene/yomikomi/issues

Include in your issue:
- Steps to reproduce the problem
- Error messages (if any)
- Dictionary file details
- Your operating system and browser

---

## Quick Reference

| Task | Command/Action |
|------|--------|
| Auto download | Click "Get Recommended Dictionaries" |
| Manual add | Click "Select File" → Choose `.sqlite` file |
| Build dictionary | `npm run make-dictionary -- -file='YourDict'` |
| Custom template | Use "Custom Template" option |

For more detailed technical documentation, visit the [main repository](https://github.com/sieugene/yomikomi).