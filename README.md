# 🐧 Linux Cron Jobs Lab

In this lab, I learned how to **view, create, and manage cron jobs** for users and the root account. The lab involved inspecting existing jobs, scheduling scripts at specific times, and correcting misconfigured cron schedules.

---

## 📋 Lab Overview

**Goal:**

* Inspect and list cron jobs for users
* Schedule scripts at precise times or intervals
* Understand cron syntax and 24-hour formatting
* Correct improperly configured jobs

**Learning Outcomes:**

* Use `crontab -l` to list scheduled jobs
* Use `crontab -e` to create or edit jobs
* Schedule tasks **daily, monthly, or at custom intervals**
* Correctly specify minutes, hours, day of month, month, and weekday

---

## 🛠 Step-by-Step Journey

### Step 1: List Existing Cron Jobs

**For a specific user (e.g., Bob):**

```bash
crontab -l
```

**For root user:**

```bash
sudo su
crontab -l
```

**Count the number of scheduled jobs:**

* Each line in the output corresponds to one job.

---

### Step 2: Inspect Scheduled Jobs

* Identify which script runs at a specific time, e.g., **11 minutes past 11 PM every Tuesday**:

```bash
crontab -l
# Look for the job with minute=11, hour=23, weekday=2
```

> 💡 Cron uses a **24-hour clock**: 11 PM = `23`.
> Day of week: Sunday=0 or 7, Monday=1, Tuesday=2, etc.

---

### Step 3: Schedule a New Cron Job

**Task:** Run a script `/usr/local/bin/last-reboot.sh` on **the first day of every month at 6 AM**.

1. Edit the cron table for the user:

```bash
crontab -e
```

2. Insert the job in **insert mode**:

```
0 6 1 * * /usr/local/bin/last-reboot.sh
```

3. Save and exit:

```bash
ESC
:wq!
```

> ✅ Minute, hour, day-of-month, month, day-of-week, followed by the command.

---

### Step 4: Correct Misconfigured Cron Jobs

**Task:** Run `/usr/local/bin/system-debugger.sh` every half hour at minute 0 and minute 30.

1. Edit cron table:

```bash
crontab -e
```

2. Insert job with correct interval syntax:

```
0,30 * * * * /usr/local/bin/system-debugger.sh
```

3. Save and exit:

```bash
ESC
:wq!
```

> 💡 Use commas `,` to specify multiple minutes in the **minute field**.
> `*` means “every” for that column.

---

### Step 5: Verify Cron Jobs

* List the user's cron jobs:

```bash
crontab -l
```

* Ensure the schedule matches the intended times.
* Check for correct **24-hour notation**, day-of-week, and day-of-month.

---

## ✅ Key Commands Summary

| Task                     | Command / Notes                   |
| ------------------------ | --------------------------------- |
| List cron jobs for user  | `crontab -l`                      |
| Edit cron jobs           | `crontab -e`                      |
| Switch to root for cron  | `sudo su`                         |
| Schedule a monthly job   | `0 6 1 * * /path/to/script.sh`    |
| Schedule every half hour | `0,30 * * * * /path/to/script.sh` |
| Exit insert mode in `vi` | `ESC`                             |
| Save & exit `vi`         | `:wq!`                            |

---

## 💡 Notes / Tips

* Always use **24-hour clock** for hours in cron.
* Minute field can take multiple values using commas, e.g., `0,30` for every half hour.
* Day-of-week uses numbers: Sunday=0 or 7, Monday=1, Tuesday=2, etc.
* Use `sudo su` to edit root cron jobs.
* Check job syntax carefully; wrong fields can prevent execution.

---

## 📌 Lab Summary

| Step                               | Status | Key Takeaways                                       |
| ---------------------------------- | ------ | --------------------------------------------------- |
| List Bob's cron jobs               | ✅      | Used `crontab -l`                                   |
| Count Bob's jobs                   | ✅      | 6 jobs scheduled                                    |
| List root cron jobs                | ✅      | Switched to root using `sudo su`                    |
| Inspect job at 23:11 every Tuesday | ✅      | Verified correct script and schedule                |
| Schedule monthly script            | ✅      | `/usr/local/bin/last-reboot.sh` at 6 AM on 1st      |
| Correct half-hour job              | ✅      | `/usr/local/bin/system-debugger.sh` at 0 and 30 min |

---

## ✅ References

* [CronHowto – Ubuntu Documentation](https://help.ubuntu.com/community/CronHowto)
* [Crontab Guru – Cron Syntax Cheat Sheet](https://crontab.guru/)
* [Linuxize – How to Use Cron](https://linuxize.com/post/scheduling-cron-jobs-with-crontab/)
