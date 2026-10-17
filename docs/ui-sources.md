# UI Sources & Citation Design

## Overview

The assistant answers questions using records loaded from the offices CSV.
Each answer about an office includes its name, room, and opening hours.

The current `reply()` function returns plain text only. Citations in this
document are mockups of how the source attribution should appear; interactive
citations require additional implementation.

## Citation rules

- Cite only the office record used to generate the answer.
- Use the office name as the source label.
- Show the room and hours from that same CSV row.
- Do not invent facts or cite external sources.
- Do not display citations for greetings, empty input, or fallback answers.
- Preserve the existing answer text unless citation formatting is explicitly
  added to the program.

## Example 1: Single office

### User

Where is the training office?

### Current program response

Training Office: room I.101, open Mon-Fri 07:30-16:30.

### Citation mockup
```text
┌─────────────────────────────────────────┐
│ Training Office: room I.101, open       │
│ Mon-Fri 07:30-16:30.                    │
│                                         │
│ Source: Training Office                 │
│ Room: I.101                             │
│ Hours: Mon-Fri 07:30-16:30              │
└─────────────────────────────────────────┘
```
The source details correspond to the CSV row matched by `reply()`.

## Example 2: Another office

### User

When does the library open?

### Current program response

Library: room B.201, open Mon-Sat 07:00-20:00.

### Citation mockup
```text
┌─────────────────────────────────────────┐
│ Library: room B.201, open               │
│ Mon-Sat 07:00-20:00.                    │
│                                         │
│ Source: Library                         │
│ Room: B.201                             │
│ Hours: Mon-Sat 07:00-20:00              │
└─────────────────────────────────────────┘
```
The citation identifies the matched Library record. The program does not
currently distinguish opening time from closing time; it returns the
complete hours string from the CSV.

## Behavior and limitations

The current implementation:

- Loads records from `offices.csv`.
- Matches an office name against the normalized user message.
- Returns the matched record's name, room, and hours.
- Returns fixed greeting or fallback messages for other inputs.

It does not currently return citation IDs, source metadata, HTML, or
structured objects.
