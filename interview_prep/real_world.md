# Real-World Implementation

Senior developers are judged on how they handle common but complex production scenarios.

## 1. Authentication & Token Refresh
- **Scenario:** The user's access token expired. How do you handle it without logging them out?
- **Solution:** Use an **Interceptor** (e.g., in `Dio`).
  - Capture the 401 response.
  - Pause the request queue.
  - Call the refresh token endpoint.
  - If successful, update the token and retry the original request.

## 2. Pagination (Infinite Scroll)
- **Problem:** Loading 1000 items at once causes jank and high memory usage.
- **Solution:** 
  - Use `ListView.builder`.
  - Maintain a `page` number or `cursor`.
  - Listen to a `ScrollController`. When `extentAfter < 200`, fetch the next page.
  - Use a "Loading" indicator at the bottom.

## 3. Offline First & Syncing
- **Local Storage:** `sqflite` (Complex), `hive` (Fast), `isar` (Modern/Fast), `shared_preferences` (Simple config).
- **Strategy:** 
  1. Fetch from local first.
  2. Fetch from remote in background.
  3. Update local and UI.

## 4. Error Handling
- Use **Functional Error Handling** (e.g., `Either<Failure, Success>` from the `dartz` or `fpdart` package).
- Avoid throwing exceptions for business errors (e.g., UserNotFound).
- Use `try-catch` only for external system failures (e.g., SocketException).

## 5. Environment Config
- Use **Flavors** (Dev, Staging, Prod).
- Use `--dart-define` to inject variables at compile time.

---
**Next Sitting Recommendation:** [Soft Skills & Strategy](./soft_skills.md) to master the psychology of senior-level interviews.
