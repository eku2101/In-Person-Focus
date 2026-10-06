# In-Person Focus

A self-contained conceptual prototype exploring whether selective notification filtering can help people stay present in a conversation while allowing important communication through. It does not recreate or control Apple's Focus system.

## Project guide

The starting observation is that repeatedly checking a phone during an in-person conversation can seem to interrupt its momentum and leave the other person less engaged. This project turns that observation into an interactive model that invites exploration rather than claiming to prove an effect.

- **README.md** (this document): project overview, instructions, and implementation guide.
- **[Design.md](Design.md)**: the question, design decisions, and how the phenomenon is represented in code.
- **[Learningnotes.md](Learningnotes.md)**: documented revisions, the role of AI assistance, limitations, and questions for further reflection.
- **[ConversationRecord.md](ConversationRecord.md)**: an edited chronological record of project conversations and approved changes, not a verbatim chat export.

## Latest improvements — October 6, 2026

The creator reviewed and approved these refinements before implementation:

- **Compare the same notifications:** see Focus off and Focus on results using the same four messages and current settings.
- **Keep consequences visible:** test controls sit beside the conversation indicators and notification results; the indicators stay visible while scrolling results when screen height allows.
- **Clarify blocking:** **BLOCKED · Held for later** explains that postponed messages are not deleted.
- **Separate interruption from response:** attention totals distinguish alert delivery, deliberately opening messages, and reconnecting.
- **Reflect on one real-world choice:** a brief question asks which notifications the user would let wait during their next conversation.
- **Keep personalization secondary:** profile pictures remain optional in a collapsed section.

These changes support the project's essential sequence: notification → priority decision → response → possible conversation effect. They encourage awareness and experimentation, not a claim of proven habit change. The design discussion and adjustments are preserved in the linked project documents.

For a quick demonstration, reset the app, leave Focus off, and send two TikTok notifications. Attention falls from 100% to 70%, and mood becomes Distracted. Reset again, turn Focus on with TikTok blocked, and send the same two notifications: attention remains at 100% and mood stays Positive. Then send a message from selected contact Mom: it is allowed, and attention falls to 95%. These outcomes follow the programmed rules; they are not experimental evidence about real conversations.

## Open and explore

Double-click `index.html` to open it in a modern browser. No installation, internet connection, build step, or server is required.

1. Choose important contacts and blocked notification categories. These controls work even when Focus is off.
2. Turn on **In-Person Focus Mode** to apply your choices.
3. Select a fictional notification and click **Send test**.
4. Read its **ALLOWED / BLOCKED** result and watch Attention and Conversation Mood.
5. Open or dismiss a message, try other settings, or take a moment to reconnect.
6. Click **Compare Focus off and on** to explore the same four notifications in a separate comparison.
7. Write one intention under **Which notifications would you let wait?** Copy it into your own notes if you want to keep it.

Turning Focus off releases waiting messages as one batch. **Reset demo** restores initial settings, 100% attention, Positive mood, and clears messages, profile pictures, comparison results, and the reflection field.

## How filtering works

| Incoming message                | Focus on       | Focus off |
| ------------------------------- | -------------- | --------- |
| Emergency                       | Always allowed | Allowed   |
| Selected contact                | Allowed        | Allowed   |
| Unselected contact              | Blocked        | Allowed   |
| Checked low-priority category   | Blocked        | Allowed   |
| Unchecked low-priority category | Allowed        | Allowed   |

BLOCKED means held quietly under **Held for later**, not deleted. Changing settings affects new arrivals. You can deliberately open a held message, which costs attention. Emergency status is part of the fictional sample data; the app does not detect real emergencies.

## Understand and edit the code

The application uses only these three files:

- **index.html** — page structure, contact/category controls, and simulated phone. Edit labels and explanatory text here.
- **styles.css** — colors, spacing, responsive layouts, and notification styles. Shared colors are defined in `:root` at the beginning.
- **app.js** — sample messages, session variables, filtering, rendering, and event handlers, with comments marking the main sections.

Useful starting points in `app.js`:

- `messages`: change fictional senders and notification text.
- `active`, `selected`, `blockedTypes`: Focus and filter settings.
- `attention`, `conversationMood`: current conversation state.
- `decision()`: determines whether an incoming notification is allowed.
- `changeAttention()`: clamps attention to 0–100 and derives the mood.
- `render()`: updates the UI from the variables.
- The `send` event handler: applies an interruption cost and routes the message.
- `interact()`: handles opening and dismissing a message.

## Conversation assumptions

These are design assumptions for exploration, not scientific measurements of feelings:

- Start at 100% attention and Positive mood.
- An allowed low-priority notification costs 15 attention points.
- An allowed contact or emergency message costs 5 points.
- A blocked notification costs no points and preserves the current mood.
- Opening a message costs 5 additional points, once per message.
- Dismissing a message costs nothing.
- Releasing a waiting batch when Focus ends costs 5 points total.
- Reconnecting restores up to 10 points.
- Mood is Positive at 80–100, Distracted at 50–79, and Disconnected below 50.

Blocking prevents further loss; it does not automatically restore attention. The interface also explains these rules under **How the simulation works**.

## Pictures and privacy

**Optional: personalize profile pictures** lets you choose a PNG, JPG, or WebP up to 5 MB per contact. The picture updates that contact's card and existing/future notifications in this tab. This is local visual syncing, not integration with real contacts or accounts.

Messages, settings, attention, and pictures stay in JavaScript memory. There is no database, login, external API, backend, analytics, or stored simulation data. A welcome explanation appears on every page load before you enter the prototype. No localStorage is used. Pictures are local object URLs, never uploaded. Reloading or resetting clears the session. No external fonts, scripts, or images are required.

## Optional developer checks

`test.cjs` contains regression checks. If Node.js is already installed, run `node test.cjs`. This file is not loaded by the application and Node.js is not needed to use the prototype.

## Compare, notice, and reflect

The **What changes with Focus?** comparison runs TikTok, Mom, Instagram, and an emergency through the same filter twice: Focus off and Focus on. Both start at 100%, use your current settings, and contain no opening actions. With default settings the results are 60% / Distracted and 90% / Positive. Changing settings marks existing results as outdated until you compare again. This separate exercise does not alter your live messages or attention score.

Live indicators distinguish attention used by alert delivery from attention used by opening messages. The totals account for clamping at 0 and 100. **BLOCKED · Held for later** means a message is postponed, not deleted. Optional profile pictures stay collapsed by default. A reflection field asks which notifications you would let wait in your next conversation; it stays in this tab only and is cleared by Reset demo or reload.

See [ConversationRecord.md](ConversationRecord.md) for the chronological project discussion record, including decomposition, repeated patterns, abstraction, and the approved changes. It is an edited record of the available conversation, not a verbatim platform export.
