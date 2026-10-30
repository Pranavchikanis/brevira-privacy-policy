# Privacy Policy for Brevira — Article Summarizer

**Effective Date:** October 30, 2026  
**Document Status:** Release Policy for Chrome Web Store Version 0.1.2  
**Extension Version:** 0.1.2  
**Contact:** brevira.support@gmail.com  
**Hosting URL:** https://pranavchikanis.github.io/brevira-privacy-policy/  
**Repository:** https://github.com/Pranavchikanis/brevira-privacy-policy  

---

> [!NOTE]  
> **Summary for Readers:** Brevira is an on-device reading assistant. When you choose to summarize a web article, the extension extracts the article text and processes it entirely on your computer using Chrome's built-in artificial intelligence (Gemini Nano). Brevira does not transmit your articles, summaries, URLs, or browsing history to external servers, third-party AI clouds, or analytics providers. When you intentionally use optional external actions (such as sharing the extension link, sending feedback via email, or joining our community Discord), those actions are initiated solely by you and transmit only the standard information needed for those external communications.

---

## 1. Scope and Purpose

This Privacy Policy explains how the **Brevira — Article Summarizer** Chrome browser extension ("Brevira", "the extension", "we", "us") handles information when you install and use the extension.

Brevira is designed to help you read and digest long-form web articles (such as news reports, essays, blog posts, and research papers) by generating structured key-point summaries within Google Chrome's native Side Panel.

This policy applies strictly to the Brevira browser extension. It does not apply to third-party websites you visit, nor does it govern Google Chrome's underlying browser operations or third-party platforms (such as your email provider or Discord).

---

## 2. Information Accessed and Processed

Brevira only accesses webpage content when you explicitly initiate an action (by clicking the Brevira toolbar icon or clicking the "Summarize Article" button in the side panel).

When invoked, the extension accesses and processes the following information locally from the active browser tab:

- **Article Content:** The primary narrative text of the webpage, isolated from peripheral website elements such as advertisements, navigation menus, sidebars, and comments.
- **Article Metadata:**
  - The document or article title.
  - The author byline (if provided in the webpage markup).
  - The article excerpt or description (if provided).
  - The webpage URL and domain name (used strictly to associate summaries with the corresponding tab and display the source website).
- **Processing Metrics:** Operational diagnostics calculated locally in your browser, including character count, substantive heading count, section sampling mode, time-to-first-token, session creation duration, inference duration, and total processing duration. These metrics exist only in volatile memory and developer console output.
- **Voluntarily Submitted Information:** If you choose to contact the developer using the "Send Feedback" feature, you voluntarily transmit your email address and any text or contact details you choose to include in your message through your personal email client.

Brevira does **not** access your browsing history, bookmarks, passwords, form entries, cookies, personal account details, or content from tabs where you have not clicked the Brevira icon.

---

## 3. How Information Is Used

The information accessed by Brevira is used strictly to provide the core functionality you request:

1. **Extraction:** Determining whether a readable article exists on the active page and filtering out boilerplate elements.
2. **Context Adaptation:** Selecting an appropriate summary depth (short, medium, or long) based on the article's length and structural complexity.
3. **Summarization:** Feeding the extracted text into Chrome's local AI model to generate concise, bulleted key points.
4. **Display & Navigation:** Presenting the structured summary, article metadata, and source preview inside Chrome's Side Panel alongside your active tab, and allowing you to toggle between the summary and extracted source view.
5. **Support Communications:** If you send an email to `brevira.support@gmail.com`, your message is used solely to respond to your inquiry, troubleshoot reported bugs, or evaluate product suggestions.

We do not use your information for advertising, profiling, user tracking, marketing, automated decision-making, or any purpose unrelated to generating on-device summaries and supporting the extension.

---

## 4. Local On-Device Processing

Brevira is built around an on-device architecture. All content extraction and AI inference occur locally on your physical machine:

- **Content Extraction:** The webpage document is cloned locally in memory and parsed using Mozilla's open-source Readability library (`@mozilla/readability`). The live webpage DOM is never mutated or modified.
- **Content Truncation & Proportional Sampling:** To protect system stability and fit within local AI context limits (maximum 20,000 characters), long articles are sampled across major headings (`<h2>`, `<h3>`, `<h4>`) so that lead sections, core arguments, and conclusions are represented without sending data off-device.
- **AI Inference:** Summaries are generated using Google Chrome's native on-device Summarizer API (powered by Gemini Nano). The AI model runs locally on supported hardware without routing requests to external inference servers.
- **Sanitization:** Generated summaries and interface copy are converted from Markdown to HTML and sanitized locally using DOMPurify (`dompurify`) to ensure safe rendering in the side panel.

No external cloud large language models (such as OpenAI, Anthropic, or remote Google cloud APIs) are connected to or used by Brevira.

---

## 5. Storage and Data Retention

