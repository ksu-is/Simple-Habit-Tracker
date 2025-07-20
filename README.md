# Simple-Habit-Tracker
This is a simple habit tracker to allow you to improve habits you choose.
My name is Emanuel Portugal and I am a senior at KSU and I decidede to choose a topic that can help us all in improving something we want to work on.
https://github.com/ksu-is/Simple-Habit-Tracker for Sprint 1 task


ON 7/15/25 started working on simple habit code by watching tutorials on commands to make the code functional.


ON 7/15/25 8:10PM I fixed lines 12-18 due to syntax error. Correct adjustments made 


ON 7/15/25 8:56 I added comments to make the code easier to read for others to analyze.

ON 7/19/25 8:26 I added the code for it be available to operate in Visual Studio Code.
import os
import datetime

DATA_FILE = "habit_log.txt"
HABITS = ["water", "reading", "walking"]

def load_data():
    if not os.path.exists(DATA_FILE):
        with open(DATA_FILE, "w") as f:
            pass  # Create empty file

    data = {}
    with open(DATA_FILE, "r") as f:
        for line in f:
            habit, date_str = line.strip().split(",")
            date = datetime.datetime.strptime(date_str, "%Y-%m-%d").date()
            data.setdefault(habit, []).append(date)
    return data

def log_habit(habit):
    today = datetime.date.today()
    with open(DATA_FILE, "a") as f:
        f.write(f"{habit},{today}\n")
    print(f"✅ Logged {habit} for today.")

def show_stats(data):
    today = datetime.date.today()
    for habit in HABITS:
        print(f"\n📊 Stats for '{habit}':")
        dates = sorted(data.get(habit, []))

        total_count = len(dates)
        streak = 0
        for days_ago in range(0, 1000):
            day = today - datetime.timedelta(days=days_ago)
            if day in dates:
                streak += 1
            else:
                if days_ago != 0:  # Allow today to be missing
                    break

        print(f"   Total logged days: {total_count}")
        print(f"   Current streak: {streak} day(s)")

def main():1
data = load_data()
print("Welcome to the Habit Tracker!")
print("Track one of the following habits today:")
for i, habit in enumerate(HABITS, 1):
        print(f"{i}. {habit}")

choice = input("Enter the number of the habit to log (or press Enter to skip): ")

if choice.isdigit() and 1 <= int(choice) <= len(HABITS):
        selected = HABITS[int(choice) - 1]
        log_habit(selected)
else:
        print("No habit logged today.")

    # Reload data to include new log
data = load_data()
show_stats(data)

if __name__ == "__main__":
    main()
