**README.md**
**POSTMORTEM - Week Ending 12/11/2023**

**IMPACT:**

*Service Downtime*
- **What service was affected?**
  The entire application running on PHP 7 experienced a crash during this period.
  
- **User Experience:**
  Users encountered difficulties accessing their accounts, and those already logged in were unable to send requests or messages.
  
- **Percentage of Users Affected:**
  Nearly 100% of users were impacted by this downtime error.
  
- **Root Cause:**
  The root cause was identified as an update implemented in the production environment while certain methods were still dependent on the previous development stack (PHP 7, Apache 5).

**TIMELINE:**

- **Issue Detection:**
  The issue was first detected on 10/11/2023 at 2:00 AM through the application deployment log, which displayed dependency alerts.

**ACTIONS TAKEN:**

- **Resolution Steps:**
  To address the issue, a rollback of the application's development state was executed.

- **Misleading Paths:**
  Initially, attempts were made to convert methods and variables to the new version, leading to complications.

- **Team/Individuals Involved:**
  The incident was escalated to the developers' team.

- **Resolution of the Incident:**
  The incident was resolved through a rollback to the previous application state, resulting in new users losing their accounts, deemed the most effective solution.

**ROOT CAUSE AND RESOLUTION:**

- **Cause:**
  The issue originated when an individual attempted to upgrade their local development stack but mistakenly upgraded the entire production environment. The error went unnoticed by DevOps, causing clients to face connection errors and request issues related to the upgraded methods.

- **Fix:**
  The issue was resolved by performing a complete rollback of the application, including data, to the previous state. Additionally, an automated daily backup at 23:59 PM was implemented.

**CORRECTIVE AND PREVENTATIVE MEASURES:**

- **Preventative Measures:**
  Developers' local environments are now set up with Docker containers, allowing them to make changes without impacting the global system.

**WAYS TO ADDRESS THE ISSUE:**

- **Steps Taken:**
  - Read log files
  - Fixed logs where errors were identified
  - Located concerned files
  - Identified the error message ("deprecated and unused methods")
  - Attempted to update methods
  - Ultimately, reset the entire application state to 01/02 using the backup server from the app file.

*End of Postmortem Report*