# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Chinese literature knowledge testing system - a collection of standalone HTML quiz applications covering classical and modern Chinese literature. Each quiz is a self-contained, interactive web application with 100 questions.

## Architecture

### File Structure
- **`index.html`** - Main landing page with chapter selection grid
- **`*-test.html`** - Individual quiz modules (6 total):
  - `jianjia-test.html` - 詩經·蒹葭 (Book of Songs)
  - `yufu-test.html` - 屈原·漁夫 (Qu Yuan)
  - `saiqi-test.html` - 王溢嘉·賽琪小姐體內的魔鬼 (Wang Yi-jia)
  - `zhuzhiwu-test.html` - 左丘明·燭之武退秦師 (Zuo Qiuming)
  - `tiangong-test.html` - 宋應星·天工開物 (Song Yingxing)
  - `kongyiji-test.html` - 魯迅·孔乙己 (Lu Xun)

### Common Pattern Across All Test Files

Each test HTML file follows an identical structure:

1. **Header Section**
   - Contains title and original text/article info
   - Has a "返回主頁" (back to home) button linking to `index.html`
   - Text content shown on start screen, hidden during quiz

2. **Quiz Flow**
   - Start screen → 100 questions → Results screen
   - Progress bar tracks completion
   - Questions displayed one at a time

3. **JavaScript Structure**
   ```javascript
   const questions = [/* 100 question objects */];
   let currentQuestion = 0;
   let userAnswers = [];
   let score = 0;

   // Key functions:
   startTest()        // Hides intro, shows first question
   showQuestion(index) // Renders question UI
   selectOption(i)    // Records answer, shows feedback
   nextQuestion()     // Advances or shows results
   previousQuestion() // Goes back
   updateProgress()   // Updates progress bar
   showResults()      // Calculates and displays score
   restartTest()      // Resets to start screen
   ```

4. **Question Object Format**
   ```javascript
   {
       question: "問題文字",
       options: ["選項A", "選項B", "選項C", "選項D"],
       correct: 1  // 0-indexed correct answer
   }
   ```

5. **Styling Convention**
   - Purple/blue gradient theme (`#667eea` to `#764ba2`)
   - Responsive grid layout
   - Inline CSS within `<style>` tags
   - Microsoft YaHei and SimSun fonts for Chinese text

## Creating New Test Modules

When adding a new test unit:

1. **Copy an existing test file** (e.g., `jianjia-test.html`) as template
2. **Update the header**:
   - Change title in `<title>` and `<h1>`
   - Replace content in `#articleInfo` or `#articleText` div
3. **Replace the questions array** with 100 new questions
4. **Update index.html**:
   - Change a `coming-soon` chapter card to active
   - Update `onclick="location.href='new-test.html'"`
   - Update chapter number, title, and description

## Key Behaviors

### Start Screen Flow
- Original text/info is visible
- Progress bar is hidden (`display: none`)
- Click "開始測驗" triggers:
  - Hide `#startScreen`
  - Hide article text (`#poemText` or `#articleInfo`)
  - Show progress bar
  - Call `showQuestion(0)`

### Question Display
- Only one question visible at a time (`.active` class)
- Answer selection shows immediate feedback (green/red)
- "下一題" button disabled until answer selected
- Navigation allows going back to review

### Results Screen
- Shows score as fraction (e.g., "85/100")
- Percentage calculated to 1 decimal place
- Grading messages based on percentage:
  - ≥90%: 優秀
  - ≥80%: 良好
  - ≥70%: 不錯
  - ≥60%: 及格
  - <60%: 需要加強

## Index Page Structure

The main `index.html` uses a card-based grid layout where:
- Active chapters have `onclick="location.href='...'"`
- Coming-soon chapters have `.coming-soon` class with overlay
- Cards use `grid-template-columns: repeat(auto-fit, minmax(300px, 1fr))`

## Development Notes

- **No build process**: All files are standalone HTML with inline CSS/JS
- **No dependencies**: Pure vanilla JavaScript, no frameworks
- **Browser compatibility**: Modern browsers with ES6+ support
- **Character encoding**: UTF-8 for Chinese characters
- **Language**: Traditional Chinese (zh-TW) for modern texts, Simplified (zh-CN) for classical

## Testing Locally

Simply open `index.html` in a web browser. All navigation is relative file paths, so the structure works offline.

## Content Guidelines

Questions for each test module are organized into categories (typically 10 categories × 10 questions):
- Background & author information
- Content comprehension
- Literary techniques
- Character analysis
- Thematic understanding
- Historical/cultural context
- Deep analysis
- Comprehensive questions
