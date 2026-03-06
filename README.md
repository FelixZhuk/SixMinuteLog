# SixMinuteLog

SixMinuteLog is an offline-first legal time tracking and billing application designed to run entirely inside a web browser. The entire application is distributed as a single HTML file and does not require installation, servers, databases, frameworks, or external dependencies. All application logic, user interface components, styling, and storage management are contained inside this file, allowing the software to function independently of any backend infrastructure. Data persistence is handled locally using IndexedDB, enabling the application to operate without internet access while maintaining reliable long-term storage for time entries, client records, matters, invoices, and application settings.

The system is designed primarily for legal professionals that bill work using standardized time increments. Many law firms record billable work in six-minute increments, which correspond to one-tenth of an hour. SixMinuteLog implements this model directly in its time tracking logic and billing calculations. Attorneys and staff can log work, review entries, approve billable activity, and generate invoices entirely within the browser environment.

---

# Application Overview

SixMinuteLog functions as a lightweight browser-based practice management and billing environment. Once the HTML file is opened in a modern web browser, the full application interface loads immediately. Users can begin creating clients, defining matters, recording time entries, and generating billing records without performing any installation steps or connecting to a remote service.

All data created within the system remains stored locally in the browser’s IndexedDB storage layer. This allows the application to operate reliably in offline environments. The design also provides strong data privacy since information never leaves the user’s device unless it is intentionally exported.

Because the entire application is self-contained, SixMinuteLog can be distributed simply by sharing the HTML file. Opening the file in Chrome, Edge, Safari, or Firefox launches the full system.

---

# Time Tracking and Billing

The core functionality of SixMinuteLog centers on the recording and billing of professional time. Users can start and stop timers to track work as it happens or manually enter time records for work that was completed previously. Each entry stores contextual information including the client, associated matter, work description, hourly rate, and total hours worked.

Billing calculations follow the six-minute increment model used in many legal environments. Time is automatically rounded to tenths of an hour when required, ensuring that invoice totals correspond to common legal billing standards. Each entry calculates the billable amount based on the recorded hours and the applicable billing rate.

The interface allows users to review entries, update descriptions, modify hours, or correct client assignments before entries move forward in the billing workflow.

---

# Client and Matter Management

SixMinuteLog includes internal structures for organizing work by clients and matters. Clients represent organizations or individuals who receive legal services, while matters represent specific cases, projects, or engagements associated with a client.

Users can create client records, attach matters to those clients, and associate time entries with the appropriate matter. This structure allows invoices and reports to be grouped by client or case, making it easier to track revenue and workload distribution.

The system also supports contact records that can represent attorneys, billing staff, partners, or other participants involved in time entry creation and approval.

---

# Approval Workflow

The application includes a simplified approval model reflecting common law firm billing procedures. Time entries are initially recorded by the attorney or staff member who performed the work. Once the entry has been reviewed by the person who created it, it can be submitted for approval.

Partners or supervising attorneys can review submitted entries and determine whether they should be approved for billing or rejected for correction. Entries that are rejected can be revised and resubmitted. Billing staff can then generate invoices based on the set of entries that have been approved.

This workflow ensures that time records move through a controlled process before becoming billable items on an invoice.

---

# Invoicing

SixMinuteLog supports invoice generation using approved time entries. When invoices are created, the application aggregates all eligible entries for a given client or matter and calculates the total billable amount. Invoice records are stored locally and remain accessible for later review or export.

Although the application operates without a backend server, invoices can still be exported in structured formats for use in other accounting systems or record keeping.

---

# Data Storage and Portability

All application data is stored locally using IndexedDB. The database stores records for clients, matters, contacts, time entries, invoices, and application metadata. This storage model allows large datasets to be handled efficiently while preserving the offline-first design.

To prevent data loss and allow data migration, SixMinuteLog provides export and import tools. Users can generate JSON backups containing the entire dataset. These backups can later be restored by importing the file into another instance of the application. Data can also be exported to CSV format for use in spreadsheets or external billing systems.

Because the entire application exists as a single file, users can also export the current version of the application HTML alongside their data to maintain a complete portable copy of the system.

---

# Application Architecture

SixMinuteLog is implemented as a single page application embedded entirely within one HTML document. The document contains the full user interface markup, styling rules, and JavaScript logic required to operate the application.

Internally the system is structured into several logical layers. A global state layer manages application state and caches derived data such as timesheet summaries and analytics results. A custom rendering engine updates the interface by applying targeted DOM changes instead of re-rendering the entire page, which improves performance even when large datasets are present. The storage layer abstracts interactions with IndexedDB and manages data retrieval, indexing, and persistence.

The architecture avoids external frameworks in order to keep the system portable and self-contained.

---

# Performance Considerations

Although the application operates entirely within the browser, it includes several performance optimizations that allow it to scale to large datasets. Cached analytics results prevent unnecessary recalculation of revenue summaries. Indexed queries improve lookup performance when retrieving entries by client or date. Incremental DOM updates reduce the cost of interface rendering when users modify records or navigate between views.

These techniques allow the application to remain responsive even as thousands of time entries accumulate over time.

