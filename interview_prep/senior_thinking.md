# Senior Mindset & Problem Solving

At the senior level, the "How" is as important as the "What."

## 1. Project Structure at Scale
- **Feature-based:** `lib/src/features/auth/...`, `lib/src/features/profile/...`.
- **Modularization:** Breaking the app into local Dart packages to improve build times and separation.

## 2. Code Review & Quality
- **Lints:** Use `flutter_lints` or `very_good_analysis`.
- **Consistency:** Ensure the team follows the same architecture (e.g., Always use Repositories).
- **Questions to ask during CR:**
  - "Is this logic testable?"
  - "Is this widget rebuilding too often?"
  - "Can we simplify this control flow?"

## 3. Common Senior-Level Coding Challenges

### The "Scroll Jank" Problem
- **Scenario:** A list with heavy images and shadows is lagging.
- **Solution:** 
  - Wrap in `RepaintBoundary`.
  - Use smaller image resolutions (`cacheWidth`).
  - Check for expensive `saveLayer()` calls (e.g., Opacity, clipping).

### The "Logic" Problems (Dart)
- **Debouncing:** When a user types in a search bar, don't call the API on every keystroke. Wait 300ms.
- **Data Transformation:** Given a complex JSON, convert it into an Entity efficiently.

## 4. Interview "Red Flags" for Seniors
- Triggering side effects in `build()`.
- Not handling errors (assuming API always works).
- Using `GlobalKey` for everything.
- Not knowing why they chose a specific state management tool.

## 5. Final Preparation Tip: "The Good Answer"
Always answer with a **Scenario → Problem → Solution** structure.
- *Bad:* "I use Clean Architecture because it's clean."
- *Good:* "In my last project, we had 50+ screens. By using Clean Architecture, we were able to switch our database from SQLite to Hive in just 2 days without touching the UI code."

---
**Conclusion:** You are ready! Review [the main index](https://github.com/carbonanik/guideline/blob/master/interview_prep/README.md) for a final broad view.
