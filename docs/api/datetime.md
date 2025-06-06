---
title: "ion-datetime"
---
import Props from '@ionic-internal/component-api/v8/datetime/props.md';
import Events from '@ionic-internal/component-api/v8/datetime/events.md';
import Methods from '@ionic-internal/component-api/v8/datetime/methods.md';
import Parts from '@ionic-internal/component-api/v8/datetime/parts.md';
import CustomProps from '@ionic-internal/component-api/v8/datetime/custom-props.mdx';
import Slots from '@ionic-internal/component-api/v8/datetime/slots.md';

import Basic from '@site/static/usage/v8/datetime/basic/index.md';

import MaxMin from '@site/static/usage/v8/datetime/date-constraints/max-min/index.md';
import Values from '@site/static/usage/v8/datetime/date-constraints/values/index.md';
import Advanced from '@site/static/usage/v8/datetime/date-constraints/advanced/index.md';

import FormatOptions from '@site/static/usage/v8/datetime/format-options/index.md';

import CustomLocale from '@site/static/usage/v8/datetime/localization/custom-locale/index.md';
import HourCycle from '@site/static/usage/v8/datetime/localization/hour-cycle/index.md';
import FirstDayOfWeek from '@site/static/usage/v8/datetime/localization/first-day-of-week/index.md';
import LocaleExtensionTags from '@site/static/usage/v8/datetime/localization/locale-extension-tags/index.md';
import TimeLabel from '@site/static/usage/v8/datetime/localization/time-label/index.md';

import MonthAndYear from '@site/static/usage/v8/datetime/presentation/month-and-year/index.md';
import Time from '@site/static/usage/v8/datetime/presentation/time/index.md';
import Date from '@site/static/usage/v8/datetime/presentation/date/index.md';

import ShowingDefaultTitle from '@site/static/usage/v8/datetime/title/showing-default-title/index.md';
import CustomizingTitle from '@site/static/usage/v8/datetime/title/customizing-title/index.md';

import ShowingConfirmationButtons from '@site/static/usage/v8/datetime/buttons/showing-confirmation-buttons/index.md';
import CustomizingButtons from '@site/static/usage/v8/datetime/buttons/customizing-buttons/index.md';
import CustomizingButtonTexts from '@site/static/usage/v8/datetime/buttons/customizing-button-texts/index.md';

import HighlightedDatesArray from '@site/static/usage/v8/datetime/highlightedDates/array/index.md';
import HighlightedDatesCallback from '@site/static/usage/v8/datetime/highlightedDates/callback/index.md';

import ShowAdjacentDays from '@site/static/usage/v8/datetime/show-adjacent-days/index.md';

import MultipleDateSelection from '@site/static/usage/v8/datetime/multiple/index.md';

import GlobalTheming from '@site/static/usage/v8/datetime/styling/global-theming/index.md';
import CalendarDaysStyling from '@site/static/usage/v8/datetime/styling/calendar-days/index.md';
import WheelStyling from '@site/static/usage/v8/datetime/styling/wheel-styling/index.md';

<head>
  <title>ion-datetime: Ionic API Input for Datetime Format Picker</title>
  <meta name="description" content="Datetimes present a picker interface to select dates and times. Ionic's API Datetime input component easily displays a preferred format, and manages values." />
</head>

import EncapsulationPill from '@components/page/api/EncapsulationPill';

<EncapsulationPill type="shadow" />

Datetimes present a calendar interface and time wheel, making it easy for users to select dates and times. Datetimes are similar to the native `input` elements of `datetime-local`, however, Ionic Framework's Datetime component makes it easy to display the date and time in the preferred format, and manage the datetime values.

## Overview

Historically, handling datetime values within JavaScript, or even within HTML
inputs, has always been a challenge. Specifically, JavaScript's `Date` object is
notoriously difficult to correctly parse apart datetime strings or to format
datetime values. Even worse is how different browsers and JavaScript versions
parse various datetime strings differently, especially per locale.

Fortunately, Ionic Framework's datetime input has been designed so developers can avoid
the common pitfalls, allowing developers to easily manipulate datetime values and give the user a simple datetime picker for a great user experience.

### ISO 8601 Datetime Format: `YYYY-MM-DDTHH:mmZ`

