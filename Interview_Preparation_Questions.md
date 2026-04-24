# Interview Preparation: Architectural & Resume-Based Questions

This document contains specialized interview questions based on the specific technologies, architectural patterns, and professional experiences detailed in your resume. These questions focus on high-level decision-making, trade-offs, and engineering impact.

---

## 1. Architecture & Monorepo Management (Tiger Analytics)
*   **The Turborepo Pipeline:** "You architected a Turborepo for 3+ enterprise apps. How did you structure your `turbo.json` to handle shared dependencies vs. app-specific builds? How did you prevent 'cache poisoning' when environment variables changed across different business units?"
*   **Remote Caching Strategy:** "In a team environment, local caching only goes so far. Did you implement Remote Caching? If so, how did it impact your CI/CD bill and developer velocity?"
*   **The `turbo prune` Workflow:** "How did you optimize your Docker multi-stage builds using `turbo prune`? What was the reduction in image size or build time?"
*   **Internal vs. External Packages:** "When designing the centralized UI library, how did you decide between transpiling shared packages 'just-in-time' versus pre-bundling them before consumption?"

## 2. High-Scale Ecosystems (GCash Integration)
*   **Dual-Thread Limitations:** "The GCash environment (based on the Alipay/Mini Program framework) uses a dual-thread architecture (Logic vs. View). How did your React plugins handle the 'bridge' latency when performing high-frequency UI updates?"
*   **Bundle Size Optimization:** "GCash has strict package size limits (often ~2MB). What specific techniques beyond standard code-splitting did you use to ensure your high-performance plugins stayed within these limits?"
*   **Non-Browser Constraints:** "Since the GCash container isn't a standard browser (no direct DOM access), how did you adapt standard React libraries that rely on `window` or `document` objects?"
*   **JSAPI Integration:** "How did you abstract the GCash-specific JSAPIs (like `my.tradePay` or `my.getStorage`) into your React plugin architecture to make it testable in a standard web environment?"

## 3. Performance Engineering & Frontend (Ergobite / Tiger)
*   **Lazy Loading at Scale:** "You implemented lazy loading for production apps. How did you handle 'cumulative layout shift' (CLS) issues when loading heavy UI components asynchronously?"
*   **Modular UI Consistency:** "When building the centralized UI library, how did you handle **versioning**? If a core component in the library had a breaking change, how did you ensure 3+ enterprise apps didn't break simultaneously?"
*   **Runtime Performance:** "In the GCash project, you mentioned 'runtime performance optimization.' Can you walk me through a specific profile you did using Chrome DevTools or the Mini Program Studio that led to a significant FPS improvement?"

## 4. Backend & Scalability (Hashtag Systems / Ergobite)
*   **Sub-200ms Latency:** "You achieved sub-200ms latency on a high-concurrency medical platform. Beyond indexing, what application-level caching or MySQL query plan optimizations were critical to hitting this target?"
*   **OOP in Node.js:** "You mentioned using OOP principles for Node.js REST APIs. Why did you choose OOP over a functional/middleware-heavy approach? How did you handle Dependency Injection or Service layers?"
*   **Real-time Notification Engine:** "For the Socket.IO engine, how did you handle horizontal scaling? If you had multiple Node.js instances, how did you ensure a user connected to Instance A received a message emitted from Instance B?"
*   **Database Scaling:** "When optimizing MySQL schemas for high concurrency, did you face any issues with **lock contention**? How did you resolve them?"

## 5. Offline-First & Mobile (Mars WMS Project)
*   **Data Integrity:** "In a warehouse (WMS) environment, a worker might pick items while offline. How did you handle **conflict resolution** if two workers picked the same 'last item' from a bin while both were offline?"
*   **Delta Synchronization:** "Instead of syncing the whole database, how did you implement 'Delta Sync'? What was the logic for tracking versioning or timestamps between the React Native client and the server?"
*   **Local Storage Choice:** "Why did you choose your specific local database (e.g., SQLite, WatermelonDB, or Realm) for the Mars WMS? How did it handle the performance of 10,000+ SKU lookups locally?"

## 6. Leadership & Impact
*   **The PMS/THC Architecting:** "When mentoring junior devs to build the Performance Management System, what was the biggest architectural mistake they made that you had to correct? Why was that correction necessary for long-term maintainability?"
*   **Developer Velocity:** "You claim to have improved developer velocity via CI/CD. What were the specific 'before and after' metrics? (e.g., Build time from 20m to 5m, or Deployment frequency from weekly to daily)."