Brevira is designed with a minimal, ephemeral data footprint. It does **not** maintain a persistent history database, and it does not store your reading history across browser restarts.

The extension uses only temporary, session-scoped memory:

- **In-Memory Cache:** While the Brevira side panel remains open, active summaries and extracted article structures are kept in volatile JavaScript memory (`Map` objects) so you can switch between tabs without losing progress.
- **Session Storage (`sessionStorage`):** Completed summaries are stored temporarily in browser session storage keyed by Chrome tab ID (`brevira_summary_[tabId]`). This allows Brevira to restore your summary if you switch to another tab and return during the same session.
- **Data Lifecycle & Cleanup:**
  - **Background Worker Cleanup:** When a tab is closed in Chrome, the background service worker listens to `chrome.tabs.onRemoved` and immediately purges that tab's authorization record and in-memory summary cache.
  - **Tab Summary Removal:** When you click "Summarize Another" or trigger a fresh generation on an article, the previous summary for that tab is removed from both in-memory storage and `sessionStorage`.
  - **Preservation of Extracted Context:** Clicking "Summarize Another" or using "Back to Summary" intentionally retains the extracted article text in volatile memory so you can inspect source text or re-summarize without repeating extraction.
  - **Session Storage Lifecycle:** Closing the side panel unloads the side panel UI document from memory. In Chromium, `sessionStorage` for an extension page may persist across side-panel openings during the same browser session. Brevira does not guarantee an exact browser-level cleanup time for temporary session storage, though stored summaries are cleared when explicitly removed (such as when re-summarizing) and are not intended to survive browser restarts.
  - **Zero Persistent Storage:** Brevira does **not** declare or use permanent storage permissions (`chrome.storage.local`, `chrome.storage.sync`, `chrome.storage.session`, IndexedDB, or browser cookies).
- **Support Email Storage and Retention:** When users voluntarily send feedback to `brevira.support@gmail.com`, the developer receives their email address and message through the configured email service, Gmail. Support emails are retained in the Gmail account until the developer manually deletes them. They are not automatically deleted when an issue is resolved. Google, as the email service provider, handles email storage and deletion according to its applicable policies. These messages are used to respond to inquiries, investigate reported issues, and consider product suggestions. They are not used for advertising, profiling, or marketing campaigns.

---

## 6. Sharing, External Links, and Network Activity

### What Brevira Does Not Transmit
- **Zero Cloud AI Inference:** Brevira never sends extracted article text or generated summaries to external servers or cloud AI providers.
- **Zero Telemetry or Analytics:** Brevira contains no tracking pixels, analytics SDKs, telemetry beacons, crash reporting libraries, or advertising networks.
- **No Data Monetization:** We do not sell, rent, monetize, or trade your data with third parties.

### User-Initiated External Actions
Brevira includes user-facing convenience actions that interact with external services only upon your explicit instruction:

1. **Share Brevira:**
   - Clicking "Share Brevira" opens the browser's native Web Share API dialog, or copies the extension's official public listing URL to your clipboard if native sharing is unavailable.
   - The share payload is strictly limited to public product information:
     - **Title:** `Brevira — Article Summarizer`
     - **Text:** `Extract and summarize long-form web articles using on-device AI in Chrome's side panel.`
     - **URL:** `https://chromewebstore.google.com/detail/phhpkeahklglmdjigdcllgopkbkbolno`
   - Brevira **never** includes the article title, webpage content, summary text, browsing history, or your personal information in the share payload.

2. **Send Feedback:**
   - Clicking "Send Feedback" allows you to select one of three categories: *Report a Bug*, *Suggest a Feature*, or *Share Your Experience*.
   - Selecting a category generates an editable email draft using a standard `mailto:` link addressed to `brevira.support@gmail.com` with a prefilled subject line (e.g., `Brevira — Bug Report`) and a structural starter template.
   - **User-Controlled Transmission:** Brevira does not send the email automatically. The extension opens your default desktop or web email client. You have full control over whether to send the email, what email account to use, and what information to write.
   - **No Automated Data Attachment:** Brevira does not automatically attach article text, generated summaries, active tab URLs, browsing history, or diagnostic system identifiers to the email.
   - A "Copy Support Email" fallback is provided for users without a configured default mail client.

3. **Join Brevira Community:**
   - Clicking "Join Community" opens the official Brevira Discord server invitation (`https://discord.gg/86yTYQw3X3`) in a new browser tab.
   - Discord is an independent third-party service governed by its own Terms of Service and Privacy Policy. Brevira does not transmit any user data, article content, or summaries to Discord.

### Distinction from Google Chrome Browser Services
While Brevira's extension code makes no background network requests, it operates inside Google Chrome. Standard browser-level network traffic may occur independently:
- **AI Model Download:** If Chrome's on-device AI model (Gemini Nano) has not yet been downloaded, Chrome downloads the model components directly from Google update servers. This download is managed entirely by Google Chrome's background updater; Brevira only monitors download percentage events to update its UI progress bar.
- **Browser Services:** Google Chrome communicates with Google servers according to your general Chrome settings (e.g. extension safety checks, browser updates, and Google account sync). Brevira has no access to or control over Chrome's browser-level telemetry.

