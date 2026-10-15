# Monitoring Desk

A single-file, offline knowledge base for daily SAP job and dump monitoring. Open `Monitoring Desk.html` in Microsoft Edge or Chrome. There is nothing to install and no server.

## What it's for
Every morning someone reads the job-monitoring email, investigates failed jobs and ABAP dumps, and decides what to do about them. Monitoring Desk keeps what they find in one shared place, so the next person doesn't start from zero.

- **Morning readings:** a quick grid of failed jobs and dumps per system/client. Each number is checked against what's normal for that day of the month and flagged when it's high.
- **Knowledge base:** one entry per job, dump or other recurring problem (RFC, interface…). Each has **known causes** with *when it happens* (for example days 20 – month end, the last 2 days, Sundays), *how to check*, *what to do* (ignore / fix ourselves / rerun / escalate / other team / monitor) and who to contact. Causes are checked against today's date: a cause that can't apply today says so ("not today, today is the 10th").
- **Log a failure** (`L`): type the job name, see the known causes ranked by whether they fit today, pick one or add the new cause you found. The entry is created automatically if it's new.
- **Incidents:** the log of everything looked into, with status (investigating, escalated, resolved, expected), follow-up updates and CSV export.
- **Trends:** dumps and failed jobs by day of the month, calendar, weekday, month by month, every system over 90 days, plus the stretches of the month that run hot. The Today page warns three days before a busy stretch starts and while you're in it.
- **Copy morning summary:** a plain-text status for mail or Teams.

## Sharing
Sync a Teams / SharePoint folder with OneDrive (a dedicated sub-folder such as `Monitoring Desk` is tidiest). Everyone opens the tool and picks the same folder. Setting the folder to *Always keep on this device* makes the first load faster.

Layout in the folder:

```
monitoring-desk.json       marker
events/YYYY-MM/*.json      one small file per save (never edited afterwards)
locks/*.json               "who is editing what", expire after 3 minutes
packs/YYYY-MM.json         optional month bundles (Settings → Compact old months)
```

## Why two people can't break it
- **Nothing is overwritten.** Each save is a new file named with the time and the user's ID, so OneDrive never has two versions of one file to choose between.
- **Soft locks.** Opening an entry or a day's readings for editing writes a lock note. Others see "Priya is editing" and are warned before they start.
- **Clashes are caught, not lost.** If someone saved the same field while you were editing, you're shown their version and choose which to keep. If OneDrive delivers two simultaneous saves later, the entry shows both versions until someone picks one. Entries created twice at the same moment are flagged and can be merged.

## Sample data
"Explore with sample data" generates six months of made-up readings, entries and incidents (with a month-end spike). It lives only in the browser and never touches the shared folder.
