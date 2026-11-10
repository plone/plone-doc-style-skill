---
type: regex
pattern: '\b(ensures?|ensuring|leverages?|leveraging|utilizes?|utilizing|seamless(ly)?|robust(ly)?|comprehensive(ly)?|crucial(ly)?|delves?|delving|streamlines?|streamlining|simply|easily|trivial)\b'
flags: i
match: not_contains
target: { source: file, path: workflows-and-permissions.md }
---
