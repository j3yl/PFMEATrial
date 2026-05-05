ts is entirely written using Gemini i aint gon cap. ion even know if this is necessary.

📋 PFMEA Manager

PFMEA Manager is a lightweight, zero-install web application designed for engineers and quality control teams to build, visualize, and manage **Process Failure Mode and Effects Analysis (PFMEA)** documents. 

Built entirely in a single HTML file, it combines a hierarchical flowchart visualizer with a robust, auto-calculating data entry table. It features cloud synchronization via Supabase and a standardized "Master Library" to quickly reuse common failure modes across projects.

---

✨ Key Features

  🛠️ Core PFMEA Engine
  -Dynamic Action Priority (AP):** Automatically calculates Risk Priority Numbers (RPN) and assigns Action Priority (High, Medium, Low) based on Severity, Occurrence, and Detection inputs.
  -Hierarchical Structure:** Organize your analysis by Project -> Process -> Component -> Sub-component.
  -Scope Definition:** Built-in metadata header to track Project Name, Revision Dates, Cross-Functional Team members, and Confidentiality levels.
  
  ⬡ Visual Flowcharting
  -Interactive Chart View:** Visually map out process flows and component relationships.
  -Drag-and-Drop Connectivity:** Visually link upstream inputs to downstream outputs.
  -Visual Risk Indicators:** Nodes automatically display color-coded dots (🔴, 🟡, 🟢) indicating the highest Action Priority present within that specific process.
  -Image Export:** One-click export of your visual process map to a `.png` file.
  
  📚 Master Library System
  -Standardized Knowledge Base:** Admins can unlock the Master Library (password protected) to manage a global database of standard failure modes.
  -Smart Dropdown Auto-fill:** Users can click the "📚" icon inside any blank row to search the Master Library and instantly populate standard Causes, Effects, and Controls.
  -Excel Synchronization:** The Master Library is managed effortlessly by importing and exporting `.xlsx` templates.
  
  💾 Data Management & Cloud Sync
  -Zero-Install Local Mode:** Can run entirely offline in the browser. Projects can be saved and shared locally via `.json` export/import.
  -Formatted Excel Export:** Generate production-ready `.xlsx` reports with merged cells, color-coded risk bands, and rotated headers matching industry PFMEA standards.
  -Supabase Cloud Sync:** Automatically saves project states and the Master Library JSON payload to a PostgreSQL cloud database using REST API.

---

💻 Technologies Used

-Frontend:** HTML5, CSS3, Vanilla JavaScript (No frameworks required)
-Styling:** CSS Variables with automatic Light/Dark mode detection based on OS settings.
-Libraries (via CDN):
  * `xlsx-js-style` - For reading and generating styled Excel documents.
  * `html-to-image` - For capturing the flowchart viewport.
-Backend / Database:** [Supabase](https://supabase.com/) (PostgreSQL REST API using `jsonb` document storage).

---

🚀 Getting Started

Because PFMEA Manager is a single-file application, there is no build step, no `npm install`, and no local server required for basic usage.

1. Clone or download the repository.
2. Double-click `index.html` to open it in any modern web browser (Chrome, Edge, Firefox).
3. Start building!

⚙️ Database Configuration (Supabase)

To enable cloud saving and the Master Library functionality across multiple users, you need to configure a Supabase project.

1. Create a new project in Supabase.
2. Go to the **Table Editor** and create two tables:
   * `pfmea_projects`
   * `global_master_library`
3. Both tables must have the following schema:
   * `id` (int8, Primary Key)
   * `data` (jsonb)
   * `updated_at` (timestamp)
   * *(For `pfmea_projects`, add a `name` column as text).*
4. **Permissions:** Ensure Row Level Security (RLS) is disabled for testing, or write specific policies to allow `SELECT`, `INSERT`, and `UPDATE` for the `anon` role.
5. **Initialize Master Library:** Manually insert one blank row into `global_master_library` with `id: 1` and `data: []`.
6. Update the `SB_URL` and `SB_KEY` variables at the bottom of the HTML file with your Supabase credentials.

---

📖 How to Use

1. **Add a Process:** Click the **+ Add** button in the top right of the Chart View or List View to create a root process step.
2. **Add Components:** Click **+ Add -> Component** to attach sub-items to your process.
3. **Connect Nodes (Chart View):** Click **⇢ Connect**, select a source node, and then click a target node to draw a relationship.
4. **Enter Failure Data:** Click on any node to open its specific PFMEA table on the right side of the screen. Click **+ Add Failure Mode Row**.
5. **Use the Master Library:** In the "Process Step" cell, click the blue book icon to insert standardized data. 
   *(Note: The default password to unlock and edit the Master Library is `Pfmea@MXS2026`).*

---

## 📝 License & Contact
*Developed for internal engineering process management.*
