=====================================================================
 README - CLIENT SCRIPT & UI POLICY (INCIDENT)
=====================================================================
Team ID     : SWTID-2026-5148
Team Leader : Mathangi S
Members     : Meena Varshini T P, Mirthika R, Muthu Priya U
Tool used   : ServiceNow (Incident form)


WHAT IS THIS PROJECT?
---------------------------------------------------------------------
When someone raises an Incident in ServiceNow, they sometimes skip
important fields or fill them wrongly. Our project fixes this by
adding some simple rules on the Incident form. The form itself stops
the user and tells them what to do.


WHAT DOES IT DO? (in simple words)
---------------------------------------------------------------------
1. UI Policy "High Impact Control"
   If Impact = 1 - High, then:
     - Assignment group becomes compulsory (must fill it).
     - Urgency becomes read-only (cannot change it).

2. Client Script - onChange
   When you change Impact to High, Urgency automatically becomes High
   and a small message shows on top.

3. Client Script - onSubmit
   If Impact is High and "Assigned to" is empty, the form will NOT
   save. It shows an error on that field.

4. Client Script - onCellEdit
   If someone tries to edit State directly from the Incident list,
   it is blocked and a pop-up says to open the Incident instead.


HOW TO MAKE IT IN SERVICENOW
---------------------------------------------------------------------
You only need a ServiceNow instance (a free Personal Developer
Instance is fine) and admin login.

Step 1 - UI Policy
  - Go to System UI > UI Policies > New
  - Name: High Impact Control, Table: Incident, Active: ticked
  - Condition: Impact is 1 - High
  - Tick "Reverse if false" and "On load"
  - Save, then open the UI Policy Actions tab at the bottom:
      * Assignment group  -> Mandatory = true
      * Urgency           -> Read only = true

Step 2 - Client Scripts (System UI > Client Scripts > New)
  a) Name: Auto set urgency for high impact
     Type: onChange, Table: Incident, Field: Impact
  b) Name: Prevent save if Assigned To missing
     Type: onSubmit, Table: Incident
  c) Name: Prevent state change via list edit
     Type: onCellEdit, Table: Incident, Field: State

The code for all three scripts is in the Project Report, last section
(Appendix). Just copy and paste it.


HOW TO TEST IT
---------------------------------------------------------------------
- Incident > Create New. Set Impact = 1 - High.
    -> Urgency changes to High and gets locked.
    -> Assignment group turns compulsory.
- Leave "Assigned to" empty and click Submit.
    -> You get an error and it does not save.
- Go to Incident > All list, double-click State on any row.
    -> You get the "cannot update from list" pop-up.


FILES, PHASE BY PHASE
---------------------------------------------------------------------
Ideation
  - Empathy_Map_Canvas_SWTID-2026-5148.docx
  - Define_Problem_Statements_SWTID-2026-5148.docx
  - Brainstorm_Idea_Prioritization_SWTID-2026-5148.docx

Requirement Analysis
  - Customer_Journey_Map_SWTID-2026-5148.pdf
  - Data_Flow_Diagram_and_User_Stories_SWTID-2026-5148.docx
  - Solution_Requirements_SWTID-2026-5148.docx
  - Technology_Stack_SWTID-2026-5148.docx

Project Design
  - Problem_Solution_Fit_SWTID-2026-5148.docx
  - Problem_Solution_Fit_Canvas_SWTID-2026-5148.pdf
  - Proposed_Solution_SWTID-2026-5148.docx
  - Solution_Architecture_SWTID-2026-5148.docx

Project Planning
  - Project_Planning_SWTID-2026-5148.docx
  - Planning_Logic_SWTID-2026-5148.docx

Project Development (Testing)
  - Functional_Performance_Test_SWTID-2026-5148.docx
  - User_Acceptance_Testing_SWTID-2026-5148.docx
  - UAT_Report_SWTID-2026-5148.pdf

Project Documentation (final)
  - Project_Report_SWTID-2026-5148.docx
  - Project_Documentation_FSD_SWTID-2026-5148.docx
