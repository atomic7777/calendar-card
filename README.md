<h1 align="center">Calendar Card for Home Assistant</h1>

<p align="center">
  <img src='https://i.imgur.com/86RGw5W.png' />
</p>

<h2>Features</h2>

* show the next 5 events on your Google Calendar (default set by home assistant)
* Set custom time format for each event
* click on event to open in your Google calendar app
* Integrate multiple calendars
* Update notifications via custom_updater
* Show event color

<h2>Track Updates</h2>

This custom card can be tracked with the help of [custom-updater](https://github.com/custom-components/custom_updater).

In your configuration.yaml

```yaml
custom_updater:
  card_urls:
    - https://raw.githubusercontent.com/ljmerza/calendar-card/master/custom_updater.json
```

<h1>Usage</h1>
<h2>Prerequisites</h2>
You should have setup Google calendar integration or Caldav integration in HomeAssistant.

<h2>Options</h2>

| Name | Type | Requirement | Description
| ---- | ---- | ------- | -----------
| type | string | **Required** | `custom:calendar-card`
| title | string | **Optional** | `Calendar` Header shown at top of card
| showProgressBar | boolean | **Optional** | `true` Option to show the progress bar
| numberOfDays | number | **Optional** | `7` Number of days to display from calendars
| entities | object | **Required** | List of calendars to display
| timeFormat | string | **Optional** | `HH:mm` Format to show event time (see [here](https://momentjs.com/docs/#/displaying/format/) for options)
| showColors | boolean | **Optional** | `false` Add event color marker to event summary
| textAllDay | string | **Optional** | `All day` Custom or translated text for all day event
| textToday | string | **Optional** | `none` Additional, custom "Today: " text for today events, to make it more visible
| textTomorrow | string | **Optional** | `none` Additional, custom "Tomorrow: " text for tomorrow events, to make it more visible. No text if not set.
| todayColor | string | **Optional** | `none` Color setting for today events, to make it more visible. Default when not set.
| tomorrowColor | string | **Optional** | `none` Color setting for tomorrow events, to make it more visible. Default when not set.
| showDot | boolean | **Optional** | `true` Add or remove the big dot in event title.
| showCurrentProgress | boolean | **Optional** | `false` Show progress of current event with a moving red dot (works only if showProgressBar is on) 
| textSizeSummary | string | **Optional** | `100` Event title text size (percent of default font size) 
| textSizeTime | string | **Optional** | `90` Event time (bottom line) text size (percent of default font size) 
| textSizeLocation | string | **Optional** | `90` Location link text size (percent of default font size) 


<h2>Configuration</h2>
Go to your config directory and create a www folder. Inside the www run

```bash
git clone https://github.com/ljmerza/calendar-card.git
```

In your ui-lovelace.yaml

```yaml
resources:
  - url: https://unpkg.com/moment@2.23.0/moment.js
    type: js
  - url: /local/calendar-card/calendar-card.js?v=1.3.1
    type: module
```

Add the custom card to views:

```yaml
views:
  - type: custom:calendar-card
    title: "My Calendar"
    numberOfDays: 14
    entities:
      - calendar.ljmerzagmailcom
      - entity: calendar.with_red_color_title
        color: red
      - calendar.atomic7777 
```

<h2>You want more than 5 Google events?</h2>

```bash
mkdir /config/custom_components/calendar
cd /config/custom_components/calendar
wget https://raw.githubusercontent.com/home-assistant/home-assistant/dev/homeassistant/components/calendar/google.py
```
Use a text editor to change the `'maxResults': 5` in `google.py` to a number of your liking.
