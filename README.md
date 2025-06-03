# 🖱️ Mouse: Local Visualizable Task Management for Cursor

## 🤔 What is Mouse?

Mouse is my take on bringing structured, visual task management right into the [Cursor AI IDE](https://cursor.sh/). It's a project ruleset I've designed to work hand-in-hand with a simple, standalone HTML file for visualizing everything. My goal here is to create a clear, manageable way for you and Cursor's AI to tackle complex tasks together. With Mouse, tasks get broken down, executed with precision, meticulously logged, and are easy to see and understand, all locally on your machine.

The core idea is simple: you need a **Mouse** to give **Cursor** precise direction. This project is my attempt to provide that "Mouse."

![mouse.gif](/assets/mouse.gif)

## 💡 Why Mouse? The Journey and Motivation

This project has been a bit of a journey for me. My first adventure into enhancing AI-assisted development was **[Rooroo](https://github.com/marv1nnnnn/rooroo)**, which, to my delight, became a pretty popular custom modeset for **[Roo code](https://roocode.com/)**.

I genuinely love Roo Code, especially its ability to juggle multiple modes, break down big tasks into smaller, manageable ones, and prompt for key decisions. However, the cost can be a factor, which led me to create Rooroo. I wanted to build a custom modeset that was super **token-efficient** and **unambiguous**, allowing even less powerful models with smaller context windows to achieve comparable results.

But **Cursor** plays by different rules with its pricing model. Suddenly, I didn't have to be so conservative with context length, meaning I could afford to be more descriptive and detailed. Plus, with the ability to use powerful models like **Gemini 2.5 Pro** via the slow pool, I could design with the assumption that top-tier AI is available.

Another game-changer for me was **Cursor's own apply diff model**. It's incredibly efficient for editing large files, much more so than other tools I've used.

So, my approach shifted. I wanted to build a framework specifically for **Cursor** that would maximize its benefits – a system where everything is **clearly logged**, following a task management pattern similar to what I found effective with Rooroo.

When I looked at existing task management tools, I found many were either a hassle to set up (often requiring custom modes or MCPs), or they were overly complex with a daunting number of features. And a lot of them lacked a simple, clear way to visualize progress.

I have this philosophy of starting simple: a **single file** is better than **multiple local files**, which is better than **local files with dependencies**, which is better than **cloud solutions**. That's what led me to create this mouse setup.

## Why is 🖱️ Mouse special?

I believe Mouse stands out because:

- **It's refreshingly simple to get going.** The visualization? Just a single HTML file (`mouse_dashboard.html`). You can open it directly in your browser or serve it with a basic HTTP server. No complicated dependencies or setup hoops to jump through.
- **The protocol is thoughtfully crafted.** I've poured a lot of thought into it, drawing inspiration from other robust prompting and task management approaches. The aim is clarity and effectiveness.
- **Everything is meticulously logged.** This makes it easy to pick up where you left off, recover from interruptions, and always have a clear audit trail of what the AI is doing.


## 🚀 Getting Started

Ready to give Mouse a try? Here's how you can get set up:

1.  **Clone the repo, or download it as a zip.** Get the files onto your local machine in whatever way you prefer.
2.  **(Optional) Check out the demo results.** This can give you a feel for how things look:
    1.  Open `mouse_dashboard.html` in your browser and upload the `.mouse` folder (from the demo or your own initial tasks) to visualize the workflow.
    2.  Alternatively, you can serve the HTML file locally. A simple way is to navigate to the directory in your terminal and run `python -m http.server` (if you have Python) or `npx http-server` (if you have Node.js/npm), then open the provided URL (usually `http://localhost:8000` or similar) in your browser.
3.  **Copy the `.cursor/rules` folder into your project's root directory.** This is where the core **Mouse protocol** and any custom project standards live, guiding the AI.
4.  **(Optional but Recommended) Copy `mouse_dashboard.html` to your project's root directory.** This makes it super easy to access the visualization for your own tasks.
5.  **You should be all set!** The AI should now be able to follow the **Mouse protocol**. If you find the model isn't quite following the rules as expected, you can gently remind it by referencing a specific rule file (e.g., by typing `@core_protocol.mouse.mdc` in the chat). This helps steer it back on course.
![cursor_use.jpg](/assets/cursor_use.jpg)

## ⚙️ How It Works (High-Level)

Want a clearer picture of how Mouse helps us collaborate? Here's a visual overview using a simple text-based diagram, followed by a breakdown:

```text
[ User Initiates Task/Goal ]
          |
          V
+---------------------------------------------------+
| Agent (Cursor AI using Mouse Protocol)            |
|---------------------------------------------------|
| Key Guiding Principles:                           |
|   - Clarity First (Ask if unsure)                 |
|   - Log Everything Actionable                     |
|   - Protect User Data                             |
|   - Follow Task Lifecycles (Pending -> Done)      |
|   - Apply Relevant Standards                      |
+---------------------------------------------------+
          |
          V
[ 1. Task Formalization & Planning ]
          |
          |--- IF SIMPLE (S/M Effort) ---> [ Task File Created: `.mouse/tasks/TASK_ID.md` ]
          |                                    (Contains: ID, Title, Status, Description, Deliverables)
          |                                    (Direct logging of steps in `HistoryLog`)
          |
          |--- IF COMPLEX (L/X Effort) --> [ Task File & Plan File Created ]
                                             [ `.mouse/tasks/TASK_ID.md` ]
                                             [ `.mouse/plans/TASK_ID_plan.md` ]
                                               (Plan includes `SubTasks`, each with:
                                                Objective, Status, `ExecutionLog`, `FinalOutputSummary`)
          |
          V
[ 2. Execution & Meticulous Logging ]
          |
          +--> [ Agent works on Task / SubTasks ]
          |      (All significant actions, file operations, tool use,
          |       and state changes are logged in the relevant
          |       `Task.HistoryLog` or `SubTask.ExecutionLog`)
          |
          V
[ 3. Local File System is the Source of Truth ]
          |
          +--> [ `.mouse/` directory stores all task & plan Markdown files ]
          |
          V
[ 4. Visualization (Optional) ]
          |
          +--> [ `mouse_dashboard.html` reads the `.mouse/` folder to display progress ]
```

Let's break down what this flow means for our work together:

1.  **You Set the Strategy:** As the **User**, you define the tasks, outline the high-level goals, and provide any necessary clarifications along the way. This is your vision, and I'm here to help execute it.

2.  **Mouse Protocol in Action (The Core Loop):** This is where the **Mouse Protocol** truly guides my actions as the AI agent:
    *   **Task Initiation & Formalization:** When you give me a task, especially one that might involve code or file changes, or is generally complex, I don't just start working. First, I formalize it by creating a **Task file** (e.g., `.mouse/tasks/MOUSE#TASK_0001.md`), as per **Protocol Section 4.2**. This file is the heart of the task and contains:
        *   **Key Info (YAML Frontmatter):** This structured section includes the unique `TaskID` (I generate this sequentially using the method in **Protocol Sec 2.2** to avoid overwriting existing tasks!), a clear `Title`, a `Description` explaining the *what* and *why*, the current `Status` (like `Pending`, `Ready`, `InProgress`, `Done` – you can see the full lifecycle in **Protocol Sec 2.4**), defined `Deliverables`, and more.
        *   **The `HistoryLog`:** This is a critical, step-by-step diary of the task's entire journey, from its creation to its completion. It tracks all state changes. For simpler tasks (**S/M effort** where no separate plan is needed), my actual work steps are logged directly here too (**Protocol Sec 2.3, 3.1**).
    *   **Planning for Complexity (L/X Effort Tasks):** If we're tackling a bigger job – what the protocol calls **`L` (Large)** or **`X` (Extra Large)** effort, or sometimes even a multi-faceted **`M` (Medium)** task – I don't just dive in (**Protocol Sec 3.1**).
        *   Instead, I create a dedicated **`PlanFile`** (e.g., `.mouse/plans/MOUSE#TASK_0001_plan.md`). This plan details my strategy and, crucially, breaks the main task into smaller, more manageable `SubTasks` (**Protocol Sec 3.2**).
        *   Each `SubTask` within the plan has its own `Objective`, its own `Status`, and its own detailed `ExecutionLog`. This log is where I record every step I take for *that specific piece* of the puzzle.
    *   **Execution & Detailed Logging:** This is where one of my core directives, "**Log Everything Actionable**" (**Core Directive #2**), really comes into play.
        *   Whether I'm working on a simple task (logging to the `Task.HistoryLog`) or a `SubTask` from a plan (logging to its dedicated `SubTask.ExecutionLog`), I record all significant actions. This includes any file changes (creations, edits, deletions – as detailed in **Protocol Sec 7.5**), any tools I use, and the decisions I make along the way.
        *   When a `SubTask` concludes (successfully or not), I meticulously fill in its `FinalOutputSummary`. This details what happened, what (if anything) was produced, any errors encountered, and any key observations. This summary is vital and actually drives the update of the `SubTask`'s `Status` in the plan file (**Protocol Sec 3.3 and 3.3.1**).
        *   **Constant Communication (Clarity First!):** If I'm ever unsure about any part of an instruction, a file path, or how a specific standard should be applied, the **Mouse Protocol** *requires* me to ask you for clarification (**Core Directive #1, Protocol Sec 5.2**). I won't guess, because accuracy is paramount.

3.  **Your Local File System is the Single Source of Truth:** All the important stuff – task details, plans, and logs – lives right there in local Markdown files inside your project's `.mouse` directory (as specified in **Protocol Sec 2.1 and 3.2**). This means no cloud dependencies for the core logic, giving you full control and transparency.

4.  **The Dashboard Brings it to Life:** The `mouse_dashboard.html` file is a simple but effective way to see what's going on. It reads those local `.mouse` files and gives you a visual overview of your project: the status of different tasks, how they might be connected, and the overall flow of execution.

## 📁 Project Structure

When you use Mouse, your project will typically have the following key directories and files, which are central to how the protocol operates:
![structure.jpg](/assets/structure.jpg)
*   **`mouse_dashboard.html`**: (Optional, but recommended in project root) The single HTML file for visualizing task progress.
*   **`.mouse/`**: This is the heart of Mouse's operational data.
    *   **`tasks/`**: Contains all individual Task files (e.g., `MOUSE#TASK_0001.md`). Each file details a specific task's metadata, description, and its complete history log.
    *   **`plans/`**: For complex tasks (L/X effort), this directory holds the corresponding Plan files (e.g., `MOUSE#TASK_0001_plan.md`). These files break down tasks into `SubTasks`, each with its own objective, status, and execution log.
*   **`.cursor/rules/`**: (Essential for guiding the AI) This directory, copied into your project root, contains:
    *   The core **Mouse Protocol** files (e.g., `core_protocol.mouse.mdc`).
    *   Any project-specific **standards** and **conventions** (e.g., `coding_standards.mouse.mdc`, `documentation_standards.mouse.mdc`) that the AI uses to ensure consistency and quality.

## 🔮 Future Potential

I'm excited about how Mouse could grow and work even more closely with some of **Cursor's** neat features, like:

*   **Cursor's Background Task System:** The clear, structured way Mouse handles tasks seems like a natural fit for **Cursor's background execution capabilities**. This could open doors for more autonomous, long-running operations that I can manage for you.
*   **Cursor's Custom Modes:** It would be fantastic to wrap Mouse up into a dedicated **Cursor custom mode**. Right now, automating that setup isn't quite there, but if Cursor adds support for defining custom modes via a JSON file or similar, the experience could become even smoother!

## Known issues

Like any project, Mouse isn't perfect, and there are a couple of things I'm still figuring out or that you might run into:

- **ID Generation Challenges:** Because Cursor model don't have a direct sense of real-time or a persistent memory of *all* past IDs in the same way a dedicated server might, generating truly unique sequential IDs can sometimes be tricky. There's a small chance IDs might occasionally overlap if many tasks are created rapidly or across different sessions without perfect synchronization.
- **Following the Protocol Perfectly:** While strive to follow the **Mouse Protocol** to the letter, different AI models (like **Gemini**, which tends to be quite good with this, or **Claude**) can also have slightly different adherence levels. Add "`@core_protocol.mouse.mdc` in the conversation will significantly improve adherence to the protocol.

---

## License

This project is available under the **MIT License**. See the `LICENSE` file for details.