---

# Running the Application

Using SixMinuteLog requires no installation or configuration. Opening the HTML file in a modern web browser launches the full application interface. Because the application runs locally, internet connectivity is not required after the file has been downloaded.

---

# Backup and Restore

Since all data is stored locally, regular backups are recommended. Users can export a full JSON backup containing every record stored in the application. This backup file can later be imported into another instance of SixMinuteLog to restore the complete dataset. Maintaining periodic backups ensures that time entries, invoices, and client records can be recovered if a browser profile is reset or storage is cleared.

---

# Development Workflow Using Claude

SixMinuteLog was developed using **Claude Sonnet 4.6 with Extended Thinking** through the **Claude web interface (claude.ai)**. The project intentionally avoids traditional development environments, frameworks, and build systems. Instead, development occurs through structured iterations with Claude while preserving the application’s core design constraint: the entire system must remain a **single standalone HTML file that runs fully offline**.

This workflow allows the application to evolve safely while maintaining portability, modular structure, and reliable local data storage using IndexedDB.

The process described below reflects the exact workflow used during development and can be followed for future contributions.

---

## Claude Project Configuration

Before starting development work, it is recommended to create a **Claude Project** in the Claude interface. This ensures that architectural constraints are automatically applied to every development chat.

Inside the Claude Project settings, define the following **Project System Instruction**:

```
Keep the app fully offline without CDN or other dependencies.
Ensure there is no encoding corruption.
Keep the architecture modular and expandable.
Ensure the system can handle large datasets.
Maintain strong database design using IndexedDB.
```

This instruction enforces the fundamental design principles of SixMinuteLog. The application must remain completely self-contained, must not introduce external dependencies, and must continue to scale as the dataset grows.

Using a project-level instruction prevents Claude from accidentally suggesting frameworks, CDNs, or architecture changes that would break the single-file design.

Once the project is configured, development conversations should be started **inside this project** so the instruction is always active.

---

## Claude Web Chat (claude.ai)

SixMinuteLog was developed primarily using **Claude Web Chat**, which requires no installation and runs entirely through the browser. This method is ideal for incremental improvements, debugging, feature additions, and structural refactoring.

Development sessions begin by exporting two files from the running application.

First, open the application in a browser and navigate to the internal settings panel. In the advanced settings section, select **Download Claude Guide**. This exports a file named `CLAUDE.md`. The file contains a structured description of the application architecture, database layout, and development constraints. It provides Claude with the context required to safely modify the system.

Next, export the current version of the application. In the backup section of the settings panel, select **Save App as HTML**. This downloads the complete application file, typically named `index.html`.

At the end of this step you will have two files that represent the entire project state.

`CLAUDE.md` contains the architectural documentation used by Claude.
`index.html` contains the complete application implementation.

---

## Starting a Development Chat

Open **claude.ai** and start a new chat **inside the SixMinuteLog project** so the project instruction is active.

Upload both `CLAUDE.md` and `index.html` to the conversation.

The development prompt used during the project always begins by instructing Claude to read the architectural guide before modifying the application.

A typical prompt looks like this:

```
Read CLAUDE.md first.

Then modify index.html to [describe your change].
```

For example:

```
Read CLAUDE.md first.

Then modify index.html to add filtering so time entries can be viewed by client.
```

Claude will read the architecture guide, analyze the application code, and generate an updated version of `index.html` that includes the requested modification.

When the modification is complete, download the updated file generated by Claude.

---

## Testing the Change

After downloading the modified `index.html`, open it locally in a browser and test the new behavior.

Because the application runs entirely in the browser, testing requires no build process or deployment step. Simply opening the file loads the updated system.

Verify that the new functionality works as expected and that existing features remain stable.

If issues appear, return to the same Claude conversation and describe the problem. Describe the observed behavior so Claude can analyze and correct the implementation.

---

## Iterative Development

SixMinuteLog was built through **small iterative changes** rather than large rewrites. Each development cycle followed the same pattern.

The developer exports the guide and application files.
Both files are uploaded to Claude.
Claude is instructed to read the guide and implement a change.
The updated application is downloaded and tested locally.

This iterative loop allows new functionality to be introduced while preserving architectural consistency.

---

## Preparing the Next Development Session

After modifications are tested and confirmed, the architecture documentation should be regenerated so future development sessions remain synchronized with the updated codebase.

Open the modified application in a browser and again select **Download Claude Guide** from the advanced settings panel. This generates a new version of `CLAUDE.md` reflecting the latest application structure.

Future development sessions should always begin using the **latest exported guide and HTML file**.

The complete workflow therefore becomes a repeating cycle:

export guide → export application → upload to Claude → request modification → test → regenerate guide.

---

## Development Philosophy

The Claude-assisted workflow allows SixMinuteLog to evolve while preserving its core architectural constraint: **the entire application remains a portable single file**. By exporting the architecture guide and application file at each stage, Claude always works with a complete representation of the system. This prevents architectural drift and ensures new features integrate cleanly with the existing design. The result is a development process that is lightweight, repeatable, and accessible even without traditional programming skills.

