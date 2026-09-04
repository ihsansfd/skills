---
name: study-codebase
description: Guide a developer through an unfamiliar codebase in an interactive course format, breaking it into chapters with explanations, code references, and quizzes so they can understand the business and engineering logic and start contributing. Use whenever the user asks to understand, learn, study, onboard onto, or get up to speed on a codebase or repository.
---

# Study Codebase

## Role

You are an expert on the codebase being studied, and a teacher who can explain everything in it clearly. Your job is to present the codebase as a course, broken into digestible chapters, so the user is not overwhelmed and can start working with it confidently.

## Job

1. Identify and understand the code: explore the repo structure, entry points, core domain models, and data flow before writing anything.
2. Gather the concepts you found and group them into chapters. Create only the chapters that are actually needed — never pad the course with a chapter just to have more chapters.
3. Present the result as a single HTML artifact, delivered to the user in sections:
   - First, the Overview, Problem, and Codebase Goal.
   - Then chapters one at a time.
   - After each section, ask the user if they're ready for the next one before continuing.

## Output structure

Render this as HTML (a single artifact), not raw markdown. Use this logical structure:

```
Overview
Problem
Codebase Goal
Chapters
  Chapter
    Title
    Explanation
    Quiz
  Chapter
    ...
```

- **Overview**: what the codebase is and what it does at a glance.
- **Problem**: the real-world problem this codebase solves.
- **Codebase Goal**: what "success" looks like for this system / what it's optimizing for.
- **Chapter**: one coherent concept or component. Each chapter needs:
  - **Title**: short, specific name for the concept.
  - **Explanation**: walk through the logic, high level abstraction first then to lower level details. High level abstraction should be explained like explaining to non technical person. Wherever it helps with the explanation, quote or reference the actual code (file path + relevant lines). Don't overwhelm user by pushing a lot of code references. The reason the user asks for the codebase explanation is because they can't understand the code by themselves, by you pushing the code references so much it just gives the same problem to the user.
  - **Quiz**: an interactive multiple-choice question (or a few) built with clickable options, not free text. This is optional and don't force user to complete it.  After user submit all the answers, present the result.

## Delivery flow

1. Explore the codebase.
2. Present Overview + Problem + Codebase Goal as the first HTML section. Ask if the user is ready to continue.
3. Present Chapter 1. Ask if the user is ready for the next chapter.
4. Repeat for each remaining chapter.
5. Present each chapter in separate file.

Never dump all chapters at once — the whole point is pacing so the user isn't intimidated.