---

## 7. AI Model Download and System Requirements

Brevira relies on Chrome's built-in on-device AI capabilities. 

- **First-Time Setup:** If Chrome's on-device AI model (Gemini Nano) is not already present on your computer, Chrome must download the model components from Google's update servers before Brevira can generate summaries.
- **Storage Requirement:** The initial model setup requires an active internet connection and sufficient local disk storage (Chrome requires at least 22 GB of free space on the volume hosting your Chrome profile to install the model).
- **Chrome-Managed Download:** The download is initiated via Chrome's native Summarizer API and handled entirely by Google Chrome. Brevira does not host, distribute, or download the model binary directly.
- **Subsequent Operation:** Once installed by Chrome, summarization runs 100% locally on your hardware.

---

## 8. Extension Permissions and Justifications

In compliance with the Chrome Web Store policy of permission minimization, Brevira requests only three scoped permissions:

| Permission | Technical Purpose | Plain Language Justification |
| :--- | :--- | :--- |
| **`activeTab`** | Grants temporary host access to the current active webpage only when you explicitly interact with Brevira. | Allows Brevira to read article text from the page you are currently viewing only after you click the toolbar icon. Brevira cannot see pages you do not actively summarize. |
| **`scripting`** | Allows dynamic script injection into the active document. | Used to inject the extraction script (`extract.js`) into the active webpage to identify article text and ignore navigation elements and advertisements. |
| **`sidePanel`** | Grants access to Chrome's native Side Panel API. | Allows Brevira to display the reading interface, model status, and generated summaries in a persistent panel alongside the webpage without cluttering the page itself. |

Brevira deliberately avoids broad host permissions (such as `<all_urls>` or `https://*/*`) and does not request background data storage, webRequest, or identity permissions.

---

## 9. Chrome Web Store User Data Policy & Limited Use Compliance

Brevira complies fully with the **Chrome Web Store User Data Policy**, including its **Limited Use** requirements:

1. **Permitted Use:** Brevira only uses information accessed from your browser to provide its primary user-facing feature: extracting and summarizing long-form articles in Chrome's side panel.
2. **No Data Transfers:** We do not transfer, transmit, or disclose user data to third parties, except when you explicitly initiate an external action (such as opening the Discord invitation or dispatching an email to our support address through your email client).
3. **No Advertising or Monetization:** We never use, sell, or transfer your webpage content, summaries, or metadata for advertising, retargeting, promotional campaigns, or credit assessment.
4. **No AI Model Training:** Your webpage content and generated summaries are processed strictly in volatile memory and are never used to train generalized artificial intelligence or machine learning models.

---

## 10. User Control and Choices

You maintain full control over your data and how the extension operates:

- **Explicit Activation:** Brevira never scans or extracts webpages automatically. Summarization only occurs when you click the extension icon or trigger an explicit action.
- **In-Progress Cancellation:** You can cancel an ongoing extraction, model download wait, or summary generation at any time by clicking the cancellation or reset buttons in the side panel.
- **Navigation Control:** You can use "View Source" to inspect the raw extracted article text and click "Back to Summary" to immediately return to your generated summary without triggering new processing.
- **Regenerating & Resetting:**
  - Clicking **"Summarize Another"** clears the generated summary for the active tab from memory and `sessionStorage` to allow a fresh summary to be created, while intentionally retaining the extracted article text in volatile memory.
  - Clicking **"Analyze New Tab"** resets the active tab's in-memory extraction and summary state.
  - Closing a browser tab prompts the background service worker to purge that tab's authorization and cache entries.
- **Disabling or Removing:** You can disable or uninstall Brevira at any time via Chrome's extension management page (`chrome://extensions`). Removing the extension deletes all extension code from your browser.

---

## 11. Changes to This Privacy Policy and Contact Information

### Policy Updates
We may update this Privacy Policy from time to time to reflect changes in our implementation, browser API standards, or legal requirements. When updates occur:
- The updated version will be committed to the project repository and published at the public hosting URL with a revised "Effective Date" at the top of this document.
- Users are encouraged to review this policy periodically to stay informed about how Brevira handles data.

### Developer & Contact Information
If you have questions, feedback, or concerns regarding this Privacy Policy or Brevira's data handling practices, please contact:

- **Developer / Publisher:** Pranav Chikanis
- **Support Email:** brevira.support@gmail.com
- **Project Repository / Issue Tracker:** https://github.com/Pranavchikanis/brevira-privacy-policy
- **Hosting URL:** https://pranavchikanis.github.io/brevira-privacy-policy/
- **Official Discord Community:** https://discord.gg/86yTYQw3X3
