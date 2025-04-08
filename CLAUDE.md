# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Build Commands
- `bundle install` - Install dependencies
- `bundle exec jekyll serve` - Run local development server
- `bundle exec jekyll build` - Build the site

## Content Guidelines
- Blog posts go in `_posts/` with filename format: `YYYY-MM-DD-title.md`
- Front matter requires: layout, title, date, categories
- Include a summary in front matter for post previews
- Use markdown for content formatting

## Posting Standards
- Technical posts should include code samples with syntax highlighting
- Code samples should be wrapped in triple backticks with language identifier
- Categories should be specific and relevant to the content
- Maintain consistent voice and technical depth across posts

## Site Configuration
- Site settings are in `_config.yml`
- Theme customization through the minima theme
- Deploy by pushing to main branch