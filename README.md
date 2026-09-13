# Dewey

Dewey is a student reminder bot on Discord that syncs assignments from .ics links supplied by learning management systems like Canvas and sends users a daily DM with what is due.

I originally built Dewey because I hated using Google Calendar for assignment reminders and already used Discord every day. I wanted my deadlines to be all easily accessed in one app I already used instead of having to goto another.

Dewey is currently used by a small group of students, with 5+ active users.

## Features

* Sync assignments from Canvas calendar feeds
* Sync assignments from D2L calendar feeds
* Upload PDF, DOCX, and TXT syllabi for deadline extraction using LLM
* View upcoming assignments with `/upcoming`
* Receive a daily 8:00 AM DM showing assignments due that day
* Store assignment information persistently using SQLite
* Deployed 24/7

## Calendar Sync

Connecting a calendar takes only a few steps:

1. Find your .ics link on your chosen LMS (Canvas / D2L).
2. Type the corresponding `/connect` command and paste in the link.
3. Review and confirm the connection.
4. Done! Dewey will import your assignments, begin tracking deadlines, and send reminders automatically.

Uploading is a one and done. No more setup is required to receive notifications.

### Demo

<img width="800" height="709" alt="deweydemorec-ezgif com-video-to-gif-converter" src="https://github.com/user-attachments/assets/e1a10c59-2a69-4c48-9feb-2bdcf192546b" />

## Syllabus Uploads

Dewey can also extract deadlines directly from syllabi with the `/syllabusupload` command! Just make sure to skim your syllabus for accurate dates then confirm.

Supported file formats:

* PDF
* DOCX
* TXT

After a file is uploaded, Dewey extracts its text and uses Gemini to identify course information and deadlines. You can then review the detected assignments before confirming and saving them.

## Daily Reminders

Every morning at **8:00 AM**, Dewey checks each user's stored assignments and sends a Discord DM containing anything due that day.

This was the main reason I created the project. I wanted assignment reminders to come directly to me and to be able to easily check upcoming tasks without a browser.

## Built With

* **Python**
* **discord.py**
* **SQLite**
* **icalendar**
* **PyMuPDF**
* **docx2python**
* **Gemini API**
* **Railway**

## How It Works

Dewey has calendar parsing, file parsing, persistent storage, and scheduled Discord notifications.

For calendar integrations, Dewey reads ICS calendar feeds provided by Canvas and D2L. Events are parsed into assignment information and stored in a SQLite database. Calendar event UIDs are also stored so previously imported assignments are not repeatedly added.

For syllabus uploads, text is extracted from the uploaded document and sent to Gemini for structured deadline extraction. The detected assignments are shown to the user for confirmation before being saved.

Scheduled tasks then check the database each morning and send users their daily reminders through Discord.

## What I Learned

Dewey was also my introduction to Python.

While building it, I learned how to work with:

* Asynchronous Python
* Discord bots and slash commands
* Modals and interactive Discord components
* SQLite databases
* ICS calendar data
* PDF and DOCX parsing
* APIs and structured data
* Third-party Python libraries
* Cloud deployment

Most of these were technologies I had not worked with before starting the project, so much of the development process came from learning new tools as I needed them.

## Challenges

One of the most challenging parts of the project was turning data from different sources into the same deadline format.

Canvas and D2L give calendar data through ICS feeds, while syllabus uploads have unstructured documents with dates in different places. Dewey has to parse those different inputs, find useful assignment information, handle dates and times, prevent duplicate calendar events, and store everything before reminders can be sent.

Building and iterating from nothing was one of the most technically interesting parts of the project as the scope increased day by day.

## Future Improvements

Some features I would like to add include:

* Manual deadline creation and editing
* More commands for viewing and filtering assignments
* Customizable reminder times
* Improved onboarding for new users
* Better organization and formatting within the Discord server
* Additional calendar and learning-platform integrations

Longer term, I would like to expand Dewey beyond Discord into a web application for managing deadlines and class notes while keeping Discord notifications for reminders.