Ionic Framework uses the [ISO 8601 datetime format](https://www.w3.org/TR/NOTE-datetime)
for its value. The value is simply a string, rather than using JavaScript's
`Date` object. Using the ISO datetime format makes it easy to serialize
and parse within JSON objects and databases.

Below are some examples of ISO 8601 formats that can be used with `ion-datetime`:

| Description          | Format                   | Datetime Value Example          |
| -------------------- | ------------------------ | ------------------------------  |
| Year                 | `YYYY`                   | `1994`                          |
| Year and Month       | `YYYY-MM`                | `1994-12`                       |
| Complete Date        | `YYYY-MM-DD`             | `1994-12-15`                    |
| Date and Time        | `YYYY-MM-DDTHH:mm`       | `1994-12-15T13:47`              |
| UTC Timezone         | `YYYY-MM-DDTHH:mm:ssZ`   | `1994-12-15T13:47:20Z`          |
| Timezone Offset      | `YYYY-MM-DDTHH:mm:ssTZD` | `1994-12-15T13:47:20+05:00`     |
| Hour and Minute      | `HH:mm`                  | `13:47`                         |

Note that the year is always four-digits, milliseconds (if it's added) is always
three-digits, and all others are always two-digits. So the number representing
January always has a leading zero, such as `01`. Additionally, the hour is
always in the 24-hour format, so `00` is `12am` on a 12-hour clock, `13` means
`1pm`, and `23` means `11pm`.

:::note
While seconds, milliseconds, and time zone can be specified using the ISO 8601 datetime format, `ion-datetime` does not provide an interface for second, millisecond, and time zone selection. Any second, millisecond, or time zone values provided will be ignored.
:::

## Basic Usage

<Basic />

## Usage with Datetime Button

If you need to present a datetime in an overlay such as a modal or a popover, we recommend using [ion-datetime-button](./datetime-button). `ion-datetime-button` should be used when space is constrained. This component displays buttons which show the current date and time values. When the buttons are tapped, the date or time pickers open in the overlay.

## Setting Values Asynchronously

If its `value` is updated programmatically after a datetime has already been created, the datetime will automatically jump to the new date. However, it is recommended to avoid updating the `value` in this way when users are able to interact with the datetime, as this could be disorienting for those currently trying to select a date. For example, if a datetime's `value` is loaded by an asynchronous process, it is recommended to hide the datetime with CSS until the value has finished updating.

## Date Constraints

### Max and Min Dates

To customize the minimum and maximum datetime values, the `min` and `max` component properties can be provided which may make more sense for the app's use-case. Following the same IS0 8601 format listed in the table above, each component can restrict which dates can be selected by the user.

The following example restricts date selection to March 2022 through May 2022 only.

<MaxMin />

### Selecting Specific Values

While the `min` and `max` properties allow you to restrict date selection to a certain range, the `monthValues`, `dayValues`, `yearValues`, `hourValues`, and `minuteValues` properties allow you choose specific days and times that users can select.

The following example allows minutes to be selected in increments of 15. It also allows for days to be selected in increments of 5.

<Values />

### Advanced Date Constraints

With the `isDateEnabled` property, developers can customize the `ion-datetime` to disable a specific day, range of dates, weekends or any custom rule using an ISO 8601 date string.
The `isDateEnabled` property accepts a function returning a boolean, indicating if a date is enabled. The function is called for each rendered calendar day, for the previous, current and next month. Custom implementations should be optimized for performance to avoid jank.

The following example shows how to disable all weekend dates. For more advanced date manipulation, we recommend using a date utility such as `date-fns`.

<Advanced />

## Localization

Ionic Framework makes use of the [Intl.DatetimeFormat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DatetimeFormat) Web API which allows us to automatically localize the month and day names according to the language and region set on the user's device.

### Custom Locale

For instances where you need a specific locale, you can use the `locale` property to set it. The locale controls both the language and the date and time formats that are displayed.

The following example shows how to set the locale to Spanish (Spain).

<CustomLocale />

:::note
The time label is not automatically localized. See [Time Label](#time-label) for more information.
:::

### Hour Cycle

`ion-datetime` will use the hour cycle that is specified by the `locale` property by default. For example, if `locale` is set to `en-US`, then `ion-datetime` will use a 12 hour cycle.

There are 4 primary hour cycle types:

| Hour cycle type | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| `'h12'`          | Hour system using 1–12; corresponds to 'h' in patterns. The 12 hour clock, with midnight starting at 12:00 am. |
| `'h23'`         | Hour system using 0–23; corresponds to 'H' in patterns. The 24 hour clock, with midnight starting at 0:00. |
| `'h11'`         | Hour system using 0–11; corresponds to 'K' in patterns. The 12 hour clock, with midnight starting at 0:00 am. |
| `'h24'`         | Hour system using 1–24; corresponds to 'k' in pattern. The 24 hour clock, with midnight starting at 24:00. |

:::note
  Source: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/Locale/hourCycle
:::


There may be scenarios where you need to have more control over which hour cycle is used. This is where the `hourCycle` property can help.

In the following example, we can use the `hourCycle` property to force `ion-datetime` to use the 12 hour cycle even though the locale is `en-GB`, which uses a 24 hour cycle by default:

<HourCycle />

### First Day of the Week

For `ion-datetime`, the default first day of the week is Sunday. As of 2022, there is no browser API that lets Ionic automatically determine the first day of the week based on a device's locale, though there is on-going work regarding this (see: [TC39 GitHub](https://github.com/tc39/ecma402/issues/6)).

<FirstDayOfWeek />

### Time Label

The time label is not automatically localized. Fortunately, Ionic makes it easy to provide custom localizations with the `time-label` slot.

<TimeLabel />

### Locale Extension Tags

`ion-datetime` also supports [locale extension tags](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/Locale) as part of the `Intl.Locale` API. These tags let you encode information about the locale in the locale string itself. Developers may prefer to use the extension tag approach if they are using the [Intl.Locale API](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/Locale) in their apps.

For example, if you wanted to use a 12 hour cycle with the `en-GB` locale, you could provide extension tags instead of using both the `locale` and `hourCycle` properties:

<LocaleExtensionTags />

:::note
Be sure to check the [Browser Compatibility Chart](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/Locale#browser_compatibility)  for `Intl.Locale` before using it in your app.
:::

## Presentation

By default, `ion-datetime` allows users to select both date and time. In addition, users have access to selecting the specific month, year, hour, and minute.

Some use cases may call for only date selection or only time selection. The `presentation` property allows you to specify which pickers to show and the order to show them in. For example, setting `date-time` will have the calendar picker appear before the time picker. Setting `time-date` will have the calendar picker appear after the time picker.

### Month and Year Selection

Month and year selection is available by passing `month-year`, `month`, or `year` to the `presentation` property.

This example shows a datetime with the `month-year` configuration.

<MonthAndYear />

### Time Selection

Time selection is available by passing `date-time`, `time-date`, or `time` to the `presentation` property.

This example shows a datetime with the `time` configuration.

<Time />

### Date Selection

Date selection is available by passing `date-time`, `time-date`, or `date` to the `presentation` property.

This example shows a datetime with the `date` configuration.

<Date />

### Wheel Style Pickers

By default, Ionic will prefer to show a grid style layout when using `presentation`. However, it is possible to show a wheel style using the `preferWheel` property. When `preferWheel` is `true`, Ionic will prefer to show the wheel style layout when possible.

Certain `presentation` options have both grid and wheel styles that developers can choose from with the `preferWheel` property. Other `presentation` values only have a wheel style and will never show a grid style. The table below shows which `presentation` values have grid or wheel styles.

| `presentation` | Has Grid Style? | Has Wheel Style? |
| -------------- | --------------- | ---------------- |
| `date`         | Yes             | Yes              |
| `date-time`    | Yes             | Yes              |
| `month`        | No              | Yes              |
| `month-year`   | No              | Yes              |
| `time`         | No              | Yes              |
| `time-date`    | Yes             | Yes              |
| `year`         | No              | Yes              |

The example below shows the wheel picker with `presentation="date-time"`.

import Wheel from '@site/static/usage/v8/datetime/presentation/wheel/index.md';

<Wheel />

## Show Adjacent Days

If the `showAdjacentDays` property is set to `true`, days from the previous and next month will be displayed in the calendar view to fill any empty spaces at the beginning or end of the month. When a user clicks on an enabled adjacent day, the calendar will smoothly animate to show that month's view.

The calendar view always displays 6 rows when `showAdjacentDays` is enabled, so days from the previous or next month will be shown as needed to fill the grid. For example, even if a month starts on the first day of the week and ends within the fifth row, days from the next month will appear at the end to complete the sixth row.

:::note
This property is only supported when using `presentation="date"` and `preferWheel="false"`.
:::

<ShowAdjacentDays />

## Multiple Date Selection

If the `multiple` property is set to `true`, multiple dates can be selected from the calendar picker. Clicking a selected date will deselect it.

:::note
This property is only supported when using `presentation="date"` and `preferWheel="false"`.
:::

<MultipleDateSelection />

## Titles

By default, `ion-datetime` does not show any header or title associated with the component. Developers can use the `showDefaultTitle` property to show the default title/header configuration. They can also use the `title` slot to customize what is rendered in the header.

### Showing the Default Title

<ShowingDefaultTitle />

### Customizing the Title

<CustomizingTitle />

## Format Options

You can customize the format of the date in the header text and the time in the time button of a Datetime component by providing `formatOptions`. The `date` and `time` in the `formatOptions` property should each be an [`Intl.DateTimeFormatOptions`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat/DateTimeFormat#options) object. If `formatOptions` is not provided, default formats will be used for dates and times.

Datetime [does not manipulate or set](#time-zones) the time zone. If `timeZone` or `timeZoneName` are provided, they will be ignored, and the time zone will be set to UTC. This ensures that the displayed value matches the selected value, rather than being converted to the user's current time zone.

Be careful with the options you provide, as they may not match the selected presentation. For example, providing `minute: 'numeric'` for a presentation of `month` may lead to unexpected behavior, displaying a month where only a time might be expected.

<FormatOptions />

## Buttons

By default, `ionChange` is emitted with the new datetime value whenever a new date is selected. To require user confirmation before emitting `ionChange`, you can either set the `showDefaultButtons` property to `true` or use the `buttons` slot to pass in a custom confirmation button. When passing in custom buttons, the confirm button must call the `confirm` method on `ion-datetime` for `ionChange` to be emitted.

### Showing Confirmation Buttons

The default Done and Cancel buttons are already preconfigured to call the [`confirm`](#confirm) and [`cancel`](#cancel) methods, respectively.

<ShowingConfirmationButtons />

### Customizing Button Texts

For simple use cases, developers can provide custom button text to the confirmation and cancel values through the `doneText` and `cancelText` properties. We recommend doing this when you only need to change the button text and do not need any custom behavior.

<CustomizingButtonTexts />

### Customizing Button Elements

Developers can provide their own buttons for advanced custom behavior.

`ion-datetime` has `confirm`, `cancel`, and `reset` methods that developers can call when clicking on custom buttons. The `reset` method also allows developers to provide a date to reset the datetime to.

<CustomizingButtons />

## Highlighting Specific Dates

Using the `highlightedDates` property, developers can style particular dates with custom text or background colors. This property can be defined as either an array of dates and their colors, or a callback that receives an ISO string and returns the colors to use.

When specifying colors, any valid CSS color format can be used. This includes hex codes, `rgba`, [color variables](../theming/colors), etc.

To maintain a consistent user experience, the style of selected date(s) will always override custom highlights.

:::note
This property is only supported when `preferWheel="false"`, and using a `presentation` of either `"date"`, `"date-time"`, or `"time-date"`.
:::

### Using Array

An array is better when the highlights apply to fixed dates, such as due dates.

<HighlightedDatesArray />

### Using Callback

A callback is better when the highlighted dates are recurring, such as birthdays or recurring meetings.

<HighlightedDatesCallback />

## Styling

### Global Theming

Ionic's powerful theming system can be used to easily change your entire app to match a certain theme. In this example, we used the [Color Creator](../theming/colors#new-color-creator) and the [Stepped Color Generator](../theming/themes#stepped-color-generator) to create a rose color palette that we can use for `ion-datetime`.

The benefit of this approach is that every component, not just `ion-datetime`, can automatically take advantage of this theme.

<GlobalTheming />

### Calendar Days

The calendar days in a grid-style `ion-datetime` can be styled using CSS shadow parts.

:::note
The example below selects the day 2 days ago, unless that day is in the previous month, then it selects a day 2 days in the future. This is done for demo purposes in order to show how to apply custom styling to all days, the current day, and the selected day.
:::

<CalendarDaysStyling />

### Wheel Pickers

The wheels used in `ion-datetime` can be styled through a combination of shadow parts and CSS variables. This applies to both the columns in wheel-style datetimes, and the month/year picker in grid-style datetimes.

<WheelStyling />

## Time Zones

Ionic's `ion-datetime` follows the [datetime-local](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/datetime-local) behavior of not manipulating or setting the time zone inside of a datetime control. In other words, a time value of "07:00" will not be adjusted according to different time zones.

We recommend using a library such as [date-fns-tz](https://github.com/marnusw/date-fns-tz) to convert a datetime value to the desired time zone.

Below is an example of formatting an ISO-8601 string to display in the time zone set on a user's device:

```typescript
import { format, utcToZonedTime } from 'date-fns-tz';

// Get the time zone set on the user's device
const userTimeZone = Intl.DateTimeFormat().resolvedOptions().timeZone;

// Create a date object from a UTC date string
const date = new Date('2014-10-25T10:46:20Z');

// Use date-fns-tz to convert from UTC to a zoned time
const zonedTime = utcToZonedTime(date, userTimeZone);

// Create a formatted string from the zoned time
format(zonedTime, 'yyyy-MM-dd HH:mm:ssXXX', { timeZone: userTimeZone });
```

### Parsing Date Values

The `ionChange` event will emit the date value as an ISO-8601 string in the event payload. It is the developer's responsibility to format it based on their application needs. We recommend using [date-fns](https://date-fns.org) to format the date value.

Below is an example of formatting an ISO-8601 string to display the month, date and year:

```typescript
import { format, parseISO } from 'date-fns';

/**
 * This is provided in the event
 * payload from the `ionChange` event.
 *
 * The value is an ISO-8601 date string.
 */
const dateFromIonDatetime = '2021-06-04T14:23:00-04:00';
const formattedString = format(parseISO(dateFromIonDatetime), 'MMM d, yyyy');

console.log(formattedString); // Jun 4, 2021
```

See https://date-fns.org/docs/format for a list of all the valid format tokens.


## Advanced Datetime Validation and Manipulation

The datetime picker provides the simplicity of selecting an exact format, and
persists the datetime values as a string using the standardized [ISO 8601
datetime format](https://www.w3.org/TR/NOTE-datetime). However, it's important
to note that `ion-datetime` does not attempt to solve all situations when
validating and manipulating datetime values. If datetime values need to be
parsed from a certain format, or manipulated (such as adding 5 days to a date,
subtracting 30 minutes, etc.), or even formatting data to a specific locale,
then we highly recommend using [date-fns](https://date-fns.org) to work with
dates in JavaScript.

## Accessibility

### Keyboard Interactions

`ion-datetime` has full keyboard support for navigating between focusable elements inside of the component. The following table details what each key does:

| Key                                  | Description                                    |
| ------------------------------------ | ---------------------------------------------- |
| <kbd>Tab</kbd>                       | Moves focus to the next focusable element.     |
| <kbd>Shift</kbd> + <kbd>Tab</kbd>    | Moves focus to the previous focusable element. |
| <kbd>Space</kbd> or <kbd>Enter</kbd> | Clicks the focusable element.                  |

#### Date Grid

| Key                                    | Description                                       |
| -------------------------------------- | ------------------------------------------------- |
| <kbd>ArrowUp</kbd>                     | Moves focus to the same day of the previous week. |
| <kbd>ArrowDown</kbd>                   | Moves focus to the same day of the next week.     |
| <kbd>ArrowRight</kbd>                  | Moves focus to the next day.                      |
| <kbd>ArrowLeft</kbd>                   | Moves focus to the previous day.                  |
| <kbd>Home</kbd>                        | Moves focus to the first day of the current week. |
| <kbd>End</kbd>                         | Moves focus to the last day of the current week.  |
| <kbd>PageUp</kbd>                      | Changes the grid of dates to the previous month.  |
| <kbd>PageDown</kbd>                    | Changes the grid of dates to the next month.      |
| <kbd>Shift</kbd> + <kbd>PageUp</kbd>   | Changes the grid of dates to the previous year.   |
| <kbd>Shift</kbd> + <kbd>PageDown</kbd> | Changes the grid of dates to the next year.       |

#### Time, Month, and Year Wheels

The wheel picker in Datetime uses [Picker](./picker) internally. See [Picker Accessibility](./picker#accessibility) for more information on accessibility features with the wheel picker.

## Interfaces

### DatetimeChangeEventDetail

```typescript
interface DatetimeChangeEventDetail {
  value?: string | null;
}
```

### DatetimeCustomEvent

While not required, this interface can be used in place of the `CustomEvent` interface for stronger typing with Ionic events emitted from this component.

```typescript
interface DatetimeCustomEvent extends CustomEvent {
  detail: DatetimeChangeEventDetail;
  target: HTMLIonDatetimeElement;
}
```

## Properties
<Props />

## Events
<Events />

## Methods
<Methods />

## CSS Shadow Parts
<Parts />

## CSS Custom Properties
<CustomProps />

## Slots
<Slots />
